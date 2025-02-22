---
title: Jak używać nazwanych wartości w zasadach usługi Azure API Management
description: Dowiedz się, jak używać nazwanych wartości w zasadach usługi Azure API Management. Nazwane wartości mogą zawierać ciągi literałów, wyrażenia zasad i wpisy tajne przechowywane w Azure Key Vault.
services: api-management
documentationcenter: ''
author: vladvino
ms.service: api-management
ms.topic: article
ms.date: 12/14/2020
ms.author: apimpm
ms.openlocfilehash: 4cde4dadee33ec1c3f91ab4770dbfe697289cef3
ms.sourcegitcommit: 2ba6303e1ac24287762caea9cd1603848331dd7a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2020
ms.locfileid: "97504736"
---
# <a name="use-named-values-in-azure-api-management-policies"></a>Używanie nazwanych wartości w zasadach usługi Azure API Management

[Zasady API Management](api-management-howto-policies.md) są zaawansowaną funkcją systemu, która umożliwia wydawcy zmianę zachowania interfejsu API za pomocą konfiguracji. Zasady to zbiór instrukcji, które są wykonywane sekwencyjnie podczas żądania lub odpowiedzi interfejsu API. Instrukcje zasad można utworzyć przy użyciu literałów wartości tekstowych, wyrażeń zasad i nazwanych wartości.

*Nazwane wartości* to globalna kolekcja par nazwa/wartość w każdym wystąpieniu API Management. Nie ma żadnego narzuconego limitu liczby elementów w kolekcji. Nazwane wartości mogą służyć do zarządzania stałymi wartościami ciągów i wpisami tajnymi w ramach wszystkich konfiguracji i zasad interfejsu API. 

:::image type="content" source="media/api-management-howto-properties/named-values.png" alt-text="Nazwane wartości w Azure Portal":::

## <a name="value-types"></a>Typy wartości

|Typ  |Opis  |
|---------|---------|
|Zwykły     |  Ciąg literału lub wyrażenie zasad     |
|Wpis tajny     |   Ciąg literału lub wyrażenie zasad, które są szyfrowane przez API Management      |
|[Magazyn kluczy](#key-vault-secrets)     |  Identyfikator wpisu tajnego przechowywanego w magazynie kluczy platformy Azure.      |

Zwykłe wartości lub wpisy tajne mogą zawierać [wyrażenia zasad](./api-management-policy-expressions.md). Na przykład wyrażenie `@(DateTime.Now.ToString())` zwraca ciąg zawierający bieżącą datę i godzinę.

Szczegółowe informacje o nazwanych atrybutach wartości można znaleźć w [dokumentacji interfejsu API REST](/rest/api/apimanagement/2020-06-01-preview/namedvalue/createorupdate)API Management.

## <a name="key-vault-secrets"></a>Wpisy tajne magazynu kluczy

Wartości tajne mogą być przechowywane jako zaszyfrowane ciągi w API Management (niestandardowe klucze tajne) lub poprzez odwoływanie się do wpisów tajnych w [Azure Key Vault](../key-vault/general/overview.md). 

Zaleca się używanie wpisów tajnych magazynu kluczy, ponieważ ułatwia to poprawę zabezpieczeń API Management:

* Wpisy tajne przechowywane w magazynach kluczy mogą być ponownie używane przez usługi
* Szczegółowe [zasady dostępu](../key-vault/general/secure-your-key-vault.md#data-plane-and-access-policies) można stosować do wpisów tajnych
* Wpisy tajne zaktualizowane w magazynie kluczy są automatycznie obracane w API Management. Po aktualizacji w magazynie kluczy nazwana wartość w API Management jest aktualizowana w ciągu 4 godzin. 

### <a name="prerequisites-for-key-vault-integration"></a>Wymagania wstępne dotyczące integracji magazynu kluczy

1. Aby uzyskać instrukcje dotyczące tworzenia magazynu kluczy, zobacz [Szybki Start: Tworzenie magazynu kluczy przy użyciu Azure Portal](../key-vault/general/quick-create-portal.md).
1. Włącz [tożsamość zarządzaną](api-management-howto-use-managed-service-identity.md) przez system lub przypisanej przez użytkownika w wystąpieniu API Management.
1. Przypisz do zarządzanej tożsamości [zasady dostępu do magazynu kluczy](../key-vault/general/assign-access-policy-portal.md) z uprawnieniami do uzyskiwania wpisów tajnych z magazynu i wyświetlania ich. Aby dodać zasady:
    1. W portalu przejdź do magazynu kluczy.
    1. Wybierz pozycję **ustawienia > zasady dostępu > + Dodaj zasady dostępu**.
    1. Wybierz pozycję **uprawnienia tajne**, a następnie wybierz pozycję **Pobierz** i **Wyświetl**.
    1. W obszarze **Wybierz podmiot zabezpieczeń** wybierz nazwę zasobu tożsamości zarządzanej. Jeśli używasz tożsamości przypisanej do systemu, podmiot zabezpieczeń jest nazwą wystąpienia API Management.
1. Utwórz lub zaimportuj klucz tajny do magazynu kluczy. Zobacz [Szybki Start: Ustawianie i pobieranie klucza tajnego z Azure Key Vault przy użyciu Azure Portal](../key-vault/secrets/quick-create-portal.md).

Aby użyć wpisu tajnego magazynu kluczy, [Dodaj lub Edytuj nazwaną wartość](#add-or-edit-a-named-value)i określ typ **magazynu kluczy**. Wybierz klucz tajny z magazynu kluczy.

> [!CAUTION]
> W przypadku używania klucza tajnego magazynu kluczy w API Management należy zachować ostrożność, aby nie usunąć wpisu tajnego, magazynu kluczy ani tożsamości zarządzanej używanej do uzyskiwania dostępu do magazynu kluczy.

Jeśli w magazynie kluczy jest włączona [zapora Key Vault](../key-vault/general/network-security.md) , poniżej przedstawiono dodatkowe wymagania dotyczące korzystania z wpisów tajnych magazynu kluczy:

* Aby uzyskać dostęp do magazynu kluczy, należy użyć tożsamości zarządzanej **przypisanej przez system** API Management.
* W zaporze Key Vault Włącz opcję **Zezwalaj na ominięcie tej zapory dla zaufanych usług firmy Microsoft** .

Jeśli wystąpienie API Management zostało wdrożone w sieci wirtualnej, należy również skonfigurować następujące ustawienia sieciowe:
* Włącz [punkt końcowy usługi](../key-vault/general/overview-vnet-service-endpoints.md) do Azure Key Vault w podsieci API Management.
* Skonfiguruj regułę sieciowej grupy zabezpieczeń (sieciowej grupy zabezpieczeń), aby zezwalać na ruch wychodzący do [tagów usługi](../virtual-network/service-tags-overview.md)AzureKeyVault i usługi azureactivedirectory. 

Aby uzyskać szczegółowe informacje, zobacz szczegóły konfiguracji sieci w artykule [nawiązywanie połączenia z siecią wirtualną](api-management-using-with-vnet.md#-common-network-configuration-issues).

## <a name="add-or-edit-a-named-value"></a>Dodawanie lub edytowanie nazwanej wartości

### <a name="add-a-key-vault-secret"></a>Dodawanie wpisu tajnego magazynu kluczy

Zapoznaj się z [wymaganiami wstępnymi dotyczącymi integracji magazynu kluczy](#prerequisites-for-key-vault-integration).

1. W [Azure Portal](https://portal.azure.com)przejdź do wystąpienia API Management.
1. W obszarze **interfejsy API** wybierz pozycję **wartości nazwane**  >  **+ Dodaj**.
1. Wprowadź identyfikator **nazwy** i wprowadź **nazwę wyświetlaną** używaną do odwoływania się do właściwości w zasadach.
1. W polu **Typ wartości** wybierz pozycję **Magazyn kluczy**.
1. Wprowadź identyfikator wpisu tajnego magazynu kluczy (bez wersji) lub wybierz **pozycję Wybierz** , aby wybrać klucz tajny z magazynu kluczy.
    > [!IMPORTANT]
    > Jeśli ręcznie wprowadzisz identyfikator tajny magazynu kluczy, upewnij się, że nie ma on informacji o wersji. W przeciwnym razie wpis tajny nie zostanie automatycznie obrócony w API Management po aktualizacji w magazynie kluczy.
1. W obszarze **tożsamość klienta** wybierz przypisaną przez system lub istniejącą tożsamość zarządzaną przez użytkownika. Dowiedz się [, jak dodać lub zmodyfikować zarządzane tożsamości w usłudze API Management](api-management-howto-use-managed-service-identity.md).
    > [!NOTE]
    > Tożsamość wymaga uprawnień do pobierania wpisów tajnych z magazynu kluczy i ich wyświetlania. Jeśli dostęp do magazynu kluczy nie został jeszcze skonfigurowany, API Management zostanie wyświetlony komunikat z prośbą o to, aby mógł on automatycznie skonfigurować tożsamość z niezbędnymi uprawnieniami.
1. Dodaj jeden lub więcej tagów opcjonalnych, aby ułatwić organizowanie nazwanych wartości, a następnie **Zapisz**.
1. Wybierz pozycję **Utwórz**.

    :::image type="content" source="media/api-management-howto-properties/add-property.png" alt-text="Dodaj wartość wpisu tajnego magazynu kluczy":::

### <a name="add-a-plain-or-secret-value"></a>Dodawanie wartości zwykłej lub tajnej

1. W [Azure Portal](https://portal.azure.com)przejdź do wystąpienia API Management.
1. W obszarze **interfejsy API** wybierz pozycję **wartości nazwane**  >  **+ Dodaj**.
1. Wprowadź identyfikator **nazwy** i wprowadź **nazwę wyświetlaną** używaną do odwoływania się do właściwości w zasadach.
1. W polu **Typ wartości** wybierz pozycję **zwykły** lub **tajny**.
1. W polu **wartość** wprowadź ciąg lub wyrażenie zasad.
1. Dodaj jeden lub więcej tagów opcjonalnych, aby ułatwić organizowanie nazwanych wartości, a następnie **Zapisz**.
1. Wybierz pozycję **Utwórz**.

Po utworzeniu nazwanej wartości można ją edytować, wybierając jej nazwę. Jeśli zmienisz nazwę wyświetlaną, wszystkie zasady odwołujące się do tej nazwanej wartości są automatycznie aktualizowane, aby używać nowej nazwy wyświetlanej.

## <a name="use-a-named-value"></a>Użyj nazwanej wartości

W przykładach w tej sekcji użyto nazwanych wartości przedstawionych w poniższej tabeli.

| Nazwa               | Wartość                      | Wpis tajny | 
|--------------------|----------------------------|--------|---------|
| ContosoHeader      | `TrackingId`                 | Fałsz  | 
| ContosoHeaderValue | ••••••••••••••••••••••     | Prawda   | 
| ExpressionProperty | `@(DateTime.Now.ToString())` | Fałsz  | 

Aby użyć nazwanej wartości w zasadach, umieść jej nazwę wyświetlaną w podwójnej parze nawiasów klamrowych `{{ContosoHeader}}` , jak pokazano w następującym przykładzie:

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

W tym przykładzie `ContosoHeader` jest używany jako nazwa nagłówka w `set-header` zasadach i `ContosoHeaderValue` jest używany jako wartość tego nagłówka. Kiedy te zasady są oceniane podczas żądania lub odpowiedzi bramy API Management `{{ContosoHeader}}` i `{{ContosoHeaderValue}}` są zastępowane odpowiednimi wartościami.

Nazwane wartości mogą być używane jako kompletne wartości atrybutów lub elementów, jak pokazano w poprzednim przykładzie, ale mogą być również wstawiane do lub połączone z częścią wyrażenia tekstu literału, jak pokazano w następującym przykładzie: 

```xml
<set-header name = "CustomHeader{{ContosoHeader}}" ...>
```

Nazwane wartości mogą również zawierać wyrażenia zasad. W poniższym przykładzie `ExpressionProperty` używane jest wyrażenie.

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

Jeśli te zasady zostaną ocenione, `{{ExpressionProperty}}` zostaną zastąpione jej wartością `@(DateTime.Now.ToString())` . Ponieważ wartość jest wyrażeniem zasad, wyrażenie jest oceniane i zasady są wykonywane w ramach jego wykonania.

Można to przetestować w Azure Portal lub [portalu dla deweloperów](api-management-howto-developer-portal.md) , wywołując operację, która ma zasady z nazwanymi wartościami w zakresie. W poniższym przykładzie operacja jest wywoływana z dwiema poprzednimi przykładowymi `set-header` zasadami z nazwanymi wartościami. Należy zauważyć, że odpowiedź zawiera dwa niestandardowe nagłówki, które zostały skonfigurowane przy użyciu zasad z nazwanymi wartościami.

:::image type="content" source="media/api-management-howto-properties/api-management-send-results.png" alt-text="Test odpowiedzi interfejsu API":::

W przypadku wyszukania wychodzącego [śledzenia interfejsu API](api-management-howto-api-inspector.md) dla wywołania, które obejmuje dwie poprzednie przykładowe zasady z nazwanymi wartościami, można zobaczyć dwie `set-header` zasady z nazwanymi wartościami, a także oszacować wyrażenie zasad dla nazwanej wartości, która zawierała wyrażenie zasad.

:::image type="content" source="media/api-management-howto-properties/api-management-api-inspector-trace.png" alt-text="Ślad Inspektora interfejsów API":::

> [!CAUTION]
> Jeśli zasady odwołują się do wpisu tajnego w Azure Key Vault, wartość z magazynu kluczy będzie widoczna dla użytkowników, którzy mają dostęp do subskrypcji obsługujących [śledzenie żądań interfejsu API](api-management-howto-api-inspector.md).

Gdy nazwane wartości mogą zawierać wyrażenia zasad, nie mogą zawierać innych nazwanych wartości. Jeśli tekst zawierający odwołanie nazwanej wartości jest używany dla wartości, na przykład `Text: {{MyProperty}}` , to odwołanie nie zostanie rozwiązane i zastąpione.

## <a name="delete-a-named-value"></a>Usuwanie nazwanej wartości

Aby usunąć nazwaną wartość, wybierz nazwę, a następnie wybierz pozycję **Usuń** z menu kontekstowego (**...**).

> [!IMPORTANT]
> Jeśli nazwana wartość jest przywoływana przez dowolne zasady API Management, nie można jej usunąć do momentu usunięcia nazwanej wartości ze wszystkich zasad, które go używają.

## <a name="next-steps"></a>Następne kroki

-   Dowiedz się więcej na temat pracy z zasadami
    -   [Zasady w API Management](api-management-howto-policies.md)
    -   [Dokumentacja zasad](./api-management-policies.md)
    -   [Wyrażenia zasad](./api-management-policy-expressions.md)

[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png

