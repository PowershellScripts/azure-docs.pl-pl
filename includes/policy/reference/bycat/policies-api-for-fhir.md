---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 01/08/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: 623822dc4356cad95b247f0c475bfa43ded7ec7a
ms.sourcegitcommit: 8dd8d2caeb38236f79fe5bfc6909cb1a8b609f4a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/08/2021
ms.locfileid: "98047426"
---
|Nazwa<br /><sub>(Azure Portal)</sub> |Opis |Efekt (s) |Wersja<br /><sub>GitHub</sub> |
|---|---|---|---|
|[Usługa Azure API for FHIR powinna używać klucza zarządzanego przez klienta (CMK) do szyfrowania danych przechowywanych w usłudze REST](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F051cba44-2429-45b9-9649-46cec11c7119) |Za pomocą klucza zarządzanego przez klienta można kontrolować szyfrowanie danych przechowywanych w interfejsie API platformy Azure dla usługi FHIR, gdy jest to wymaganie prawne lub zgodne. Klucze zarządzane przez klienta udostępniają również podwójne szyfrowanie przez dodanie drugiej warstwy szyfrowania na podstawie wartości domyślnej wykonanej przy użyciu kluczy zarządzanych przez usługę. |Inspekcja, wyłączona |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/API%20for%20FHIR/HealthcareAPIs_EnableByok_Audit.json) |
|[Interfejs API platformy Azure dla usługi FHIR powinien korzystać z prywatnego linku](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1ee56206-5dd1-42ab-b02d-8aae8b1634ce) |Interfejs API platformy Azure dla usługi FHIR powinien mieć co najmniej jedno zatwierdzone prywatne połączenie z punktem końcowym. Klienci w sieci wirtualnej mogą bezpiecznie uzyskiwać dostęp do zasobów, które mają prywatne połączenia punktów końcowych za pomocą linków prywatnych. Aby uzyskać więcej informacji, odwiedź stronę: [https://aka.ms/fhir-privatelink](https://aka.ms/fhir-privatelink) . |Inspekcja, wyłączona |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/API%20for%20FHIR/HealthcareAPIs_PrivateLink_Audit.json) |
|[Mechanizm CORS nie powinien zezwalać każdej domenie na dostęp do interfejsu API dla FHIR](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0fea8f8a-4169-495d-8307-30ec335f387d) |Współużytkowanie zasobów między źródłami (CORS) nie powinno zezwalać wszystkim domenom na dostęp do interfejsu API dla FHIR. Aby chronić interfejs API dla usługi FHIR, Usuń dostęp dla wszystkich domen i jawnie Zdefiniuj domeny, które mogą nawiązywać połączenia. |Inspekcja, wyłączona |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/API%20for%20FHIR/HealthcareAPIs_RestrictCORSAccess_Audit.json) |
