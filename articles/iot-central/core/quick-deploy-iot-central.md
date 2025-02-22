---
title: Szybki Start — Tworzenie aplikacji IoT Central platformy Azure | Microsoft Docs
description: Szybki Start — Tworzenie nowej aplikacji IoT Central platformy Azure. Utwórz aplikację, korzystając z bezpłatnego planu cenowego lub jednego z standardowych planów cenowych.
author: viv-liu
ms.author: viviali
ms.date: 11/23/2020
ms.topic: quickstart
ms.service: iot-central
services: iot-central
manager: corywink
ms.openlocfilehash: c5847f686e0712370a1de898eca5735608671e9a
ms.sourcegitcommit: d79513b2589a62c52bddd9c7bd0b4d6498805dbe
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97670897"
---
# <a name="quickstart---create-an-azure-iot-central-application"></a>Szybki Start — Tworzenie aplikacji IoT Central platformy Azure

Ten przewodnik Szybki Start przedstawia sposób tworzenia aplikacji IoT Central platformy Azure.

## <a name="create-an-application"></a>Tworzenie aplikacji

Przejdź do witryny [Azure IoT Central Build](https://aka.ms/iotcentral) . Następnie zaloguj się przy użyciu konta osobistego, służbowego lub szkolnego firmy Microsoft.

Tworzysz nową aplikację z listy IoT Central szablonów odpowiednich dla branż, aby pomóc szybko rozpocząć pracę, lub Zacznij od podstaw przy użyciu szablonu **niestandardowych aplikacji** . W tym przewodniku szybki start użyjesz szablonu **aplikacji niestandardowej** .

Aby utworzyć nową aplikację usługi Azure IoT Central przy użyciu szablonu **aplikacji niestandardowej** :

1. Przejdź do strony **kompilacja** :

    :::image type="content" source="media/quick-deploy-iot-central/iotcentralcreate-new-application.png" alt-text="Tworzenie strony aplikacji IoT":::

1. Wybierz pozycję **aplikacje niestandardowe** i upewnij się, że wybrano szablon **aplikacja niestandardowa** .

1. Usługa Azure IoT Central automatycznie sugeruje **nazwę aplikacji** w oparciu o wybrany szablon aplikacji. Możesz użyć tej nazwy lub wprowadzić własną przyjazną nazwę aplikacji.

1. Usługa Azure IoT Central generuje również unikatowy prefiks **adresu URL aplikacji** na podstawie nazwy aplikacji. Ten adres URL jest używany do uzyskiwania dostępu do aplikacji. Zmień ten prefiks adresu URL na bardziej zapamiętany, jeśli chcesz.

    :::image type="content" source="media/quick-deploy-iot-central/iotcentralcreate-custom.png" alt-text="IoT Central tworzenia strony aplikacji przez platformę Azure":::

    :::image type="content" source="media/quick-deploy-iot-central/iotcentralcreate-billinginfo.png" alt-text="Informacje dotyczące rozliczeń IoT Central platformy Azure":::

    > [!Tip]
    > Jeśli na poprzedniej stronie została wybrana opcja **aplikacja niestandardowa** , zostanie wyświetlona lista rozwijana **szablonu aplikacji** . Lista rozwijana może zawierać inne szablony, które zostały udostępnione przez organizację.

1. Wybierz, aby utworzyć tę aplikację przy użyciu 7-dniowego planu cenowego w wersji próbnej lub jednego z standardowych planów cenowych:

    - Aplikacje tworzone za pomocą planu *bezpłatnego* są bezpłatne przez siedem dni i obsługują maksymalnie pięć urządzeń. Możesz przekonwertować je tak, aby używały standardowego planu cenowego w dowolnym momencie przed wygaśnięciem.
        > [!NOTE]
        > Aplikacje utworzone za pomocą planu *bezpłatnego* nie wymagają subskrypcji platformy Azure i dlatego nie będą znajdować się na liście w subskrypcji platformy azure na Azure Portal. W portalu IoT Central można wyświetlać i zarządzać bezpłatnymi aplikacjami.          
    - W przypadku aplikacji tworzonych przy użyciu planu *standardowego* są naliczane opłaty za poszczególne urządzenia. możesz wybrać **Standardowy** plan cenowy 0, **Standardowy 1** lub **standardowy 2** z dwoma bezpłatnymi urządzeniami. Dowiedz się więcej o planach cen bezpłatnych i standardowych na [stronie cennika usługi Azure IoT Central](https://azure.microsoft.com/pricing/details/iot-central/). Jeśli tworzysz aplikację przy użyciu standardowego planu cenowego, musisz wybrać *katalog*, *subskrypcję platformy Azure* i *lokalizację*:
        - *Katalog* jest Azure Active Directory, w którym tworzysz aplikację. Azure Active Directory zawiera tożsamości użytkowników, poświadczenia i inne informacje o organizacji. Jeśli nie masz Azure Active Directory, po utworzeniu subskrypcji platformy Azure zostanie utworzony jeden z nich.
        - *Subskrypcja platformy Azure* umożliwia tworzenie wystąpień usług platformy Azure. IoT Central udostępniają zasoby w ramach subskrypcji. Jeśli nie masz subskrypcji platformy Azure, możesz ją utworzyć bezpłatnie na [stronie rejestracji na platformie Azure](https://aka.ms/createazuresubscription). Po utworzeniu subskrypcji platformy Azure przejdź z powrotem do strony **Nowa aplikacja** . Twoja nowa subskrypcja zostanie wyświetlona na liście rozwijanej **subskrypcja platformy Azure** .
        - *Lokalizacja jest lokalizacją* geograficzną, [w której chcesz](https://azure.microsoft.com/global-infrastructure/geographies/) utworzyć aplikację. Zazwyczaj należy wybrać lokalizację, która jest fizycznie najbliżej Twoich urządzeń, aby uzyskać optymalną wydajność. Po wybraniu lokalizacji nie można przenieść aplikacji do innej lokalizacji.

1. Przejrzyj warunki i postanowienia, a następnie wybierz pozycję **Utwórz** w dolnej części strony. Po kilku minutach IoT Central aplikacja jest gotowa do użycia:

    :::image type="content" source="media/quick-deploy-iot-central/iotcentral-application.png" alt-text="Aplikacja IoT Central platformy Azure":::

## <a name="next-steps"></a>Następne kroki

W tym przewodniku Szybki start utworzono aplikację usługi IoT Central. Oto sugerowany następny krok, aby kontynuować uczenie się IoT Central:

> [!div class="nextstepaction"]
> [Dodawanie symulowanego urządzenia do aplikacji IoT Central](./quick-create-simulated-device.md)

Jeśli jesteś deweloperem urządzenia i chcesz szczegółowe do pewnego kodu, sugerowanym następnym krokiem jest:
> [!div class="nextstepaction"]
> [Tworzenie i łączenie aplikacji klienckiej z aplikacją usługi Azure IoT Central](./tutorial-connect-device.md)