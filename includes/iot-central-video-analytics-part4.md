---
title: plik dołączania
description: plik dołączania
services: iot-central
author: dominicbetts
ms.service: iot-central
ms.topic: include
ms.date: 10/06/2020
ms.author: dobett
ms.custom: include file
ms.openlocfilehash: 0b3ccc31c9159b5d7b1615add89e8fdc308bf8df
ms.sourcegitcommit: d6e92295e1f161a547da33999ad66c94cf334563
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2020
ms.locfileid: "96763463"
---
### <a name="publish-the-device-template"></a>Publikowanie szablonu urządzenia

Aby można było dodać urządzenie do aplikacji, należy opublikować szablon urządzenia:

1. W szablonie urządzenia **bramy LVA Edge w wersji 2** wybierz pozycję **Publikuj**.

1. Na stronie **Publikuj ten szablon urządzenia na potrzeby aplikacji** wybierz pozycję **Publikuj**.

**LVA graniczny Gateway v2** jest teraz dostępna jako typ urządzenia do użycia na stronie **urządzenia** w aplikacji.

## <a name="migrate-the-gateway-device"></a>Migrowanie urządzenia bramy

Istniejące urządzenie **Gateway-001** używa szablonu urządzenia **bramy LVA Edge** . Aby użyć nowego manifestu wdrożenia, Przeprowadź migrację urządzenia do nowego szablonu urządzenia:

Aby przeprowadzić migrację urządzenia z **bramą-001** :

1. Przejdź do strony **urządzenia** i wybierz urządzenie **bramy-001** w celu wyróżnienia go na liście.

1. Wybierz pozycję **Migruj**. Jeśli ikona **migracji** nie jest widoczna, wybierz pozycję **...** , aby wyświetlić więcej opcji.

    :::image type="content" source="media/iot-central-video-analytics-part4/migrate-device.png" alt-text="Migrowanie urządzenia bramy do nowej wersji":::

1. Na liście w oknie dialogowym **Migrowanie** wybierz pozycję **LVA Edge Gateway v2**, a następnie wybierz pozycję **Migruj**.

Po kilku sekundach migracja zostanie zakończona. Urządzenie korzysta teraz z szablonu urządzenia **LVA Edge Gateway v2** z dostosowanym manifestem wdrożenia.

Obecnie nie ma żadnych urządzeń korzystających z oryginalnego szablonu urządzenia **bramy LVA Edge** . Usuń ten szablon urządzenia:

1. Przejdź do strony **Szablony urządzeń** i wybierz szablon urządzenia **bramy LVA Edge** .

1. Wybierz pozycję **Usuń** , aby usunąć szablon urządzenia.

### <a name="get-the-device-credentials"></a>Pobieranie poświadczeń urządzenia

Wymagane są poświadczenia zezwalające urządzeniu na łączenie się z aplikacją IoT Central. Pobierz poświadczenia urządzenia:

1. Na stronie **urządzenia** wybierz urządzenie **bramy-001** .

1. Wybierz pozycję **Połącz**.

1. Na stronie **połączenie urządzenia** zanotuj *scratchpad.txt* pliku z **zakresem identyfikatorów**, **identyfikatorem urządzenia** i **kluczem podstawowym** urządzenia. Te wartości są używane później.

1. Upewnij się, że metoda połączenia jest ustawiona na **sygnaturę dostępu współdzielonego**.

1. Wybierz pozycję **Zamknij**.

## <a name="next-steps"></a>Następne kroki

Aplikacja IoT Central została utworzona przy użyciu szablonu **wideo Analytics — obiekty i wykrywanie ruchu** , utworzyła szablon urządzenia dla urządzenia bramy i dodał urządzenie bramy do aplikacji.

Jeśli chcesz wypróbować aplikację do wykrywania obiektów wideo i wykrycia ruchu przy użyciu modułów IoT Edge, na których uruchomiono maszynę wirtualną w chmurze z symulowanymi strumieniami wideo:

> [!div class="nextstepaction"]
> [Tworzenie wystąpienia IoT Edge dla analiz wideo (maszyna wirtualna z systemem Linux)](../articles/iot-central/retail/tutorial-video-analytics-iot-edge-vm.md)

Jeśli chcesz wypróbować aplikację do wykrywania obiektów wideo i wykrycia ruchu przy użyciu modułów IoT Edge, na których działa rzeczywiste urządzenie z **ONVIFą** kamerą:

> [!div class="nextstepaction"]
> [Tworzenie wystąpienia IoT Edge dla analiz wideo (Intel NUC)](../articles/iot-central/retail/tutorial-video-analytics-iot-edge-nuc.md)
