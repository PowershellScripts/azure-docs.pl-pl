---
title: Korzystanie z pulpitu nawigacyjnego konsoli czujnika
description: Pulpit nawigacyjny umożliwia szybkie wyświetlenie stanu zabezpieczeń sieci. Zapewnia ogólne omówienie zagrożeń dla całego systemu na osi czasu wraz z informacjami o powiązanych urządzeniach.
author: shhazam-ms
manager: rkarlin
ms.author: shhazam
ms.date: 11/03/2020
ms.topic: article
ms.service: azure
ms.openlocfilehash: 735b1ce4391598d05a1bf0b4486503092f4de37d
ms.sourcegitcommit: 8be279f92d5c07a37adfe766dc40648c673d8aa8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/31/2020
ms.locfileid: "97842917"
---
# <a name="the-dashboard"></a>Pulpit nawigacyjny

Pulpit nawigacyjny umożliwia szybkie wyświetlenie stanu zabezpieczeń sieci. Zapewnia ogólne omówienie zagrożeń dla całego systemu na osi czasu wraz z informacjami o powiązanych urządzeniach, w tym:

- Alerty o różnych poziomach ważności:

- Krytyczne

- Duży

- Mały

- Ostrzeżenia

- Dwa mierniki na środku strony wskazują pakiety na sekundę (PPS) i niepotwierdzone alerty (UA). **PPS** to liczba pakietów potwierdzonych przez system na sekundę. **UA** to liczba alertów, które nie zostały jeszcze potwierdzone.

- Lista niepotwierdzonych alertów wraz z ich opisem.

- Oś czasu z opisem alertu.

:::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/dashboard-alert-screen-v2.png" alt-text="Pulpit nawigacyjny":::

## <a name="viewing-the-latest-alerts"></a>Wyświetlanie najnowszych alertów

Wskaźnik niepotwierdzonych alertów (UA) na środku strony wskazuje liczbę takich alertów. Aby wyświetlić listę alertów, wybierz pozycję **więcej alertów** w dolnej części strony pulpit nawigacyjny lub wybierz pozycję **alerty** w menu po stronie.

:::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/unhandled-alerts-list.png" alt-text="Niepotwierdzone alerty":::

## <a name="status-boxes"></a>Pola stanu

Każde pole Stan zostało opisane w tej sekcji.

| Pole stanu i mierniki | Opis |
| -------------- | -------------- |
| :::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/critical-alert-status-box-v2.png" alt-text="Alerty krytyczne"::: | **Alerty krytyczne** — pole w górnej części strony wskazuje liczbę alertów krytycznych. Zaznacz to pole, aby wyświetlić opisy alertów na osi czasu i na liście w miernikach (jeśli istnieją).                              |
| :::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/major-alert-status-box-v2.png" alt-text="Alerty główne"::: | **Alerty główne** — pole w prawym górnym rogu strony wskazuje liczbę głównych alertów. Zaznacz to pole, aby wyświetlić opisy alertów na osi czasu i na liście w miernikach (jeśli istnieją).                                     |
| :::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/minor-alert-status-box-v2.png" alt-text="Alerty pomocnicze"::: | **Alerty pomocnicze** — pole w lewym dolnym rogu strony wskazuje liczbę drobnych alertów. Zaznacz to pole, aby wyświetlić opisy alertów na osi czasu i na liście w miernikach (jeśli istnieją).                                   |
| :::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/warnings-alert-status-box-v2.png" alt-text="Alerty ostrzegawcze"::: | **Alerty ostrzegawcze** — pole w dolnej części strony wskazuje liczbę alertów ostrzegawczych. Zaznacz to pole, aby wyświetlić opisy alertów na osi czasu i na liście w miernikach (jeśli istnieją).                             |
| :::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/all-alert-status-box-v2.png" alt-text="All Alerts"::: | **Wszystkie alerty** — pole w prawym dolnym rogu strony wskazuje łączną liczbę alertów krytycznych, głównych, pomocniczych i ostrzeżeń. Zaznacz to pole, aby wyświetlić opisy alertów na osi czasu i na liście w miernikach (jeśli istnieją). |
| :::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/packets-per-second-gauge-v2.png" alt-text="Liczba pakietów na sekundę"::: | **Pakiety na sekundę (PPS)** — Metryka PPS jest wskaźnikiem wydajności sieci. |
| :::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/unacknowledged-events-gauge-v2.png" alt-text="Zdarzenia niepotwierdzone (UA)"::: | **Niepotwierdzone zdarzenia** — ta Metryka wskazuje liczbę niepotwierdzonych zdarzeń.

## <a name="using-the-timeline"></a>Korzystanie z osi czasu

Alerty są wyświetlane wzdłuż pionowej osi czasu, która zawiera informacje o dacie i godzinie.

Oś czasu wyświetlana graficznie:

- Alerty krytyczne

- Alerty główne

- Alerty pomocnicze

- Alerty ostrzegawcze

:::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/timeline-of-events.png" alt-text="Wykres osi czasu":::

## <a name="viewing-alerts"></a>Wyświetlanie alertów

Wybierz strzałkę w dół znajdującą **się u dołu** pola alertu, aby wyświetlić informacje o wpisie i urządzeniach alertu.

:::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/extended-alert-screen.png" alt-text="Informacje o wpisie i urządzeniach alertu":::

- Wybierz urządzenie lub **Pokaż urządzenia** , aby wyświetlić mapę trybu fizycznego. Urządzenia poddane są wyróżnione.

- Wybierz pozycję :::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/excel-icon.png" alt-text="Excel"::: , aby wyeksportować plik CSV dotyczący alertu.

- Tylko Administratorzy i analitycy zabezpieczeń — wybierz pozycję :::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/approve-all-icon.png" alt-text="Potwierdź wszystkie"::: , aby **potwierdzić wszystkie** skojarzone alerty.

- Wybierz wpis alertu, aby wyświetlić typ i opis alertu:

- Wybierz pozycję :::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/pdf-icon.png" alt-text="PDF":::, aby pobrać raport o alercie jako plik PDF.

- Wybierz pozycję :::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/pin-icon.png" alt-text="Przypnij":::, aby przypiąć lub odpiąć alert.

- Wybierz pozycję :::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/download-icon.png" alt-text="Pobierz"::: , aby zbadać alert, pobierając plik PCAP zawierający analizę protokołu sieciowego.

- Wybierz pozycję :::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/cloud-download-icon.png" alt-text="chmura"::: , aby pobrać FILTROWANY plik PCAP, który zawiera tylko pakiety powiązane z alertami, co zmniejsza rozmiar pliku wyjściowego i pozwala na bardziej ukierunkowaną analizę. Można go wyświetlić za pomocą programu [Wireshark](https://www.wireshark.org/).

- Wybierz pozycję :::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/navigate-icon.png" alt-text="Nawigacja"::: , aby przejść do osi czasu zdarzenia w czasie żądanego alertu.

- Administratorzy i analitycy zabezpieczeń — zmiana stanu alertu z niepotwierdzonego na potwierdzony. Wybierz pozycję nauka, aby zatwierdzić wykrytą aktywność.

:::image type="content" source="media/how-to-work with-the-sensor-console-dashboard/unauthorized-internet-connectivity-detection-v3.png" alt-text="Wykryto nieautoryzowaną łączność z Internetem":::

## <a name="see-also"></a>Zobacz także

[Pracuj z alertami na czujniku](how-to-work-with-alerts-on-your-sensor.md)
