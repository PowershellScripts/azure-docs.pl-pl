---
title: Samouczek — publikowanie wersji interfejsu API za pomocą usługi Azure API Management
description: Wykonaj kroki tego samouczka, aby dowiedzieć się, jak publikować wiele wersji interfejsu API w API Management.
author: vladvino
ms.service: api-management
ms.custom: mvc
ms.topic: tutorial
ms.date: 10/30/2020
ms.author: apimpm
ms.openlocfilehash: 4a107b4cc0dbf0b0845211ca64691fb0e792a47c
ms.sourcegitcommit: 66b0caafd915544f1c658c131eaf4695daba74c8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97679085"
---
# <a name="tutorial-publish-multiple-versions-of-your-api"></a>Samouczek: Publikowanie wielu wersji interfejsu API 

Istnieją przypadki, w których wszystkie wywołania interfejsu API mogą korzystać z tej samej wersji. Gdy obiekty wywołujące chcą uaktualnić do nowszej wersji, chcą, że podejście jest łatwe do zrozumienia. Jak pokazano w tym samouczku, można dostarczyć wiele *wersji* na platformie Azure API Management. 

W przypadku programu w tle zobacz [wersje & poprawki](https://azure.microsoft.com/blog/versions-revisions/).

Z tego samouczka dowiesz się, jak wykonywać następujące czynności:

> [!div class="checklist"]
> * Dodawanie nowej wersji do istniejącego interfejsu API
> * Wybieranie schematu wersji
> * Dodawanie wersji do produktu
> * Przeglądanie portalu dla deweloperów w celu wyświetlenia wersji

:::image type="content" source="media/api-management-getstarted-publish-versions/azure-portal.png" alt-text="Wersja pokazana w Azure Portal":::

## <a name="prerequisites"></a>Wymagania wstępne

+ Poznaj [terminologię dotyczącą usługi Azure API Management](api-management-terminology.md).
+ Wykonaj następujące kroki szybkiego startu: [Tworzenie wystąpienia usługi Azure API Management](get-started-create-service-instance.md).
+ Ponadto wykonaj zadania z następującego samouczka: [Importowanie i publikowanie pierwszego interfejsu API](import-and-publish.md).

## <a name="add-a-new-version"></a>Dodawanie nowej wersji

1. W [Azure Portal](https://portal.azure.com)przejdź do wystąpienia API Management.
1. Wybierz pozycję **Interfejsy API**.
1. Z listy interfejsów API wybierz pozycję **Wersja demonstracyjna interfejsu API Conference**. 
1. Wybierz menu kontekstowe (**...**) obok pozycji **interfejs API konferencji demonstracyjnej**.
1. Wybierz pozycję **Dodaj wersję**.

:::image type="content" source="media/api-management-getstarted-publish-versions/add-version-menu.png" alt-text="Menu kontekstowe interfejsu API — Dodawanie wersji":::


> [!TIP]
> Wersje można również włączyć podczas tworzenia nowego interfejsu API. Na ekranie **Dodawanie interfejsu API** wybierz pozycję **wersja ten interfejs API?**.

## <a name="choose-a-versioning-scheme"></a>Wybieranie schematu przechowywania wersji

Na platformie Azure API Management wybierz sposób, w jaki obiekty wywołujące określają wersję interfejsu API, wybierając *schemat obsługi wersji*: **ścieżkę, nagłówek** lub **ciąg zapytania**. W poniższym przykładzie *ścieżka* jest używana jako schemat przechowywania wersji.

Wprowadź wartości z poniższej tabeli. Następnie wybierz pozycję **Utwórz** , aby utworzyć swoją wersję.

:::image type="content" source="media/api-management-getstarted-publish-versions/add-version.png" alt-text="Okno dodawania wersji":::



|Ustawienie   |Wartość  |Opis  |
|---------|---------|---------|
|**Nazwa**     |  *Demonstracja-Konferencja-API-v1*       |  Unikatowa nazwa w wystąpieniu API Management.<br/><br/>Ponieważ wersja jest w rzeczywistości nowym interfejsem API opartym na [wersji](api-management-get-started-revise-api.md)interfejsu API, to ustawienie jest nazwą nowego interfejsu API.   |
|**Schemat przechowywania wersji**     |  **Ścieżka**       |  Metody wywołujące określają wersję interfejsu API.     |
|**Identyfikator wersja**     |  *wersjach*       |  Wskaźnik specyficzny dla schematu wersji. **Ścieżka** SUFIKSU adresu URL interfejsu API. <br/><br/> Jeśli wybrano **nagłówek** lub **ciąg zapytania** , wprowadź dodatkową wartość: nazwę parametru nagłówka lub ciągu zapytania.<br/><br/> Zostanie wyświetlony przykład użycia.        |
|**Produkty**     |  **Nieograniczona liczba**       |  Opcjonalnie jeden lub więcej produktów, z którymi jest skojarzona wersja interfejsu API. Aby opublikować interfejs API, musisz skojarzyć go z produktem. Możesz również później [dodać wersję do produktu](#add-the-version-to-a-product) .      |

Po utworzeniu wersji jest ona teraz wyświetlana poniżej **interfejsu API konferencji demonstracyjnej** na liście interfejsów API. Zobaczysz teraz dwa interfejsy API: **Original** i **V1**.

![Wersje wymienione na liście w sekcji interfejsów API w witrynie Azure Portal](media/api-management-getstarted-publish-versions/version-list.png)

Teraz można edytować i konfigurować **1** jako interfejs API, który jest oddzielony od **oryginału**. Zmiany wprowadzane w jednej wersji nie wpływają na drugą.

> [!Note]
> Jeśli zostanie dodana wersja do interfejsu API bez wersji, automatycznie zostanie utworzona **oryginalna** . Ta wersja odpowiada na domyślny adres URL. Utworzenie oryginalnej wersji gwarantuje, że wszelkie istniejące obiekty wywołujące nie zostaną przerwane przez proces dodawania wersji. Jeśli tworzysz nowy interfejs API z wersjami włączonymi na początku, oryginalny nie zostanie utworzony.

## <a name="add-the-version-to-a-product"></a>Dodawanie wersji do produktu

Aby wywołujący mogli zobaczyć nową wersję, musi zostać ona dodana do *produktu*. Jeśli wersja nie została jeszcze dodana do produktu, możesz ją dodać do produktu w dowolnym momencie.

Na przykład, aby dodać wersję do produktu **nieograniczonego** :
1. W Azure Portal przejdź do wystąpienia API Management.
1. Wybierz pozycję **produkty**  >  **nieograniczone**  >  **interfejsy API**  >  **+ Dodaj**.
1. Wybieranie **interfejsu API konferencji demonstracyjnej**, wersja **V1**.
1. Kliknij pozycję **Wybierz**.

:::image type="content" source="media/api-management-getstarted-publish-versions/08-add-multiple-versions-03-add-version-product.png" alt-text="Dodawanie wersji do produktu":::

## <a name="browse-the-developer-portal-to-see-the-version"></a>Przeglądanie portalu dla deweloperów w celu wyświetlenia wersji

Po wypróbowaniu portalu dla [deweloperów](api-management-howto-developer-portal-customize.md)można zobaczyć wersje interfejsu API w tym miejscu.

1. Wybierz opcję **Portal dla deweloperów** z górnego menu.
2. Wybierz pozycję **Interfejsy API**, a następnie wybierz pozycję **Wersja demonstracyjna interfejsu API Conference**.
3. Powinna zostać wyświetlona lista rozwijana z wieloma wersjami obok nazwy interfejsu API.
4. Wybierz opcję **v1**.
5. Zwróć uwagę na **Adres URL żądania** pierwszej operacji na liście. Pozycja pokazuje, że ścieżka adresu URL interfejsu API uwzględnia ciąg **v1**.

## <a name="next-steps"></a>Następne kroki

W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Dodawanie nowej wersji do istniejącego interfejsu API
> * Wybieranie schematu wersji 
> * Dodawanie wersji do produktu
> * Przeglądanie portalu dla deweloperów w celu wyświetlenia wersji

Przejdź do następnego samouczka:

> [!div class="nextstepaction"]
> [Dostosowywanie stylu stron portalu deweloperów](api-management-howto-developer-portal-customize.md)
