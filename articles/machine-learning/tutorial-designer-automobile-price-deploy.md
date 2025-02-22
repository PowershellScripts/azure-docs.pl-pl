---
title: 'Samouczek: Wdrażanie modeli ML przy użyciu narzędzia Projektant'
titleSuffix: Azure Machine Learning
description: Tworzenie rozwiązania do analizy predykcyjnej w programie Azure Machine Learning Designer. Uczenie, ocenę i wdrożenie modelu uczenia maszynowego przy użyciu modułów przeciągania i upuszczania.
author: likebupt
ms.author: keli19
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: tutorial
ms.date: 01/15/2021
ms.custom: designer
ms.openlocfilehash: 6bba5ad17cbb6f1ed72d06b37c6d6af9ebd26495
ms.sourcegitcommit: 08458f722d77b273fbb6b24a0a7476a5ac8b22e0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/15/2021
ms.locfileid: "98246472"
---
# <a name="tutorial-deploy-a-machine-learning-model-with-the-designer"></a>Samouczek: Wdrażanie modelu uczenia maszynowego za pomocą narzędzia Projektant


Można wdrożyć model predykcyjny opracowany w pierwszej części [samouczka](tutorial-designer-automobile-price-train-score.md) , aby dać innym osobom szansę korzystania z niego. W części pierwszej został przeszkolony model. Teraz można generować nowe prognozy na podstawie danych wejściowych użytkownika. W tej części samouczka zostaną wykonane następujące czynności:

> [!div class="checklist"]
> * Utwórz potok wnioskowania w czasie rzeczywistym.
> * Utwórz klaster inferencing.
> * Wdróż punkt końcowy w czasie rzeczywistym.
> * Przetestuj punkt końcowy w czasie rzeczywistym.

## <a name="prerequisites"></a>Wymagania wstępne

Wykonaj [jedną z części samouczka](tutorial-designer-automobile-price-train-score.md) , aby dowiedzieć się, jak szkolić i oceny model uczenia maszynowego w projektancie.

[!INCLUDE [machine-learning-missing-ui](../../includes/machine-learning-missing-ui.md)]

## <a name="create-a-real-time-inference-pipeline"></a>Tworzenie potoku w czasie rzeczywistym

Aby wdrożyć potok, należy najpierw skonwertować potok szkoleniowy do potoku w czasie rzeczywistym. Ten proces powoduje usunięcie modułów szkoleniowych i dodanie danych wejściowych i wyjściowych usługi sieci Web do obsługi żądań.

### <a name="create-a-real-time-inference-pipeline"></a>Tworzenie potoku w czasie rzeczywistym

1. Nad kanwą potoku wybierz pozycję **Utwórz**  >  **potok wnioskowania w czasie rzeczywistym**.

    :::image type="content" source="./media/tutorial-designer-automobile-price-deploy/tutorial2-create-inference-pipeline.png"alt-text="Zrzut ekranu przedstawiający miejsce znalezienia przycisku Utwórz potok":::

    Potok powinien teraz wyglądać następująco: 

   ![Zrzut ekranu przedstawiający oczekiwaną konfigurację potoku po przygotowaniu go do wdrożenia](./media/tutorial-designer-automobile-price-deploy/real-time-inference-pipeline.png)

    Po wybraniu opcji **Utwórz potok wnioskowania** kilka rzeczy zostanie wykonanych:
    
    * Szkolony model jest przechowywany jako moduł **DataSet** w palecie modułów. Można go znaleźć w obszarze **Moje zestawy danych**.
    * Moduły szkoleniowe, takie jak **model uczenia** i **dane podzielone** , są usuwane.
    * Zapisany model przeszkolony zostanie dodany z powrotem do potoku.
    * Dodawane są moduły danych **wejściowych** i **usług** sieci Web. Te moduły pokazują, gdzie dane użytkownika są wprowadzane do potoku i gdzie są zwracane dane.

    > [!NOTE]
    > Domyślnie dane **wejściowe usługi sieci Web** będą oczekiwać tego samego schematu danych co dane szkoleniowe, które są używane do tworzenia potoku predykcyjnego. W tym scenariuszu cena jest uwzględniona w schemacie. Cena nie jest jednak używana jako współczynnik podczas przewidywania.
    >

1. Wybierz pozycję **Prześlij**, a następnie użyj tego samego elementu docelowego obliczeń i eksperymentu, który został użyty w części pierwszej.

    Jeśli jest to pierwsze uruchomienie, ukończenie działania potoku może potrwać do 20 minut. Domyślne ustawienia obliczeń mają minimalny rozmiar węzła równy 0, co oznacza, że projektant musi przydzielić zasoby po stanie bezczynności. Powtarzające się uruchomienia potoku będą trwać krócej od czasu przydziału zasobów obliczeniowych. Ponadto projektant używa buforowanych wyników dla każdego modułu, aby zwiększyć wydajność.

1. Wybierz pozycję **Wdróż**.

## <a name="create-an-inferencing-cluster"></a>Tworzenie klastra inferencing

W wyświetlonym oknie dialogowym możesz wybrać dowolny z istniejących klastrów usługi Azure Kubernetes Service (AKS), aby wdrożyć model. Jeśli nie masz klastra AKS, wykonaj następujące kroki, aby go utworzyć.

1. Wybierz pozycję **obliczenia** w wyświetlonym oknie dialogowym, aby przejść do strony **obliczenia** .

1. Na Wstążce Nawigacja wybierz pozycję **klastry wnioskowania**  >  **+ Nowy**.

    ![Zrzut ekranu przedstawiający sposób uzyskiwania do okienka nowy klaster wnioskowania](./media/tutorial-designer-automobile-price-deploy/new-inference-cluster.png)
   
1. W okienku klaster wnioskowania Skonfiguruj nową usługę Kubernetes.

1. Wprowadź *AKS-COMPUTE* dla **nazwy obliczeniowej**.
    
1. Wybierz region znajdujący się w pobliżu, który jest dostępny dla **regionu**.

1. Wybierz przycisk **Utwórz**.

    > [!NOTE]
    > Utworzenie nowej usługi AKS trwa około 15 minut. Stan aprowizacji można sprawdzić na stronie **klastry wnioskowania** .
    >

## <a name="deploy-the-real-time-endpoint"></a>Wdrażanie punktu końcowego w czasie rzeczywistym

Po zakończeniu aprowizacji usługi AKS Wróć do potoku inferencing w czasie rzeczywistym, aby zakończyć wdrażanie.

1. Wybierz pozycję **Wdróż** powyżej kanwy.

1. Wybierz pozycję **wdróż nowy punkt końcowy** w czasie rzeczywistym. 

1. Wybierz utworzony klaster AKS.

    :::image type="content" source="./media/tutorial-designer-automobile-price-deploy/setup-endpoint.png"alt-text="Zrzut ekranu przedstawiający sposób konfigurowania nowego punktu końcowego w czasie rzeczywistym":::

    Możesz również zmienić ustawienia **Zaawansowane** dla punktu końcowego w czasie rzeczywistym.
    
    |Ustawienie zaawansowane|Opis|
    |---|---|
    |Włącz diagnostykę Application Insights i zbieranie danych| Czy włączyć usługę Azure Application Ingishts, aby zbierać dane ze wdrożonych punktów końcowych. </br> Domyślnie: FAŁSZ |
    |Limit czasu oceniania| Limit czasu (w milisekundach) wymuszania dla wywołań oceniania do usługi sieci Web.</br>Domyślnie: 60000|
    |Skalowanie automatyczne włączone|   Określa, czy włączyć skalowanie automatyczne dla usługi sieci Web.</br>Domyślnie: prawda|
    |Minimalna liczba replik| Minimalna liczba kontenerów, które mają być używane podczas automatycznego skalowania tej usługi sieci Web.</br>Domyślnie: 1|
    |Maksymalna liczba replik| Maksymalna liczba kontenerów, które mają być używane podczas automatycznego skalowania tej usługi sieci Web.</br> Domyślnie: 10|
    |Wykorzystanie docelowe|Użycie docelowe (w procentach z 100), które ma być podejmowane przez Autoskalowanie dla tej usługi sieci Web.</br> Domyślnie: 70|
    |Okres odświeżania|Jak często (w sekundach) funkcja automatycznego skalowania próbuje skalować tę usługę sieci Web.</br> Domyślnie: 1|
    |Pojemność rezerwowa procesora CPU|Liczba rdzeni procesora CPU do przydzielenia dla tej usługi sieci Web.</br> Domyślnie: 0,1|
    |Pojemność rezerwowa pamięci|Ilość pamięci (w GB) do przydzielenia dla tej usługi sieci Web.</br> Domyślnie: 0,5|
        

1. Wybierz pozycję **Wdróż**. 

    Powiadomienie o powodzeniu powyżej kanwy pojawia się po zakończeniu wdrażania. Może to potrwać kilka minut.

> [!TIP]
> Możesz również wdrożyć w usłudze **Azure Container instance** (ACI), jeśli wybierzesz pozycję **Azure Container instance** dla **typu obliczenia** w polu ustawienie punktu końcowego w czasie rzeczywistym.
> Usługa Azure Container instance służy do testowania i programowania. Użyj ACI dla obciążeń opartych na PROCESORAch o niskiej skali, które wymagają mniej niż 48 GB pamięci RAM.

## <a name="view-the-real-time-endpoint"></a>Wyświetlanie punktu końcowego w czasie rzeczywistym

Po zakończeniu wdrażania można wyświetlić punkt końcowy w czasie rzeczywistym, przechodząc do strony **punkty końcowe** .

1. Na stronie **punkty końcowe** Wybierz wdrożony punkt końcowy.

1. Na karcie **szczegóły** można zobaczyć więcej informacji, takich jak identyfikator URI REST, stan i Tagi.

1. Na karcie **Korzystanie** można znaleźć klucze zabezpieczeń i ustawić metody uwierzytelniania.

1. Na karcie **dzienniki wdrażania** można znaleźć szczegółowe dzienniki wdrożenia w punkcie końcowym w czasie rzeczywistym. 

Aby uzyskać więcej informacji na temat konsumowania usługi sieci Web, zobacz [Korzystanie z modelu wdrożonego jako usługa WebService](how-to-consume-web-service.md)

## <a name="clean-up-resources"></a>Czyszczenie zasobów

[!INCLUDE [aml-ui-cleanup](../../includes/aml-ui-cleanup.md)]

## <a name="next-steps"></a>Następne kroki

W tym samouczku przedstawiono najważniejsze kroki w temacie Tworzenie, wdrażanie i Używanie modelu uczenia maszynowego w projektancie. Aby dowiedzieć się więcej na temat korzystania z projektanta, zobacz następujące linki:

+ [Przykłady projektanta](samples-designer.md): informacje dotyczące rozwiązywania innych rodzajów problemów za pomocą projektanta.
+ [Użyj Azure Machine Learning Studio w sieci wirtualnej platformy Azure](how-to-enable-studio-virtual-network.md).