---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 01/08/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: 7952c79054b72d98b91642c5b0d6f3db4eade1ce
ms.sourcegitcommit: 8dd8d2caeb38236f79fe5bfc6909cb1a8b609f4a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/08/2021
ms.locfileid: "98047451"
---
|Nazwa<br /><sub>(Azure Portal)</sub> |Opis |Efekt (s) |Wersja<br /><sub>GitHub</sub> |
|---|---|---|---|
|[Urządzenia brzegowe Azure Stack powinny używać podwójnego szyfrowania](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb4ac1030-89c5-4697-8e00-28b5ba6a8811) |Aby zabezpieczyć dane przechowywane na urządzeniu, upewnij się, że jest on szyfrowany podwójnie, dostęp do danych jest kontrolowany, a po zdezaktywowaniu urządzenia dane są bezpiecznie usuwane z dysków danych. Podwójne szyfrowanie to użycie dwóch warstw szyfrowania: BitLocker XTS-AES 256-bitowe szyfrowanie na woluminach danych i wbudowane szyfrowanie dysków twardych. Więcej informacji zawiera dokumentacja dotycząca określonego urządzenia brzegowego stosu. |Inspekcja, Odmów, wyłączone |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Stack%20Edge/AzureStackEdge_DoubleEncryption_Audit.json) |
