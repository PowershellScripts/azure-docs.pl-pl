---
title: Wyzwalanie potoków Azure Machine Learning
titleSuffix: Azure Machine Learning
description: Potoki wyzwalane umożliwiają automatyzowanie rutynowych, czasochłonnych zadań, takich jak przetwarzanie danych, szkolenia i monitorowanie.
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.author: laobri
author: lobrien
ms.date: 12/16/2020
ms.topic: conceptual
ms.custom: how-to, devx-track-python
ms.openlocfilehash: 9038d6bc9cd061200ef4553242889776f30d2dc1
ms.sourcegitcommit: f6f928180504444470af713c32e7df667c17ac20
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/07/2021
ms.locfileid: "97964562"
---
# <a name="trigger-machine-learning-pipelines-with-azure-machine-learning-sdk-for-python"></a>Wyzwalanie potoków uczenia maszynowego za pomocą zestawu SDK Azure Machine Learning dla języka Python

W tym artykule dowiesz się, jak programowo zaplanować uruchamianie potoku na platformie Azure. Można utworzyć harmonogram na podstawie czasu, który upłynął lub zmiany w systemie plików. Harmonogramy oparte na czasie mogą służyć do wykonywania codziennych zadań, takich jak monitorowanie dryfowania danych. Harmonogramy oparte na zmianach mogą służyć do reagowania na zmiany nieregularne lub nieprzewidywalne, takie jak nowe przekazane dane lub stare dane. Po zapoznaniu się ze sposobem tworzenia harmonogramów dowiesz się, jak je pobrać i dezaktywować. Na koniec dowiesz się, jak używać aplikacji logiki platformy Azure, aby umożliwić bardziej złożoną logikę wyzwalającą lub zachowanie.

## <a name="prerequisites"></a>Wymagania wstępne

* Subskrypcja platformy Azure. Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://aka.ms/AMLFree).

* Środowisko języka Python, w którym jest zainstalowany zestaw SDK Azure Machine Learning dla języka Python. Aby uzyskać więcej informacji, zobacz [Tworzenie środowisk wielokrotnego użytku i zarządzanie nimi na potrzeby szkoleń i wdrażania przy użyciu Azure Machine Learning.](how-to-use-environments.md)

* Obszar roboczy Machine Learning z opublikowanym potokiem. Można użyć wbudowanego [tworzenia i uruchamiania potoków uczenia maszynowego z zestawem SDK Azure Machine Learning](how-to-create-your-first-pipeline.md).

## <a name="initialize-the-workspace--get-data"></a>Inicjowanie obszaru roboczego & pobieranie danych

Do zaplanowania potoku konieczne będzie odwołanie do obszaru roboczego, identyfikator opublikowanego potoku oraz nazwę eksperymentu, w którym ma zostać utworzony harmonogram. Te wartości można uzyskać przy użyciu następującego kodu:

```Python
import azureml.core
from azureml.core import Workspace
from azureml.pipeline.core import Pipeline, PublishedPipeline
from azureml.core.experiment import Experiment

ws = Workspace.from_config()

experiments = Experiment.list(ws)
for experiment in experiments:
    print(experiment.name)

published_pipelines = PublishedPipeline.list(ws)
for published_pipeline in  published_pipelines:
    print(f"{published_pipeline.name},'{published_pipeline.id}'")

experiment_name = "MyExperiment" 
pipeline_id = "aaaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" 
```

## <a name="create-a-schedule"></a>Tworzenie harmonogramu

Aby uruchomić potok cyklicznie, należy utworzyć harmonogram. A powoduje `Schedule` skojarzenie potoku, eksperymentu i wyzwalacza. Wyzwalacz może być obiektem `ScheduleRecurrence` opisującym oczekiwania między uruchomieniami lub ścieżką magazynu danych, która określa katalog, w którym mają być monitorowane zmiany. W obu przypadkach potrzebny będzie identyfikator potoku i nazwa eksperymentu, w którym ma zostać utworzony harmonogram.

W górnej części pliku języka Python zaimportuj `Schedule` klasy i `ScheduleRecurrence` :

```python

from azureml.pipeline.core.schedule import ScheduleRecurrence, Schedule
```

### <a name="create-a-time-based-schedule"></a>Tworzenie harmonogramu opartego na czasie

`ScheduleRecurrence`Konstruktor ma wymagany `frequency` argument, który musi być jednym z następujących ciągów: "minute", "Hour", "Day", "Week" lub "Month". Wymaga również `interval` argumentu Integer określającego, ile `frequency` jednostek powinna upłynąć między harmonogramem. Opcjonalne argumenty umożliwiają bardziej szczegółowe określenie czasu rozpoczęcia, zgodnie z opisem w dokumentacji [zestawu SDK ScheduleRecurrence](/python/api/azureml-pipeline-core/azureml.pipeline.core.schedule.schedulerecurrence?preserve-view=true&view=azure-ml-py).

Utwórz `Schedule` Uruchamianie co 15 minut:

```python
recurrence = ScheduleRecurrence(frequency="Minute", interval=15)
recurring_schedule = Schedule.create(ws, name="MyRecurringSchedule", 
                            description="Based on time",
                            pipeline_id=pipeline_id, 
                            experiment_name=experiment_name, 
                            recurrence=recurrence)
```

### <a name="create-a-change-based-schedule"></a>Tworzenie harmonogramu opartego na zmianach

Potoki wyzwalane przez zmiany plików mogą być bardziej wydajne niż harmonogramy oparte na czasie. Na przykład możesz chcieć wykonać krok przetwarzania wstępnego, gdy plik zostanie zmieniony lub gdy nowy plik zostanie dodany do katalogu danych. Możesz monitorować wszelkie zmiany w magazynie danych lub zmiany w określonym katalogu w magazynie danych. W przypadku monitorowania określonego katalogu zmiany w podkatalogach tego katalogu _nie_ będą powodowały uruchomienia.

Aby utworzyć plik — reaktywny `Schedule` , należy ustawić `datastore` parametr w wywołaniu metody [Schedule. Create](/python/api/azureml-pipeline-core/azureml.pipeline.core.schedule.schedule?preserve-view=true&view=azure-ml-py#&preserve-view=truecreate-workspace--name--pipeline-id--experiment-name--recurrence-none--description-none--pipeline-parameters-none--wait-for-provisioning-false--wait-timeout-3600--datastore-none--polling-interval-5--data-path-parameter-name-none--continue-on-step-failure-none--path-on-datastore-none---workflow-provider-none---service-endpoint-none-). Aby monitorować folder, należy ustawić `path_on_datastore` argument.

`polling_interval`Argument pozwala określić, w minutach, częstotliwość sprawdzania zmian w magazynie danych.

Jeśli potok został skonstruowany przy użyciu [ścieżki datapath](/python/api/azureml-core/azureml.data.datapath.datapath?preserve-view=true&view=azure-ml-py) [PipelineParameter](/python/api/azureml-pipeline-core/azureml.pipeline.core.pipelineparameter?preserve-view=true&view=azure-ml-py), można ustawić tę zmienną na nazwę zmienionego pliku przez ustawienie `data_path_parameter_name` argumentu.

```python
datastore = Datastore(workspace=ws, name="workspaceblobstore")

reactive_schedule = Schedule.create(ws, name="MyReactiveSchedule", description="Based on input file change.",
                            pipeline_id=pipeline_id, experiment_name=experiment_name, datastore=datastore, data_path_parameter_name="input_data")
```

### <a name="optional-arguments-when-creating-a-schedule"></a>Opcjonalne argumenty podczas tworzenia harmonogramu

Oprócz argumentów omówionych wcześniej, można ustawić `status` argument na, aby `"Disabled"` utworzyć nieaktywny harmonogram. Na koniec `continue_on_step_failure` umożliwia przekazanie wartości logicznej, która zastąpi domyślne zachowanie potoku.

## <a name="view-your-scheduled-pipelines"></a>Wyświetlanie zaplanowanych potoków

W przeglądarce sieci Web przejdź do Azure Machine Learning. W sekcji **punkty końcowe** panelu nawigacji wybierz pozycję **punkty końcowe potoku**. Spowoduje to przejście do listy potoków opublikowanych w obszarze roboczym.

![Strona potoki elementu AML](./media/how-to-trigger-published-pipeline/scheduled-pipelines.png)

Na tej stronie można wyświetlić informacje podsumowujące dotyczące wszystkich potoków w obszarze roboczym: nazwy, opisy, Stany i tak dalej. Aby przejść do szczegółów, kliknij potok. Na otrzymanej stronie znajduje się więcej szczegółów na temat potoku i można przechodzić do poszczególnych uruchomień.

## <a name="deactivate-the-pipeline"></a>Dezaktywuj potok

Jeśli masz `Pipeline` opublikowaną wersję, ale nie została ona zaplanowana, możesz ją wyłączyć przy użyciu:

```python
pipeline = PublishedPipeline.get(ws, id=pipeline_id)
pipeline.disable()
```

W przypadku zaplanowania potoku należy najpierw anulować harmonogram. Pobierz identyfikator harmonogramu z portalu lub uruchamiając:

```python
ss = Schedule.list(ws)
for s in ss:
    print(s)
```

Gdy chcesz `schedule_id` wyłączyć, uruchom polecenie:

```python
def stop_by_schedule_id(ws, schedule_id):
    s = next(s for s in Schedule.list(ws) if s.id == schedule_id)
    s.disable()
    return s

stop_by_schedule_id(ws, schedule_id)
```

Po ponownym uruchomieniu należy `Schedule.list(ws)` uzyskać pustą listę.

## <a name="use-azure-logic-apps-for-complex-triggers"></a>Użyj Azure Logic Apps dla wyzwalaczy złożonych 

Bardziej złożone reguły wyzwalacza lub zachowanie można utworzyć za pomocą [aplikacji logiki platformy Azure](../logic-apps/logic-apps-overview.md).

Aby wyzwolić potok Machine Learning za pomocą aplikacji logiki platformy Azure, potrzebny jest punkt końcowy REST dla opublikowanego potoku Machine Learning. [Tworzenie i publikowanie potoku](how-to-create-your-first-pipeline.md). Następnie Znajdź punkt końcowy REST, `PublishedPipeline` używając identyfikatora potoku:

```python
# You can find the pipeline ID in Azure Machine Learning studio

published_pipeline = PublishedPipeline.get(ws, id="<pipeline-id-here>")
published_pipeline.endpoint 
```

## <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki

Teraz Utwórz wystąpienie [aplikacji logiki platformy Azure](../logic-apps/logic-apps-overview.md) . Jeśli chcesz, [Użyj środowiska usługi integracji (ISE)](../logic-apps/connect-virtual-network-vnet-isolated-environment.md) i [Skonfiguruj klucz zarządzany przez klienta](../logic-apps/customer-managed-keys-integration-service-environment.md) do użycia przez aplikację logiki.

Po udostępnieniu aplikacji logiki wykonaj następujące kroki, aby skonfigurować wyzwalacz dla potoku:

1. [Utwórz tożsamość zarządzaną przypisaną przez system](../logic-apps/create-managed-service-identity.md) , aby umożliwić aplikacji dostęp do obszar roboczy usługi Azure Machine Learning.

1. Przejdź do widoku projektanta aplikacji logiki i wybierz szablon pustej aplikacji logiki. 
    > [!div class="mx-imgBorder"]
    > ![Pusty szablon](media/how-to-trigger-published-pipeline/blank-template.png)

1. W projektancie Wyszukaj **obiekt BLOB**. Wybierz opcję **gdy obiekt BLOB jest dodawany lub modyfikowany (tylko właściwości)** , a następnie Dodaj ten wyzwalacz do aplikacji logiki.
    > [!div class="mx-imgBorder"]
    > ![Dodawanie wyzwalacza](media/how-to-trigger-published-pipeline/add-trigger.png)

1. Wprowadź informacje o połączeniu dla konta usługi BLOB Storage, które chcesz monitorować pod kątem dodatków lub modyfikacji obiektów BLOB. Wybierz kontener do monitorowania. 
 
    Wybierz **Interwał** i **częstotliwość** sondowania w poszukiwaniu aktualizacji, które są dla Ciebie wykonywane.  

    > [!NOTE]
    > Ten wyzwalacz będzie monitorować wybrany kontener, ale nie będzie monitorował podfolderów.

1. Dodaj akcję HTTP, która będzie uruchamiana, gdy zostanie wykryty nowy lub zmodyfikowany obiekt BLOB. Wybierz pozycję **+ nowy krok**, a następnie wyszukaj i wybierz akcję http.

  > [!div class="mx-imgBorder"]
  > ![Wyszukaj akcję HTTP](media/how-to-trigger-published-pipeline/search-http.png)

  Aby skonfigurować akcję, użyj następujących ustawień:

  | Ustawienie | Wartość | 
  |---|---|
  | Akcja HTTP | POST |
  | URI |punkt końcowy do opublikowanego potoku, który został znaleziony jako [warunek wstępny](#prerequisites) |
  | Tryb uwierzytelniania | Tożsamość zarządzana |

1. Skonfiguruj harmonogram, aby ustawić wartość dowolnej [ścieżki dataPipelineParameters](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/machine-learning-pipelines/intro-to-pipelines/aml-pipelines-showcasing-datapath-and-pipelineparameter.ipynb) :

    ```json
    {
      "DataPathAssignments": {
        "input_datapath": {
          "DataStoreName": "<datastore-name>",
          "RelativePath": "@{triggerBody()?['Name']}" 
        }
      },
      "ExperimentName": "MyRestPipeline",
      "ParameterAssignments": {
        "input_string": "sample_string3"
      },
      "RunSource": "SDK"
    }
    ```

    Użyj `DataStoreName` dodanych do obszaru roboczego jako [warunek wstępny](#prerequisites).
     
    > [!div class="mx-imgBorder"]
    > ![Ustawienia protokołu HTTP](media/how-to-trigger-published-pipeline/http-settings.png)

1. Wybierz pozycję **Zapisz** , a harmonogram jest teraz gotowy.

> [!IMPORTANT]
> Jeśli używasz kontroli dostępu opartej na rolach (Azure RBAC) na potrzeby zarządzania dostępem do potoku, [Ustaw uprawnienia dla scenariusza potoku (szkolenie lub ocenianie)](how-to-assign-roles.md#common-scenarios).

## <a name="next-steps"></a>Następne kroki

W tym artykule użyto zestawu SDK Azure Machine Learning dla języka Python w celu zaplanowania potoku na dwa różne sposoby. Jeden harmonogram powtarza się w oparciu o czas zegara, który upłynął. Drugi harmonogram jest uruchamiany, jeśli plik zostanie zmodyfikowany w określonym `Datastore` lub w katalogu w tym magazynie. Pokazano, jak używać portalu do badania potoku i poszczególnych uruchomień. Wiesz już, jak wyłączyć harmonogram, aby potok przestanie działać. Na koniec utworzono aplikację logiki platformy Azure w celu wyzwolenia potoku. 

Aby uzyskać więcej informacji, zobacz:

> [!div class="nextstepaction"]
> [Korzystanie z potoków Azure Machine Learning na potrzeby oceniania partii](tutorial-pipeline-batch-scoring-classification.md)

* Dowiedz się więcej o [potokach](concept-ml-pipelines.md)
* Dowiedz się więcej o [eksplorowaniu Azure Machine Learning za pomocą Jupyter](samples-notebooks.md)