---
title: Podstawa zabezpieczeń platformy Azure dla usługi Azure Defender dla IoT
description: Linia bazowa zabezpieczeń usługi Azure Defender for IoT zawiera wskazówki i zasoby dotyczące procedur związanych z wdrażaniem zaleceń dotyczących zabezpieczeń określonych w teście zabezpieczeń platformy Azure.
author: msmbaldwin
ms.service: defender-for-iot
ms.topic: conceptual
ms.date: 11/19/2020
ms.author: mbaldwin
ms.custom: subject-security-benchmark
ms.openlocfilehash: 6fbd70c1de99818e2baf73d15ed365db3a54e43d
ms.sourcegitcommit: 08458f722d77b273fbb6b24a0a7476a5ac8b22e0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/15/2021
ms.locfileid: "98246727"
---
# <a name="azure-security-baseline-for-azure-defender-for-iot"></a>Podstawa zabezpieczeń platformy Azure dla usługi Azure Defender dla IoT

Ta linia bazowa zabezpieczeń stosuje wskazówki z [wersji 2,0 usługi Azure Security test](../security/benchmarks/overview.md) do Microsoft Azure Defender for IoT. Test porównawczy zabezpieczeń platformy Azure zawiera zalecenia dotyczące sposobu zabezpieczania rozwiązań w chmurze na platformie Azure. Zawartość jest pogrupowana według **kontroli zabezpieczeń** zdefiniowanych przez usługę Azure Security test i powiązane wskazówki dotyczące usługi Azure Defender dla IoT. **Formanty** nie mają zastosowania do usługi Azure Defender dla IoT zostały wykluczone.

Aby dowiedzieć się, jak usługa Azure Defender for IoT jest całkowicie mapowana na test porównawczy zabezpieczeń platformy Azure, zobacz [pełny plik mapowania zabezpieczeń usługi Azure Defender for IoT](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines).

## <a name="identity-management"></a>Zarządzanie tożsamością

*Aby uzyskać więcej informacji, zobacz [Test porównawczy platformy Azure: zarządzanie tożsamościami](../security/benchmarks/security-controls-v2-identity-management.md).*

### <a name="im-1-standardize-azure-active-directory-as-the-central-identity-and-authentication-system"></a>IM-1: Standaryzacja usługi Azure Active Directory jako centralnego systemu tożsamości i uwierzytelniania

**Wskazówki**: usługa Azure Defender for IoT jest zintegrowana z usługami Azure Active Directory (Azure AD), domyślną usługą zarządzania tożsamościami i dostępem platformy Azure. Należy przeprowadzić standaryzację usługi Azure AD, aby zarządzać zarządzaniem tożsamościami i dostępem w organizacji w programie:

- Microsoft Cloud zasoby, takie jak Azure Portal, Azure Storage, Azure Virtual Machine (Linux i Windows), Azure Key Vault, PaaS i SaaS.

- Zasoby organizacji, takie jak aplikacje na platformie Azure lub formowe zasoby sieciowe.

Zabezpieczanie usługi Azure AD powinno mieć wysoki priorytet w zakresie zabezpieczeń w chmurze w organizacji. Usługa Azure AD zapewnia wskaźnik bezpieczeństwa tożsamości, który pomaga ocenić stan zabezpieczeń tożsamości w porównaniu z zaleceniami dotyczącymi najlepszych rozwiązań firmy Microsoft. Skorzystaj ze wskaźnika, aby ocenić, jak ściśle Twoja konfiguracja spełnia zalecenia dotyczące najlepszych rozwiązań, i ulepszać stan zabezpieczeń.

Usługa Azure AD obsługuje tożsamość zewnętrzną, która umożliwia użytkownikom bez konto Microsoft logowania się do aplikacji i zasobów przy użyciu tożsamości zewnętrznej.

- [Dzierżawa w usłudze Azure Active Directory](../active-directory/develop/single-and-multi-tenant-apps.md) 

- [Jak utworzyć i skonfigurować wystąpienie usługi Azure AD](../active-directory/fundamentals/active-directory-access-create-new-tenant.md) 

- [Używanie zewnętrznych dostawców tożsamości w aplikacji](../active-directory/external-identities/identity-providers.md) 

- [Co to jest wskaźnik bezpieczeństwa tożsamości w usłudze Azure Active Directory](../active-directory/fundamentals/identity-secure-score.md)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="im-3-use-azure-ad-single-sign-on-sso-for-application-access"></a>IM-3: Korzystanie z logowania jednokrotnego usługi Azure AD na potrzeby dostępu do aplikacji

**Wskazówki**: usługa Azure Defender for IoT używa Azure Active Directory, aby zapewnić zarządzanie tożsamościami i dostępem do zasobów platformy Azure, aplikacji w chmurze i aplikacji lokalnych. Obejmuje to tożsamości przedsiębiorstwa, takie jak pracownicy, a także tożsamości zewnętrzne, takie jak partnerzy, dostawcy i dostawcy. Umożliwia to logowanie jednokrotne w celu zarządzania i bezpiecznego dostępu do danych i zasobów organizacji w środowisku lokalnym i w chmurze. Połącz wszystkich użytkowników, aplikacje i urządzenia z usługą Azure AD w celu zapewnienia bezproblemowego, bezpiecznego dostępu, lepszego wglądu i większej kontroli.

- [Informacje na temat logowania jednokrotnego aplikacji za pomocą usługi Azure AD](../active-directory/manage-apps/what-is-single-sign-on.md)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="im-4-use-strong-authentication-controls-for-all-azure-active-directory-based-access"></a>IM-4: Używanie kontrolek silnego uwierzytelniania dla całego dostępu opartego na usłudze Azure Active Directory

**Wskazówki**: usługa Azure Defender for IoT używa Azure Active Directory, które obsługują kontrolę silnego uwierzytelniania za pośrednictwem uwierzytelniania wieloskładnikowego (MFA) i silnych metod bezhaseł.

- Uwierzytelnianie wieloskładnikowe — włącz usługę Azure AD MFA i postępuj zgodnie z zaleceniami dotyczącymi zarządzania tożsamościami i dostępem w usłudze Azure Security Center, aby zapoznać się z najlepszymi rozwiązaniami w konfiguracji usługi MFA. Usługę MFA można wymusić na wszystkich lub wybranych użytkownikach albo na poziomie poszczególnych użytkowników na podstawie warunków logowania i czynników ryzyka.
- Uwierzytelnianie bezhasło — dostępne są trzy opcje uwierzytelniania bezhasła: funkcja Windows Hello dla firm, aplikacja Microsoft Authenticator i lokalne metody uwierzytelniania, takie jak karty inteligentne.

W przypadku użytkowników z uprawnieniami administratora i uprzywilejowanego upewnij się, że jest używana najwyższa Metoda silnego uwierzytelniania, a następnie zastąp odpowiednie zasady silnego uwierzytelniania innym użytkownikom.

- [Jak włączyć usługę MFA na platformie Azure](../active-directory/authentication/howto-mfa-getstarted.md) 

- [Wprowadzenie do opcji uwierzytelniania bez hasła w przypadku usługi Azure Active Directory](../active-directory/authentication/concept-authentication-passwordless.md) 

- [Domyślne zasady haseł usługi Azure AD](../active-directory/authentication/concept-sspr-policy.md#password-policies-that-only-apply-to-cloud-user-accounts)

- [Eliminowanie nieprawidłowych haseł przy użyciu ochrony haseł w usłudze Azure AD](../active-directory/authentication/concept-password-ban-bad.md)

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

### <a name="im-5-monitor-and-alert-on-account-anomalies"></a>IM-5: Monitorowanie anomalii kont i wyświetlanie alertów

**Wskazówki**: usługa Azure Defender for IoT jest zintegrowana z Azure Active Directory, w którym znajdują się następujące źródła danych:

Logowania — raporty aktywności logowania zawierają informacje na temat użycia zarządzanych aplikacji i działań użytkownika związane z logowaniem.

Dzienniki inspekcji — udostępnia możliwość śledzenia wszystkich zmian wprowadzanych przez różne funkcje usługi Azure AD za pomocą dzienników. Działania umieszczane w dziennikach inspekcji to na przykład zmiany wprowadzone w dowolnych zasobach usługi Azure AD, takie jak dodawanie lub usuwanie użytkowników, aplikacji, grup, ról i zasad.

Ryzykowne logowania — ryzykowne logowanie jest wskaźnikiem próby logowania, które mogło zostać wykonane przez osobę, która nie jest prawowitym właścicielem konta użytkownika.

Użytkownicy oflagowani w związku z ryzykiem — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone.

Te źródła danych można zintegrować z Azure Monitor, wskaźnikiem produktów platformy Azure lub systemami SIEM innych firm.

Usługa Azure Security Center może również wysyłać alerty dotyczące określonych podejrzanych działań, takich jak nadmierna liczba nieudanych prób uwierzytelnienia, czy przestarzałe konta w subskrypcji.

Usługa Azure Advanced Threat Protection (ATP) to rozwiązanie z zakresu zabezpieczeń, które może używać sygnałów usługi Active Directory do identyfikowania, wykrywania i badania zaawansowanych zagrożeń, naruszonych tożsamości i złośliwych działań wewnętrznych.

- [Raporty dotyczące inspekcji w usłudze Azure AD](../active-directory/reports-monitoring/concept-audit-logs.md) 

- [Jak wyświetlić ryzykowne logowania w usłudze Azure AD](../active-directory/identity-protection/overview-identity-protection.md) 

- [Identyfikowanie użytkowników usługi Azure AD oflagowanych na skutek ryzykownego działania](../active-directory/identity-protection/overview-identity-protection.md) 

- [Jak monitorować działania użytkowników związane z tożsamościami i dostępem w usłudze Azure Security Center](../security-center/security-center-identity-access.md) 

- [Alerty w module analizy zagrożeń usługi Azure Security Center](../security-center/alerts-reference.md) 

- [Jak zintegrować dzienniki aktywności platformy Azure z usługą Azure Monitor](../active-directory/reports-monitoring/howto-integrate-activity-logs-with-log-analytics.md)

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

## <a name="privileged-access"></a>Dostęp uprzywilejowany

*Aby uzyskać więcej informacji, zobacz [Test porównawczy platformy Azure: dostęp uprzywilejowany](../security/benchmarks/security-controls-v2-privileged-access.md).*

### <a name="pa-2-restrict-administrative-access-to-business-critical-systems"></a>PA-2: Ogranicz dostęp administracyjny do systemów o krytycznym znaczeniu dla firmy

**Wskazówki**: usługa Azure Defender for IoT korzysta z usługi Azure RBAC, aby odizolować dostęp do systemów o krytycznym znaczeniu dla firmy, ograniczając konta, które mają przyznane uprzywilejowany dostęp do subskrypcji i grup zarządzania, w których się znajdują.

Upewnij się, że ograniczono również dostęp do systemów zarządzania, tożsamości i zabezpieczeń, które mają dostęp administracyjny do krytycznych dostępów firmy, takich jak kontrolery domena usługi Active Directory (DC), narzędzia zabezpieczeń i narzędzia do zarządzania systemem, z agentami zainstalowanymi w systemach krytycznych dla działalności firmy. Osoby atakujące, którzy naruszają te systemy zarządzania i zabezpieczeń, mogą natychmiast weaponize je w celu naruszenia krytycznych zasobów firmy.

Wszystkie typy kontroli dostępu powinny być wyrównane do strategii segmentacji przedsiębiorstwa w celu zapewnienia spójnej kontroli dostępu.

- [Składniki platformy Azure i Model referencyjny](/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151) 

- [Dostęp do grupy zarządzania](../governance/management-groups/overview.md#management-group-access) 

- [Administratorzy subskrypcji platformy Azure](../cost-management-billing/manage/add-change-subscription-administrator.md)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="pa-4-set-up-emergency-access-in-azure-ad"></a>PA-4: Konfigurowanie dostępu awaryjnego w usłudze Azure AD

**Wskazówki**: usługa Azure Defender for IoT jest zintegrowana z usługą Azure Active Directory w celu zarządzania swoimi zasobami. Aby zapobiec przypadkowemu zablokowaniu organizacji usługi Azure AD, skonfiguruj konto dostępu awaryjnego w celu uzyskania dostępu, gdy nie można używać normalnych kont administracyjnych. Konta dostępu awaryjnego są zwykle wysoce uprzywilejowane i nie powinny być przypisane do konkretnych osób. Konta dostępu awaryjnego są ograniczone do sytuacji awaryjnych lub nagłych, w których normalne konta administracyjne nie mogą być używane.

Należy upewnić się, że poświadczenia (takie jak hasło, certyfikat lub karta inteligentna) dla kont dostępu awaryjnego są bezpieczne i znane tylko osobom, które są upoważnione do ich używania tylko w sytuacji awaryjnej.

- [Zarządzanie kontami dostępu awaryjnego w usłudze Azure AD](../active-directory/roles/security-emergency-access.md)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="pa-5-automate-entitlement-management"></a>PA-5: Automatyzowanie zarządzania uprawnieniami 

**Wskazówki**: usługa Azure Defender for IoT jest zintegrowana z usługą Azure Active Directory w celu zarządzania swoimi zasobami. Użyj funkcji zarządzania prawami usługi Azure AD, aby zautomatyzować przepływy pracy żądania dostępu, w tym przydziały dostępu, przeglądy i wygaśnięcie. Obsługiwane jest również podwójne lub wieloetapowe zatwierdzenie.

- [Co to są przeglądy dostępu do usługi Azure AD](../active-directory/governance/access-reviews-overview.md) 

- [Co to jest zarządzanie prawami w usłudze Azure AD](../active-directory/governance/entitlement-management-overview.md)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="pa-7-follow-just-enough-administration-least-privilege-principle"></a>DU-7: Przestrzeganie podejścia wystarczającego zakresu administracji (zasada stosowania najniższych uprawnień) 

**Wskazówki**: usługa Azure Defender for IoT jest zintegrowana z kontrolą dostępu opartą na ROLACH (RBAC) na platformie Azure w celu zarządzania swoimi zasobami. Usługa Azure RBAC umożliwia zarządzanie dostępem do zasobów platformy Azure za pomocą przypisań ról. Te role można przypisać do użytkowników, grup jednostek usługi i zarządzanych tożsamości. Dla niektórych zasobów istnieją wstępnie zdefiniowane wbudowane role i te role można zinwentaryzować lub wykonywać względem nich zapytania za pomocą narzędzi takich jak interfejs wiersza polecenia platformy Azure, program Azure PowerShell lub witryna Azure Portal. Uprawnienia przypisywane do zasobów z użyciem kontroli dostępu opartej na rolach platformy Azure powinny być zawsze ograniczone do tego, co jest wymagane przez te role. To uzupełnia podejście dostępu just in time (JIT) usługi Azure AD Privileged Identity Management (PIM) i powinno być okresowo weryfikowane.

Używaj wbudowanych ról do przydzielenia uprawnień i utwórz własną rolę tylko wtedy, gdy jest to wymagane.

- [Co to jest kontrola dostępu oparta na rolach (Azure RBAC)](../role-based-access-control/overview.md) 

- [Jak skonfigurować kontrolę RBAC na platformie Azure](../role-based-access-control/role-assignments-portal.md) 

- [Jak korzystać z przeglądów tożsamości i dostępu w usłudze Azure AD](../active-directory/governance/access-reviews-overview.md)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

## <a name="data-protection"></a>Ochrona danych

*Aby uzyskać więcej informacji, zobacz [Test porównawczy platformy Azure: ochrona danych](../security/benchmarks/security-controls-v2-data-protection.md).*

### <a name="dp-1-discovery-classify-and-label-sensitive-data"></a>DP-1: Odnajdywanie, klasyfikowanie i etykietowanie danych poufnych

**Wskazówki**: odkrywanie, klasyfikowanie i etykietowanie poufnych danych, dzięki czemu można zaprojektować odpowiednie kontrolki, aby zapewnić, że poufne informacje są przechowywane, przetwarzane i przesyłane bezpiecznie przez systemy technologiczne organizacji. 

Użyj usługi Azure Information Protection (i skojarzonego z nią narzędzia do skanowania), aby zlokalizować informacje poufne w dokumentach pakietu Office na platformie Azure, lokalnie, w pakiecie Office 365 i w innych lokalizacjach. 

Usługa Azure SQL Information Protection może pomóc w klasyfikacji i etykietowaniu informacji przechowywanych w bazach danych Azure SQL Database.

- [Tagowanie informacji poufnych przy użyciu usługi Azure Information Protection](/azure/information-protection/what-is-information-protection) 

- [Jak wdrożyć usługę Azure SQL Data Discovery](../azure-sql/database/data-discovery-and-classification-overview.md)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="dp-2-protect-sensitive-data"></a>DP-2: Ochrona poufnych danych

**Wskazówki**: Ochrona poufnych danych przez ograniczenie dostępu przy użyciu Access Control opartej na rolach (Azure RBAC), kontroli dostępu opartej na sieci i określonych kontrolek w usługach platformy Azure (takich jak szyfrowanie w SQL i innych bazach danych). 

Aby zapewnić spójną kontrolę dostępu, wszystkie typy kontroli dostępu powinny być dostosowane do strategii segmentacji przedsiębiorstwa. Strategię segmentacji przedsiębiorstwa powinna być również oparta na lokalizacji poufnych lub krytycznych danych i systemów.

W odniesieniu do platformy podstawowej zarządzanej przez firmę Microsoft, firma Microsoft traktuje całą zawartość kliencką jako poufną i zapewnia ochronę przed utratą i narażeniem danych klientów. Aby zapewnić bezpieczeństwo danych klientów na platformie Azure, firma Microsoft zaimplementowała pewne domyślne mechanizmy kontroli i możliwości ochrony danych.

- [Kontrola dostępu oparta na rolach na platformie Azure (RBAC)](../role-based-access-control/overview.md)

- [Informacje na temat ochrony danych klientów na platformie Azure](../security/fundamentals/protection-customer-data.md)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="dp-4-encrypt-sensitive-information-in-transit"></a>DP-4: Szyfrowanie poufnych informacji podczas przesyłania

**Wskazówki**: aby uzupełnić kontrolę dostępu, przesyłane dane powinny być chronione przed atakami "poza pasmem" (np. przechwytywaniem ruchu) przy użyciu szyfrowania, aby zapewnić, że osoby atakujące nie mogą łatwo odczytać ani zmodyfikować danych. 

Chociaż jest to opcjonalne dla ruchu w sieciach prywatnych, ma to kluczowe znaczenie dla ruchu w sieciach zewnętrznych i publicznych. W przypadku ruchu HTTP upewnij się, że wszyscy klienci łączący się z zasobami platformy Azure mogą negocjować protokół TLS w wersji 1.2 lub nowszej. W celu zarządzania zdalnego należy użyć protokołu SSH (dla systemu Linux) lub protokołu RDP/TLS (w systemie Windows), a nie z nieszyfrowanym protokołem. Przestarzałe protokoły SSL, TLS i SSH oraz słabe szyfry powinny być wyłączone.  

Domyślnie platforma Azure zapewnia szyfrowanie danych przesyłanych między centrami danych platformy Azure. 

- [Informacje o szyfrowaniu podczas przesyłania na platformę Azure](../security/fundamentals/encryption-overview.md#encryption-of-data-in-transit)

- [Informacje o zabezpieczeniach protokołu TLS](/security/engineering/solving-tls1-problem)

- [Podwójne szyfrowanie danych na platformie Azure podczas przesyłania](../security/fundamentals/double-encryption.md#data-in-transit)

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

## <a name="asset-management"></a>Zarządzanie zasobami

*Aby uzyskać więcej informacji, zobacz [Test porównawczy platformy Azure: zarządzanie elementami zawartości](../security/benchmarks/security-controls-v2-asset-management.md).*

### <a name="am-1-ensure-security-team-has-visibility-into-risks-for-assets"></a>ZZ-1: Upewnij się, że zespół ds. zabezpieczeń ma wgląd w ryzyko związane z zasobami

**Wskazówki**: Upewnij się, że zespoły ds. zabezpieczeń mają przyznane uprawnienia czytelnika zabezpieczeń w dzierżawie i subskrypcjach platformy Azure, aby umożliwić im monitorowanie zagrożeń bezpieczeństwa przy użyciu usługi Azure Security Center. 

W zależności od istniejącej struktury obowiązków zespołu ds. zabezpieczeń, monitorowanie zagrożeń bezpieczeństwa może być obowiązkiem centralnego zespołu ds. zabezpieczeń lub zespołu lokalnego. Niemniej jednak informacje na temat zabezpieczeń i ryzyka muszą być zawsze agregowane centralnie w ramach danej organizacji. 

Uprawnienia czytelnika zabezpieczeń mogą być stosowane szeroko do całej dzierżawy (główna grupa zarządzania) lub do zakresu w postaci grup zarządzania lub określonych subskrypcji. 

Do uzyskania wglądu w obciążenia i usługi mogą być wymagane dodatkowe uprawnienia. 

- [Omówienie roli czytelnika zabezpieczeń](../role-based-access-control/built-in-roles.md#security-reader)

- [Omówienie grup zarządzania platformy Azure](../governance/management-groups/overview.md)

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: Klient

### <a name="am-3-use-only-approved-azure-services"></a>AM-3: Używanie tylko zatwierdzonych usług platformy Azure

**Wskazówki**: Użyj Azure Policy do inspekcji i ograniczania usług, które użytkownicy mogą inicjować w Twoim środowisku. Usługa Azure Resource Graph umożliwia wykonywanie zapytań dotyczących zasobów i odnajdywanie ich w ramach subskrypcji. Za pomocą usługi Azure Monitor można tworzyć reguły wyzwalające alerty w przypadku wykrycia niezatwierdzonej usługi.

- [Konfigurowanie Azure Policy i zarządzanie nimi](../governance/policy/tutorials/create-and-manage.md)

- [Jak odmówić określonego typu zasobu za pomocą Azure Policy](../governance/policy/samples/built-in-policies.md#general)

- [Jak tworzyć zapytania za pomocą eksploratora usługi Azure Resource Graph](../governance/resource-graph/first-query-portal.md)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="am-4-ensure-security-of-asset-lifecycle-management"></a>ZZ-4: zapewnienie bezpieczeństwa zarządzania cyklem życia zasobów

**Wskazówki**: Utwórz lub zaktualizuj zasady zabezpieczeń, które dotyczą procesów zarządzania cyklem życia zasobów dla modyfikacji o dużym wpływie. Modyfikacje te obejmują zmiany w zakresie: dostawców tożsamości i dostępu, czułości danych, konfiguracji sieci i przypisywania uprawnień administracyjnych.

Usuń zasoby platformy Azure, gdy nie są już potrzebne.

- [Usuwanie grupy zasobów i zasobów platformy Azure](../azure-resource-manager/management/delete-resource-group.md)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="am-5-limit-users-ability-to-interact-with-azure-resource-manager"></a>AM-5: ograniczanie możliwości korzystania przez użytkowników z Azure Resource Manager

**Wskazówki**: korzystanie z dostępu warunkowego usługi Azure AD w celu ograniczenia możliwości współpracy użytkowników z Azure Resource Manager przez skonfigurowanie "blokowania dostępu" dla aplikacji "Microsoft Azure Management".

- [Jak skonfigurować dostęp warunkowy, aby blokować dostęp do usługi Azure Resources](../role-based-access-control/conditional-access-azure-management.md)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

## <a name="incident-response"></a>Reagowanie na zdarzenia

*Aby uzyskać więcej informacji, zobacz [Test porównawczy platformy Azure: reagowanie na zdarzenia](../security/benchmarks/security-controls-v2-incident-response.md).*

### <a name="ir-1-preparation--update-incident-response-process-for-azure"></a>IR-1: Przygotowanie — aktualizowanie procesu reagowania na zdarzenia na platformie Azure

**Wskazówka**: Upewnij się, że organizacja ma procesy reagowania na zdarzenia związane z bezpieczeństwem, zaktualizował te procesy na platformie Azure i regularnie wykonuje je w celu zapewnienia gotowości.

- [Implementowanie zabezpieczeń w środowisku przedsiębiorstwa](/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

- [Przewodnik po odpowiedziach na zdarzenia](/microsoft-365/downloads/IR-Reference-Guide.pdf)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="ir-2-preparation--setup-incident-notification"></a>IR-2: Przygotowanie — powiadomienie o zdarzeniu konfiguracji

**Wskazówka**: Skonfiguruj informacje kontaktowe dotyczące zdarzenia zabezpieczeń w usłudze Azure Security Center. Informacje kontaktowe są używane przez firmę Microsoft do skontaktowania się z Tobą, jeśli centrum Microsoft Security Response Center (MSRC) wykryje, że dostęp do danych jest uzyskiwany przez nieuprawnioną lub nieautoryzowaną osobę. Dostępne są również opcje dostosowywania alertów dotyczących zdarzeń i powiadomień w różnych usługach platformy Azure w zależności od potrzeb związanych z odpowiedzią na zdarzenia. 

- [Jak ustawić kontakt ds. zabezpieczeń usługi Azure Security Center](../security-center/security-center-provide-security-contact-details.md)

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

### <a name="ir-3-detection-and-analysis--create-incidents-based-on-high-quality-alerts"></a>IR-3: wykrywanie i analiza — Tworzenie zdarzeń na podstawie alertów o wysokiej jakości 

**Wskazówka**: Upewnij się, że masz proces tworzenia alertów o wysokiej jakości i mierzenia jakości alertów. Dzięki temu można wyciągać wnioski z przeszłych zdarzeń i określić priorytety alertów dla analityków, dzięki czemu nie będą oni tracić czasu na wyniki fałszywie dodatnie. 

Alerty o wysokiej jakości można tworzyć na podstawie doświadczeń z przeszłych zdarzeń, sprawdzonych źródeł społeczności oraz narzędzi przeznaczonych do generowania i czyszczenia alertów przez połączenie i skorelowanie różnorodnych źródeł sygnałów. 

Azure Security Center oferuje alerty wysokiej jakości dla wielu zasobów platformy Azure. Można użyć łącznika danych usługi ASC do przesyłania strumieniowego alertów do usługi Azure Sentinel. Usługa Azure Sentinel umożliwia tworzenie zaawansowanych reguł alertów w celu automatycznego generowania zdarzeń na potrzeby badania. 

Eksportuj alerty i zalecenia usługi Azure Security Center przy użyciu funkcji eksportowania, aby pomóc identyfikować zagrożenia dla zasobów platformy Azure. Eksportuj alerty i zalecenia ręcznie lub w stały, ciągły sposób.

- [Jak skonfigurować eksportowanie](../security-center/continuous-export.md)

- [Jak przesłać strumieniowo alerty do usługi Azure Sentinel](../sentinel/connect-azure-security-center.md)

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: Klient

### <a name="ir-4-detection-and-analysis--investigate-an-incident"></a>RZ-4: wykrywanie i analiza — badanie zdarzenia

**Wskazówki**: Upewnij się, że analitycy mogą wykonywać zapytania i używać różnorodnych źródeł danych podczas badania potencjalnych zdarzeń w celu uzyskania pełnego obrazu tego, co się stało. Należy zbierać różne dzienniki, aby śledzić działania potencjalnej osoby atakującej w ramach całego łańcucha zagrożeń, aby uniknąć efektu martwego pola.  Należy również upewnić się, że szczegółowe informacje i wnioski są rejestrowane dla innych analityków i na potrzeby przyszłych badań.  

Źródła danych do badania obejmują scentralizowane źródła dzienników, które są już zbierane w ramach usług i działających systemów, ale mogą również obejmować:

- Dane sieciowe — użyj dzienników przepływów sieciowych grup zabezpieczeń, usługi Azure Network Watcher i usługi Azure Monitor do przechwytywania dzienników przepływu sieci i innych informacji analitycznych. 

- Migawki uruchomionych systemów: 

    - Użyj funkcji migawek maszyny wirtualnej platformy Azure, aby utworzyć migawkę dysku działającego systemu. 

    - Użyj natywnej możliwości zrzutu pamięci systemu operacyjnego, aby utworzyć migawkę pamięci uruchomionego systemu.

    - Użyj funkcji migawki w ramach usług platformy Azure lub w ramach własnego oprogramowania, aby utworzyć migawki uruchomionych systemów.

Usługa Azure Sentinel zapewnia szeroką analizę danych dla praktycznie każdego źródła dzienników i portalu zarządzania przypadkami do zarządzania pełnym cyklem życia zdarzeń. Informacje analityczne podczas badania mogą być powiązane ze zdarzeniami pod kątem śledzenia i raportowania. 

- [Tworzenie migawek dysku maszyny z systemem Windows](../virtual-machines/windows/snapshot-copy-managed-disk.md)

- [Tworzenie migawek dysku maszyny z systemem Linux](../virtual-machines/linux/snapshot-copy-managed-disk.md)

- [Informacje diagnostyczne pomocy technicznej oraz kolekcja zrzutów pamięci platformy Microsoft Azure](https://azure.microsoft.com/support/legal/support-diagnostic-information-collection/) 

- [Badanie zdarzeń za pomocą usługi Azure Sentinel](../sentinel/tutorial-investigate-cases.md)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="ir-5-detection-and-analysis--prioritize-incidents"></a>IR-5: Wykrywanie i analiza — określanie priorytetów zdarzeń

**Wskazówki**: Zapewnij kontekst analitykom, na których zdarzeniach należy skupić się w pierwszej kolejności w oparciu o poziom ważności alertów i poufność aktywów. 

Usługa Azure Security Center przypisuje poziom ważności do każdego alertu, aby pomóc w ustaleniu, które alerty powinny być zbadane w pierwszej kolejności. Ważność jest oparta na tym, jak dobrze Security Center znajduje się w wyszukiwaniu lub analitycznie używanych do wystawiania alertu, a także poziom pewności, że istniało złośliwe zamiar za działanie, które spowodowało wygenerowanie alertu.

Ponadto oznacz zasoby przy użyciu tagów i utwórz system nazewnictwa, aby zidentyfikować i sklasyfikować zasoby platformy Azure, szczególnie te, które przetwarzają dane poufne.  Odpowiedzialność za korygowanie alertów w oparciu o krytyczne znaczenie zasobów platformy Azure i środowisko, w którym wystąpiło zdarzenie, leży po stronie użytkownika.

- [Alerty zabezpieczeń w Centrum zabezpieczeń Azure](../security-center/security-center-alerts-overview.md)

- [Organizowanie zasobów platformy Azure przy użyciu tagów](../azure-resource-manager/management/tag-resources.md)

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: Klient

### <a name="ir-6-containment-eradication-and-recovery--automate-the-incident-handling"></a>IR-6: Zawieranie, eliminowanie i odzyskiwanie — automatyzacja obsługi zdarzeń

**Wskazówka**: Automatyzuj ręczne powtarzające się zadania w celu przyspieszenia czasu reakcji i zmniejszenia obciążenia dla analityków. Wykonanie ręcznych zadań trwa dłużej, spowalnia każde zdarzenie i zmniejsza liczbę zdarzeń, które może obsłużyć analityk. Zadania wykonywane ręcznie zwiększają również zmęczenie analityków, co zwiększa ryzyko wystąpienia błędu ludzkiego, który powoduje opóźnienia, a także pogarsza zdolność analityków do skoncentrowania się na złożonych zadaniach. Korzystając z funkcji automatyzacji przepływów pracy w usłudze Azure Security Center i Azure Sentinel, można automatycznie wyzwalać akcje lub uruchamiać element playbook w odpowiedzi na przychodzące alerty zabezpieczeń. Element playbook wykonuje akcje, takie jak wysyłanie powiadomień, wyłączanie kont i izolowanie problematycznych sieci. 

- [Konfigurowanie automatyzacji przepływu pracy w usłudze Security Center](../security-center/workflow-automation.md)

- [Konfigurowanie automatycznych reakcji na zagrożenia w usłudze Azure Security Center](../security-center/tutorial-security-incident.md#triage-security-alerts)

- [Konfigurowanie automatycznych reakcji na zagrożenia w usłudze Azure Sentinel](../sentinel/tutorial-respond-threats-playbook.md)

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: Klient

## <a name="posture-and-vulnerability-management"></a>Stan zabezpieczeń i zarządzanie lukami w zabezpieczeniach

*Aby uzyskać więcej informacji, zobacz [Test porównawczy platformy Azure: stan zabezpieczeń i zarządzanie lukami w zabezpieczeniach](../security/benchmarks/security-controls-v2-posture-vulnerability-management.md).*

### <a name="pv-8-conduct-regular-attack-simulation"></a>PV-8: Przeprowadzanie regularnej symulacji ataków

**Wskazówka**: W razie potrzeby przeprowadź test penetracyjny lub działania typu „red team” na zasobach platformy Azure i zapewnij korektę wszystkich krytycznych ustaleń dotyczących zabezpieczeń.
Postępuj zgodnie z regułami testowania penetracji w chmurze firmy Microsoft, aby upewnić się, że testy penetracyjne nie naruszają zasad firmy Microsoft. Korzystaj ze strategii firmy Microsoft i wykonywania testów typu „red team” i testów na żywo w zarządzanej przez firmę Microsoft infrastrukturze, usługach i aplikacjach w chmurze.

- [Testy penetracyjne na platformie Azure](../security/fundamentals/pen-testing.md)

- [Reguły testów penetracyjnych zaangażowania](https://www.microsoft.com/msrc/pentest-rules-of-engagement?rtc=1) 

- [Testy typu „red team” w chmurze firmy Microsoft](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Udostępnione

## <a name="governance-and-strategy"></a>Ład i strategia

*Aby uzyskać więcej informacji, zobacz [Test porównawczy platformy Azure: ład i strategia](../security/benchmarks/security-controls-v2-governance-strategy.md).*

### <a name="gs-1-define-asset-management-and-data-protection-strategy"></a>GS-1: Definiowanie strategii zarządzania elementami zawartości i ochrony danych 

**Wskazówka**: Zadbaj o to, aby udokumentować i udostępnić wyraźną strategię monitorowania i ochrony systemów i danych. Ustalaj priorytety odnajdywania, oceny, ochrony i monitorowania danych oraz systemów o krytycznym znaczeniu dla firmy. 

Ta strategia powinna obejmować udokumentowane wskazówki, zasady i standardy dla następujących elementów: 

-   Standard klasyfikacji danych zgodny z ryzykiem biznesowym

-   Wgląd organizacji zabezpieczeń w czynniki ryzyka i spis elementów zawartości 

-   Zatwierdzenie przez organizację zabezpieczeń usług platformy Azure do użycia 

-   Bezpieczeństwo elementów zawartości w całym cyklu życia

-   Wymagana strategia kontroli dostępu zgodnie z klasyfikacją danych organizacji

-   Korzystanie z natywnych i zewnętrznych funkcji ochrony danych platformy Azure

-   Wymagania dotyczące szyfrowania danych dla przypadków użycia w trakcie przesyłania i w czasie spoczynku

-   Odpowiednie standardy kryptograficzne

Aby uzyskać więcej informacji, zapoznaj się z następującymi dokumentami:
- [Zalecenie dotyczące architektury zabezpieczeń platformy Azure — magazyn, dane i szyfrowanie](/azure/architecture/framework/security/storage-data-encryption?bc=%2fsecurity%2fcompass%2fbreadcrumb%2ftoc.json&toc=%2fsecurity%2fcompass%2ftoc.json)

- [Podstawy zabezpieczeń platformy Azure — zabezpieczenia, szyfrowanie i magazynowanie danych platformy Azure](../security/fundamentals/encryption-overview.md)

- [Cloud Adoption Framework — najlepsze rozwiązania z zakresu zabezpieczeń i szyfrowania danych platformy Azure](../security/fundamentals/data-encryption-best-practices.md?bc=%2fazure%2fcloud-adoption-framework%2f_bread%2ftoc.json&toc=%2fazure%2fcloud-adoption-framework%2ftoc.json)

- [Test porównawczy zabezpieczeń platformy Azure — zarządzanie elementami zawartości](../security/benchmarks/security-controls-v2-asset-management.md)

- [Test porównawczy zabezpieczeń platformy Azure — ochrona danych](../security/benchmarks/security-controls-v2-data-protection.md)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="gs-2-define-enterprise-segmentation-strategy"></a>GS-2: Definiowanie strategii segmentacji przedsiębiorstwa 

**Wskazówka**: Ustanów strategię całego przedsiębiorstwa w zakresie segmentacji dostępu do elementów zawartości przy użyciu kombinacji tożsamości, sieci, aplikacji, subskrypcji, grupy zarządzania i innych mechanizmów kontroli.

Należy starannie zrównoważyć potrzebę rozdzielania zabezpieczeń, aby umożliwić codzienne działanie systemów, które muszą komunikować się ze sobą i uzyskiwać dostęp do danych.

Upewnij się, że strategia segmentacji jest zaimplementowana spójnie dla różnych typów kontroli, w tym zabezpieczeń sieci, modeli tożsamości i dostępu, a także modeli uprawnień/dostępu i procesów ludzkich.

- [Wskazówki dotyczące strategii segmentacji na platformie Azure (wideo)](/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151)

- [Wskazówki dotyczące strategii segmentacji na platformie Azure (dokument)](/security/compass/governance#enterprise-segmentation-strategy)

- [Wyrównywanie segmentacji sieci przy użyciu strategii segmentacji przedsiębiorstwa](/security/compass/network-security-containment#align-network-segmentation-with-enterprise-segmentation-strategy)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="gs-3-define-security-posture-management-strategy"></a>GS-3: Definiowanie strategii zarządzania stanem zabezpieczeń

**Wskazówka**: Nieustannie mierz i ograniczaj ryzyko dla poszczególnych elementów zawartości i środowiska, w którym są hostowane. Ustalaj priorytety elementów zawartości o wysokiej wartości i wysoce narażonych na ataki obszarów, takich jak opublikowane aplikacje, punkty danych przychodzących i wychodzących sieci, punkty końcowe użytkowników i administratorów itp.

- [Test porównawczy zabezpieczeń platformy Azure — stan i zarządzanie lukami w zabezpieczeniach](../security/benchmarks/security-controls-v2-posture-vulnerability-management.md)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="gs-4-align-organization-roles-responsibilities-and-accountabilities"></a>GS-4: Dopasuj role organizacji, obowiązki i odpowiedzialność

**Wskazówka**: Zadbaj o to, aby udokumentować i udostępnić wyraźną strategię dotyczącą ról i obowiązków w organizacji zabezpieczeń. Ustalaj priorytety w celu wyraźnego określenia odpowiedzialności za decyzje dotyczące zabezpieczeń, informując wszystkie osoby o współużytkowanym modelu odpowiedzialności i informując zespoły techniczne o technologii do zabezpieczania chmury.

- [Najlepsze rozwiązanie dotyczące zabezpieczeń platformy Azure 1 — ludzie: informowanie zespołów o podróży zabezpieczeń w chmurze](/azure/cloud-adoption-framework/security/security-top-10#1-people-educate-teams-about-the-cloud-security-journey)

- [Najlepsze rozwiązanie dotyczące zabezpieczeń platformy Azure 2 — ludzie: informowanie zespołów o technologii zabezpieczeń w chmurze](/azure/cloud-adoption-framework/security/security-top-10#2-people-educate-teams-on-cloud-security-technology)

- [Najlepsze rozwiązanie dotyczące zabezpieczeń platformy Azure 3 — proces: przypisywanie odpowiedzialności za decyzje dotyczące zabezpieczeń chmury](/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="gs-5-define-network-security-strategy"></a>GS-5: Definiowanie strategii zabezpieczeń sieci

**Wskazówka**: Ustanów metodę zabezpieczeń sieci platformy Azure jako część ogólnej strategii kontroli dostępu zabezpieczeń w organizacji.  

Ta strategia powinna obejmować udokumentowane wskazówki, zasady i standardy dla następujących elementów: 

-   Scentralizowane zarządzanie siecią i odpowiedzialność w zakresie zabezpieczeń

-   Model segmentacji sieci wirtualnej zgodny ze strategią segmentacji przedsiębiorstwa

-   Strategia korygowania w różnych scenariuszach zagrożeń i ataków

-   Strategia internetowa i dotycząca brzegowego ruchu przychodzącego i wychodzącego

-   Strategia międzyłączności w chmurze hybrydowej i środowisku lokalnym

-   Aktualne artefakty zabezpieczeń sieci (np. diagramy sieciowe, architektura sieci referencyjnej)

Aby uzyskać więcej informacji, zapoznaj się z następującymi dokumentami:
- [Najlepsze rozwiązanie dotyczące zabezpieczeń platformy Azure 11 — architektura. Pojedyncza ujednolicona strategia zabezpieczeń](/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy)

- [Test porównawczy zabezpieczeń platformy Azure — zabezpieczenia sieci](../security/benchmarks/security-controls-v2-network-security.md)

- [Omówienie zabezpieczeń sieci platformy Azure](../security/fundamentals/network-overview.md)

- [Strategia architektury sieci przedsiębiorstwa](/azure/cloud-adoption-framework/ready/enterprise-scale/architecture)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="gs-6-define-identity-and-privileged-access-strategy"></a>GS-6: Definiowanie strategii dotyczącej tożsamości i dostępu uprzywilejowanego

**Wskazówka**: Ustanów metody obsługi tożsamości i dostępu uprzywilejowanego na platformie Azure jako część ogólnej strategii kontroli dostępu zabezpieczeń w organizacji.  

Ta strategia powinna obejmować udokumentowane wskazówki, zasady i standardy dla następujących elementów: 

-   Scentralizowany system tożsamości i uwierzytelniania oraz połączenie z innymi wewnętrznymi i zewnętrznymi systemami tożsamości

-   Metody silnego uwierzytelniania w różnych przypadkach użycia i warunkach

-   Ochrona użytkowników z wysokim poziomem uprawnień

-   Monitorowanie i obsługa nietypowych działań użytkowników  

-   Przegląd tożsamości i dostępu użytkownika oraz proces uzgadniania

Aby uzyskać więcej informacji, zapoznaj się z następującymi dokumentami:

- [Test porównawczy zabezpieczeń platformy Azure — zarządzanie tożsamością](../security/benchmarks/security-controls-v2-identity-management.md)

- [Test porównawczy zabezpieczeń platformy Azure — dostęp uprzywilejowany](../security/benchmarks/security-controls-v2-privileged-access.md)

- [Najlepsze rozwiązanie dotyczące zabezpieczeń platformy Azure 11 — architektura. Pojedyncza ujednolicona strategia zabezpieczeń](/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy)

- [Omówienie zabezpieczeń zarządzania tożsamościami platformy Azure](../security/fundamentals/identity-management-overview.md)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="gs-7-define-logging-and-threat-response-strategy"></a>GS-7: Definiowanie strategii rejestrowania i reagowania na zagrożenia

**Wskazówka**: Ustanów strategię rejestrowania i reagowania na zagrożenia, aby szybko wykrywać i eliminować zagrożenia oraz spełnić wymagania dotyczące zgodności. Ustalaj priorytety, dostarczając analitykom alerty wysokiej jakości i bezproblemowe środowisko, aby umożliwić im skoncentrowanie się na zagrożeniach, a nie na integracji i ręcznych działaniach. 

Ta strategia powinna obejmować udokumentowane wskazówki, zasady i standardy dla następujących elementów: 

-   Rola i obowiązki organizacji w zakresie operacji zabezpieczeń (SecOps) 

-   Dobrze zdefiniowany proces reagowania na zdarzenia zgodnie z NIST lub inną platformą branżową 

-   Przechwytywanie i przechowywanie dzienników w celu zapewnienia obsługi wykrywania zagrożeń, reagowania na zdarzenia i zgodności

-   Scentralizowana widoczność i korelacja informacji dotyczących zagrożeń przy użyciu rozwiązania SIEM, natywnych możliwości platformy Azure i innych źródeł 

-   Plan komunikacji i powiadomień z klientami, dostawcami i publicznymi zainteresowanymi stronami

-   Używanie natywnych i zewnętrznych platform Azure do obsługi zdarzeń, takich jak rejestrowanie i wykrywanie zagrożeń, postępowania dowodowe oraz korygowanie i eliminowanie ataków

-   Procesy obsługi zdarzeń i działań po zdarzeniu, takie jak zdobyte doświadczenia i przechowywanie dowodów

Aby uzyskać więcej informacji, zapoznaj się z następującymi dokumentami:

- [Test porównawczy zabezpieczeń platformy Azure — rejestrowanie i wykrywanie zagrożeń](../security/benchmarks/security-controls-v2-logging-threat-detection.md)

- [Test porównawczy zabezpieczeń platformy Azure — reagowanie na zdarzenia](../security/benchmarks/security-controls-v2-incident-response.md)

- [Najlepsze rozwiązanie dotyczące zabezpieczeń platformy Azure 4 — proces. Aktualizowanie procesów reagowania na zdarzenia dla chmury](/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

- [Przewodnik dotyczący decyzji w zakresie platformy wdrażania Azure, rejestrowania i raportowania](/azure/cloud-adoption-framework/decision-guides/logging-and-reporting/)

- [Skalowanie, zarządzanie i monitorowanie w przedsiębiorstwie na platformie Azure](/azure/cloud-adoption-framework/ready/enterprise-scale/management-and-monitoring)

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

## <a name="next-steps"></a>Następne kroki

- Zobacz [Omówienie testu porównawczego zabezpieczeń platformy Azure w wersji 2](../security/benchmarks/overview.md)
- Dowiedz się więcej o [punktach odniesienia zabezpieczeń platformy Azure](../security/benchmarks/security-baselines-overview.md)