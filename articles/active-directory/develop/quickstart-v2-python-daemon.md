---
title: 'Szybki Start: wywoływanie Microsoft Graph z demona języka Python | Azure'
titleSuffix: Microsoft identity platform
description: W tym przewodniku szybki start dowiesz się, jak proces języka Python może uzyskać token dostępu i wywołać interfejs API chroniony przez punkt końcowy platformy tożsamości firmy Microsoft przy użyciu własnej tożsamości aplikacji
services: active-directory
author: jmprieur
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: quickstart
ms.workload: identity
ms.date: 10/22/2019
ms.author: jmprieur
ms.custom: aaddev, identityplatformtop40, devx-track-python, scenarios:getting-started, languages:Python
ms.openlocfilehash: 47aaf67c9ae2402e0445de60de439b77242bd87d
ms.sourcegitcommit: c136985b3733640892fee4d7c557d40665a660af
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/13/2021
ms.locfileid: "98178232"
---
# <a name="quickstart-acquire-a-token-and-call-microsoft-graph-api-from-a-python-console-app-using-apps-identity"></a>Szybki Start: uzyskiwanie tokenu i wywoływanie Microsoft Graph interfejsu API z aplikacji konsolowej języka Python przy użyciu tożsamości aplikacji

W tym przewodniku szybki start pobrano i uruchomiono przykład kodu, który pokazuje, jak aplikacja Python może uzyskać token dostępu przy użyciu tożsamości aplikacji w celu wywołania interfejsu API Microsoft Graph i wyświetlenia [listy użytkowników](/graph/api/user-list) w katalogu. Przykład kodu demonstruje, jak zadanie nienadzorowane lub usługa systemu Windows mogą być uruchamiane przy użyciu tożsamości aplikacji, a nie tożsamości użytkownika. 

> [!div renderon="docs"]
> ![Pokazuje sposób działania przykładowej aplikacji wygenerowanej przez ten przewodnik Szybki Start](media/quickstart-v2-netcore-daemon/netcore-daemon-intro.svg)

## <a name="prerequisites"></a>Wymagania wstępne

Do uruchomienia tego przykładu potrzebne są:

- [Python 2.7 +](https://www.python.org/downloads/release/python-2713) lub [Python 3 +](https://www.python.org/downloads/release/python-364/)
- [MSAL Python](https://github.com/AzureAD/microsoft-authentication-library-for-python)

> [!div renderon="docs"]
> ## <a name="register-and-download-your-quickstart-app"></a>Rejestrowanie i pobieranie aplikacji Szybki start

> [!div renderon="docs" class="sxs-lookup"]
>
> Dostępne są dwie opcje uruchomienia aplikacji szybkiego startu: Express (opcja 1 poniżej) i ręczna (opcja 2)
>
> ### <a name="option-1-register-and-auto-configure-your-app-and-then-download-your-code-sample"></a>Opcja 1. Zarejestrowanie i automatyczne skonfigurowanie aplikacji, a następnie pobranie przykładowego kodu
>
> 1. Przejdź do środowiska szybkiego startu w <a href="https://portal.azure.com/?Microsoft_AAD_RegisteredApps=true#blade/Microsoft_AAD_RegisteredApps/applicationsListBlade/quickStartType/PythonDaemonQuickstartPage/sourceType/docs" target="_blank">Azure Portal rejestracje aplikacji <span class="docon docon-navigate-external x-hidden-focus"></span> </a> .
> 1. Wprowadź nazwę aplikacji i wybierz pozycję **Zarejestruj**.
> 1. Postępuj zgodnie z instrukcjami, aby pobrać i automatycznie skonfigurować nową aplikację za pomocą tylko jednego kliknięcia.
>
> ### <a name="option-2-register-and-manually-configure-your-application-and-code-sample"></a>Opcja 2. Zarejestrowanie i ręczne skonfigurowanie aplikacji oraz przykładowego kodu

> [!div renderon="docs"]
> #### <a name="step-1-register-your-application"></a>Krok 1. Rejestrowanie aplikacji
> Aby ręcznie zarejestrować aplikację i dodać informacje na temat rejestracji aplikacji do rozwiązania, wykonaj następujące czynności:
>
> 1. Zaloguj się do <a href="https://portal.azure.com/" target="_blank">Azure Portal <span class="docon docon-navigate-external x-hidden-focus"></span> </a>.
> 1. Jeśli masz dostęp do wielu dzierżawców, Użyj filtru **katalogów i subskrypcji** :::image type="icon" source="./media/common/portal-directory-subscription-filter.png" border="false"::: w górnym menu, aby wybrać dzierżawcę, w którym chcesz zarejestrować aplikację.
> 1. Wyszukaj i wybierz pozycję **Azure Active Directory**.
> 1. W obszarze **Zarządzaj** wybierz pozycję **rejestracje aplikacji**  >  **Nowa rejestracja**.
> 1. Wprowadź **nazwę** aplikacji, na przykład `Daemon-console` . Użytkownicy Twojej aplikacji mogą zobaczyć tę nazwę i można ją później zmienić.
> 1. Wybierz pozycję **Zarejestruj**.
> 1. W obszarze **Zarządzanie** wybierz pozycję **Certyfikaty i wpisy tajne**.
> 1. W obszarze wpisy **tajne klienta** wybierz pozycję **Nowy wpis tajny klienta**, wprowadź nazwę, a następnie wybierz pozycję **Dodaj**. Zapisz wartość klucza tajnego w bezpiecznej lokalizacji do użycia w późniejszym kroku.
> 1. W obszarze **Zarządzaj** wybierz pozycję **uprawnienia interfejsu API**  >  **Dodaj uprawnienie**. Wybierz **Microsoft Graph**.
> 1. Wybierz pozycję **Uprawnienia aplikacji**.
> 1. W obszarze węzeł **użytkownika** wybierz pozycję **użytkownik. odczyt. wszystkie**, a następnie wybierz pozycję **Dodaj uprawnienia**.

> [!div class="sxs-lookup" renderon="portal"]
> ### <a name="download-and-configure-your-quickstart-app"></a>Pobieranie i konfigurowanie aplikacji Szybki Start
>
> #### <a name="step-1-configure-your-application-in-azure-portal"></a>Krok 1. Konfigurowanie aplikacji w witrynie Azure Portal
> Aby działał przykładowy kod z tego przewodnika Szybki start, musisz utworzyć klucz tajny klienta i dodać uprawnienie aplikacji **User.Read.All** interfejsu API programu Graph.
> > [!div renderon="portal" id="makechanges" class="nextstepaction"]
> > [Wprowadź zmiany automatycznie]()
>
> > [!div id="appconfigured" class="alert alert-info"]
> > ![Już skonfigurowano](media/quickstart-v2-netcore-daemon/green-check.png) Twoja aplikacja została skonfigurowana za pomocą tych atrybutów.

#### <a name="step-2-download-your-python-project"></a>Krok 2. Pobieranie projektu języka Python

> [!div renderon="docs"]
> [Pobierz projekt demona języka Python](https://github.com/Azure-Samples/ms-identity-python-daemon/archive/master.zip)

> [!div renderon="portal" id="autoupdate" class="sxs-lookup nextstepaction"]
> [Pobierz przykład kodu](https://github.com/Azure-Samples/ms-identity-python-daemon/archive/master.zip)

> [!div class="sxs-lookup" renderon="portal"]
> > [!NOTE]
> > `Enter_the_Supported_Account_Info_Here`


> [!div renderon="docs"]
> #### <a name="step-3-configure-your-python-project"></a>Krok 3. Konfigurowanie projektu języka Python
>
> 1. Wyodrębnij plik zip do folderu lokalnego blisko folderu głównego dysku, na przykład **C:\Azure-Samples**.
> 1. Przejdź do podfolderu **1-Call-MsGraph-WithSecret "**.
> 1. Edytuj **parameters.jsna** i Zastąp wartości pól `authority` `client_id` oraz `secret` następującym fragmentem kodu:
>
>    ```json
>    "authority": "https://login.microsoftonline.com/Enter_the_Tenant_Id_Here",
>    "client_id": "Enter_the_Application_Id_Here",
>    "secret": "Enter_the_Client_Secret_Here"
>    ```
>    Gdzie:
>    - `Enter_the_Application_Id_Here` jest **identyfikatorem aplikacji (klienta)** dla zarejestrowanej aplikacji.
>    - `Enter_the_Tenant_Id_Here` — zastąp tę wartość wartością **Identyfikator dzierżawy** lub **Nazwa dzierżawy** (na przykład contoso.microsoft.com)
>    - `Enter_the_Client_Secret_Here` — zastąp tę wartość kluczem tajnym klienta utworzonym w kroku 1.
>
> > [!TIP]
> > Aby znaleźć wartości **Identyfikator aplikacji (klienta)**, **Identyfikator katalogu (dzierżawy)**, przejdź do strony **Przegląd** aplikacji w witrynie Azure Portal. Aby wygenerować nowy klucz, przejdź do strony **Certyfikaty i klucze tajne**.

> [!div class="sxs-lookup" renderon="portal"]
> #### <a name="step-3-admin-consent"></a>Krok 3. zgoda administratora

> [!div renderon="docs"]
> #### <a name="step-4-admin-consent"></a>Krok 4. Zgoda administratora

Jeśli spróbujesz uruchomić aplikację w tym momencie, otrzymasz komunikat o błędzie *HTTP 403 — Dostęp zabroniony* : `Insufficient privileges to complete the operation` . Ten błąd występuje, ponieważ każde *uprawnienie tylko do aplikacji* wymaga zgody administratora: Administrator globalny katalogu musi wyrazić zgodę na swoją aplikację. Wybierz jedną z poniższych opcji, w zależności od roli:

##### <a name="global-tenant-administrator"></a>Administrator globalny dzierżawy

> [!div renderon="docs"]
> Jeśli jesteś administratorem globalnym dzierżawy, przejdź do strony **Uprawnienia interfejsu API** w obszarze rejestracji aplikacji (w wersji zapoznawczej) witryny Azure Portal i wybierz pozycję **Wyraź zgodę administratora dla katalogu {nazwa dzierżawy}** ({nazwa dzierżawy} jest nazwą katalogu).

> [!div renderon="portal" class="sxs-lookup"]
> Jeśli jesteś administratorem globalnym, przejdź do strony **Uprawnienia interfejsu API** i wybierz pozycję **Wyraź zgodę administratora dla katalogu wpisz_tutaj_nazwę_dzierżawy**
> > [!div id="apipermissionspage"]
> > [Przejdź do strony Uprawnienia interfejsu API]()

##### <a name="standard-user"></a>Użytkownik standardowy

Jeśli jesteś użytkownikiem standardowym Twojej dzierżawy, musisz poprosił administratora globalnego o przyznanie zgody administratora dla aplikacji. Aby to zrobić, udostępnij administratorowi następujący adres URL:

```url
https://login.microsoftonline.com/Enter_the_Tenant_Id_Here/adminconsent?client_id=Enter_the_Application_Id_Here
```

> [!div renderon="docs"]
>> Gdzie:
>> * `Enter_the_Tenant_Id_Here` — zastąp tę wartość wartością **Identyfikator dzierżawy** lub **Nazwa dzierżawy** (na przykład contoso.microsoft.com)
>> * `Enter_the_Application_Id_Here` jest **identyfikatorem aplikacji (klienta)** dla zarejestrowanej aplikacji.

> [!div class="sxs-lookup" renderon="portal"]
> #### <a name="step-4-run-the-application"></a>Krok 4. Uruchamianie aplikacji

> [!div renderon="docs"]
> #### <a name="step-5-run-the-application"></a>Krok 5. Uruchomienie aplikacji

Musisz zainstalować zależności tego przykładu raz

```console
pip install -r requirements.txt
```

Następnie uruchom aplikację za pomocą wiersza polecenia lub konsoli programu:

```console
python confidential_client_secret_sample.py parameters.json
```

Powinno zostać wyświetlone dane wyjściowe konsoli część fragmentu kodu JSON reprezentująca listę użytkowników w katalogu usługi Azure AD.

> [!IMPORTANT]
> Aplikacja w tym przewodniku Szybki start używa klucza tajnego klienta do identyfikowania się jako klienta poufnego. Ponieważ klucz tajny klienta jest dodawany jako zwykły tekst w plikach projektu, ze względów bezpieczeństwa zaleca się używanie certyfikatu zamiast klucza tajnego klienta, zanim będzie można uznać aplikację za produkcyjną. Aby uzyskać więcej informacji na temat korzystania z certyfikatu, zobacz [te instrukcje](https://github.com/Azure-Samples/ms-identity-python-daemon/blob/master/2-Call-MsGraph-WithCertificate/README.md) w tym samym repozytorium GitHub dla tego przykładu, ale w drugim folderze **2-Call-MsGraph-WithCertificate**

## <a name="more-information"></a>Więcej informacji

### <a name="msal-python"></a>MSAL Python

[MSAL Python](https://github.com/AzureAD/microsoft-authentication-library-for-python) to biblioteka służąca do logowania użytkowników i żądania tokenów używanych w celu uzyskania dostępu do interfejsu API chronionego przez platformę tożsamości firmy Microsoft. Zgodnie z opisem, ten przewodnik Szybki Start żąda tokenów przy użyciu tożsamości własnej aplikacji zamiast uprawnień delegowanych. W tym przypadku przepływ uwierzytelniania jest określany jako *[przepływ OAuth poświadczeń klienta](v2-oauth2-client-creds-grant-flow.md)*. Aby uzyskać więcej informacji na temat używania języka Python MSAL z aplikacjami demona, zobacz [ten artykuł](scenario-daemon-overview.md).

 Możesz zainstalować MSAL Python, uruchamiając następujące polecenie PIP.

```powershell
pip install msal
```

### <a name="msal-initialization"></a>Inicjowanie biblioteki MSAL

Aby dodać odwołanie do biblioteki MSAL, dodaj następujący kod:

```Python
import msal
```

Następnie zainicjuj bibliotekę MSAL, używając następującego kodu:

```Python
app = msal.ConfidentialClientApplication(
    config["client_id"], authority=config["authority"],
    client_credential=config["secret"])
```

> | Gdzie: |Opis |
> |---------|---------|
> | `config["secret"]` | Klucz tajny klienta utworzony dla aplikacji w witrynie Azure Portal. |
> | `config["client_id"]` | Jest **identyfikatorem aplikacji (klienta)** dla aplikacji zarejestrowanej w witrynie Azure Portal. Tę wartość można znaleźć na stronie **Przegląd** aplikacji w witrynie Azure Portal. |
> | `config["authority"]`    | Punkt końcowy usługi STS na potrzeby uwierzytelnienia użytkownika. W chmurze publicznej jest to zwykle `https://login.microsoftonline.com/{tenant}`, gdzie {tenant} jest nazwą dzierżawy lub identyfikatorem dzierżawy.|

Więcej informacji można znaleźć w [dokumentacji dotyczącej metody `ConfidentialClientApplication`](https://msal-python.readthedocs.io/en/latest/#confidentialclientapplication)

### <a name="requesting-tokens"></a>Przesyłanie żądań tokenów

Aby zażądać tokenu przy użyciu tożsamości aplikacji, należy użyć metody `AcquireTokenForClient`:

```Python
result = None
result = app.acquire_token_silent(config["scope"], account=None)

if not result:
    logging.info("No suitable token exists in cache. Let's get a new one from AAD.")
    result = app.acquire_token_for_client(scopes=config["scope"])
```

> |Gdzie:| Opis |
> |---------|---------|
> | `config["scope"]` | Zawiera żądane zakresy. W przypadku klientów poufnych format powinien być podobny do `{Application ID URI}/.default`, aby wskazać, że żądane zakresy są zdefiniowane statycznie w obiekcie aplikacji ustawionym w witrynie Azure Portal (w przypadku programu Microsoft Graph element `{Application ID URI}` wskazuje na adres `https://graph.microsoft.com`). W przypadku niestandardowych interfejsów API sieci Web `{Application ID URI}` jest zdefiniowany w sekcji **UWIDACZNIANIE interfejsu API** w rejestracji aplikacji w witrynie Azure Portal (wersja zapoznawcza). |

Więcej informacji można znaleźć w [dokumentacji dotyczącej metody `AcquireTokenForClient`](https://msal-python.readthedocs.io/en/latest/#msal.ConfidentialClientApplication.acquire_token_for_client)

[!INCLUDE [Help and support](../../../includes/active-directory-develop-help-support-include.md)]

## <a name="next-steps"></a>Następne kroki

Aby dowiedzieć się więcej na temat aplikacji demonów, zobacz stronę docelową scenariusza

> [!div class="nextstepaction"]
> [Aplikacja demona, która wywołuje interfejsy API sieci Web](scenario-daemon-overview.md)
