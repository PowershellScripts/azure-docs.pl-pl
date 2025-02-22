---
title: Zaplanuj rozwiązanie do obsługi połączeń telefonicznych i SMS usługi Azure Communications Services
titleSuffix: An Azure Communication Services concept document
description: Dowiedz się, jak efektywnie zaplanować korzystanie z numerów telefonów i telefonowania.
author: prakulka
manager: nmurav
services: azure-communication-services
ms.author: prakulka
ms.date: 10/05/2020
ms.topic: overview
ms.custom: references_regions
ms.service: azure-communication-services
ms.openlocfilehash: 271d7ce38d50fd21975327eb1f21528aeacc485e
ms.sourcegitcommit: dea56e0dd919ad4250dde03c11d5406530c21c28
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/09/2020
ms.locfileid: "96937240"
---
# <a name="plan-your-telephony-and-sms-solution"></a>Planowanie rozwiązania do obsługi telefonii i wiadomości SMS

[!INCLUDE [Public Preview Notice](../../includes/public-preview-include.md)]
[!INCLUDE [Regional Availability Notice](../../includes/regional-availability-include.md)]

Usługi Azure Communication Services umożliwiają korzystanie z numerów telefonów w celu wykonywania połączeń głosowych i wysyłania wiadomości SMS przy użyciu sieci telefonicznej (PSTN). W tym dokumencie będziemy przeglądać typy numerów telefonów, opcje konfiguracji i dostępność regionów w celu planowania rozwiązania do obsługi połączeń telefonicznych i SMS przy użyciu usług komunikacyjnych.





## <a name="phone-number-types-in-azure-communication-services"></a>Typy numerów telefonów w usłudze Azure Communications Services
 
Usługi komunikacyjne oferują dwa typy numerów telefonów: **lokalna** i **bezpłatna**. 

### <a name="local-numbers"></a>Numery lokalne
Numery lokalne (geograficzne) to 10-cyfrowy numer telefonu składający się z lokalnych kodów obszaru w Stany Zjednoczone. Na przykład `+1 (206) XXX-XXXX` jest numerem lokalnym z kodem obszaru `206` . Ten kod obszaru jest przypisywany do miasta Seattle. Te numery telefonów są zwykle używane przez użytkowników indywidualnych i lokalnych. Usługi Azure Communication Services oferują numery lokalne w Stany Zjednoczone. Te liczby mogą służyć do nawiązywać połączeń telefonicznych, ale nie do wysyłania wiadomości SMS. 

### <a name="toll-free-numbers"></a>Bezpłatne numery telefonów
Numer bezpłatny to 10-cyfrowe numery telefonów z unikatowymi kodami obszarów, które można wywoływać z dowolnego numeru telefonu. Na przykład `+1 (800) XXX-XXXX` jest numerem bezpłatnym w Ameryka Północna regionie. Te numery telefonów są zwykle używane na potrzeby obsługi klienta. Usługi Azure Communication Services oferują bezpłatne numery telefonów w Stanach Zjednoczonych. Te liczby mogą służyć do nawiązywać połączeń telefonicznych i wysyłania wiadomości SMS. Numery bezpłatne nie mogą być używane przez osoby i mogą być przypisane tylko do aplikacji.

#### <a name="choosing-a-phone-number-type"></a>Wybieranie typu numeru telefonu

Jeśli Twój numer telefonu będzie używany przez aplikację (na przykład w celu wykonywania wywołań lub wysyłania komunikatów w imieniu usługi), możesz wybrać numer bezpłatny lub lokalny. Możesz wybrać numer bezpłatny, jeśli aplikacja wysyła wiadomości SMS i/lub wykonujące wywołania.

Jeśli Twój numer telefonu jest używany przez osobę (na przykład użytkownika aplikacji wywołującej), należy użyć lokalnego numeru telefonu (geograficznego). 

W poniższej tabeli zestawiono te typy numerów telefonów: 

| Typ numeru telefonu | Przykład                              | Dostępność kraju    | Możliwość numeru telefonu |Typowy przypadek użycia                                                                                                     |
| ----------------- | ------------------------------------ | ----------------------- | ------------------------|------------------------------------------------------------------------------------------------------------------- |
| Lokalne (geograficzne)        | + 1 (Local Area Code) XXX XX XX  | USA                      | Wywoływanie (wychodzące) | Przypisywanie numerów telefonów użytkownikom w aplikacjach  |
| Toll-Free         | + 1 (bezpłatny *numer* kierunkowy) XXX XX XX | USA                      | Wywoływanie (wychodzące), SMS (przychodzące/wychodzące)| Przypisywanie numerów telefonów do interaktywnych systemów odpowiedzi głosowych (IVR)/botów, aplikacji SMS                                        |


## <a name="phone-number-features-in-azure-communication-services"></a>Funkcje numeru telefonu w usłudze Azure Communications Services 

[!INCLUDE [Emergency Calling Notice](../../includes/emergency-calling-notice-include.md)]

W przypadku większości numerów telefonów pozwalamy skonfigurować zestaw funkcji "a La koszyka". Te funkcje mogą być wybierane w ramach dzierżawy numerów telefonów w ramach usług Azure Communications Services.

Funkcje, które są dostępne dla użytkownika, zależą od kraju, w którym pracujesz, w przypadku użycia i wybranego typu numeru telefonu. Te funkcje różnią się w zależności od kraju ze względu na wymagania prawne. Usługi Azure Communication Services oferują następujące funkcje numeru telefonu:

- **Jednokierunkowe wychodzące wiadomości SMS** Ta opcja umożliwia wysyłanie wiadomości SMS do użytkowników. Może to być przydatne w scenariuszach powiadamiania i uwierzytelniania dwuskładnikowego. 
- **Dwukierunkowe przychodzące i wychodzące wiadomości SMS** Ta opcja umożliwia wysyłanie i odbieranie wiadomości od użytkowników przy użyciu numerów telefonów. Może to być przydatne w scenariuszach obsługi klienta.
- **Jednokierunkowe połączenie wychodzące telefonu** Ta opcja umożliwia nawiązywanie połączeń z użytkownikami i Konfigurowanie identyfikatora rozmówcy dla wywołań wychodzących umieszczonych przez usługę. Może to być przydatne w scenariuszach obsługi klienta i powiadomień głosowych.

## <a name="countryregion-availability"></a>Dostępność kraju/regionu

W poniższej tabeli przedstawiono, gdzie można uzyskać różne typy numerów telefonów wraz z funkcjami wywołań przychodzących i wychodzących oraz programem SMS związanymi z tymi typami numerów telefonów.

|Typ liczbowy| Uzyskaj numery w | Wykonaj wywołania do                                        | Odbierz wywołania z                                    |Wyślij komunikaty do       | Odbierz komunikaty z |
|-----------| ------------------ | ---------------------------------------------------  |-------------------------------------------------------|-----------------------|--------|
| Lokalne (geograficzne)  | USA                 | Stany Zjednoczone, Kanada, Zjednoczone Królestwo, Niemcy, Francja,. + Więcej *| Stany Zjednoczone, Kanada, Zjednoczone Królestwo, Niemcy, Francja,. + Więcej * |Niedostępne| Niedostępne |
| Toll-Free | USA                 | USA                                                   | USA                                                    |USA                | USA |

* Aby uzyskać więcej informacji o miejscach docelowych wywołań i cenach, zobacz [stronę z cennikiem](../pricing.md).

## <a name="azure-subscriptions-eligibility"></a>Uprawnienia do subskrypcji platformy Azure

Aby uzyskać numer telefonu, musisz mieć płatną subskrypcję platformy Azure. Numerów telefonów nie można nabyć na kontach próbnych ani za pomocą bezpłatnych kredytów na korzystanie z platformy Azure. 

Obecnie dostępność numeru telefonu jest ograniczona do subskrypcji platformy Azure, które mają adres rozliczeniowy w Stany Zjednoczone.

## <a name="next-steps"></a>Następne kroki

### <a name="quickstarts"></a>Przewodniki Szybki start

- [Pobierz numer telefonu](../../quickstarts/telephony-sms/get-phone-number.md)
- [Umieść wywołanie](../../quickstarts/voice-video-calling/calling-client-samples.md)
- [Wysyłanie wiadomości SMS](../../quickstarts/telephony-sms/send.md)

### <a name="conceptual-documentation"></a>Dokumentacja dotycząca pojęć

- [Pojęcia dotyczące głosu i wideo](../voice-video-calling/about-call-types.md)
- [Przepływy wywołań](../call-flows.md)
- [Cennik](../pricing.md)
