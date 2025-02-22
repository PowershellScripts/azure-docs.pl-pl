---
title: Debugowanie zadań platformy Apache Spark uruchomionych w usłudze Azure HDInsight
description: Śledzenie i debugowanie zadań uruchomionych w klastrze Spark w usłudze Azure HDInsight za pomocą interfejsu użytkownika, interfejsu użytkownika platformy Spark i serwera historii platformy Spark
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: how-to
ms.custom: hdinsightactive,seoapr2020
ms.date: 04/23/2020
ms.openlocfilehash: 366c77ff94773163b71845b1ccbc6072c503734a
ms.sourcegitcommit: 28c93f364c51774e8fbde9afb5aa62f1299e649e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/30/2020
ms.locfileid: "97822305"
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a>Debugowanie zadań platformy Apache Spark uruchomionych w usłudze Azure HDInsight

W tym artykule dowiesz się, jak śledzić i debugować zadania Apache Spark uruchomione w klastrach usługi HDInsight. Debuguj przy użyciu interfejsu użytkownika Apache Hadoop PRZĘDZy, interfejsu użytkownika Spark i serwera historii platformy Spark. Rozpoczęcie zadania platformy Spark przy użyciu notesu dostępnego z klastrem Spark, **Uczenie maszynowe: analizy predykcyjnej danych inspekcji żywności przy użyciu MLLib**. Wykonaj następujące kroki, aby śledzić aplikację, która została przesłana przy użyciu innego podejścia, a na przykład do **przesyłania danych z platformy Spark**.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

## <a name="prerequisites"></a>Wymagania wstępne

* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [Tworzenie klastra platformy Apache Spark w usłudze Azure HDInsight](apache-spark-jupyter-spark-sql.md).

* Należy rozpocząć pracę z notesem, **[Uczenie maszynowe: Analiza predykcyjna danych inspekcji żywności przy użyciu MLLib](apache-spark-machine-learning-mllib-ipython.md)**. Aby uzyskać instrukcje dotyczące sposobu uruchamiania tego notesu, Użyj linku.  

## <a name="track-an-application-in-the-yarn-ui"></a>Śledzenie aplikacji w interfejsie użytkownika PRZĘDZy

1. Uruchom interfejs użytkownika PRZĘDZy. Wybierz pozycję **przędza** w obszarze **pulpity nawigacyjne klastra**.

    ![Azure Portal uruchamiania interfejsu użytkownika PRZĘDZy](./media/apache-spark-job-debugging/launch-apache-yarn-ui.png)

   > [!TIP]  
   > Alternatywnie można również uruchomić interfejs użytkownika PRZĘDZy z interfejsu użytkownika Ambari. Aby uruchomić interfejs użytkownika Ambari, wybierz pozycję **Ambari Home** w obszarze **pulpity nawigacyjne klastra**. W interfejsie użytkownika Ambari **Przejdź do**  >  okna **szybkie linki** do > aktywnego Menedżer zasobów > **Menedżer zasobów interfejsie użytkownika**.

2. Ponieważ uruchomiono zadanie Spark przy użyciu notesów Jupyter, aplikacja ma nazwę **remotesparkmagics** (nazwa wszystkich aplikacji uruchamianych z notesów). Wybierz identyfikator aplikacji dla nazwy aplikacji, aby uzyskać więcej informacji o zadaniu. Ta akcja powoduje uruchomienie widoku aplikacji.

    ![Serwer historii platformy Spark Znajdź identyfikator aplikacji platformy Spark](./media/apache-spark-job-debugging/find-application-id1.png)

    W przypadku takich aplikacji, które są uruchamiane z notesów Jupyter, stan jest zawsze **uruchamiany** , dopóki nie zamkniesz notesu.

3. W widoku aplikacji możesz przejść do szczegółów, aby dowiedzieć się więcej o kontenerach skojarzonych z aplikacją i dziennikach (stdout/stderr). Interfejs użytkownika Spark można również uruchomić, klikając link odpowiadający **adresowi URL śledzenia**, jak pokazano poniżej.

    ![Pobieranie dzienników kontenerów z serwera historii platformy Spark](./media/apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-the-spark-ui"></a>Śledzenie aplikacji w interfejsie użytkownika Spark

W interfejsie użytkownika platformy Spark można przechodzić do szczegółów zadań platformy Spark, które są duplikowane przez uruchomioną wcześniej aplikację.

1. Aby uruchomić interfejs użytkownika Spark, w widoku aplikacji wybierz łącze z **adresem URL śledzenia**, jak pokazano na poniższym zrzucie ekranu. Można wyświetlić wszystkie zadania platformy Spark uruchamiane przez aplikację uruchomioną w Jupyter Notebook.

    ![Karta zadań serwera historii platformy Spark](./media/apache-spark-job-debugging/view-apache-spark-jobs.png)

2. Wybierz kartę **wykonawcy** , aby wyświetlić informacje dotyczące przetwarzania i magazynowania dla każdego wykonawcy. Możesz również pobrać stos wywołań, wybierając łącze **zrzut wątku** .

    ![Karta modułów wykonujących serwer historii platformy Spark](./media/apache-spark-job-debugging/view-spark-executors.png)

3. Wybierz kartę **etapy** , aby wyświetlić etapy skojarzone z aplikacją.

    ![Karta etapy serwera historii platformy Spark](./media/apache-spark-job-debugging/view-apache-spark-stages.png "Wyświetl etapy platformy Spark")

    Każdy etap może mieć wiele zadań, dla których można wyświetlić statystyki wykonywania, jak pokazano poniżej.

    ![Szczegóły karty etapy serwera historii platformy Spark](./media/apache-spark-job-debugging/view-spark-stages-details.png "Wyświetl szczegóły etapów platformy Spark")

4. Na stronie szczegóły etapu można uruchomić wizualizację DAG. Rozwiń link **wizualizacji DAG** w górnej części strony, jak pokazano poniżej.

    ![Wyświetl wizualizację DAG etapów platformy Spark](./media/apache-spark-job-debugging/view-spark-stages-dag-visualization.png)

    DAG lub Direct Aclyic Graph reprezentuje różne etapy aplikacji. Każde niebieskie pole na grafie reprezentuje operację Spark wywoływaną z aplikacji.

5. Na stronie szczegóły etapu można również uruchomić widok oś czasu aplikacji. Rozwiń link **oś czasu zdarzeń** w górnej części strony, jak pokazano poniżej.

    ![Wyświetl oś czasu zdarzeń etapów platformy Spark](./media/apache-spark-job-debugging/view-spark-stages-event-timeline.png)

    Ten obraz przedstawia zdarzenia platformy Spark w formie osi czasu. Widok oś czasu jest dostępny na trzech poziomach, między zadaniami, w ramach zadania i w obrębie etapu. Powyższy obraz przechwytuje Widok osi czasu dla danego etapu.

   > [!TIP]  
   > W przypadku zaznaczenia pola wyboru **Włącz powiększanie** , można przewijać w lewo i w prawo w widoku oś czasu.

6. Inne karty w interfejsie użytkownika Spark zawierają również użyteczne informacje o wystąpieniu platformy Spark.

   * Karta magazyn — Jeśli aplikacja tworzy RDD, można znaleźć informacje na karcie Magazyn.
   * Karta środowisko — ta karta zawiera przydatne informacje o wystąpieniu platformy Spark, takie jak:
     * Wersja Scala
     * Katalog dziennika zdarzeń skojarzony z klastrem
     * Liczba rdzeni wykonawców dla aplikacji

## <a name="find-information-about-completed-jobs-using-the-spark-history-server"></a>Znajdowanie informacji o ukończonych zadaniach przy użyciu serwera historii platformy Spark

Po zakończeniu zadania informacje o zadaniu są utrwalane na serwerze historii platformy Spark.

1. Aby uruchomić serwer historii platformy Spark, na stronie **Przegląd** wybierz pozycję **serwer historii platformy Spark** w obszarze **pulpity nawigacyjne klastra**.

    ![Azure Portal uruchomić serwer historii platformy Spark](./media/apache-spark-job-debugging/launch-spark-history-server.png "Uruchom historię platformy Spark serwer1")

   > [!TIP]  
   > Alternatywnie można również uruchomić interfejs użytkownika serwera historii platformy Spark z poziomu interfejsu użytkownika Ambari. Aby uruchomić interfejs użytkownika Ambari, w bloku przegląd wybierz pozycję **Strona główna Ambari** w obszarze **pulpity nawigacyjne klastra**. W interfejsie użytkownika Ambari przejdź do strony **Spark2**  >  **szybkie linki**  >  **Spark2 interfejs użytkownika serwera historii**.

2. Zobaczysz wszystkie ukończone aplikacje wymienione na liście. Wybierz identyfikator aplikacji, aby przejść do aplikacji w celu uzyskania dodatkowych informacji.

    ![Zakończone aplikacje serwera historii platformy Spark](./media/apache-spark-job-debugging/view-completed-applications.png "Uruchom historię platformy Spark Serwer2")

## <a name="see-also"></a>Zobacz także

* [Zarządzanie zasobami klastra Apache Spark w usłudze Azure HDInsight](apache-spark-resource-manager.md)
* [Debugowanie Apache Spark zadań przy użyciu rozszerzonego serwera historii platformy Spark](apache-azure-spark-history-server.md)
* [Debuguj Apache Spark aplikacji z Azure Toolkit for IntelliJ za pośrednictwem protokołu SSH](apache-spark-intellij-tool-debug-remotely-through-ssh.md)
