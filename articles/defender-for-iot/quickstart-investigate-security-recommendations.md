---
title: 'Szybki Start: Badanie zaleceń dotyczących zabezpieczeń'
description: Sprawdź zalecenia dotyczące zabezpieczeń w usłudze Defender for IoT Security Service.
services: defender-for-iot
ms.service: defender-for-iot
documentationcenter: na
author: mlottner
manager: rkarlin
editor: ''
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/09/2020
ms.author: mlottner
ms.openlocfilehash: 66b5694823096f0747ea099b631a53198a819816
ms.sourcegitcommit: 8be279f92d5c07a37adfe766dc40648c673d8aa8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/31/2020
ms.locfileid: "97835044"
---
# <a name="quickstart-investigate-security-recommendations"></a>Szybki Start: Badanie zaleceń dotyczących zabezpieczeń


Analiza czasowa i łagodzenie rekomendacji w usłudze Defender for IoT to najlepszy sposób na zwiększenie bezpieczeństwa stan i zmniejszenie obszaru ataków na rozwiązanie IoT.

W tym przewodniku szybki start zapoznajemy informacje dostępne w poszczególnych zaleceniach dotyczących zabezpieczeń IoT i wyjaśnisz, jak przejść do szczegółów poszczególnych zaleceń i powiązanych urządzeń, aby zmniejszyć ryzyko.

Zaczynajmy.

## <a name="investigate-new-recommendations"></a>Zbadaj nowe zalecenia

Lista zaleceń dotyczących IoT Hub zawiera wszystkie zagregowane zalecenia dotyczące zabezpieczeń dla IoT Hub.

1.  W Azure Portal Otwórz **IoT Hub** , który chcesz zbadać pod kątem nowych zaleceń.

1.  Z menu **zabezpieczenia** wybierz pozycję **zalecenia**. Wszystkie zalecenia dotyczące zabezpieczeń dla IoT Hub będą wyświetlane, a zalecenia z **nową** flagą oznaczają zalecenia z ostatnich 24 godzin. 

    :::image type="content" source="media/quickstart/investigate-security-recommendations-expanded.png#lightbox" alt-text="Badanie zaleceń dotyczących zabezpieczeń za pomocą usługi ASC dla IoT] (Media/szybkiego startu/investigate-security-recommendations-inline.png)":::


1.  Wybierz i Otwórz wszelkie zalecenia z listy, aby otworzyć Szczegóły zalecenia i przejść do szczegółów.

## <a name="security-recommendation-details"></a>Szczegóły zalecenia dotyczącego zabezpieczeń

Otwórz każde zagregowane zalecenie, aby wyświetlić szczegółowy opis zalecenia, kroki zaradcze, identyfikator urządzenia dla każdego urządzenia, które wywołało zalecenie. Wyświetla również ważność rekomendacji i bezpośredni dostęp do badania przy użyciu Log Analytics.

1.  Wybierz i Otwórz wszelkie zalecenia dotyczące zabezpieczeń z  \>  \> listy **rekomendacje dotyczące** zabezpieczeń IoT Hub.

1.  Zapoznaj się z **opisem** zalecenia, **ważności**, **szczegóły urządzenia** wszystkich urządzeń, które wydały to zalecenie w okresie agregacji. 

1.  Po przejrzeniu konkretnych rekomendacji należy użyć instrukcji **ręcznego rozwiązywania** problemów, aby pomóc skorygować i rozwiązać problem, który spowodował zaleceń. 

    [ :::image type="content" source="media/quickstart/remediate-security-recommendations-expanded.png#lightbox" alt-text="Koryguj zalecenia dotyczące zabezpieczeń za pomocą usługi ASC dla IoT] (Media/szybkiego startu/remediate-security-recommendations-inline.png)":::


1.  Zapoznaj się ze szczegółami rekomendacji określonego urządzenia, wybierając odpowiednie urządzenie na stronie przechodzenia do szczegółów.

    [ :::image type="content" source="media/quickstart/explore-security-recommendation-detail-expanded.png#lightbox" alt-text="Badanie określonych zaleceń dotyczących zabezpieczeń dla urządzenia za pomocą usługi ASC dla IoT] (Media/szybkiego startu/explore-security-recommendation-detail-inline.png)":::


1.  Jeśli wymagane jest dalsze badanie, **Zbadaj zalecenie w log Analytics** przy użyciu linku. 


## <a name="next-steps"></a>Następne kroki

Przejdź do następnego artykułu, aby dowiedzieć się, jak tworzyć alerty niestandardowe...

> [!div class="nextstepaction"]
> [Tworzenie alertów niestandardowych](quickstart-create-custom-alerts.md)
