---
title: 'Samouczek: integracja Azure Active Directory z systemem LMS Microsoft Docs'
description: Dowiedz się, jak skonfigurować logowanie jednokrotne między usługą Azure Active Directory i usługą Absorb LMS.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 04/02/2019
ms.author: jeedes
ms.openlocfilehash: 3d90d35e113b5f9757faf59681bb2532b66f2b09
ms.sourcegitcommit: d79513b2589a62c52bddd9c7bd0b4d6498805dbe
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97673872"
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a>Samouczek: integracja Azure Active Directory z systemem LMS

Z tego samouczka dowiesz się, jak zintegrować usługę Absorb LMS z usługą Azure Active Directory (Azure AD).
Integracja usługi Absorb LMS z usługą Azure AD zapewnia następujące korzyści:

* Kontrolowanie w usłudze Azure AD, kto ma dostęp do usługi Absorb LMS.
* Umożliwianie użytkownikom automatycznego logowania się do usługi Absorb LMS (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
* Możesz zarządzać swoimi kontami w jednej centralnej lokalizacji — witrynie Azure Portal.

Jeśli chcesz dowiedzieć się więcej na temat integracji aplikacji SaaS z usługą Azure AD, zobacz [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).
Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem [utwórz bezpłatne konto](https://azure.microsoft.com/free/).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD z usługą Absorb LMS, potrzebne są następujące elementy:

* Subskrypcja usługi Azure AD. Jeśli nie masz środowiska usługi Azure AD, możesz uzyskać [bezpłatne konto](https://azure.microsoft.com/free/)
* Subskrypcja usługi Absorb LMS z obsługą logowania jednokrotnego

> [!NOTE]
> Ta integracja jest również dostępna do użycia w środowisku chmury dla instytucji rządowych USA usługi Azure AD. Tę aplikację można znaleźć w galerii aplikacji w chmurze dla instytucji rządowych USA usługi Azure AD i skonfigurować ją w taki sam sposób, jak w przypadku chmury publicznej.

## <a name="scenario-description"></a>Opis scenariusza

W tym samouczku skonfigurujesz i przetestujesz logowanie jednokrotne usługi Azure AD w środowisku testowym.

* Usługa Absorb LMS obsługuje logowanie jednokrotne inicjowane przez **dostawcę tożsamości**

## <a name="adding-absorb-lms-from-the-gallery"></a>Dodawanie usługi Absorb LMS z galerii

Aby skonfigurować integrację usługi Absorb LMS z usługą Azure AD, należy dodać usługę Absorb LMS z galerii do listy zarządzanych aplikacji SaaS.

**Aby dodać usługę Absorb LMS z galerii, wykonaj następujące czynności:**

1. W witrynie **[Azure Portal](https://portal.azure.com)** w panelu nawigacyjnym po lewej stronie kliknij ikonę usługi **Azure Active Directory**.

    ![Przycisk Azure Active Directory](common/select-azuread.png)

2. Przejdź do grupy **Aplikacje dla przedsiębiorstw** i wybierz opcję **Wszystkie aplikacje**.

    ![Blok Aplikacje dla przedsiębiorstw](common/enterprise-applications.png)

3. Aby dodać nową aplikację, kliknij przycisk **Nowa aplikacja** w górnej części okna dialogowego.

    ![Przycisk Nowa aplikacja](common/add-new-app.png)

4. W polu wyszukiwania wpisz ciąg **Absorb LMS**, wybierz pozycję **Absorb LMS** z panelu wyników, a następnie kliknij przycisk **Dodaj**, aby dodać aplikację.

    ![Usługa Absorb LMS na liście wyników](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie logowania jednokrotnego usługi Azure AD

W tej sekcji skonfigurujesz i przetestujesz logowanie jednokrotne usługi Azure AD w usłudze Absorb LMS, korzystając z danych testowego użytkownika **Britta Simon**.
Aby logowanie jednokrotne działało, należy ustanowić relację połączenia między użytkownikiem usługi Azure AD i powiązanym użytkownikiem usługi Absorb LMS.

Aby skonfigurować i przetestować logowanie jednokrotne usługi Azure AD w usłudze Absorb LMS, należy wykonać czynności opisane w poniższych blokach konstrukcyjnych:

1. **[Konfigurowanie logowania jednokrotnego usługi Azure AD](#configure-azure-ad-single-sign-on)** — aby umożliwić użytkownikom korzystanie z tej funkcji.
2. **[Konfigurowanie logowania jednokrotnego w usłudze Absorb LMS](#configure-absorb-lms-single-sign-on)** — aby skonfigurować ustawienia logowania jednokrotnego po stronie aplikacji.
3. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)** — aby przetestować logowanie jednokrotne usługi Azure AD z użytkownikiem Britta Simon.
4. **[Przypisywanie użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)** — aby umożliwić użytkownikowi Britta Simon korzystanie z logowania jednokrotnego usługi Azure AD.
5. **[Tworzenie użytkownika testowego usługi Absorb LMS](#create-absorb-lms-test-user)** — aby mieć w usłudze Absorb LMS odpowiednik użytkownika Britta Simon połączony z reprezentacją użytkownika w usłudze Azure AD.
6. **[Testowanie logowania jednokrotnego](#test-single-sign-on)** — aby sprawdzić, czy konfiguracja działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie logowania jednokrotnego usługi Azure AD

W tej sekcji włączysz logowanie jednokrotne usługi Azure AD w witrynie Azure Portal.

Aby skonfigurować logowanie jednokrotne usługi Azure AD w usłudze Absorb LMS, wykonaj następujące kroki:

1. W witrynie [Azure Portal](https://portal.azure.com/) na stronie integracji aplikacji **Absorb LMS** wybierz pozycję **Logowanie jednokrotne**.

    ![Link do konfigurowania logowania jednokrotnego](common/select-sso.png)

2. W oknie dialogowym **Wybieranie metody logowania jednokrotnego** wybierz tryb **SAML/WS-Fed**, aby włączyć logowanie jednokrotne.

    ![Wybieranie trybu logowania jednokrotnego](common/select-saml-option.png)

3. Na stronie **Konfigurowanie logowania jednokrotnego za pomocą protokołu SAML** kliknij ikonę **Edytuj**, aby otworzyć okno dialogowe **Podstawowa konfiguracja protokołu SAML**.

    ![Edycja podstawowej konfiguracji protokołu SAML](common/edit-urls.png)

4. Na stronie **Konfigurowanie logowania jednokrotnego za pomocą protokołu SAML** kliknij przycisk **Edytuj**, aby otworzyć okno dialogowe **Podstawowa konfiguracja protokołu SAML**.

    ![Informacje dotyczące domeny i adresów URL logowania jednokrotnego w usłudze Absorb LMS](common/idp-intiated.png)

    Jeśli korzystasz z **interfejsu użytkownika usługi Absorb 5**, użyj następującej konfiguracji:

    a. W polu tekstowym **Identyfikator** wpisz adres URL, używając następującego wzorca: `https://company.myabsorb.com/account/saml`

    b. W polu tekstowym **Adres URL odpowiedzi** wpisz adres URL, korzystając z następującego wzorca: `https://company.myabsorb.com/account/saml`

    Jeśli korzystasz ze **środowiska nowego ucznia usługi Absorb 5**, użyj następującej konfiguracji:

    a. W polu tekstowym **Identyfikator** wpisz adres URL, używając następującego wzorca: `https://company.myabsorb.com/api/rest/v2/authentication/saml`

    b. W polu tekstowym **Adres URL odpowiedzi** wpisz adres URL, korzystając z następującego wzorca: `https://company.myabsorb.com/api/rest/v2/authentication/saml`

    > [!NOTE]
    > Te wartości nie są prawdziwe. Zastąp te wartości rzeczywistymi wartościami identyfikatora i adresu URL odpowiedzi. W celu uzyskania tych wartości skontaktuj się z [zespołem pomocy technicznej klienta usługi Absorb LMS](https://support.absorblms.com/hc/). Przydatne mogą się również okazać wzorce przedstawione w sekcji **Podstawowa konfiguracja protokołu SAML** w witrynie Azure Portal.

5. Na poniższym zrzucie ekranu przedstawiono listę atrybutów domyślnych, gdzie atrybut **nameidentifier** jest mapowany na atrybut **user.userprincipalname**.

    ![image (obraz)](common/edit-attribute.png)

6. Na stronie **Konfigurowanie logowania jednokrotnego za pomocą protokołu SAML** w sekcji **Certyfikat podpisywania SAML** kliknij link **Pobierz**, aby pobrać **kod XML metadanych federacji** na podstawie podanych opcji zgodnie z wymaganiami i zapisać go na komputerze.

    ![Link do pobierania certyfikatu](common/metadataxml.png)

7. W sekcji **Konfigurowanie usługi Absorb LMS** skopiuj odpowiednie adresy URL zgodnie z wymaganiami.

    ![Kopiowanie adresów URL konfiguracji](common/copy-configuration-urls.png)

    a. Adres URL logowania

    b. Identyfikator usługi Azure AD

    c. Adres URL wylogowywania

### <a name="configure-absorb-lms-single-sign-on"></a>Konfigurowanie logowania jednokrotnego w usłudze Absorb LMS

1. W nowym oknie przeglądarki internetowej zaloguj się jako administrator do firmowej witryny usługi Absorb LMS.

2. Wybierz przycisk **Account** (Konto) w prawym górnym rogu.

    ![Przycisk Account (Konto)](./media/absorblms-tutorial/1.png)

3. W okienku Account (Konto) wybierz pozycję **Portal Settings** (Ustawienia portalu).

    ![Link Portal Settings (Ustawienia portalu)](./media/absorblms-tutorial/2.png)

4. Wybierz kartę **Manage SSO Settings** (Zarządzaj ustawieniami logowania jednokrotnego).

    ![Karta Users (Użytkownicy)](./media/absorblms-tutorial/managesso.png)

5. Na stronie **Manage Single Sign-On Settings** (Zarządzanie ustawieniami logowania jednokrotnego) wykonaj następujące czynności:

    ![Strona konfiguracji logowania jednokrotnego](./media/absorblms-tutorial/settings.png)

    a. W polu tekstowym **Name** (Nazwa) wprowadź nazwę, np. Logowanie jednokrotne witryny Azure AD Marketplace.

    b. W polu **Method** (Metoda) wybierz pozycję **SAML**.

    c. W Notatniku otwórz certyfikat pobrany z witryny Azure Portal. Usuń tagi **---BEGIN CERTIFICATE---** i **---END CERTIFICATE---**. Następnie w polu **Key** (Klucz) wklej pozostałą zawartość.

    d. W polu **Mode** (Tryb) wybierz pozycję **Identity Provider Initiated** (Inicjowane przez dostawcę tożsamości).

    e. W polu **Id Property** (Właściwość identyfikatora) wybierz atrybut, który został skonfigurowany jako identyfikator użytkownika w usłudze Azure AD. Na przykład jeśli wybrano pozycję *NameIdentifier* w usłudze Azure AD, wybierz pozycję **username**.

    f. W polu **Signature Type** (Typ podpisu) wybierz pozycję **Sha256**.

    przykład W polu **Login URL** (Adres URL logowania) wklej wartość pola **Adres URL na potrzeby uzyskiwania dostępu przez użytkowników** ze strony **Właściwości** aplikacji w witrynie Azure Portal.

    h. W polu **Logout URL** (Adres URL wylogowywania) wklej wartość pola **Adres URL wylogowywania** skopiowaną z okna **Konfigurowanie logowania** w witrynie Azure Portal.

    i. Przełącz opcję **Automatically Redirect** (Automatyczne przekierowywanie) na wartość **On** (Włączone).

6. Wybierz pozycję **Zapisz.**

    ![Przełącznik zezwalania na logowanie tylko za pomocą funkcji logowania jednokrotnego](./media/absorblms-tutorial/save.png)

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

W tej sekcji w witrynie Azure Portal utworzysz użytkownika testowego o nazwie Britta Simon.

1. W witrynie Azure Portal w okienku po lewej stronie wybierz pozycję **Azure Active Directory**, wybierz opcję **Użytkownicy**, a następnie wybierz pozycję **Wszyscy użytkownicy**.

    ![Linki „Użytkownicy i grupy” i „Wszyscy użytkownicy”](common/users.png)

2. Wybierz pozycję **nowy użytkownik** w górnej części ekranu.

    ![Przycisk Nowy użytkownik](common/new-user.png)

3. We właściwościach użytkownika wykonaj następujące kroki.

    ![Okno dialogowe Użytkownik](common/user-properties.png)

    a. W polu **Nazwa** wprowadź **BrittaSimon**.

    b. W polu **Nazwa użytkownika** wpisz `brittasimon\@yourcompanydomain.extension`  
    Na przykład BrittaSimon@contoso.com

    c. Zaznacz pole wyboru **Pokaż hasło** i zanotuj wartość wyświetlaną w polu Hasło.

    d. Kliknij pozycję **Utwórz**.

### <a name="assign-the-azure-ad-test-user"></a>Przypisywanie użytkownika testowego usługi Azure AD

W tej sekcji włączysz użytkownikowi Britta Simon możliwość korzystania z logowania jednokrotnego platformy Azure, udzielając dostępu do usługi Absorb LMS.

1. W witrynie Azure Portal wybierz pozycję **Aplikacje dla przedsiębiorstw** i **Wszystkie aplikacje**, a następnie wybierz pozycję **Absorb LMS**.

    ![Blok Aplikacje dla przedsiębiorstw](common/enterprise-applications.png)

2. Na liście aplikacji wpisz nazwę usługi **Absorb LMS** i wybierz ją.

    ![Link do usługi Absorb LMS na liście aplikacji](common/all-applications.png)

3. W menu po lewej stronie wybierz pozycję **Użytkownicy i grupy**.

    ![Link „Użytkownicy i grupy”](common/users-groups-blade.png)

4. Kliknij przycisk **Dodaj użytkownika**, a następnie wybierz pozycję **Użytkownicy i grupy** w oknie dialogowym **Dodawanie przypisania**.

    ![Okienko Dodawanie przypisania](common/add-assign-user.png)

5. W oknie dialogowym **Użytkownicy i grupy** wybierz użytkownika **Britta Simon** na liście użytkowników, a następnie kliknij przycisk **Wybierz** u dołu ekranu.

6. Jeśli oczekujesz, że masz dowolną wartość roli w potwierdzeniu SAML, w oknie dialogowym **Wybierz rolę** wybierz odpowiednią rolę dla użytkownika z listy, a następnie kliknij przycisk **Wybierz** w dolnej części ekranu.

7. W oknie dialogowym **Dodawanie przypisania** kliknij przycisk **Przypisz**.

### <a name="create-absorb-lms-test-user"></a>Tworzenie użytkownika testowego usługi Absorb LMS

Aby użytkownicy usługi Azure AD mogli zalogować się do usługi Absorb LMS, muszą być oni skonfigurowani w usłudze Absorb LMS. W przypadku usługi Absorb LMS aprowizacja to zadanie wykonywane ręcznie.

**Aby skonfigurować aprowizację użytkowników, wykonaj następujące kroki:**

1. Zaloguj się jako administrator do firmowej witryny usługi Absorb LMS.

2. W okienku **Users** (Użytkownicy) wybierz pozycję **Users** (Użytkownicy).

    ![Link Users (Użytkownicy)](./media/absorblms-tutorial/absorblms_userssub.png)

3. Wybierz kartę **User** (Użytkownik).

    ![Lista rozwijana Add New (Dodaj nowego)](./media/absorblms-tutorial/absorblms_createuser.png)

4. Na stronie **Add User** (Dodawanie użytkownika) wykonaj następujące czynności:

    ![Strona Add User (Dodawanie użytkownika)](./media/absorblms-tutorial/user.png)

    a. W polu **First Name** (Imię) wpisz imię, np. **Britta**.

    b. W polu **Last Name** (Nazwisko) wpisz nazwisko, np. **Simon**.

    c. W polu **Username** (Nazwa użytkownika) wpisz imię i nazwisko, np. **Britta Simon**.

    d. W polu **Password** (Hasło) wpisz hasło użytkownika.

    e. W polu **Confirm Password** (Potwierdź hasło) ponownie wpisz hasło.

    f. Ustaw przełącznik **Is Active** (Jest aktywny) na wartość **Active** (Aktywny).

5. Wybierz pozycję **Zapisz.**

    ![Przełącznik zezwalania na logowanie tylko za pomocą funkcji logowania jednokrotnego](./media/absorblms-tutorial/save.png)

    > [!NOTE]
    > Domyślnie aprowizacja użytkowników nie jest włączona w ramach logowania jednokrotnego. Jeśli klient chce włączyć tę funkcję, musi ją skonfigurować w sposób opisany w [tej](https://support.absorblms.com/hc/en-us/articles/360014083294-Incoming-SAML-2-0-SSO-Account-Provisioning) dokumentacji. Ponadto należy pamiętać, że aprowizacja użytkowników jest dostępna tylko w **środowisku nowego ucznia usługi Absorb 5** przy użyciu adresu URL usługi ACS: `https://company.myabsorb.com/api/rest/v2/authentication/saml`

### <a name="test-single-sign-on"></a>Testowanie logowania jednokrotnego

W tej sekcji przetestujesz konfigurację logowania jednokrotnego usługi Azure AD przy użyciu panelu dostępu.

Po kliknięciu kafelka Absorb LMS na panelu dostępu powinno nastąpić automatyczne zalogowanie do usługi Absorb LMS, dla której skonfigurowano logowanie jednokrotne. Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](../user-help/my-apps-portal-end-user-access.md).

## <a name="additional-resources"></a>Zasoby dodatkowe

- [Lista samouczków dotyczących sposobu integrowania aplikacji SaaS z usługą Azure Active Directory](./tutorial-list.md)

- [Czym jest dostęp do aplikacji i logowanie jednokrotne za pomocą usługi Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

- [Co to jest dostęp warunkowy w usłudze Azure Active Directory?](../conditional-access/overview.md)