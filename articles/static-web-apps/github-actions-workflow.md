---
title: Przepływy pracy akcji GitHub dla Web Apps statycznej platformy Azure
description: Dowiedz się, jak za pomocą repozytoriów usługi GitHub skonfigurować ciągłe wdrażanie w usłudze Azure static Web Apps.
services: static-web-apps
author: craigshoemaker
ms.service: static-web-apps
ms.topic: conceptual
ms.date: 05/08/2020
ms.author: cshoe
ms.openlocfilehash: 5e6188ca2e8e0972e86bed578144a29a96570876
ms.sourcegitcommit: 5e762a9d26e179d14eb19a28872fb673bf306fa7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2021
ms.locfileid: "97901202"
---
# <a name="github-actions-workflows-for-azure-static-web-apps-preview"></a>Przepływy pracy akcji GitHub dla usługi Azure static Web Apps Preview

Podczas tworzenia nowego zasobu statycznej aplikacji sieci Web platformy Azure Program Azure generuje przepływ pracy akcji GitHub, który umożliwia kontrolowanie ciągłego wdrażania aplikacji. Przepływ pracy jest oparty na pliku YAML. Ten artykuł zawiera szczegółowe informacje dotyczące struktury i opcji pliku przepływu pracy.

Wdrożenia są inicjowane przez [wyzwalacze](#triggers), które uruchamiają [zadania](#jobs) zdefiniowane przez poszczególne [etapy](#steps).

## <a name="file-location"></a>Lokalizacja pliku

Po połączeniu repozytorium GitHub z usługą Azure static Web Apps do repozytorium zostanie dodany plik przepływu pracy.

Wykonaj następujące kroki, aby wyświetlić wygenerowany plik przepływu pracy.

1. Otwórz repozytorium aplikacji w serwisie GitHub.
1. Na karcie _kod_ kliknij `.github/workflows` folder.
1. Kliknij plik o nazwie, która wygląda podobnie `azure-static-web-apps-<RANDOM_NAME>.yml` .

Plik YAML w repozytorium będzie wyglądać podobnie do poniższego przykładu:

```yml
name: Azure Static Web Apps CI/CD

on:
  push:
    branches:
    - master
  pull_request:
    types: [opened, synchronize, reopened, closed]
    branches:
    - master

jobs:
  build_and_deploy_job:
    if: github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed')
    runs-on: ubuntu-latest
    name: Build and Deploy Job
    steps:
    - uses: actions/checkout@v2
      with:
        submodules: true
    - name: Build And Deploy
      id: builddeploy
      uses: Azure/static-web-apps-deploy@v0.0.1-preview
      with:
        azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_MANGO_RIVER_0AFDB141E }}
        repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for GitHub integrations (i.e. PR comments)
        action: 'upload'
        ###### Repository/Build Configurations - These values can be configured to match you app requirements. ######
        app_location: '/' # App source code path
        api_location: 'api' # Api source code path - optional
        output_location: 'dist' # Built app content directory - optional
        ###### End of Repository/Build Configurations ######

  close_pull_request_job:
    if: github.event_name == 'pull_request' && github.event.action == 'closed'
    runs-on: ubuntu-latest
    name: Close Pull Request Job
    steps:
    - name: Close Pull Request
      id: closepullrequest
      uses: Azure/static-web-apps-deploy@v0.0.1-preview
      with:
        azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_MANGO_RIVER_0AFDB141E }}
        action: 'close'
```

## <a name="triggers"></a>Wyzwalacze

[Wyzwalacz](https://help.github.com/actions/reference/events-that-trigger-workflows) akcji usługi GitHub powiadamia przepływ pracy z akcjami usługi GitHub w celu uruchomienia zadań opartych na wyzwalaczach zdarzeń. Wyzwalacze są wyświetlane przy użyciu `on` właściwości w pliku przepływu pracy.

```yml
on:
  push:
    branches:
    - master
  pull_request:
    types: [opened, synchronize, reopened, closed]
    branches:
    - master
```

Za pomocą ustawień skojarzonych z `on` właściwością można zdefiniować gałęzie wyzwalające zadanie i ustawić wyzwalacze do uruchamiania dla różnych stanów żądań ściągnięcia.

W tym przykładzie przepływ pracy jest uruchamiany w miarę zmiany gałęzi _głównej_ . Zmiany rozpoczynające przepływ pracy obejmują wypychanie zatwierdzeń i otwieranie żądań ściągnięcia względem wybranej gałęzi.

## <a name="jobs"></a>Stanowiska

Każdy wyzwalacz zdarzenia wymaga programu obsługi zdarzeń. [Zadania](https://help.github.com/actions/reference/workflow-syntax-for-github-actions#jobs) definiują, co się dzieje w przypadku wyzwolenia zdarzenia.

W pliku statycznego przepływu pracy Web Apps są dostępne dwa zadania.

| Nazwa  | Opis |
|---------|---------|
|`build_and_deploy_job` | Wykonuje się w przypadku wypychania zatwierdzeń lub otwarcia żądania ściągnięcia względem gałęzi wymienionej we `on` właściwości. |
|`close_pull_request_job` | Wykonuje tylko po zamknięciu żądania ściągnięcia, które usuwa środowisko przejściowe utworzone na podstawie żądań ściągnięcia. |

## <a name="steps"></a>Kroki

Kroki są zadaniami sekwencyjnymi dla zadania. Krok wykonuje akcje, takie jak instalowanie zależności, uruchamianie testów i wdrażanie aplikacji w środowisku produkcyjnym.

Plik przepływu pracy definiuje następujące kroki.

| Zadanie  | Kroki  |
|---------|---------|
| `build_and_deploy_job` |<ol><li>Sprawdza repozytorium w środowisku działania.<li>Kompiluje i wdraża repozytorium w usłudze Azure static Web Apps.</ol>|
| `close_pull_request_job` | <ol><li>Powiadamia Web Apps statycznej platformy Azure o zamknięciu żądania ściągnięcia.</ol>|

## <a name="build-and-deploy"></a>Tworzenie i wdrażanie

Krok o nazwie `Build and Deploy` builds i Deploys w wystąpieniu usługi Azure Static Web Apps. W `with` sekcji można dostosować następujące wartości dla danego wdrożenia.

```yml
with:
    azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_MANGO_RIVER_0AFDB141E }}
    repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for GitHub integrations (i.e. PR comments)
    action: 'upload'
    ###### Repository/Build Configurations - These values can be configured to match you app requirements. ######
    app_location: '/' # App source code path
    api_location: 'api' # Api source code path - optional
    output_location: 'dist' # Built app content directory - optional
    ###### End of Repository/Build Configurations ######
```

| Właściwość | Opis | Wymagane |
|---|---|---|
| `app_location` | Lokalizacja kodu aplikacji.<br><br>Na przykład wprowadź, `/` czy kod źródłowy aplikacji znajduje się w katalogu głównym repozytorium, czy `/app` kod aplikacji znajduje się w katalogu o nazwie `app` . | Tak |
| `api_location` | Lokalizacja kodu Azure Functions.<br><br>Na przykład wprowadź, `/api` czy kod aplikacji znajduje się w folderze o nazwie `api` . Jeśli w folderze nie zostanie wykryta żadna aplikacja Azure Functions, kompilacja nie powiedzie się, a przepływ pracy zakłada, że nie potrzebujesz interfejsu API. | Nie |
| `output_location` | Lokalizacja katalogu wyjściowego kompilacji względem `app_location` .<br><br>Na przykład, jeśli kod źródłowy aplikacji znajduje się w lokalizacji `/app` i skrypt kompilacji wyprowadza pliki do `/app/build` folderu, a następnie ustawi `build` jako `output_location` wartość. | Nie |

`repo_token`Wartości, `action` , i `azure_static_web_apps_api_token` są ustawiane przez statyczne Web Apps platformy Azure, nie powinny być ręcznie zmieniane.

## <a name="custom-build-commands"></a>Niestandardowe polecenia kompilacji

Możesz mieć precyzyjną kontrolę nad tym, jakie polecenia są uruchamiane podczas wdrażania. Poniższe polecenia można zdefiniować w `with` sekcji zadania.

Wdrożenie zawsze wywołuje `npm install` przed dowolnym poleceniem niestandardowym.

| Polecenie            | Opis |
|---------------------|-------------|
| `app_build_command` | Definiuje niestandardowe polecenie do uruchomienia podczas wdrażania aplikacji zawartości statycznej.<br><br>Na przykład, aby skonfigurować kompilację produkcyjną dla aplikacji kątowej, należy utworzyć skrypt npm o nazwie `build-prod` do uruchomienia `ng build --prod` i wprowadzić `npm run build-prod` jako polecenie niestandardowe. Jeśli pole pozostanie puste, przepływ pracy próbuje `npm run build` uruchomić `npm run build:Azure` polecenia lub.  |
| `api_build_command` | Definiuje niestandardowe polecenie do uruchomienia podczas wdrażania aplikacji interfejsu API Azure Functions. |

## <a name="route-file-location"></a>Lokalizacja pliku tras

Możesz dostosować przepływ pracy, aby wyszukać [routes.js](routes.md) w dowolnym folderze w repozytorium. Poniższe właściwości można zdefiniować w `with` sekcji zadania.

| Właściwość            | Opis |
|---------------------|-------------|
| `routes_location` | Określa lokalizację katalogu, w którym znajduje się _routes.js_ pliku. Ta lokalizacja jest określana względem katalogu głównego repozytorium. |

 Jawne informacje o lokalizacji _routes.jsw_ pliku są szczególnie ważne, jeśli krok kompilacji platformy frontonu nie przenosi tego pliku do `output_location` domyślnego.

## <a name="environment-variables"></a>Zmienne środowiskowe

Można ustawić zmienne środowiskowe dla kompilacji za pośrednictwem `env` sekcji konfiguracji zadania.

```yaml
jobs:
  build_and_deploy_job:
    if: github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed')
    runs-on: ubuntu-latest
    name: Build and Deploy Job
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true
      - name: Build And Deploy
        id: builddeploy
        uses: Azure/static-web-apps-deploy@v0.0.1-preview
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}
          repo_token: ${{ secrets.GITHUB_TOKEN }}
          action: "upload"
          ###### Repository/Build Configurations
          app_location: "/"
          api_location: "api"
          output_location: "public"
          ###### End of Repository/Build Configurations ######
        env: # Add environment variables here
          HUGO_VERSION: 0.58.0
```

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Przeglądanie żądań ściągnięcia w środowiskach przedprodukcyjnych](review-publish-pull-requests.md)
