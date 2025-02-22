---
title: Wdrażanie konfiguracji przy użyciu metodyki GitOps w klastrach platformy Kubernetes z włączoną usługą Azure Arc (wersja zapoznawcza)
services: azure-arc
ms.service: azure-arc
ms.date: 05/19/2020
ms.topic: article
author: mlearned
ms.author: mlearned
description: Użyj GitOps, aby skonfigurować klaster Kubernetes z obsługą usługi Azure ARC (wersja zapoznawcza)
keywords: GitOps, Kubernetes, K8s, Azure, ARC, Azure Kubernetes Service, AKS, kontenery
ms.openlocfilehash: 906021377cbfd6960769f98f9dbd15a5c430c71f
ms.sourcegitcommit: 19ffdad48bc4caca8f93c3b067d1cf29234fef47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/06/2021
ms.locfileid: "97955335"
---
# <a name="deploy-configurations-using-gitops-on-arc-enabled-kubernetes-cluster-preview"></a>Wdrażanie konfiguracji przy użyciu metodyki GitOps w klastrach platformy Kubernetes z włączoną usługą Azure Arc (wersja zapoznawcza)

GitOps, w odniesieniu do Kubernetes, jest podejściem do deklarowania żądanego stanu konfiguracji Kubernetes (wdrożenia, przestrzenie nazw itp.) w repozytorium git, a następnie wdrożenia tych konfiguracji w klastrze przy użyciu operatora. Ten dokument obejmuje konfigurację takich przepływów pracy w klastrach Kubernetes z obsługą usługi Azure Arc.

Połączenie między klastrem a repozytorium git jest tworzone w Azure Resource Manager jako `Microsoft.KubernetesConfiguration/sourceControlConfigurations` zasób rozszerzenia. `sourceControlConfiguration`Właściwości zasobu przedstawiają miejsce i sposób przepływu zasobów Kubernetes z usługi git do klastra. `sourceControlConfiguration`Dane są przechowywane w postaci zaszyfrowanej w bazie danych Azure Cosmos DB w celu zapewnienia poufności danych.

`config-agent`Działający w klastrze jest odpowiedzialny za obserwowanie nowych lub zaktualizowanych `sourceControlConfiguration` zasobów rozszerzeń w zasobie Kubernetes z obsługą usługi Azure ARC, w celu wdrożenia operatora strumienia w celu obejrzenia repozytorium git dla każdej z nich `sourceControlConfiguration` i zastosowania wszelkich aktualizacji dokonanych w dowolnym z nich `sourceControlConfiguration` . Istnieje możliwość utworzenia wielu `sourceControlConfiguration` zasobów w tym samym klastrze Kubernetes z obsługą usługi Azure Arc w celu osiągnięcia wielu dzierżawców. Każdy z nich można utworzyć `sourceControlConfiguration` z innym `namespace` zakresem, aby ograniczyć wdrożenia do odpowiednich przestrzeni nazw.

Repozytorium git może zawierać manifesty formatu YAML, które opisują wszystkie ważne zasoby Kubernetes, w tym obszary nazw, ConfigMaps, wdrożenia, DaemonSets itp.  Może również zawierać wykresy Helm na potrzeby wdrażania aplikacji. Typowym zestawem scenariuszy jest definiowanie konfiguracji bazowej dla organizacji, która może obejmować typowe role i powiązania platformy Azure, agentów monitorowania i rejestrowania oraz usług w całym klastrze.

Ten sam wzorzec może służyć do zarządzania większą kolekcją klastrów, które mogą być wdrażane w środowiskach heterogenicznych. Na przykład można mieć jedno repozytorium definiujące konfigurację bazową organizacji i zastosować je do dziesiątek klastrów Kubernetes jednocześnie. [Usługa Azure Policy umożliwia automatyzację](use-azure-policy.md) tworzenia `sourceControlConfiguration` z określonym zestawem parametrów we wszystkich zasobach Kubernetes z obsługą usługi Azure Arc w ramach zakresu (subskrypcji lub grupy zasobów).

Ten przewodnik wprowadzający przeprowadzi Cię przez proces stosowania zestawu konfiguracji z zakresem administratora klastra.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym artykule przyjęto założenie, że masz istniejący Kubernetes połączony klaster usługi Azure Arc. Jeśli potrzebny jest podłączony klaster, zobacz temat [łączenie się z klastrem szybki start](./connect-cluster.md).

## <a name="create-a-configuration"></a>Utwórz konfigurację

[Przykładowe repozytorium](https://github.com/Azure/arc-k8s-demo) używane w tym dokumencie jest strukturalne wokół osoby będącej operatorem klastra, który chce udostępnić kilka przestrzeni nazw, wdrożyć typowe obciążenie i zapewnić konfigurację specyficzną dla zespołu. Użycie tego repozytorium powoduje utworzenie następujących zasobów w klastrze:

**Przestrzenie nazw:** `cluster-config` , `team-a` , `team-b` 
 **wdrożenie:** `cluster-config/azure-vote` 
 **ConfigMap:**`team-a/endpoints`

`config-agent`Sonduje platformę Azure pod kątem nowych lub zaktualizowanych `sourceControlConfiguration` co 30 sekund, co jest maksymalny czas potrzebny `config-agent` na pobranie nowej lub zaktualizowanej konfiguracji.
W przypadku kojarzenia repozytorium prywatnego z programem `sourceControlConfiguration` upewnij się, że wykonano również kroki opisane w temacie [Zastosuj konfigurację z prywatnego repozytorium git](#apply-configuration-from-a-private-git-repository).

### <a name="using-azure-cli"></a>Korzystanie z interfejsu wiersza polecenia platformy Azure

Użyj rozszerzenia interfejsu wiersza polecenia platformy Azure, aby `k8sconfiguration` połączyć połączony klaster z [przykładowym repozytorium git](https://github.com/Azure/arc-k8s-demo). Ta konfiguracja zostanie nadana nazwie `cluster-config` , nakazuje agentowi wdrożenie operatora w `cluster-config` przestrzeni nazw i nadanie `cluster-admin` uprawnień operatora.

```console
az k8sconfiguration create --name cluster-config --cluster-name AzureArcTest1 --resource-group AzureArcTest --operator-instance-name cluster-config --operator-namespace cluster-config --repository-url https://github.com/Azure/arc-k8s-demo --scope cluster --cluster-type connectedClusters
```

**Rozdzielczości**

```console
Command group 'k8sconfiguration' is in preview. It may be changed/removed in a future release.
{
  "complianceStatus": {
    "complianceState": "Pending",
    "lastConfigApplied": "0001-01-01T00:00:00",
    "message": "{\"OperatorMessage\":null,\"ClusterState\":null}",
    "messageLevel": "3"
  },
  "configurationProtectedSettings": {},
  "enableHelmOperator": false,
  "helmOperatorProperties": null,
  "id": "/subscriptions/<sub id>/resourceGroups/<group name>/providers/Microsoft.Kubernetes/connectedClusters/<cluster name>/providers/Microsoft.KubernetesConfiguration/sourceControlConfigurations/cluster-config",
  "name": "cluster-config",
  "operatorInstanceName": "cluster-config",
  "operatorNamespace": "cluster-config",
  "operatorParams": "--git-readonly",
  "operatorScope": "cluster",
  "operatorType": "Flux",
  "provisioningState": "Succeeded",
  "repositoryPublicKey": "",
  "repositoryUrl": "https://github.com/Azure/arc-k8s-demo",
  "resourceGroup": "MyRG",
  "sshKnownHostsContents": "",
  "systemData": {
    "createdAt": "2020-11-24T21:22:01.542801+00:00",
    "createdBy": null,
    "createdByType": null,
    "lastModifiedAt": "2020-11-24T21:22:01.542801+00:00",
    "lastModifiedBy": null,
    "lastModifiedByType": null
  },
  "type": "Microsoft.KubernetesConfiguration/sourceControlConfigurations"
  ```

#### <a name="use-a-public-git-repo"></a>Używanie publicznego repozytorium git

| Parametr | Format |
| ------------- | ------------- |
| --Repository-URL | http [s]://Server/repo [. git] lub git://Server/repo [. git]

#### <a name="use-a-private-git-repo-with-ssh-and-flux-created-keys"></a>Korzystanie z prywatnego repozytorium git z użyciem kluczy SSH i strumieniowego tworzenia

| Parametr | Format | Uwagi
| ------------- | ------------- | ------------- |
| --Repository-URL | ssh://user@server/repo[. git] lub user@server:repo [. git] | `git@` może zastąpić `user@`

> [!NOTE]
> Klucz publiczny wygenerowany przez strumień musi zostać dodany do konta użytkownika w dostawcy usługi git. Jeśli klucz zostanie dodany do repozytorium, a nie > konto użytkownika, użyj `git@` zamiast `user@` adresu URL. [Wyświetl więcej szczegółów](#apply-configuration-from-a-private-git-repository)

#### <a name="use-a-private-git-repo-with-ssh-and-user-provided-keys"></a>Korzystanie z prywatnego repozytorium git z kluczami SSH i dostarczonymi przez użytkownika

| Parametr | Format | Uwagi |
| ------------- | ------------- | ------------- |
| --Repository-URL  | ssh://user@server/repo[. git] lub user@server:repo [. git] | `git@` może zastąpić `user@` |
| --SSH-Private-Key | klucz szyfrowany algorytmem Base64 w [formacie PEM](https://aka.ms/PEMformat) | Podaj klucz bezpośrednio |
| --SSH-Private-Key-File | Pełna ścieżka do pliku lokalnego | Podaj pełną ścieżkę do pliku lokalnego, który zawiera klucz w formacie PEM

> [!NOTE]
> Podaj własny klucz prywatny bezpośrednio lub w pliku. Klucz musi mieć [Format PEM](https://aka.ms/PEMformat) i kończyć się znakiem nowego wiersza (\n).  Skojarzony klucz publiczny należy dodać do konta użytkownika w dostawcy usługi git. Jeśli klucz zostanie dodany do repozytorium zamiast konta użytkownika, Użyj zamiast `git@` `user@` . [Wyświetl więcej szczegółów](#apply-configuration-from-a-private-git-repository)

#### <a name="use-a-private-git-host-with-ssh-and-user-provided-known-hosts"></a>Korzystanie z prywatnego hosta git z użyciem protokołów SSH i znanych przez użytkownika

| Parametr | Format | Uwagi |
| ------------- | ------------- | ------------- |
| --Repository-URL  | ssh://user@server/repo[. git] lub user@server:repo [. git] | `git@` może zastąpić `user@` |
| --znane-hosty SSH | kodowane algorytmem Base64 | Informacje o znanych hostach udostępnione bezpośrednio |
| --SSH-known-hosts-File | Pełna ścieżka do pliku lokalnego | znane hostowanie zawartości udostępnionej w pliku lokalnym

> [!NOTE]
> Operator strumień przechowuje listę typowych hostów Git w rozpoznawanym pliku hosts w celu uwierzytelnienia repozytorium git przed nawiązaniem połączenia SSH. Jeśli używasz nietypowego repozytorium Git lub własnego hosta git, może być konieczne podanie klucza hosta, aby upewnić się, że strumień może identyfikować repozytorium. Możesz podać swoją znaną zawartość hostów bezpośrednio lub w pliku. [Wyświetlanie specyfikacji formatu zawartości znane hosty](https://aka.ms/KnownHostsFormat).
> Można go użyć w połączeniu z jednym z opisanych powyżej scenariuszy protokołu SSH.

#### <a name="use-a-private-git-repo-with-https"></a>Korzystanie z prywatnego repozytorium git z protokołem HTTPS

| Parametr | Format | Uwagi |
| ------------- | ------------- | ------------- |
| --Repository-URL | https://server/repo[. git] | HTTPS z uwierzytelnianiem podstawowym |
| --https-User | nieprzetworzone lub zakodowane algorytmem Base64 | Nazwa użytkownika protokołu HTTPS |
| --https-Key | nieprzetworzone lub zakodowane algorytmem Base64 | Osobisty token dostępu HTTPS lub hasło

> [!NOTE]
> Prywatna autoryzacja wydania HTTPS Helm jest obsługiwana tylko z użyciem wykresu operatora Helm w wersji >= 1.2.0.  Wersja 1.2.0 jest używana domyślnie.
> Prywatne uwierzytelnianie w wersji Helm protokołu HTTPS nie jest obecnie obsługiwane w przypadku klastrów zarządzanych usług Azure Kubernetes Services.
> Jeśli potrzebujesz strumieniowego dostępu do repozytorium Git za pomocą serwera proxy, musisz zaktualizować agentów usługi Azure ARC przy użyciu ustawień serwera proxy. [Więcej informacji](https://docs.microsoft.com/azure/azure-arc/kubernetes/connect-cluster#connect-using-an-outbound-proxy-server)

#### <a name="additional-parameters"></a>Dodatkowe parametry

Aby dostosować konfigurację, poniżej przedstawiono więcej parametrów, których można użyć:

`--enable-helm-operator` : *Opcjonalny* przełącznik umożliwiający włączenie obsługi wdrożeń wykresów Helm.

`--helm-operator-params` : *Opcjonalne* wartości wykresu dla operatora Helm (jeśli włączone).  Na przykład '--Set Helm. Versions = v3 '.

`--helm-operator-chart-version` : *Opcjonalna* wersja wykresu dla operatora Helm (jeśli jest włączona). Wartość domyślna: "1.2.0".

`--operator-namespace` : *Opcjonalna* nazwa przestrzeni nazw operatora. Wartość domyślna: "default". Maksymalnie 23 znaki.

`--operator-params` : Parametry *opcjonalne* dla operatora. Musi być określona w cudzysłowie pojedynczym. Na przykład ```--operator-params='--git-readonly --git-path=releases --sync-garbage-collection' ```

Opcje obsługiwane w--operator-params

| Opcja | Opis |
| ------------- | ------------- |
| --git-branch  | Gałąź repozytorium git do użycia na potrzeby manifestów Kubernetes. Wartość domyślna to "Master". |
| --git-Path  | Ścieżka względna w repozytorium Git na potrzeby strumieniowego lokalizowania manifestów Kubernetes. |
| --git-ReadOnly | Repozytorium Git będzie uznawane za tylko do odczytu; Strumień nie będzie próbować zapisywać do niego. |
| --Manifest-Generation  | Jeśli ta funkcja jest włączona, strumień będzie szukać metadanych. strumień. YAML i Run Kustomize lub innych generatorów manifestów. |
| --git-sondowa-Interval  | Okres, w którym można sondować repozytorium git dotyczące nowych zatwierdzeń. Wartość domyślna to "5 m" (5 minut). |
| --Sync-Collector-Collection  | Jeśli ta funkcja jest włączona, strumień spowoduje usunięcie utworzonych przez siebie zasobów, ale nie są już dostępne w usłudze git. |
| --git-Label  | Etykieta, aby śledzić postęp synchronizacji, używany do tagowania gałęzi git.  Wartość domyślna to "strumień-Sync". |
| --git-User  | Nazwa użytkownika dla zatwierdzenia git. |
| --git-email  | Wiadomość e-mail do użycia na potrzeby zatwierdzenia git. |

* Jeśli nie ustawiono opcji "--Git-User" lub "--Git-email" (co oznacza, że nie chcesz mieć strumienia do zapisu w repozytorium), a następnie--plik git-ReadOnly zostanie automatycznie ustawiony (jeśli nie został jeszcze ustawiony).

Aby uzyskać więcej informacji, zobacz [Dokumentacja strumienia](https://aka.ms/FluxcdReadme).

> [!TIP]
> Istnieje możliwość utworzenia sourceControlConfiguration w Azure Portal na karcie **GitOps** zasobu Kubernetes z włączoną funkcją Azure Arc.

## <a name="validate-the-sourcecontrolconfiguration"></a>Weryfikowanie sourceControlConfiguration

Za pomocą interfejsu wiersza polecenia platformy Azure Sprawdź, czy `sourceControlConfiguration` został pomyślnie utworzony.

```console
az k8sconfiguration show --name cluster-config --cluster-name AzureArcTest1 --resource-group AzureArcTest --cluster-type connectedClusters
```

Należy pamiętać, że `sourceControlConfiguration` zasób jest aktualizowany ze stanem zgodności, komunikatami i informacjami o debugowaniu.

**Rozdzielczości**

```console
Command group 'k8sconfiguration' is in preview. It may be changed/removed in a future release.
{
  "complianceStatus": {
    "complianceState": "Installed",
    "lastConfigApplied": "2020-12-10T18:26:52.801000+00:00",
    "message": "...",
    "messageLevel": "Information"
  },
  "configurationProtectedSettings": {},
  "enableHelmOperator": false,
  "helmOperatorProperties": {
    "chartValues": "",
    "chartVersion": ""
  },
  "id": "/subscriptions/<sub id>/resourceGroups/AzureArcTest/providers/Microsoft.Kubernetes/connectedClusters/AzureArcTest1/providers/Microsoft.KubernetesConfiguration/sourceControlConfigurations/cluster-config",
  "name": "cluster-config",
  "operatorInstanceName": "cluster-config",
  "operatorNamespace": "cluster-config",
  "operatorParams": "--git-readonly",
  "operatorScope": "cluster",
  "operatorType": "Flux",
  "provisioningState": "Succeeded",
  "repositoryPublicKey": "...",
  "repositoryUrl": "git://github.com/Azure/arc-k8s-demo.git",
  "resourceGroup": "AzureArcTest",
  "sshKnownHostsContents": null,
  "systemData": {
    "createdAt": "2020-12-01T03:58:56.175674+00:00",
    "createdBy": null,
    "createdByType": null,
    "lastModifiedAt": "2020-12-10T18:30:56.881219+00:00",
    "lastModifiedBy": null,
    "lastModifiedByType": null
},
  "type": "Microsoft.KubernetesConfiguration/sourceControlConfigurations"
}
```

Gdy `sourceControlConfiguration` jest tworzony, kilka rzeczy odbywa się pod okapem:

1. Monitory usługi Azure Arc `config-agent` Azure Resource Manager dla nowych lub zaktualizowanych konfiguracji ( `Microsoft.KubernetesConfiguration/sourceControlConfigurations` )
1. `config-agent` Zauważ nową `Pending` konfigurację
1. `config-agent` Odczytuje właściwości konfiguracji i przygotowuje się do wdrożenia zarządzanego wystąpienia programu `flux`
    * `config-agent` tworzy docelowy obszar nazw
    * `config-agent` przygotowuje konto usługi Kubernetes z odpowiednimi uprawnieniami ( `cluster` lub `namespace` zakresem)
    * `config-agent` wdraża wystąpienie programu `flux`
    * `flux` generuje klucz SSH i rejestruje klucz publiczny (w przypadku korzystania z opcji SSH z kluczami generowanymi strumieniowo)
1. `config-agent` zgłasza stan z powrotem do `sourceControlConfiguration` zasobu na platformie Azure

Podczas procesu aprowizacji `sourceControlConfiguration` wystąpią pewne zmiany stanu. Monitoruj postęp przy użyciu `az k8sconfiguration show ...` powyższego polecenia:

1. `complianceStatus` -> `Pending`: reprezentuje Stany początkowe i w toku
1. `complianceStatus` -> `Installed`: udało `config-agent` się pomyślnie skonfigurować klaster i wdrożyć go `flux` bez błędu
1. `complianceStatus` -> `Failed`: `config-agent` Wystąpił błąd podczas wdrażania `flux` , szczegółowe informacje powinny być dostępne w `complianceStatus.message` treści odpowiedzi

## <a name="apply-configuration-from-a-private-git-repository"></a>Zastosuj konfigurację z prywatnego repozytorium git

Jeśli używasz prywatnego repozytorium git, musisz skonfigurować klucz publiczny SSH w repozytorium. Klucz publiczny można skonfigurować w odniesieniu do określonego repozytorium Git lub użytkownika git, który ma dostęp do repozytorium. Klucz publiczny SSH będzie taki sam, jak ty lub który generuje strumień.

**Pobierz swój własny klucz publiczny**

Jeśli wygenerowałeś własne klucze SSH, masz już klucze prywatne i publiczne.

**Pobierz klucz publiczny przy użyciu interfejsu wiersza polecenia platformy Azure (przydatne, jeśli strumień generuje klucze)**

```console
$ az k8sconfiguration show --resource-group <resource group name> --cluster-name <connected cluster name> --name <configuration name> --cluster-type connectedClusters --query 'repositoryPublicKey' 
Command group 'k8sconfiguration' is in preview. It may be changed/removed in a future release.
"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAREDACTED"
```

**Pobierz klucz publiczny z Azure Portal (przydatne, jeśli strumień generuje klucze)**

1. W Azure Portal przejdź do zasobu połączonego klastra.
2. Na stronie zasób wybierz pozycję "GitOps" i sprawdź listę konfiguracji dla tego klastra.
3. Wybierz konfigurację, która używa prywatnego repozytorium git.
4. W otwartym oknie kontekstu w dolnej części okna Skopiuj **klucz publiczny repozytorium**.

Jeśli używasz usługi GitHub, użyj jednej z następujących dwóch opcji:

**Opcja 1: Dodawanie klucza publicznego do konta użytkownika (dotyczy wszystkich repozytoriów na Twoim koncie)**

1. Otwórz witrynę GitHub, kliknij ikonę profilu w prawym górnym rogu strony.
2. Kliknij pozycję **Ustawienia**
3. Kliknij **klucze SSH i GPG**
4. Kliknij **nowy klucz SSH**
5. Podaj tytuł
6. Wklej klucz publiczny (bez cudzysłowów)
7. Kliknij pozycję **Dodaj klucz SSH**

**Opcja 2: Dodaj klucz publiczny jako klucz wdrożenia do repozytorium git (dotyczy tylko tego repozytorium)**

1. Otwórz witrynę GitHub, przejdź do repozytorium, kliknij pozycję **Ustawienia**, a następnie pozycję **Wdróż klucze** .
2. Kliknij pozycję **Dodaj klucz wdrożenia**
3. Podaj tytuł
4. Sprawdź **Zezwalanie na dostęp do zapisu**
5. Wklej klucz publiczny (bez cudzysłowów)
6. Kliknij pozycję **Dodaj klucz**

**Jeśli używasz repozytorium usługi Azure DevOps, Dodaj klucz do kluczy SSH**

1. W obszarze **Ustawienia użytkownika** w prawym górnym rogu (obok obrazu profilu) kliknij pozycję **klucze publiczne SSH**
1. Wybierz pozycję  **+ nowy klucz**
1. Podaj nazwę
1. Wklej klucz publiczny bez żadnych otaczających cudzysłowów
1. Kliknij przycisk **Dodaj**

## <a name="validate-the-kubernetes-configuration"></a>Weryfikowanie konfiguracji Kubernetes

Po `config-agent` zainstalowaniu wystąpienia zasoby, które znajdują się `flux` w repozytorium git, powinny zacząć przepływać do klastra. Sprawdź, czy zostały utworzone obszary nazw, wdrożenia i zasoby:

```console
kubectl get ns --show-labels
```

**Rozdzielczości**

```console
NAME              STATUS   AGE    LABELS
azure-arc         Active   24h    <none>
cluster-config    Active   177m   <none>
default           Active   29h    <none>
itops             Active   177m   fluxcd.io/sync-gc-mark=sha256.9oYk8yEsRwWkR09n8eJCRNafckASgghAsUWgXWEQ9es,name=itops
kube-node-lease   Active   29h    <none>
kube-public       Active   29h    <none>
kube-system       Active   29h    <none>
team-a            Active   177m   fluxcd.io/sync-gc-mark=sha256.CS5boSi8kg_vyxfAeu7Das5harSy1i0gc2fodD7YDqA,name=team-a
team-b            Active   177m   fluxcd.io/sync-gc-mark=sha256.vF36thDIFnDDI2VEttBp5jgdxvEuaLmm7yT_cuA2UEw,name=team-b
```

Możemy zobaczyć, że `team-a` zostały `team-b` `itops` `cluster-config` utworzone przestrzenie nazw,,, i.

Ten `flux` operator został wdrożony w `cluster-config` przestrzeni nazw, co zostało przekazane przez nasz `sourceControlConfig` :

```console
kubectl -n cluster-config get deploy  -o wide
```

**Rozdzielczości**

```console
NAME             READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES                         SELECTOR
cluster-config   1/1     1            1           3h    flux         docker.io/fluxcd/flux:1.16.0   instanceName=cluster-config,name=flux
memcached        1/1     1            1           3h    memcached    memcached:1.5.15               name=memcached
```

## <a name="further-exploration"></a>Dalsza eksploracja

Inne zasoby wdrożone w ramach repozytorium konfiguracji można eksplorować:

```console
kubectl -n team-a get cm -o yaml
kubectl -n itops get all
```

## <a name="delete-a-configuration"></a>Usuń konfigurację

Usuń `sourceControlConfiguration` przy użyciu interfejsu wiersza polecenia platformy Azure lub Azure Portal.  Po zainicjowaniu polecenia Usuń `sourceControlConfiguration` zasób zostanie natychmiast usunięty na platformie Azure, a pełne usunięcie skojarzonych z nim obiektów powinno wystąpić w ciągu 10 minut.  Jeśli `sourceControlConfiguration` stan jest w stanie niepowodzenia po jego usunięciu, pełne usunięcie skojarzonych obiektów może potrwać do godziny.

> [!NOTE]
> Po utworzeniu sourceControlConfiguration z zakresem przestrzeni nazw istnieje możliwość, że użytkownicy z `edit` powiązaniem roli w przestrzeni nazw mają wdrażać obciążenia w tej przestrzeni nazw. Gdy ten `sourceControlConfiguration` zakres przestrzeni nazw zostanie usunięty, przestrzeń nazw pozostaje nienaruszona i nie zostanie usunięta, aby uniknąć przerywania tych obciążeń.  W razie konieczności można ręcznie usunąć tę przestrzeń nazw z polecenia kubectl.
> Wszelkie zmiany w klastrze, które były wynikiem wdrożeń z śledzonego repozytorium git, nie są usuwane po `sourceControlConfiguration` usunięciu.

```console
az k8sconfiguration delete --name cluster-config --cluster-name AzureArcTest1 --resource-group AzureArcTest --cluster-type connectedClusters
```

**Rozdzielczości**

```console
Command group 'k8sconfiguration' is in preview. It may be changed/removed in a future release.
```

## <a name="next-steps"></a>Następne kroki

- [Użyj Helm z konfiguracją kontroli źródła](./use-gitops-with-helm.md)
- [Zarządzanie konfiguracją klastra przy użyciu Azure Policy](./use-azure-policy.md)
