---
title: Jednostki wystąpień BareMetal na platformie Azure
description: Dowiedz się, jak identyfikować jednostki wystąpień BareMetal i korzystać z nich za pomocą Azure Portal.
ms.topic: how-to
ms.date: 1/4/2021
ms.openlocfilehash: 30e1661e82546dbaf6d8dc4288ad896df89f401e
ms.sourcegitcommit: aeba98c7b85ad435b631d40cbe1f9419727d5884
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/04/2021
ms.locfileid: "97861032"
---
# <a name="manage-baremetal-instances-through-the-azure-portal"></a>Zarządzanie wystąpieniami BareMetal za pomocą witryny Azure Portal
 
W tym artykule pokazano, jak [Azure Portal](https://portal.azure.com/) są wyświetlane [wystąpienia BareMetal](baremetal-overview-architecture.md). W tym artykule przedstawiono również czynności, które można wykonać w Azure Portal ze wdrożonymi jednostkami wystąpienia BareMetal. 
 
## <a name="register-the-resource-provider"></a>Rejestrowanie dostawcy zasobów
Dostawca zasobów platformy Azure dla wystąpień BareMetal zapewnia widoczność wystąpień w Azure Portal, obecnie w publicznej wersji zapoznawczej. Domyślnie subskrypcja platformy Azure używana dla wdrożeń wystąpień BareMetal rejestruje dostawcę zasobów *BareMetalInfrastructure* . Jeśli nie widzisz wdrożonych jednostek wystąpienia usługi BareMetal, musisz zarejestrować dostawcę zasobów w ramach subskrypcji. 

Istnieją dwa sposoby rejestrowania dostawcy zasobów wystąpienia BareMetal:
 
* [Interfejs wiersza polecenia platformy Azure](#azure-cli)
 
* [Witryna Azure Portal](#azure-portal)
 
### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
 
Zaloguj się do subskrypcji platformy Azure, która jest używana na potrzeby wdrożenia wystąpienia BareMetal za pomocą interfejsu wiersza polecenia platformy Azure. Dostawcę zasobów BareMetalInfrastructure można zarejestrować przy użyciu:

```azurecli-interactive
az provider register --namespace Microsoft.BareMetalInfrastructure
```
 
Aby uzyskać więcej informacji, zobacz artykuł [dostawcy zasobów platformy Azure i ich typy](../../../azure-resource-manager/management/resource-providers-and-types.md#azure-powershell).
 
### <a name="azure-portal"></a>Azure Portal
 
Dostawcę zasobów BareMetalInfrastructure można zarejestrować za pomocą Azure Portal.
 
Musisz wyświetlić swoją subskrypcję w Azure Portal a następnie kliknąć dwukrotnie subskrypcję używaną do wdrożenia jednostek wystąpienia usługi BareMetal.
 
1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).

1. W menu witryny Azure Portal wybierz pozycję **Wszystkie usługi**.

1. W polu **wszystkie usługi** wprowadź **subskrypcję**, a następnie wybierz pozycję **subskrypcje**.

1. Wybierz subskrypcję z listy subskrypcji do wyświetlenia.

1. Wybierz pozycję **dostawcy zasobów** i wprowadź **BareMetalInfrastructure** w polu wyszukiwania. Dostawca zasobów powinien być **zarejestrowany**, ponieważ obraz pokazuje.
 
>[!NOTE]
>Jeśli dostawca zasobów nie jest zarejestrowany, wybierz pozycję **zarejestruj**.
 
:::image type="content" source="media/baremetal-infrastructure-portal/register-resource-provider-azure-portal.png" alt-text="Zrzut ekranu pokazujący zarejestrowaną jednostkę wystąpienia BareMetal":::
 
## <a name="baremetal-instance-units-in-the-azure-portal"></a>Jednostki wystąpienia BareMetal w Azure Portal
 
Po przesłaniu żądania wdrożenia wystąpienia BareMetal należy określić subskrypcję platformy Azure, która nawiązuje połączenie z wystąpieniami BareMetal. Użyj tej samej subskrypcji, która jest używana do wdrażania warstwy aplikacji, która działa w odniesieniu do jednostek wystąpienia BareMetal.
 
Podczas wdrażania wystąpień usługi BareMetal zostanie utworzona nowa [Grupa zasobów platformy Azure](../../../azure-resource-manager/management/manage-resources-portal.md) w ramach subskrypcji platformy Azure użytej w żądaniu wdrożenia. Ta nowa grupa zasobów zawiera listę wszystkich jednostek wystąpienia usługi BareMetal, które zostały wdrożone w określonej subskrypcji.

1. W subskrypcji BareMetal w Azure Portal wybierz pozycję **grupy zasobów**.
 
   :::image type="content" source="media/baremetal-infrastructure-portal/view-baremetal-instance-units-azure-portal.png" alt-text="Zrzut ekranu przedstawiający listę grup zasobów":::

1. Zlokalizuj nową grupę zasobów na liście.
 
   :::image type="content" source="media/baremetal-infrastructure-portal/filter-resource-groups.png" alt-text="Zrzut ekranu pokazujący jednostkę wystąpienia BareMetal na liście filtrowanych grup zasobów" lightbox="media/baremetal-infrastructure-portal/filter-resource-groups.png":::
   
   >[!TIP]
   >Można filtrować według subskrypcji użytej do wdrożenia wystąpienia usługi BareMetal. Po przefiltrowaniu do odpowiedniej subskrypcji może istnieć długa lista grup zasobów. Poszukaj jednego z **TXXX** , gdzie xxx to trzy cyfry, takie jak **-T250**.

1. Wybierz nową grupę zasobów, aby wyświetlić jej szczegóły. Obraz przedstawia jedną wdrożoną jednostkę wystąpienia BareMetal.
   
   >[!NOTE]
   >Jeśli w ramach tej samej subskrypcji platformy Azure wdrożono kilka dzierżawców wystąpień BareMetal, zobaczysz wiele grup zasobów platformy Azure.
 
## <a name="view-the-attributes-of-a-single-instance"></a>Wyświetlanie atrybutów pojedynczego wystąpienia
 
Można wyświetlić szczegóły pojedynczej jednostki. Na liście wystąpienia BareMetal wybierz pojedyncze wystąpienie, które chcesz wyświetlić.
 
:::image type="content" source="media/baremetal-infrastructure-portal/view-attributes-single-baremetal-instance.png" alt-text="Zrzut ekranu pokazujący atrybuty jednostki wystąpienia BareMetal pojedynczego wystąpienia" lightbox="media/baremetal-infrastructure-portal/view-attributes-single-baremetal-instance.png":::
 
Atrybuty w obrazie różnią się od atrybutów maszyny wirtualnej platformy Azure. Po lewej stronie zobaczysz grupę zasobów, region platformy Azure oraz nazwę i Identyfikator subskrypcji. Jeśli masz przypisane znaczniki, zobaczysz je tutaj. Domyślnie jednostki wystąpienia BareMetal nie mają przypisanych tagów.
 
Po prawej stronie zobaczysz nazwę jednostki, system operacyjny, adres IP i jednostkę SKU, która pokazuje liczbę wątków procesora CPU i pamięci. Zobaczysz również stan zasilacza i wersja sprzętowa (poprawka sygnatury wystąpienia BareMetal). Stan zasilania wskazuje, czy jednostka sprzętowa jest włączona, czy wyłączona. Jednak szczegóły systemu operacyjnego nie wskazują, czy jest on uruchomiony.
 
Możliwe wersje sprzętu to:

* Poprawka 3 (rev 3)

* Poprawka 4 (rev 4)
 
* Poprawka 4,2 (rev 4,2)
 
>[!NOTE]
>Rev 4,2 to najnowsza BareMetal infrastruktura z wykorzystaniem istniejącej architektury rev 4. Rev 4 zapewnia bliższą bliskość hostom maszyn wirtualnych platformy Azure. W przypadku opóźnień sieci między maszynami wirtualnymi platformy Azure i jednostkami wystąpienia BareMetal wdrożonymi w znacznikach lub wierszach z 4. Możesz uzyskać dostęp do wystąpień BareMetal i zarządzać nimi za pomocą Azure Portal. Aby uzyskać więcej informacji, zobacz [infrastruktura BareMetal na platformie Azure](baremetal-overview-architecture.md).
 
Ponadto po prawej stronie znajduje się nazwa [grupy umieszczania usługi Azure zbliżeniowe](../../../virtual-machines/linux/co-location.md) , która jest tworzona automatycznie dla każdej wdrożonej jednostki wystąpienia BareMetal. Odwołuje się do grupy położenia zbliżeniowe podczas wdrażania maszyn wirtualnych platformy Azure, które obsługują warstwę aplikacji. W przypadku korzystania z grupy umieszczania zbliżeniowe skojarzonej z jednostką wystąpienia BareMetal upewnij się, że maszyny wirtualne platformy Azure zostaną wdrożone blisko jednostki wystąpienia BareMetal.
 
>[!TIP]
>Aby zlokalizować warstwę aplikacji w tym samym centrum danych platformy Azure w wersji 4. x, zobacz [grupy umieszczania zbliżeniowe platformy Azure w celu uzyskania optymalnego opóźnienia sieci](../../../virtual-machines/workloads/sap/sap-proximity-placement-scenarios.md).
 
## <a name="check-activities-of-a-single-instance"></a>Sprawdź działania pojedynczego wystąpienia
 
Możesz sprawdzić działania pojedynczej jednostki. Jednym z głównych działań zarejestrowanych jest ponowne uruchomienie jednostki. Wymienione dane obejmują stan działania, sygnaturę czasową wyzwalane przez działanie, Identyfikator subskrypcji i użytkownika platformy Azure, który wyzwolił działanie.
 
:::image type="content" source="media/baremetal-infrastructure-portal/check-activities-single-baremetal-instance.png" alt-text="Zrzut ekranu przedstawiający działania jednostki wystąpienia BareMetal" lightbox="media/baremetal-infrastructure-portal/check-activities-single-baremetal-instance.png":::
 
Zmiany metadanych jednostki na platformie Azure są również rejestrowane w dzienniku aktywności. Oprócz zainicjowanego ponownego uruchomienia można zobaczyć działanie **BareMetallnstances zapisu**. To działanie nie wprowadza żadnych zmian w jednostce wystąpienia BareMetal, ale dokumentuje zmiany w metadanych jednostki na platformie Azure.
 
Po dodaniu lub usunięciu [znacznika](../../../azure-resource-manager/management/tag-resources.md) do wystąpienia jest możliwe inne działanie, które jest rejestrowane.
 
## <a name="add-and-delete-an-azure-tag-to-an-instance"></a>Dodawanie i usuwanie tagu platformy Azure do wystąpienia
 
Możesz dodać tagi platformy Azure do jednostki wystąpienia BareMetal lub usunąć je. Sposób przypisywania tagów nie różni się od przypisywania tagów do maszyn wirtualnych. Podobnie jak w przypadku maszyn wirtualnych, znaczniki istnieją w metadanych platformy Azure, a dla wystąpień BareMetal mają takie same ograniczenia jak Tagi maszyn wirtualnych.
 
Usuwanie tagów działają tak samo jak w przypadku maszyn wirtualnych. Stosowanie i usuwanie tagu są wymienione w dzienniku aktywności jednostki wystąpienia BareMetal.
 
## <a name="check-properties-of-an-instance"></a>Sprawdź właściwości wystąpienia
 
Po uzyskaniu wystąpień możesz przejść do sekcji właściwości, aby wyświetlić zebrane dane o wystąpieniach. Zebrane dane obejmują łączność z platformą Azure, zaplecze magazynu, Identyfikator obwodu ExpressRoute, unikatowy identyfikator zasobu i Identyfikator subskrypcji. Te informacje będą używane w żądaniach obsługi lub podczas konfigurowania konfiguracji migawki magazynu.
 
Inną krytyczną informacją, która widzisz, jest adres IP magazynu NFS. Izoluje on magazyn do **dzierżawy** w stosie wystąpienia BareMetal. Ten adres IP będzie używany podczas edytowania [pliku konfiguracji kopii zapasowych migawek magazynu](../../../virtual-machines/workloads/sap/hana-backup-restore.md#set-up-storage-snapshots).
 
:::image type="content" source="media/baremetal-infrastructure-portal/baremetal-instance-properties.png" alt-text="Zrzut ekranu pokazujący ustawienia właściwości wystąpienia BareMetal" lightbox="media/baremetal-infrastructure-portal/baremetal-instance-properties.png":::
 
## <a name="restart-a-unit-through-the-azure-portal"></a>Uruchom ponownie jednostkę za pomocą Azure Portal
 
Istnieją różne sytuacje, w których system operacyjny nie kończy ponownego uruchamiania, co wymaga ponownego uruchomienia urządzenia w jednostce wystąpienia BareMetal. Możesz ponownie uruchomić jednostkę bezpośrednio z Azure Portal:
 
Wybierz pozycję **Uruchom ponownie** , a następnie przycisk **tak** , aby potwierdzić ponowne uruchomienie jednostki.
 
:::image type="content" source="media/baremetal-infrastructure-portal/baremetal-instance-restart.png" alt-text="Zrzut ekranu pokazujący sposób ponownego uruchomienia jednostki wystąpienia BareMetal":::
 
Po ponownym uruchomieniu jednostki wystąpienia BareMetal wystąpi opóźnienie. W tym opóźnieniu stan siły jest przenoszony od **początku** do **uruchomionego**, co oznacza, że system operacyjny został całkowicie uruchomiony. W związku z tym po ponownym uruchomieniu nie można zalogować się do jednostki, gdy tylko stan zostanie **uruchomiony**.
 
>[!IMPORTANT]
>W zależności od ilości pamięci w jednostce wystąpienia BareMetal ponowne uruchomienie i ponowne uruchomienie sprzętu i systemu operacyjnego może trwać do godziny.
 
## <a name="open-a-support-request-for-baremetal-instances"></a>Otwórz żądanie obsługi dla wystąpień usługi BareMetal
 
Można przesłać żądania pomocy technicznej przeznaczone dla jednostki wystąpienia BareMetal.
1. W Azure Portal, w obszarze **Pomoc i obsługa techniczna**, Utwórz **[nowe żądanie pomocy technicznej](https://rc.portal.azure.com/#create/Microsoft.Support)** i podaj następujące informacje dotyczące biletu:
 
   - **Typ problemu:** Wybierz typ problemu
 
   - **Subskrypcja:** Wybierz swoją subskrypcję
 
   - **Usługa:** Infrastruktura BareMetal
 
   - **Zasób:** Podaj nazwę wystąpienia
 
   - **Podsumowanie:** Podaj podsumowanie żądania
 
   - **Typ problemu:** Wybierz typ problemu
 
   - **Podtyp problemu:** Wybierz podtyp dla problemu

1. Wybierz kartę **rozwiązania** , aby znaleźć rozwiązanie problemu. Jeśli nie możesz znaleźć rozwiązania, przejdź do następnego kroku.

1. Wybierz kartę **szczegóły** , a następnie wybierz, czy problem dotyczy maszyn wirtualnych czy jednostek wystąpienia BareMetal. Te informacje ułatwiają kierowanie prośby o pomoc techniczną do właściwych specjalistów.

1. Wskaż, kiedy problem pojawił się i wybierz region wystąpienia.

1. Podaj więcej szczegółowych informacji o żądaniu i Przekaż plik w razie konieczności.

1. Wybierz pozycję **Przegląd + Utwórz** , aby przesłać żądanie.
 
Potwierdzenie Twojego wniosku może potrwać do pięciu dni roboczych.

## <a name="next-steps"></a>Następne kroki

Jeśli chcesz dowiedzieć się więcej o obciążeniach, zobacz [typy obciążeń BareMetal](../../../virtual-machines/workloads/sap/get-started.md).