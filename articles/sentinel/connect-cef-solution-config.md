---
title: Skonfiguruj rozwiązanie zabezpieczeń, aby połączyć dane CEF z wersją zapoznawczą platformy Azure wskaźnikiem | Microsoft Docs
description: Dowiedz się, jak skonfigurować rozwiązanie zabezpieczeń, aby połączyć dane CEF z platformą Azure.
services: sentinel
documentationcenter: na
author: yelevin
manager: rkarlin
editor: ''
ms.service: azure-sentinel
ms.subservice: azure-sentinel
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/30/2019
ms.author: yelevin
ms.openlocfilehash: fec3f25c4b401ff7c3bc73d249b716b9c12e6529
ms.sourcegitcommit: 65db02799b1f685e7eaa7e0ecf38f03866c33ad1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/03/2020
ms.locfileid: "96548549"
---
# <a name="step-2-configure-your-security-solution-to-send-cef-messages"></a>Krok 2. Konfigurowanie rozwiązania zabezpieczeń do wysyłania komunikatów CEF

W tym kroku zostaną wykonane niezbędne zmiany konfiguracji dotyczące samego rozwiązania zabezpieczeń w celu wysłania dzienników do agenta CEF.

## <a name="configure-a-solution-with-a-connector"></a>Konfigurowanie rozwiązania za pomocą łącznika

Jeśli rozwiązanie zabezpieczeń ma już istniejący łącznik, użyj instrukcji specyficznych dla łącznika w następujący sposób:

- [AI Vectra Detect](connect-ai-vectra-detect.md)
- [Check Point](connect-checkpoint.md)
- [Cisco](connect-cisco.md)
- [ExtraHop Reveal(x)](connect-extrahop.md)
- [F5 ASM](connect-f5.md)  
- [Produkty firmy Forcepoint](connect-forcepoint-casb-ngfw.md)
- [Fortinet](connect-fortinet.md)
- [Illusive Networks AMS](connect-illusive-attack-management-system.md)
- [Łączenie z rozwiązaniem One Identity Safeguard](connect-one-identity.md)
- [Palo Alto Networks](connect-paloalto.md)
- [Trend Micro Deep Security](connect-trend-micro.md)
- [Zscaler](connect-zscaler.md)
## <a name="configure-any-other-solution"></a>Skonfiguruj inne rozwiązanie

Jeśli łącznik nie istnieje dla określonego rozwiązania zabezpieczającego, należy użyć poniższych ogólnych instrukcji dotyczących przekazywania dzienników do agenta CEF.

1. Przejdź do określonego artykułu konfiguracyjnego, aby zapoznać się z instrukcjami dotyczącymi sposobu konfigurowania rozwiązania do wysyłania komunikatów CEF. Jeśli Twoje rozwiązanie nie znajduje się na liście, na urządzeniu należy ustawić te wartości tak, aby urządzenie wysyła niezbędne dzienniki w niezbędnym formacie do agenta dziennika systemu Azure wskaźnikowego na podstawie agenta Log Analytics. Te parametry można modyfikować w urządzeniu, o ile są one również modyfikowane w demona dziennika systemowego w ramach agenta wskaźnikowego platformy Azure.
    - Protokół = TCP
    - Port = 514
    - Format = CEF
    - Adres IP — upewnij się, że wysłano komunikaty CEF na adres IP maszyny wirtualnej dedykowanej do tego celu.

   To rozwiązanie obsługuje dziennik systemowy RFC 3164 lub RFC 5424.

1. Aby wyszukać zdarzenia CEF w Log Analytics, wprowadź `CommonSecurityLog` w oknie zapytania.

1. Przejdź do kroku 3: [Weryfikowanie łączności](connect-cef-verify.md).

> [!NOTE]
> **Zmiana źródła pola TimeGenerated**
>
> - Domyślnie agent Log Analytics wypełnia pole *TimeGenerated* w schemacie, gdy agent otrzymał zdarzenie z demona dziennika systemowego. W efekcie czas, w którym zdarzenie zostało wygenerowane w systemie źródłowym, nie jest rejestrowany na platformie Azure.
>
> - Można jednak uruchomić następujące polecenie, które spowoduje pobranie i uruchomienie `TimeGenerated.py` skryptu. Ten skrypt konfiguruje agenta Log Analytics, aby wypełnić pole *TimeGenerated* z oryginalnym czasem zdarzenia w jego systemie źródłowym, zamiast czasu odebranego przez agenta.
>
>    ```bash
>    wget -O TimeGenerated.py https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/DataConnectors/CEF/TimeGenerated.py && python TimeGenerated.py {ws_id}
>    ```

## <a name="next-steps"></a>Następne kroki

W tym dokumencie przedstawiono sposób łączenia urządzeń CEF z platformą Azure — wskaźnikiem. Aby dowiedzieć się więcej na temat platformy Azure, zobacz następujące artykuły:
- Dowiedz się [, jak uzyskać wgląd w dane oraz potencjalne zagrożenia](quickstart-get-visibility.md).
- Rozpocznij [wykrywanie zagrożeń za pomocą platformy Azure — wskaźnik](./tutorial-detect-threats-built-in.md).