---
title: 'Samouczek: ładowanie danych & uruchamianie zapytań za pomocą usługi Azure HDInsight Apache Spark'
description: Samouczek — informacje na temat ładowania danych i uruchamiania interakcyjnych zapytań w klastrach Spark w usłudze Azure HDInsight.
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: tutorial
ms.custom: hdinsightactive,mvc
ms.date: 02/12/2020
ms.openlocfilehash: 85c4298c0c83480c244cc12238c21160a4a4282e
ms.sourcegitcommit: 28c93f364c51774e8fbde9afb5aa62f1299e649e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/30/2020
ms.locfileid: "97822118"
---
# <a name="tutorial-load-data-and-run-queries-on-an-apache-spark-cluster-in-azure-hdinsight"></a>Samouczek: ładowanie danych i uruchamianie zapytań w klastrze platformy Apache Spark w usłudze Azure HDInsight

W tym samouczku dowiesz się, jak utworzyć ramkę danych z pliku CSV oraz jak uruchamiać interakcyjne zapytania Spark SQL względem klastra [Apache Spark](https://spark.apache.org/) w usłudze Azure HDInsight. Na platformie Spark ramka danych jest rozproszoną kolekcją danych zorganizowanych w nazwanych kolumnach. Jest równoważna tabeli w relacyjnej bazie danych lub ramce danych w języku R/Python.

Z tego samouczka dowiesz się, jak wykonywać następujące czynności:
> [!div class="checklist"]
> * Tworzenie ramki danych z pliku csv
> * Uruchamianie zapytań na ramce danych

## <a name="prerequisites"></a>Wymagania wstępne

Klaster Apache Spark w usłudze HDInsight. Zobacz [Tworzenie klastra Apache Spark](./apache-spark-jupyter-spark-sql-use-portal.md).

## <a name="create-a-jupyter-notebook"></a>Tworzenie notesu Jupyter

Jupyter Notebook to interakcyjne środowisko notesu, które obsługuje różne języki programowania. Notes pozwala na interakcję z danymi, łączenie kodu z tekstem markdown i wykonywanie prostych wizualizacji.

1. Edytuj adres URL `https://SPARKCLUSTER.azurehdinsight.net/jupyter` , zastępując go `SPARKCLUSTER` nazwą klastra Spark. Następnie wprowadź edytowany adres URL w przeglądarce sieci Web. Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania dla klastra.

2. Na stronie sieci Web Jupyter wybierz pozycję **Nowy**  >  **PySpark** , aby utworzyć Notes.

   ![Utwórz Jupyter Notebook do uruchamiania interakcyjnego zapytania Spark SQL](./media/apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-spark-sql-query.png "Utwórz Jupyter Notebook do uruchamiania interakcyjnego zapytania Spark SQL")

   Nowy Notes zostanie utworzony i otwarty z nazwą bez tytułu ( `Untitled.ipynb` ).

    > [!NOTE]  
    > Dzięki temu, że tworzenie notesu odbywa się przy użyciu jądra PySpark, po uruchomieniu pierwszej komórki kodu sesja `spark` jest tworzona automatycznie. Nie jest konieczne jawne tworzenie sesji.

## <a name="create-a-dataframe-from-a-csv-file"></a>Tworzenie ramki danych z pliku csv

Aplikacje mogą tworzyć ramki danych bezpośrednio z plików lub folderów w magazynie zdalnym, takich jak usługa Azure Storage lub Azure Data Lake Storage; z tabeli programu Hive; lub z innych źródeł danych obsługiwanych przez platformę Spark, takich jak Cosmos DB, Azure SQL DB, DW i tak dalej. Poniższy zrzut ekranu przedstawia migawkę pliku HVAC.csv używanego w tym samouczku. Plik csv jest zainstalowany na wszystkich klastrach HDInsight Spark. Dane dotyczą zmian temperatury w niektórych budynkach.

![Migawka danych dla interakcyjnego zapytania Spark SQL](./media/apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Migawka danych dla interakcyjnego zapytania Spark SQL")

1. Wklej następujący kod do pustej komórki Jupyter Notebook, a następnie naciśnij klawisze **SHIFT + ENTER** , aby uruchomić kod. Kod importuje typy wymagane w tym scenariuszu:

    ```python
    from pyspark.sql import *
    from pyspark.sql.types import *
    ```

    Podczas uruchamiania interakcyjnego zapytania w programie Jupyter w oknie przeglądarki internetowej lub w tytule karty wyświetlany jest stan **(Busy)** (Zajęty) wraz z tytułem notesu. Widoczne jest także pełne kółko obok tekstu **PySpark** w prawym górnym rogu. Po zakończeniu zadania zmienia się ono w pusty okrąg.

    ![Stan interakcyjnego zapytania Spark SQL](./media/apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Stan interakcyjnego zapytania Spark SQL")

1. Zwróć uwagę na zwrócony identyfikator sesji. Na powyższym rysunku identyfikator sesji to 0. W razie potrzeby można pobrać szczegóły sesji, przechodząc do `https://CLUSTERNAME.azurehdinsight.net/livy/sessions/ID/statements` lokalizacji gdzie ClusterName jest nazwą klastra Spark, a identyfikatorem jest numer identyfikatora sesji.

1. Uruchom następujący kod, aby utworzyć ramkę danych i tabelę tymczasową (**hvac**).

    ```python
    # Create a dataframe and table from sample data
    csvFile = spark.read.csv('/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv', header=True, inferSchema=True)
    csvFile.write.saveAsTable("hvac")
    ```

## <a name="run-queries-on-the-dataframe"></a>Uruchamianie zapytań na ramce danych

Po utworzeniu tabeli możesz uruchomić interakcyjne zapytanie na danych.

1. W pustej komórce notesu uruchom następujący kod:

    ```sql
    %%sql
    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```

   Zostanie wyświetlona następująca tabela danych wyjściowych.

     ![Wyniki tabeli danych wyjściowych interaktywnego zapytania Spark](./media/apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Wyniki tabeli danych wyjściowych interaktywnego zapytania Spark")

2. Wyniki można również przeglądać w postaci innych wizualizacji. Aby wyświetlić wykres warstwowy dla tych samych danych wyjściowych, wybierz pozycję **Area** (Obszar), a następnie ustaw inne wartości, jak pokazano poniżej.

    ![Wykres warstwowy wyników interakcyjnego zapytania Spark](./media/apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Wykres warstwowy wyników interakcyjnego zapytania Spark")

3. Na pasku menu Notes przejdź do **pliku**  >  **Zapisz i Utwórz punkt kontrolny**.

4. Jeśli zamierzasz teraz otworzyć [następny samouczek](apache-spark-use-bi-tools.md), pozostaw notes otwarty. W przeciwnym razie Zamknij Notes, aby zwolnić zasoby klastra: na pasku menu Notes przejdź do **pliku**  >   **Zamknij i zatrzymywanie**.

## <a name="clean-up-resources"></a>Czyszczenie zasobów

Dzięki usłudze HDInsight Twoje notesy danych i Jupyter są przechowywane w usłudze Azure Storage lub Azure Data Lake Storage, dzięki czemu można bezpiecznie usunąć klaster, gdy nie jest używany. Opłaty są naliczone również za klaster usługi HDInsight, nawet wtedy, gdy nie jest używany. Ze względu na to, że opłaty za klaster są dużo razy większe niż opłaty za magazyn, sprawia to, że należy usunąć klastry, gdy nie są używane. Jeśli planujesz natychmiastowe rozpoczęcie pracy z następnym samouczkiem, warto zachować klaster.

Otwórz klaster w witrynie Azure Portal, a następnie wybierz pozycję **Usuń**.

![Usuwanie klastra usługi HDInsight](./media/apache-spark-load-data-run-query/hdinsight-azure-portal-delete-cluster.png "Usuwanie klastra usługi HDInsight")

Dodatkowo możesz wybrać nazwę grupy zasobów, aby otworzyć stronę grupy zasobów, a następnie wybrać pozycję **Usuń grupę zasobów**. Usunięcie grupy zasobów powoduje usunięcie zarówno klastra Spark w usłudze HDInsight, jak i domyślnego konta magazynu.

## <a name="next-steps"></a>Następne kroki

W tym samouczku przedstawiono sposób tworzenia ramki danych z pliku CSV oraz uruchamiania interakcyjnych zapytań Spark SQL w klastrze Apache Spark w usłudze Azure HDInsight. Przejdź do następnego artykułu, aby dowiedzieć się, w jaki sposób można ściągnąć dane zarejestrowane na platformie Apache Spark do narzędzia analizy biznesowej, takiego jak usługa Power BI.

> [!div class="nextstepaction"]
> [Analizowanie danych przy użyciu narzędzi do analizy biznesowej](apache-spark-use-bi-tools.md)
