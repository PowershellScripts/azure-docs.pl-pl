---
title: 'Samouczek Azure Active Directory: integracja logowania jednokrotnego (SSO) z usługą Resource Central | Microsoft Docs'
description: Dowiedz się, jak skonfigurować Logowanie jednokrotne między usługami Azure Active Directory i Resource Central.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: CelesteDG
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 11/06/2020
ms.author: jeedes
ms.openlocfilehash: 2430de60b3de5812090496fa66e36b3d7515c6b1
ms.sourcegitcommit: 4295037553d1e407edeb719a3699f0567ebf4293
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/30/2020
ms.locfileid: "96327376"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-resource-central"></a>Samouczek: integracja z logowaniem jednokrotnym (SSO) Azure Active Directory przy użyciu Centrum zasobów

W tym samouczku dowiesz się, jak zintegrować usługę Resource Central z Azure Active Directory (Azure AD). Podczas integrowania zasobów centralnych z usługą Azure AD można:

* Kontrolka w usłudze Azure AD, która ma dostęp do centrum zasobów.
* Zezwól użytkownikom na automatyczne logowanie do zasobów centralnych przy użyciu kont usługi Azure AD.
* Zarządzaj kontami w jednej centralnej lokalizacji — Azure Portal.

## <a name="prerequisites"></a>Wymagania wstępne

Aby rozpocząć, potrzebne są następujące elementy:

* Subskrypcja usługi Azure AD. Jeśli nie masz subskrypcji, możesz uzyskać [bezpłatne konto](https://azure.microsoft.com/free/).
* Subskrypcja z włączonym logowaniem jednokrotnym (SSO) zasobów.

## <a name="scenario-description"></a>Opis scenariusza

W tym samouczku skonfigurujesz i testujesz Logowanie jednokrotne usługi Azure AD w środowisku testowym.

* Usługa Resource Central obsługuje logowanie jednokrotne w usłudze **SP**

* Centrum zasobów jest obsługiwane przez funkcję aprowizacji użytkowników **just in Time**

## <a name="adding-resource-central-from-the-gallery"></a>Dodawanie zasobów centralnych z galerii

Aby skonfigurować integrację zasobów centralnych z usługą Azure AD, należy dodać centrum zasobów z galerii do listy zarządzanych aplikacji SaaS.

1. Zaloguj się do Azure Portal przy użyciu konta służbowego lub konto Microsoft prywatnego.
1. W okienku nawigacji po lewej stronie wybierz usługę **Azure Active Directory** .
1. Przejdź do **aplikacji przedsiębiorstwa** , a następnie wybierz pozycję **wszystkie aplikacje**.
1. Aby dodać nową aplikację, wybierz pozycję **Nowa aplikacja**.
1. W sekcji **Dodaj z galerii** wpisz **zasób środkowe** w polu wyszukiwania.
1. Wybierz pozycję **zasób centralnie** z panelu wyników, a następnie Dodaj aplikację. Poczekaj kilka sekund, gdy aplikacja zostanie dodana do dzierżawy.


## <a name="configure-and-test-azure-ad-sso-for-resource-central"></a>Konfigurowanie i testowanie rejestracji jednokrotnej usługi Azure AD dla zasobów centralnych

Skonfiguruj i przetestuj Logowanie jednokrotne usługi Azure AD za pomocą Centrum zasobów przy użyciu użytkownika testowego o nazwie **B. Simon**. Aby logowanie jednokrotne działało, należy ustanowić relację linku między użytkownikiem usługi Azure AD i powiązanym użytkownikiem w centrum zasobów.

Aby skonfigurować i przetestować Logowanie jednokrotne usługi Azure AD przy użyciu Centrum zasobów, wykonaj następujące czynności:

1. **[Skonfiguruj Logowanie jednokrotne usługi Azure AD](#configure-azure-ad-sso)** , aby umożliwić użytkownikom korzystanie z tej funkcji.
    1. **[Utwórz użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)** — aby przetestować Logowanie jednokrotne w usłudze Azure AD za pomocą usługi B. Simon.
    1. **[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)** — aby umożliwić usłudze B. Simon korzystanie z logowania jednokrotnego w usłudze Azure AD.
1. **[Skonfiguruj centralne Logowanie jednokrotne](#configure-resource-central-sso)** w celu skonfigurowania ustawień logowania jednokrotnego na stronie aplikacji.
    1. **[Utwórz zasób test centralny zasobów](#create-resource-central-test-user)** , aby uzyskać odpowiednika B. Simon w usłudze Resource Central, która jest połączona z reprezentacją użytkownika w usłudze Azure AD.
1. **[Przetestuj Logowanie jednokrotne](#test-sso)** — aby sprawdzić, czy konfiguracja działa.

## <a name="configure-azure-ad-sso"></a>Konfigurowanie rejestracji jednokrotnej w usłudze Azure AD

Wykonaj następujące kroki, aby włączyć logowanie jednokrotne usługi Azure AD w Azure Portal.

1. W Azure Portal na stronie integracja z **centralną aplikacją zasobów** Znajdź sekcję **Zarządzanie** i wybierz pozycję **Logowanie jednokrotne**.
1. Na stronie **Wybierz metodę logowania jednokrotnego** wybierz pozycję **SAML**.
1. Na stronie **Konfigurowanie logowania jednokrotnego przy użyciu języka SAML** kliknij ikonę Edytuj/pióro, aby określić **podstawową konfigurację języka SAML** , aby edytować ustawienia.

   ![Edycja podstawowej konfiguracji protokołu SAML](common/edit-urls.png)

1. W sekcji **Podstawowa konfiguracja języka SAML** wprowadź wartości dla następujących pól:

    a. W polu tekstowym **Adres URL logowania** wpisz adres URL, używając następującego wzorca: `https://<DOMAIN_NAME>/ResourceCentral`

    b. W polu tekstowym **Identyfikator (identyfikator jednostki)** wpisz adres URL, używając następującego wzorca: `https://<DOMAIN_NAME>/ResourceCentral`

    c. W polu tekstowym **Adres URL odpowiedzi** wpisz adres URL, korzystając z następującego wzorca: `https://<DOMAIN_NAME>/ResourceCentral/ExAuth/Saml2Authentication/Acs`

    > [!NOTE]
    > Te wartości nie są prawdziwe. Zastąp je rzeczywistymi wartościami adresu URL logowania, identyfikatora i adresu URL odpowiedzi. Aby uzyskać te wartości, skontaktuj się z [zespołem pomocy technicznej dla klientów centralnych zasobów](mailto:st@aod.vn) . Przydatne mogą się również okazać wzorce przedstawione w sekcji **Podstawowa konfiguracja protokołu SAML** w witrynie Azure Portal.

1. Na stronie **Konfigurowanie logowania jednokrotnego przy użyciu języka SAML** w sekcji **certyfikat podpisywania SAML** Znajdź **certyfikat (base64)** i wybierz pozycję **Pobierz** , aby pobrać certyfikat i zapisać go na komputerze.

    ![Link do pobierania certyfikatu](common/certificatebase64.png)

1. W sekcji **Konfigurowanie zasobów centralnych** skopiuj odpowiednie adresy URL na podstawie wymagań.

    ![Kopiowanie adresów URL konfiguracji](common/copy-configuration-urls.png)
### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

W tej sekcji utworzysz użytkownika testowego w Azure Portal o nazwie B. Simon.

1. W lewym okienku w Azure Portal wybierz pozycję **Azure Active Directory**, wybierz pozycję **Użytkownicy**, a następnie wybierz pozycję **Wszyscy użytkownicy**.
1. Wybierz pozycję **nowy użytkownik** w górnej części ekranu.
1. We właściwościach **użytkownika** wykonaj następujące kroki:
   1. W polu **Nazwa** wprowadź wartość `B.Simon`.  
   1. W polu **Nazwa użytkownika** wprowadź wartość username@companydomain.extension . Na przykład `B.Simon@contoso.com`.
   1. Zaznacz pole wyboru **Pokaż hasło** i zanotuj wartość wyświetlaną w polu **Hasło**.
   1. Kliknij pozycję **Utwórz**.

### <a name="assign-the-azure-ad-test-user"></a>Przypisywanie użytkownika testowego usługi Azure AD

W tej sekcji włączysz usługę B. Simon, aby korzystać z logowania jednokrotnego na platformie Azure przez przyznanie dostępu do centrum zasobów.

1. W Azure Portal wybierz pozycję **aplikacje dla przedsiębiorstw**, a następnie wybierz pozycję **wszystkie aplikacje**.
1. Na liście Aplikacje wybierz pozycję **zasób centralny**.
1. Na stronie Przegląd aplikacji Znajdź sekcję **Zarządzanie** i wybierz pozycję **Użytkownicy i grupy**.
1. Wybierz pozycję **Dodaj użytkownika**, a następnie w oknie dialogowym **Dodawanie przypisania** wybierz pozycję **Użytkownicy i grupy** .
1. W oknie dialogowym **Użytkownicy i grupy** wybierz pozycję **B. Simon** z listy Użytkownicy, a następnie kliknij przycisk **Wybierz** w dolnej części ekranu.
1. Jeśli oczekujesz, że rola ma być przypisana do użytkowników, możesz wybrać ją z listy rozwijanej **Wybierz rolę** . Jeśli nie skonfigurowano roli dla tej aplikacji, zostanie wyświetlona wybrana rola "domyślny dostęp".
1. W oknie dialogowym **Dodawanie przypisania** kliknij przycisk **Przypisz** .

## <a name="configure-resource-central-sso"></a>Skonfiguruj centralne Logowanie jednokrotne zasobów

Aby skonfigurować Logowanie jednokrotne na stronie **centralnej zasobów** , musisz wysłać pobrany **certyfikat (base64)** i odpowiednie skopiowane adresy URL z Azure Portal do [zespołu pomocy centralnej zasobów](mailto:rc@aod.vn). Ustawią oni to ustawienie tak, aby połączenie logowania jednokrotnego SAML było ustawione właściwie po obu stronach.

### <a name="create-resource-central-test-user"></a>Tworzenie użytkownika testowego zasobów centralnych

W tej sekcji użytkownik o nazwie Britta Simon został utworzony w centrum zasobów. Funkcja Resource Central obsługuje Inicjowanie obsługi użytkowników just-in-Time, która jest domyślnie włączona. W tej sekcji nie musisz niczego robić. Jeśli użytkownik nie istnieje jeszcze w centrum zasobów, zostanie utworzony nowy po uwierzytelnieniu.

## <a name="test-sso"></a>Testuj Logowanie jednokrotne 

W tej sekcji przetestujesz konfigurację logowania jednokrotnego usługi Azure AD przy użyciu następujących opcji. 

* Kliknij pozycję **Testuj tę aplikację** w Azure Portal. Spowoduje to przekierowanie na adres URL logowania centralnego zasobu, w którym można zainicjować przepływ logowania. 

* Bezpośrednio przejdź do adresu URL logowania do zasobów centralnych i zainicjuj w nim przepływ logowania.

* Możesz użyć panelu programu Microsoft Access. Po kliknięciu kafelka centrum zasobów w panelu dostępu zostanie on przekierowany do adresu URL logowania centralnego zasobu. Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](../user-help/my-apps-portal-end-user-access.md).


## <a name="next-steps"></a>Następne kroki

Po skonfigurowaniu centrum zasobów można wymusić kontrolę sesji, co chroni eksfiltracji i niefiltrowanie danych poufnych organizacji w czasie rzeczywistym. Kontrolka sesji rozciąga się od dostępu warunkowego. [Dowiedz się, jak wymuszać kontrolę sesji za pomocą Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-any-app).