---
title: Podstawa zabezpieczeń platformy Azure dla usługi Azure cache for Redis
description: Podstawa zabezpieczeń platformy Azure dla usługi Azure cache for Redis
author: msmbaldwin
ms.service: security
ms.topic: conceptual
ms.date: 03/16/2020
ms.author: mbaldwin
ms.custom: subject-security-benchmark
ms.openlocfilehash: 10277f18dd2a7ddaa436794839669e34f0ee95c3
ms.sourcegitcommit: 2bd0a039be8126c969a795cea3b60ce8e4ce64fc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/14/2021
ms.locfileid: "98195913"
---
# <a name="azure-security-baseline-for-azure-cache-for-redis"></a>Podstawa zabezpieczeń platformy Azure dla usługi Azure cache for Redis

Podstawowa baza danych zabezpieczeń Azure dla usługi Azure cache for Redis zawiera zalecenia, które pomogą ulepszyć zabezpieczenia stan wdrożenia.

Punkt odniesienia dla tej usługi jest rysowany w [wersji 1,0 usługi Azure Security test](../security/benchmarks/overview.md), która zawiera zalecenia dotyczące sposobu zabezpieczania rozwiązań w chmurze na platformie Azure z naszymi najlepszymi wskazówkami.

Aby uzyskać więcej informacji, zobacz [podstawy zabezpieczeń platformy Azure — omówienie](../security/benchmarks/security-baselines-overview.md).

## <a name="network-security"></a>Bezpieczeństwo sieci

*Aby uzyskać więcej informacji, zobacz [Kontrola zabezpieczeń: zabezpieczenia sieci](../security/benchmarks/security-control-network-security.md).*

### <a name="11-protect-resources-using-network-security-groups-or-azure-firewall-on-your-virtual-network"></a>1,1: Ochrona zasobów przy użyciu sieciowych grup zabezpieczeń lub zapory platformy Azure na Virtual Network

**Wskazówki**: Wdróż wystąpienie usługi Azure cache for Redis w sieci wirtualnej (VNET). Sieć wirtualna jest siecią prywatną w chmurze. Gdy usługa Azure cache for Redis jest skonfigurowana przy użyciu sieci wirtualnej, nie jest ona publicznie adresowana i można uzyskać do niej dostęp tylko z maszyn wirtualnych i aplikacji w sieci wirtualnej.

Możesz również określić reguły zapory z zakresem adresów IP początkowy i końcowy. Po skonfigurowaniu reguł zapory tylko połączenia klienckie z określonych zakresów adresów IP mogą łączyć się z pamięcią podręczną.

Jak skonfigurować obsługę Virtual Network w przypadku pamięci podręcznej systemu Azure w warstwie Premium dla Redis:

https://docs.microsoft.com/azure/azure-cache-for-redis/cache-how-to-premium-vnet

Jak skonfigurować usługę Azure cache for Redis reguły zapory:

https://docs.microsoft.com/azure/azure-cache-for-redis/cache-configure#firewall

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: Klient

### <a name="12-monitor-and-log-the-configuration-and-traffic-of-vnets-subnets-and-nics"></a>1,2: Monitoruj i Rejestruj konfigurację oraz ruch sieci wirtualnych, podsieci i kart sieciowych

**Wskazówki**: gdy Virtual Machines są wdrożone w tej samej sieci wirtualnej co wystąpienie usługi Azure cache for Redis, można użyć sieciowych grup zabezpieczeń (sieciowej grupy zabezpieczeń), aby zmniejszyć ryzyko eksfiltracji danych. Włącz dzienniki przepływu sieciowej grupy zabezpieczeń i Wyślij dzienniki do konta usługi Azure Storage na potrzeby inspekcji ruchu. Możesz również wysłać dzienniki przepływu sieciowej grupy zabezpieczeń do obszaru roboczego Log Analytics i użyć Analiza ruchu, aby uzyskać wgląd w przepływ ruchu w chmurze platformy Azure. Niektóre zalety Analiza ruchu to możliwość wizualizacji aktywności sieciowej i identyfikowania aktywnych punktów, identyfikowania zagrożeń bezpieczeństwa, zrozumienia wzorców przepływu ruchu i wyznaczania konfiguracji sieci.

Jak włączyć dzienniki przepływu sieciowej grupy zabezpieczeń:

https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-portal

Jak włączyć i używać Analiza ruchu:

https://docs.microsoft.com/azure/network-watcher/traffic-analytics

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

### <a name="13-protect-critical-web-applications"></a>1,3: Ochrona krytycznych aplikacji sieci Web

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone dla aplikacji sieci Web działających na Azure App Service lub zasobach obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="14-deny-communications-with-known-malicious-ip-addresses"></a>1,4: odmowa komunikacji ze znanymi złośliwymi adresami IP

**Wskazówki**: wdrażanie za pomocą usługi Azure Virtual Network (VNET) zapewnia ulepszone zabezpieczenia i izolację pamięci podręcznej platformy Azure dla usługi Redis, a także podsieci, zasady kontroli dostępu i inne funkcje w celu dodatkowego ograniczenia dostępu. W przypadku wdrożenia w sieci wirtualnej usługa Azure cache for Redis nie jest publicznie adresowana i można do niej uzyskać dostęp tylko z maszyn wirtualnych i aplikacji w sieci wirtualnej.

Włącz DDoS Protection Standard na sieci wirtualnych skojarzonym z pamięcią podręczną platformy Azure dla wystąpień Redis, aby chronić przed atakami typu "odmowa usługi" (DDoS). Użyj Azure Security Center zintegrowanej analizy zagrożeń, aby odmówić komunikacji ze znanymi złośliwymi lub nieużywanymi adresami IP.

Jak skonfigurować obsługę Virtual Network w przypadku pamięci podręcznej systemu Azure w warstwie Premium dla Redis:

https://docs.microsoft.com/azure/azure-cache-for-redis/cache-how-to-premium-vnet

Zarządzaj standardem Azure DDoS Protection przy użyciu Azure Portal:

https://docs.microsoft.com/azure/virtual-network/manage-ddos-protection

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

### <a name="15-record-network-packets-and-flow-logs"></a>1,5: rejestrowanie pakietów sieciowych i dzienników przepływów

**Wskazówki**: gdy maszyny wirtualne są wdrażane w tej samej sieci wirtualnej co wystąpienie usługi Azure cache for Redis, można użyć sieciowych grup zabezpieczeń (sieciowej grupy zabezpieczeń) w celu zmniejszenia ryzyka eksfiltracji danych. Włącz dzienniki przepływu sieciowej grupy zabezpieczeń i Wyślij dzienniki do konta usługi Azure Storage na potrzeby inspekcji ruchu. Możesz również wysłać dzienniki przepływu sieciowej grupy zabezpieczeń do obszaru roboczego Log Analytics i użyć Analiza ruchu, aby uzyskać wgląd w przepływ ruchu w chmurze platformy Azure. Niektóre zalety Analiza ruchu to możliwość wizualizacji aktywności sieciowej i identyfikowania aktywnych punktów, identyfikowania zagrożeń bezpieczeństwa, zrozumienia wzorców przepływu ruchu i wyznaczania konfiguracji sieci.

Jak włączyć dzienniki przepływu sieciowej grupy zabezpieczeń:

https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-portal

Jak włączyć i używać Analiza ruchu:

https://docs.microsoft.com/azure/network-watcher/traffic-analytics

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

### <a name="16-deploy-network-based-intrusion-detectionintrusion-prevention-systems-idsips"></a>1,6: Wdróż systemy zapobiegania wykrywaniu dostępu do sieci/dostępu intruzów (identyfikatory/adresy IP)

**Wskazówki**: Jeśli korzystasz z usługi Azure cache for Redis z aplikacjami sieci Web działającymi na Azure App Service lub wystąpieniami obliczeniowymi, wdróż wszystkie zasoby w usłudze Azure Virtual Network (VNET) i zabezpiecz je za pomocą zapory aplikacji sieci Web platformy Azure (WAF) w Application Gateway sieci Web. Skonfiguruj WAF do uruchamiania w "trybie zapobiegania". Tryb zapobiegania blokuje wtargnięcie i ataki wykrywane przez zasady. Osoba atakująca otrzymuje wyjątek "403 nieautoryzowany dostęp", a połączenie jest zamknięte. Tryb zapobiegania rejestruje takie ataki w dziennikach WAF.

Alternatywnie możesz wybrać ofertę z portalu Azure Marketplace, która obsługuje funkcje identyfikatorów/adresów IP z możliwościami inspekcji ładunku i/lub wykrywania anomalii.

Informacje o możliwościach usługi Azure WAF:

https://docs.microsoft.com/azure/web-application-firewall/ag/ag-overview

Jak wdrożyć usługę Azure WAF:

https://docs.microsoft.com/azure/web-application-firewall/ag/create-waf-policy-ag

Portal Azure Marketplace:

https://azuremarketplace.microsoft.com/marketplace/?term=Firewall

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: Klient

### <a name="17-manage-traffic-to-web-applications"></a>1,7: zarządzanie ruchem do aplikacji sieci Web

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone dla aplikacji sieci Web działających na Azure App Service lub zasobach obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="18-minimize-complexity-and-administrative-overhead-of-network-security-rules"></a>1,8: Minimalizacja złożoności i kosztów administracyjnych reguł zabezpieczeń sieci

**Wskazówki**: używanie tagów usługi sieci wirtualnej do definiowania kontroli dostępu do sieci w grupach zabezpieczeń sieci (sieciowej grupy zabezpieczeń) lub w zaporze platformy Azure. Podczas tworzenia reguł zabezpieczeń można użyć tagów usługi zamiast konkretnych adresów IP. Określając nazwę tagu usługi (np. ApiManagement) w odpowiednim polu źródłowym lub docelowym reguły, można zezwolić na ruch dla odpowiedniej usługi lub go odrzucić. Firma Microsoft zarządza prefiksami adresów, które obejmują tag usługi, i automatycznie aktualizuje tag usługi jako adresy.

Możesz również użyć grup zabezpieczeń aplikacji (ASG), aby uprościć złożoną konfigurację zabezpieczeń. Grupy zabezpieczeń aplikacji umożliwiają skonfigurowanie zabezpieczeń sieci jako naturalnego rozszerzenia struktury aplikacji, co pozwala na grupowanie maszyn wirtualnych i definiowanie zasad zabezpieczeń sieci na podstawie tych grup.

Tagi usługi sieci wirtualnej:

https://docs.microsoft.com/azure/virtual-network/service-tags-overview

Grupy zabezpieczeń aplikacji:

https://docs.microsoft.com/azure/virtual-network/security-overview#application-security-groups

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="19-maintain-standard-security-configurations-for-network-devices"></a>1,9: Obsługa standardowych konfiguracji zabezpieczeń dla urządzeń sieciowych

**Wskazówki**: Definiowanie i implementowanie standardowych konfiguracji zabezpieczeń dla zasobów sieciowych związanych z pamięcią podręczną platformy Azure dla wystąpień Redis z Azure Policy. Użyj aliasów Azure Policy w przestrzeniach nazw "Microsoft. cache" i "Microsoft. Network", aby utworzyć niestandardowe zasady inspekcji lub wymuszania konfiguracji sieci pamięci podręcznej platformy Azure dla wystąpień Redis. Możesz również używać wbudowanych definicji zasad, takich jak:

Należy włączyć tylko bezpieczne połączenia z Redis Cache

Należy włączyć Standard DDoS Protection

Możesz również użyć planów platformy Azure, aby uprościć duże wdrożenia platformy Azure przez pakowanie kluczowych artefaktów, takich jak szablony Azure Resource Manager (ARM), kontrola dostępu oparta na rolach (RBAC) na platformie Azure i zasady, w ramach jednej definicji planu. Łatwo stosuj plan do nowych subskrypcji i środowisk, a następnie dostosuj kontrolę i zarządzanie przy użyciu wersji.

Jak skonfigurować Azure Policy i zarządzać nimi:

https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage

Jak utworzyć Azure Blueprint:

https://docs.microsoft.com/azure/governance/blueprints/create-blueprint-portal

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="110-document-traffic-configuration-rules"></a>1,10: udokumentowanie reguł konfiguracji ruchu

**Wskazówki**: Użyj tagów dla zasobów sieciowych skojarzonych z pamięcią podręczną platformy Azure w celu wdrożenia Redis, aby logicznie zorganizować je w taksonomię.

Tworzenie i używanie tagów:

https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="111-use-automated-tools-to-monitor-network-resource-configurations-and-detect-changes"></a>1,11: Użyj zautomatyzowanych narzędzi do monitorowania konfiguracji zasobów sieciowych i wykrywania zmian

**Wskazówki**: Użyj dziennika aktywności platformy Azure do monitorowania konfiguracji zasobów sieciowych i wykrywania zmian zasobów sieciowych związanych z pamięcią podręczną platformy Azure dla wystąpień Redis. Tworzenie alertów w ramach Azure Monitor, które będą wyzwalane po wprowadzeniu zmian w krytycznych zasobach sieciowych.

Jak wyświetlać i pobierać zdarzenia dziennika aktywności platformy Azure:

https://docs.microsoft.com/azure/azure-monitor/platform/activity-log-view

Jak utworzyć alerty w Azure Monitor:

https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

## <a name="logging-and-monitoring"></a>Rejestrowanie i monitorowanie

*Aby uzyskać więcej informacji, zobacz [Kontrola zabezpieczeń: rejestrowanie i monitorowanie](../security/benchmarks/security-control-logging-monitoring.md).*

### <a name="21-use-approved-time-synchronization-sources"></a>2,1: Użyj źródeł synchronizacji zatwierdzonego czasu

**Wskazówki**: Firma Microsoft utrzymuje źródło czasu używane dla zasobów platformy Azure, takich jak usługa Azure cache for Redis, dla sygnatur czasowych w dziennikach.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Microsoft

### <a name="22-configure-central-security-log-management"></a>2,2: Skonfiguruj centralne zarządzanie dziennikami zabezpieczeń

**Wskazówki**: Włączanie ustawień diagnostycznych dziennika aktywności platformy Azure i wysyłanie dzienników do obszaru roboczego log Analytics, usługi Azure Event Hub lub konta usługi Azure Storage w celu archiwizacji. Dzienniki aktywności zapewniają wgląd w operacje wykonane w pamięci podręcznej platformy Azure dla wystąpień Redis na poziomie płaszczyzny kontroli. Korzystając z danych dziennika aktywności platformy Azure, można określić "co, kto i kiedy" dla każdej operacji zapisu (PUT, POST, DELETE) wykonanej na poziomie płaszczyzny kontroli dla pamięci podręcznej platformy Azure dla wystąpień Redis.

Jak włączyć ustawienia diagnostyczne dla dziennika aktywności platformy Azure: https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-settings-legacy

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: Klient

### <a name="23-enable-audit-logging-for-azure-resources"></a>2,3: Włączanie rejestrowania inspekcji dla zasobów platformy Azure

**Wskazówki**: Włączanie ustawień diagnostycznych dziennika aktywności platformy Azure i wysyłanie dzienników do obszaru roboczego log Analytics, usługi Azure Event Hub lub konta usługi Azure Storage w celu archiwizacji. Dzienniki aktywności zapewniają wgląd w operacje wykonane w pamięci podręcznej platformy Azure dla wystąpień Redis na poziomie płaszczyzny kontroli. Korzystając z danych dziennika aktywności platformy Azure, można określić "co, kto i kiedy" dla każdej operacji zapisu (PUT, POST, DELETE) wykonanej na poziomie płaszczyzny kontroli dla pamięci podręcznej platformy Azure dla wystąpień Redis.

Chociaż metryki są dostępne przez włączenie ustawień diagnostycznych, rejestrowanie inspekcji w płaszczyźnie danych nie jest jeszcze dostępne dla usługi Azure cache for Redis.

Jak włączyć ustawienia diagnostyczne dla dziennika aktywności platformy Azure: https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-settings-legacy

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: Klient

### <a name="24-collect-security-logs-from-operating-systems"></a>2,4: Zbierz dzienniki zabezpieczeń z systemów operacyjnych

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="25-configure-security-log-storage-retention"></a>2,5: Konfigurowanie przechowywania magazynu dzienników zabezpieczeń

**Wskazówki**: w Azure monitor ustawić okres przechowywania dziennika dla log Analytics obszarów roboczych skojarzonych z pamięcią podręczną platformy Azure dla wystąpień Redis zgodnie z przepisami obowiązującymi w organizacji.

Należy zauważyć, że rejestrowanie inspekcji w płaszczyźnie danych nie jest jeszcze dostępne dla usługi Azure cache for Redis.

Jak ustawić parametry przechowywania dziennika:

https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage#change-the-data-retention-period

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="26-monitor-and-review-logs"></a>2,6: dzienniki monitorowania i przeglądania

**Wskazówki**: Włączanie ustawień diagnostycznych dziennika aktywności platformy Azure i wysyłanie dzienników do obszaru roboczego log Analytics. Wykonuj zapytania w Log Analytics, aby wyszukiwać terminy, identyfikować trendy, analizować wzorce i udostępniać wiele innych szczegółowych informacji na podstawie danych dziennika aktywności, które mogły zostać zebrane dla usługi Azure cache for Redis.

Należy zauważyć, że rejestrowanie inspekcji w płaszczyźnie danych nie jest jeszcze dostępne dla usługi Azure cache for Redis.

Jak włączyć ustawienia diagnostyczne dla dziennika aktywności platformy Azure: https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-settings-legacy

Jak zbierać i analizować dzienniki aktywności platformy Azure w obszarze roboczym Log Analytics w Azure Monitor: https://docs.microsoft.com/azure/azure-monitor/platform/activity-log-collect

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="27-enable-alerts-for-anomalous-activity"></a>2,7: Włączanie alertów dla nietypowego działania

**Wskazówki**: można skonfigurować w taki sposób, aby otrzymywać alerty na podstawie metryk i dzienników aktywności związanych z pamięcią podręczną platformy Azure dla wystąpień Redis. Azure Monitor umożliwia skonfigurowanie alertu w celu wysłania powiadomienia e-mail, wywołania elementu webhook lub wywoływać aplikację logiki platformy Azure.

Chociaż metryki są dostępne przez włączenie ustawień diagnostycznych, rejestrowanie inspekcji w płaszczyźnie danych nie jest jeszcze dostępne dla usługi Azure cache for Redis.

Jak skonfigurować alerty dla usługi Azure cache for Redis: https://docs.microsoft.com/azure/azure-cache-for-redis/cache-how-to-monitor#alerts

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="28-centralize-anti-malware-logging"></a>2,8: scentralizowanie rejestrowania chroniącego przed złośliwym oprogramowaniem

**Wskazówki**: nie dotyczy; Usługa Azure cache for Redis nie przetwarza ani nie tworzy dzienników związanych z oprogramowaniem chroniącym przed złośliwym kodem.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="29-enable-dns-query-logging"></a>2,9: Włączanie rejestrowania zapytań DNS

**Wskazówki**: nie dotyczy; Usługa Azure cache for Redis nie przetwarza ani nie tworzy dzienników związanych z usługą DNS.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="210-enable-command-line-audit-logging"></a>2,10: Włączanie rejestrowania inspekcji w wierszu polecenia

**Wskazówki**: nie dotyczy; te wytyczne są przeznaczone dla zasobów obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

## <a name="identity-and-access-control"></a>Tożsamość i kontrola dostępu

*Aby uzyskać więcej informacji, zobacz [Kontrola zabezpieczeń: tożsamość i Access Control](../security/benchmarks/security-control-identity-access-control.md).*

### <a name="31-maintain-an-inventory-of-administrative-accounts"></a>3,1: obsługa spisu kont administracyjnych

**Wskazówki**: Azure Active Directory (AD) ma wbudowane role, które muszą być jawnie przypisane i są queryable. Za pomocą modułu Azure AD PowerShell można wykonywać zapytania ad hoc w celu odnajdywania kont należących do grup administracyjnych.

Jak uzyskać rolę katalogu w usłudze Azure AD przy użyciu programu PowerShell: https://docs.microsoft.com/powershell/module/azuread/get-azureaddirectoryrole?view=azureadps-2.0

Jak uzyskać członków roli katalogu w usłudze Azure AD przy użyciu programu PowerShell: https://docs.microsoft.com/powershell/module/azuread/get-azureaddirectoryrolemember?view=azureadps-2.0

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

### <a name="32-change-default-passwords-where-applicable"></a>3,2: Zmień domyślne hasła, jeśli ma to zastosowanie

**Wskazówki**: płaszczyzna kontroli dostęp do usługi Azure cache for Redis jest kontrolowany za pomocą Azure Active Directory (AD). Usługa Azure AD nie ma koncepcji domyślnych haseł. 

Dostęp za pomocą płaszczyzny danych do usługi Azure cache for Redis jest kontrolowany przez klucze dostępu. Te klucze są używane przez klientów nawiązujących połączenie z pamięcią podręczną i mogą być ponownie generowane w dowolnym momencie.

Nie zaleca się tworzenia domyślnych haseł do aplikacji. Zamiast tego można przechowywać hasła w Azure Key Vault a następnie używać Azure Active Directory do pobierania ich.

Jak ponownie wygenerować pamięć podręczną platformy Azure dla kluczy dostępu Redis: https://docs.microsoft.com/azure/azure-cache-for-redis/cache-configure#settings

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Współużytkowane

### <a name="33-use-dedicated-administrative-accounts"></a>3,3: Użyj dedykowanych kont administracyjnych

**Wskazówki**: Tworzenie standardowych procedur operacyjnych dotyczących korzystania z dedykowanych kont administracyjnych. Użyj Azure Security Center Zarządzanie tożsamościami i dostępem, aby monitorować liczbę kont administracyjnych.

Ponadto, aby ułatwić śledzenie dedykowanych kont administracyjnych, można użyć zaleceń z Azure Security Center lub wbudowanych zasad platformy Azure, takich jak:

- Do subskrypcji powinien być przypisany więcej niż jeden właściciel

- Przestarzałe konta z uprawnieniami właściciela powinny zostać usunięte z subskrypcji

- Konta zewnętrzne z uprawnieniami właściciela powinny zostać usunięte z subskrypcji

Jak używać Azure Security Center do monitorowania tożsamości i dostępu (wersja zapoznawcza): https://docs.microsoft.com/azure/security-center/security-center-identity-access

Jak używać Azure Policy: https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage


**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

### <a name="34-use-single-sign-on-sso-with-azure-active-directory"></a>3,4: Korzystaj z logowania jednokrotnego (SSO) z usługą Azure Active Directory

**Wskazówki**: usługa Azure cache for Redis korzysta z kluczy dostępu do uwierzytelniania użytkowników i nie obsługuje logowania jednokrotnego na poziomie płaszczyzny danych. Dostęp do płaszczyzny kontroli dla usługi Azure cache for Redis jest dostępny za pośrednictwem interfejsu API REST i obsługuje logowanie jednokrotne. Aby przeprowadzić uwierzytelnianie, należy ustawić nagłówek autoryzacji dla żądań na token sieci Web JSON uzyskany z Azure Active Directory.

Informacje o usłudze Azure cache for Redis — interfejs API REST: https://docs.microsoft.com/rest/api/redis/

Opis logowania jednokrotnego w usłudze Azure AD: https://docs.microsoft.com/azure/active-directory/manage-apps/what-is-single-sign-on


**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="35-use-multi-factor-authentication-for-all-azure-active-directory-based-access"></a>3,5: Użyj uwierzytelniania wieloskładnikowego, aby uzyskać dostęp oparty na Azure Active Directory

**Wskazówki**: Włączanie Azure Active Directory (AD) Multi-Factor Authentication (MFA) i postępuj zgodnie z zaleceniami dotyczącymi zarządzania tożsamościami i dostępem Azure Security Center.

Jak włączyć usługę MFA na platformie Azure: https://docs.microsoft.com/azure/active-directory/authentication/howto-mfa-getstarted

Jak monitorować tożsamość i dostęp w Azure Security Center: https://docs.microsoft.com/azure/security-center/security-center-identity-access

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

### <a name="36-use-dedicated-machines-privileged-access-workstations-for-all-administrative-tasks"></a>3,6: Używaj dedykowanych maszyn (uprzywilejowany dostęp do stacji roboczych) dla wszystkich zadań administracyjnych

**Wskazówki**: Użyj stacji roboczych dostępu uprzywilejowanego (dostępem uprzywilejowanym) z usługą Multi-Factor Authentication (MFA) skonfigurowaną w celu logowania się i konfigurowania zasobów platformy Azure.

Dowiedz się więcej o stacjach roboczych uprzywilejowanego dostępu:

https://4sysops.com/archives/understand-the-microsoft-privileged-access-workstation-paw-security-model/

Jak włączyć usługę MFA na platformie Azure:

https://docs.microsoft.com/azure/active-directory/authentication/howto-mfa-getstarted

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="37-log-and-alert-on-suspicious-activity-from-administrative-accounts"></a>3,7: dziennik i alert dotyczący podejrzanego działania z kont administracyjnych

**Wskazówki**: Użyj Azure Active Directory (AD) PRIVILEGED Identity Management (PIM) do generowania dzienników i alertów w przypadku wystąpienia podejrzanych lub niebezpiecznych działań w środowisku.

Ponadto za pomocą funkcji wykrywania ryzyka usługi Azure AD można wyświetlać alerty i raporty na temat ryzykownego zachowania użytkowników.

Jak wdrożyć Privileged Identity Management (PIM): https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-deployment-plan

Informacje o wykrywaniu ryzyka usługi Azure AD: https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-risk-events

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

### <a name="38-manage-azure-resources-from-only-approved-locations"></a>3,8: zarządzanie zasobami platformy Azure tylko z zatwierdzonych lokalizacji

**Wskazówki**: Skonfiguruj nazwane lokalizacje w Azure Active Directory (AD) dostęp warunkowy, aby zezwolić na dostęp tylko z określonych logicznych grup zakresów lub krajów/regionów adresów IP.

Jak skonfigurować nazwane lokalizacje na platformie Azure: https://docs.microsoft.com/azure/active-directory/reports-monitoring/quickstart-configure-named-locations

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="39-use-azure-active-directory"></a>3,9: Użyj Azure Active Directory

**Wskazówki**: Użyj Azure Active Directory (AD) jako centralnego systemu uwierzytelniania i autoryzacji. Usługa Azure AD chroni dane przy użyciu silnego szyfrowania danych przechowywanych i przesyłanych. Usługa Azure AD również Sole, skróty i bezpieczne przechowywanie poświadczeń użytkownika.

Uwierzytelniania usługi Azure AD nie można używać do bezpośredniego dostępu do usługi Azure cache for Redis ", jednak poświadczenia usługi Azure AD mogą być używane do administrowania na poziomie płaszczyzny kontroli (tj. Azure Portal) do sterowania usługą Azure cache dla kluczy dostępu Redis.


**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

### <a name="310-regularly-review-and-reconcile-user-access"></a>3,10: regularnie Przeglądaj i Uzgodnij dostęp użytkowników

**Wskazówki**: Azure Active Directory (AD) zawiera dzienniki ułatwiające odnajdywanie starych kont. Ponadto za pomocą przeglądów dostępu do tożsamości platformy Azure można efektywnie zarządzać członkostwem w grupach, dostępem do aplikacji dla przedsiębiorstw i przypisaniami ról. Dostęp użytkowników może być regularnie przeglądany, aby upewnić się, że tylko Ci użytkownicy mają ciągły dostęp. 

Informacje o raportowaniu usługi Azure AD: https://docs.microsoft.com/azure/active-directory/reports-monitoring/

Jak korzystać z przeglądów dostępu do tożsamości platformy Azure: https://docs.microsoft.com/azure/active-directory/governance/access-reviews-overview

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

### <a name="311-monitor-attempts-to-access-deactivated-accounts"></a>3,11: Monitor próbuje uzyskać dostęp do zdezaktywowanych kont

**Wskazówki**: masz dostęp do źródeł działań związanych z logowaniem do Azure Active Directory (AD), inspekcją i ryzykiem związanym z dziennikiem zdarzeń, które umożliwiają integrację z platformą Azure — wskaźnikiem lub SIEMem innych firm.

Proces ten można usprawnić, tworząc ustawienia diagnostyczne dla kont użytkowników usługi Azure AD i wysyłając dzienniki inspekcji i dzienniki logowania do obszaru roboczego Log Analytics. Żądane alerty dzienników można skonfigurować w ramach Log Analytics.

Jak zintegrować dzienniki aktywności platformy Azure z Azure Monitor: https://docs.microsoft.com/azure/active-directory/reports-monitoring/howto-integrate-activity-logs-with-log-analytics

Jak przejść do tablicy wskaźnikowej platformy Azure: https://docs.microsoft.com/azure/sentinel/quickstart-onboard

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: Klient

### <a name="312-alert-on-account-login-behavior-deviation"></a>3,12: odchylenia zachowania podczas logowania do konta

**Wskazówki**: w celu odróżnienia działania logowania do konta na płaszczyźnie kontroli Użyj funkcji ochrony tożsamości Azure Active Directory (AD) i wykrywania ryzyka, aby skonfigurować automatyczne odpowiedzi na wykryte podejrzane działania związane z tożsamościami użytkowników. Możesz również pozyskać dane do usługi Azure wskaźnikowej na potrzeby dalszej analizy.

Jak wyświetlić ryzykowne logowania usługi Azure AD: https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-risky-sign-ins

Jak skonfigurować i włączyć zasady dotyczące ryzyka związanego z ochroną tożsamości: https://docs.microsoft.com/azure/active-directory/identity-protection/howto-identity-protection-configure-risk-policies

Jak dołączyć wskaźnik na platformie Azure: https://docs.microsoft.com/azure/sentinel/quickstart-onboard

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: Klient

### <a name="313-provide-microsoft-with-access-to-relevant-customer-data-during-support-scenarios"></a>3,13: Zapewnij firmie Microsoft dostęp do odpowiednich danych klienta w scenariuszach pomocy technicznej

**Wskazówki**: nie są jeszcze dostępne; Skrytka klienta nie jest jeszcze obsługiwana w przypadku usługi Azure cache for Redis.

Lista usług obsługiwanych przez Skrytka klienta:

https://docs.microsoft.com/azure/security/fundamentals/customer-lockbox-overview#supported-services-and-scenarios-in-general-availability

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: nie dotyczy

## <a name="data-protection"></a>Ochrona danych

*Aby uzyskać więcej informacji, zobacz [Kontrola zabezpieczeń: Ochrona danych](../security/benchmarks/security-control-data-protection.md).*

### <a name="41-maintain-an-inventory-of-sensitive-information"></a>4,1: przechowywanie spisu poufnych informacji

**Wskazówki**: Użyj tagów, aby pomóc w śledzeniu zasobów platformy Azure, które przechowują lub przetwarzają informacje poufne.

Tworzenie i używanie tagów:

https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="42-isolate-systems-storing-or-processing-sensitive-information"></a>4,2: Izoluj systemy przechowujące lub przetwarzające informacje poufne

**Wskazówki**: implementowanie oddzielnych subskrypcji i/lub grup zarządzania na potrzeby tworzenia, testowania i produkcji. Pamięć podręczna Azure dla wystąpień Redis powinna być oddzielona przez sieć wirtualną/podsieć i odpowiednio oznakowane. Opcjonalnie użyj usługi Azure cache for Redis, aby zdefiniować reguły, tak aby tylko połączenia klienckie z określonych zakresów adresów IP mogły łączyć się z pamięcią podręczną.

Jak utworzyć dodatkowe subskrypcje platformy Azure:

https://docs.microsoft.com/azure/billing/billing-create-subscription

Jak utworzyć Grupy zarządzania:

https://docs.microsoft.com/azure/governance/management-groups/create

Jak wdrożyć usługę Azure cache for Redis w sieci wirtualnej:

https://docs.microsoft.com/azure/azure-cache-for-redis/cache-how-to-premium-vnet

Jak skonfigurować usługę Azure cache for Redis reguły zapory:

https://docs.microsoft.com/azure/azure-cache-for-redis/cache-configure#firewall

Tworzenie i używanie tagów:

https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: Klient

### <a name="43-monitor-and-block-unauthorized-transfer-of-sensitive-information"></a>4,3: Monitoruj i blokuj nieautoryzowany transfer informacji poufnych

**Wskazówki**: nie są jeszcze dostępne; funkcje identyfikacji, klasyfikacji i zapobiegania utracie danych nie są jeszcze dostępne dla usługi Azure cache for Redis.

Firma Microsoft zarządza podstawową infrastrukturą dla usługi Azure cache for Redis i ma zaimplementowane ścisłe kontrole, aby zapobiec utracie lub narażeniu danych klientów.

Zrozumienie ochrony danych klientów na platformie Azure: https://docs.microsoft.com/azure/security/fundamentals/protection-customer-data

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: Współużytkowane

### <a name="44-encrypt-all-sensitive-information-in-transit"></a>4,4: Szyfruj wszystkie poufne informacje podczas przesyłania

**Wskazówki**: usługa Azure cache for Redis wymaga domyślnie komunikacji szyfrowanej przy użyciu protokołu TLS. Protokoły TLS w wersji 1,0, 1,1 i 1,2 są obecnie obsługiwane. Jednak protokoły TLS 1,0 i 1,1 znajdują się na ścieżce, aby wycofać całe branże, więc Użyj protokołu TLS 1,2, jeśli jest to możliwe. Jeśli Biblioteka klienta lub narzędzie nie obsługuje protokołu TLS, można włączyć nieszyfrowane połączenia za pomocą Azure Portal lub interfejsów API zarządzania. W takich przypadkach, gdy połączenia szyfrowane nie są możliwe, będzie zalecane umieszczenie pamięci podręcznej i aplikacji klienckiej w sieci wirtualnej.

Informacje o szyfrowaniu podczas przesyłania dla usługi Azure cache for Redis:

https://docs.microsoft.com/azure/azure-cache-for-redis/cache-best-practices

Zrozumienie wymaganych portów używanych w scenariuszach pamięci podręcznej sieci wirtualnej:

https://docs.microsoft.com/azure/azure-cache-for-redis/cache-how-to-premium-vnet#outbound-port-requirements

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Współużytkowane

### <a name="45-use-an-active-discovery-tool-to-identify-sensitive-data"></a>4,5: Użyj aktywnego narzędzia do odnajdywania, aby identyfikować poufne dane

**Wskazówki**: funkcje identyfikacji, klasyfikacji i zapobiegania utracie danych nie są jeszcze dostępne dla usługi Azure cache for Redis. Wystąpienia tagów zawierające poufne informacje jako takie i Implementuj rozwiązanie innych firm, jeśli jest to wymagane do celów zgodności.

W przypadku podstawowej platformy zarządzanej przez firmę Microsoft Firma Microsoft traktuje całą zawartość klienta jako poufną i nadaje im dużą długość, aby chronić przed utratą i narażeniem danych przez klienta. Aby zapewnić bezpieczeństwo danych klienta na platformie Azure, firma Microsoft wdrożyła i utrzymuje pakiet niezawodnych kontroli i możliwości ochrony danych.

Zrozumienie ochrony danych klientów na platformie Azure: https://docs.microsoft.com/azure/security/fundamentals/protection-customer-data

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: Klient

### <a name="46-use-azure-rbac-to-control-access-to-resources"></a>4,6: korzystanie z usługi Azure RBAC do kontrolowania dostępu do zasobów

**Wskazówki**: Użyj kontroli dostępu opartej na rolach (Azure RBAC) na platformie Azure, aby kontrolować dostęp do pamięci podręcznej platformy Azure dla płaszczyzny kontroli Redis (tj. Azure Portal). 

Jak skonfigurować usługę Azure RBAC:

https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="47-use-host-based-data-loss-prevention-to-enforce-access-control"></a>4,7: Wymuś kontrolę dostępu przy użyciu ochrony przed utratą danych opartą na hoście

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych.

Firma Microsoft zarządza podstawową infrastrukturą dla usługi Azure cache for Redis i ma zaimplementowane ścisłe kontrole, aby zapobiec utracie lub narażeniu danych klientów.

Zrozumienie ochrony danych klientów na platformie Azure:

https://docs.microsoft.com/azure/security/fundamentals/protection-customer-data

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="48-encrypt-sensitive-information-at-rest"></a>4,8: Szyfruj poufne informacje w spoczynku

**Wskazówki**: pamięć podręczna systemu Azure dla Redis przechowuje dane klientów w pamięci, a jednocześnie silnie chronione przez wiele formantów wdrożonych przez firmę Microsoft pamięć nie jest domyślnie szyfrowana. Jeśli jest to wymagane przez organizację, Zaszyfruj zawartość przed przechowywaniem w pamięci podręcznej platformy Azure dla Redis.

W przypadku korzystania z usługi Azure cache for Redis z funkcją "Redis danych trwałości" dane są wysyłane do konta usługi Azure Storage, które jest używane i zarządzane przez użytkownika. Można skonfigurować trwałość z poziomu bloku "New Azure cache for Redis" podczas tworzenia pamięci podręcznej oraz w menu zasobów dla istniejących pamięci podręcznych w warstwie Premium.

Dane w usłudze Azure Storage są szyfrowane i odszyfrowywane w sposób niewidoczny dla użytkownika przy użyciu 256-bitowego szyfrowania AES, jednego z najsilniejszych szyfrów blokowych i jest zgodny ze standardem FIPS 140-2. Nie można wyłączyć szyfrowania usługi Azure Storage. Możesz polegać na kluczach zarządzanych przez firmę Microsoft na potrzeby szyfrowania konta magazynu lub można zarządzać szyfrowaniem przy użyciu własnych kluczy.

Jak skonfigurować trwałość w pamięci podręcznej platformy Azure dla Redis: https://docs.microsoft.com/azure/azure-cache-for-redis/cache-how-to-premium-persistence

Informacje o szyfrowaniu dla kont usługi Azure Storage: https://docs.microsoft.com/azure/storage/common/storage-service-encryption

Opis ochrony danych klientów platformy Azure: https://docs.microsoft.com/azure/security/fundamentals/protection-customer-data

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Współużytkowane

### <a name="49-log-and-alert-on-changes-to-critical-azure-resources"></a>4,9: Rejestruj i Ostrzegaj o zmianach krytycznych zasobów platformy Azure

**Wskazówki**: Użyj Azure monitor z dziennikiem aktywności platformy Azure, aby utworzyć alerty, kiedy zmiany są wprowadzane do wystąpień produkcyjnych usługi Azure cache for Redis i innych krytycznych lub powiązanych zasobów.

Jak utworzyć alerty dla zdarzeń dziennika aktywności platformy Azure:

https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

## <a name="vulnerability-management"></a>Zarządzanie lukami w zabezpieczeniach

*Aby uzyskać więcej informacji, zobacz [Kontrola zabezpieczeń: Zarządzanie lukami w zabezpieczeniach](../security/benchmarks/security-control-vulnerability-management.md).*

### <a name="51-run-automated-vulnerability-scanning-tools"></a>5,1: uruchamianie narzędzi do skanowania automatycznych luk w zabezpieczeniach

**Wskazówki**: Postępuj zgodnie z zaleceniami Azure Security Center na Zabezpieczanie pamięci podręcznej systemu Azure dla wystąpień Redis i powiązanych zasobów.

Firma Microsoft przeprowadza zarządzanie lukami w systemach bazowych, które obsługują usługę Azure cache for Redis.

Informacje Azure Security Center zalecenia: https://docs.microsoft.com/azure/security-center/recommendations-reference

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Współużytkowane

### <a name="52-deploy-automated-operating-system-patch-management-solution"></a>5,2: Wdróż automatyczne rozwiązanie do zarządzania poprawkami systemu operacyjnego

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="53-deploy-automated-third-party-software-patch-management-solution"></a>5,3: Wdróż zautomatyzowane rozwiązanie do zarządzania poprawkami oprogramowania innych firm

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="54-compare-back-to-back-vulnerability-scans"></a>5,4: porównanie luk w zabezpieczeniach z tyłu do tyłu

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="55-use-a-risk-rating-process-to-prioritize-the-remediation-of-discovered-vulnerabilities"></a>5,5: Użyj procesu oceny ryzyka, aby określić priorytety korygowania odkrytych luk w zabezpieczeniach

**Wskazówki**: Firma Microsoft przeprowadza zarządzanie lukami w systemach bazowych, które obsługują usługę Azure cache for Redis.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Microsoft

## <a name="inventory-and-asset-management"></a>Zarządzanie magazynem i zasobami

*Aby uzyskać więcej informacji, zobacz [Kontrola zabezpieczeń: Spis i zarządzanie zasobami](../security/benchmarks/security-control-inventory-asset-management.md).*

### <a name="61-use-azure-asset-discovery"></a>6,1: Użyj odnajdywania zasobów platformy Azure

**Wskazówki**: Użyj grafu zasobów platformy Azure do wykonywania zapytań/odnajdywania wszystkich zasobów (takich jak obliczenia, magazyn, Sieć, porty i protokoły itp.) w ramach subskrypcji.  Upewnij się, że masz odpowiednie uprawnienia (odczyt) w dzierżawie i Wylicz wszystkie subskrypcje platformy Azure oraz zasoby w ramach subskrypcji.

Mimo że klasyczne zasoby platformy Azure mogą zostać odnalezione za pośrednictwem grafu zasobów, zdecydowanie zaleca się tworzenie i używanie Azure Resource Manager zasobów do przodu.

Jak tworzyć zapytania przy użyciu grafu zasobów platformy Azure: https://docs.microsoft.com/azure/governance/resource-graph/first-query-portal

Jak wyświetlić subskrypcje platformy Azure: https://docs.microsoft.com/powershell/module/az.accounts/get-azsubscription?view=azps-3.0.0

Opis kontroli RBAC platformy Azure: https://docs.microsoft.com/azure/role-based-access-control/overview

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="62-maintain-asset-metadata"></a>6,2: Konserwowanie metadanych zasobów

**Wskazówki**: stosowanie tagów do zasobów platformy Azure, dzięki czemu metadane są logicznie zorganizowane w taksonomię.

Tworzenie i używanie tagów:

https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="63-delete-unauthorized-azure-resources"></a>6,3: Usuń nieautoryzowane zasoby platformy Azure

**Wskazówki**: używanie tagowania, grup zarządzania i oddzielnych subskrypcji, gdzie to konieczne, do organizowania i śledzenia usługi Azure cache dla wystąpień Redis i powiązanych zasobów. Regularnie Uzgadniaj spis i zapewnij, że nieautoryzowane zasoby są usuwane z subskrypcji w odpowiednim czasie.

Ponadto należy używać Azure Policy do umieszczania ograniczeń dotyczących typu zasobów, które można utworzyć w subskrypcjach klientów, przy użyciu następujących wbudowanych definicji zasad:

- Niedozwolone typy zasobów

- Dozwolone typy zasobów

Jak utworzyć dodatkowe subskrypcje platformy Azure: https://docs.microsoft.com/azure/billing/billing-create-subscription

Jak utworzyć Grupy zarządzania: https://docs.microsoft.com/azure/governance/management-groups/create

Tworzenie i używanie tagów: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="64-maintain-an-inventory-of-approved-azure-resources-and-software-titles"></a>6,4: przechowywanie spisu zatwierdzonych zasobów platformy Azure i tytułów oprogramowania

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych i platformy Azure jako całości.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="65-monitor-for-unapproved-azure-resources"></a>6,5: Monitoruj niezatwierdzone zasoby platformy Azure

**Wskazówki**: Użyj Azure Policy, aby wprowadzić ograniczenia dotyczące typu zasobów, które można utworzyć w subskrypcjach klientów, przy użyciu następujących wbudowanych definicji zasad:

Niedozwolone typy zasobów

Dozwolone typy zasobów

Ponadto za pomocą usługi Azure Resource Graph można wykonywać zapytania/odnajdywać zasoby w ramach subskrypcji.

Jak skonfigurować Azure Policy i zarządzać nimi:

https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage

Jak tworzyć zapytania za pomocą usługi Azure Graph:

https://docs.microsoft.com/azure/governance/resource-graph/first-query-portal

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="66-monitor-for-unapproved-software-applications-within-compute-resources"></a>6,6: Monitoruj niezatwierdzone aplikacje oprogramowania w ramach zasobów obliczeniowych

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="67-remove-unapproved-azure-resources-and-software-applications"></a>6,7: Usuń niezatwierdzone zasoby platformy Azure i aplikacje oprogramowania

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych i platformy Azure jako całości.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="68-use-only-approved-applications"></a>6,8: Używaj tylko zatwierdzonych aplikacji

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="69-use-only-approved-azure-services"></a>6,9: Używaj tylko zatwierdzonych usług platformy Azure

**Wskazówki**: Użyj Azure Policy, aby wprowadzić ograniczenia dotyczące typu zasobów, które można utworzyć w subskrypcjach klientów, przy użyciu następujących wbudowanych definicji zasad:

Niedozwolone typy zasobów

Dozwolone typy zasobów

Jak skonfigurować Azure Policy i zarządzać nimi:

https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage

Jak odmówić określonego typu zasobu Azure Policy:

https://docs.microsoft.com/azure/governance/policy/samples/not-allowed-resource-types

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="610-implement-approved-application-list"></a>6,10: Zaimplementuj listę zatwierdzonych aplikacji

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="611-limit-users-ability-to-interact-with-azure-resources-manager-via-scripts"></a>6,11: Ogranicz możliwość korzystania przez użytkowników z usługi Azure Resources za pośrednictwem skryptów

**Wskazówki**: Skonfiguruj dostęp warunkowy platformy Azure, aby ograniczyć możliwość współpracy użytkowników z Azure Resource Manager (ARM) przez skonfigurowanie "blokowania dostępu" dla aplikacji "Microsoft Azure Management".

Jak skonfigurować dostęp warunkowy w celu blokowania dostępu do ARM:

https://docs.microsoft.com/azure/role-based-access-control/conditional-access-azure-management

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="612-limit-users-ability-to-execute-scripts-within-compute-resources"></a>6,12: Ogranicz możliwość wykonywania skryptów w zasobach obliczeniowych przez użytkowników

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="613-physically-or-logically-segregate-high-risk-applications"></a>6,13: fizyczne lub logiczne rozdzielenie aplikacji wysokiego ryzyka

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone dla aplikacji sieci Web działających na Azure App Service lub zasobach obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

## <a name="secure-configuration"></a>Bezpieczna konfiguracja

*Aby uzyskać więcej informacji, zobacz [Kontrola zabezpieczeń: bezpieczna konfiguracja](../security/benchmarks/security-control-secure-configuration.md).*

### <a name="71-establish-secure-configurations-for-all-azure-resources"></a>7,1: Ustanów bezpieczne konfiguracje dla wszystkich zasobów platformy Azure

**Wskazówki**: Definiowanie i implementowanie standardowych konfiguracji zabezpieczeń dla usługi Azure cache dla wystąpień Redis z Azure Policy. Użyj aliasów Azure Policy w przestrzeni nazw "Microsoft. cache", aby utworzyć zasady niestandardowe do inspekcji lub wymuszania konfiguracji pamięci podręcznej platformy Azure dla wystąpień Redis. Możesz również używać wbudowanych definicji zasad związanych z pamięcią podręczną platformy Azure dla wystąpień Redis, takich jak:

Należy włączyć tylko bezpieczne połączenia z Redis Cache

Jak wyświetlić dostępne aliasy Azure Policy: https://docs.microsoft.com/powershell/module/az.resources/get-azpolicyalias?view=azps-3.3.0

Jak skonfigurować Azure Policy i zarządzać nimi: https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="72-establish-secure-operating-system-configurations"></a>7,2: Ustanów bezpieczne konfiguracje systemów operacyjnych

**Wskazówki**: nie dotyczy; te wytyczne są przeznaczone dla zasobów obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="73-maintain-secure-azure-resource-configurations"></a>7,3: obsługa bezpiecznych konfiguracji zasobów platformy Azure

**Wskazówki**: Użyj Azure Policy [Odmów] i [Wdróż, jeśli nie istnieje], aby wymusić bezpieczne ustawienia dla zasobów platformy Azure.

Jak skonfigurować Azure Policy i zarządzać nimi: https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage

Opis efektów Azure Policy: https://docs.microsoft.com/azure/governance/policy/concepts/effects

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="74-maintain-secure-operating-system-configurations"></a>7,4: Zachowaj konfiguracje bezpiecznego systemu operacyjnego

**Wskazówki**: nie dotyczy; te wytyczne są przeznaczone dla zasobów obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="75-securely-store-configuration-of-azure-resources"></a>7,5: bezpiecznie przechowuj konfigurację zasobów platformy Azure

**Wskazówki**: Jeśli używasz niestandardowych definicji Azure Policy lub szablonów Azure Resource Manager dla pamięci podręcznej platformy Azure dla wystąpień Redis i powiązanych zasobów, użyj Azure Repos, aby bezpiecznie przechowywać kod i zarządzać nim.

Jak przechowywać kod w usłudze Azure DevOps: https://docs.microsoft.com/azure/devops/repos/git/gitworkflow?view=azure-devops

Dokumentacja Azure Repos: https://docs.microsoft.com/azure/devops/repos/index?view=azure-devops

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="76-securely-store-custom-operating-system-images"></a>7,6: bezpieczne przechowywanie niestandardowych obrazów systemu operacyjnego

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="77-deploy-system-configuration-management-tools"></a>7,7: Wdrażanie narzędzi do zarządzania konfiguracją systemu

**Wskazówki**: Użyj aliasów Azure Policy w przestrzeni nazw "Microsoft. cache", aby utworzyć zasady niestandardowe na potrzeby alertów, inspekcji i wymuszania konfiguracji systemu. Dodatkowo opracowuj proces i potok na potrzeby zarządzania wyjątkami zasad.

Jak skonfigurować Azure Policy i zarządzać nimi: https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="78-deploy-system-configuration-management-tools-for-operating-systems"></a>7,8: Wdrażanie narzędzi do zarządzania konfiguracją systemu dla systemów operacyjnych

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="79-implement-automated-configuration-monitoring-for-azure-services"></a>7,9: Zaimplementuj automatyczne monitorowanie konfiguracji dla usług platformy Azure

**Wskazówki**: Użyj aliasów Azure Policy w przestrzeni nazw "Microsoft. cache", aby utworzyć zasady niestandardowe na potrzeby alertów, inspekcji i wymuszania konfiguracji systemu. Użyj Azure Policy [Audit], [Odmów] i [Wdróż, jeśli nie istnieje], aby automatycznie wymusić konfiguracje dla swojej pamięci podręcznej platformy Azure dla wystąpień Redis i powiązanych zasobów.

Jak skonfigurować Azure Policy i zarządzać nimi: https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="710-implement-automated-configuration-monitoring-for-operating-systems"></a>7,10: Zaimplementuj automatyczne monitorowanie konfiguracji dla systemów operacyjnych

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="711-manage-azure-secrets-securely"></a>7,11: bezpieczne zarządzanie wpisami tajnymi platformy Azure

**Wskazówki**: w przypadku maszyn wirtualnych platformy Azure lub aplikacji sieci Web działających na Azure App Service używanym do uzyskiwania dostępu do pamięci podręcznej platformy Azure dla wystąpień Redis należy używać tożsamość usługi zarządzanej w połączeniu z Azure Key Vault, aby uprościć i zabezpieczyć pamięć podręczną systemu Azure na potrzeby zarządzania tajnymi Redis. Upewnij się, że Key Vault usuwanie trwałe jest włączone.

Jak przeprowadzić integrację z tożsamościami zarządzanymi przez platformę Azure:

https://docs.microsoft.com/azure/azure-app-configuration/howto-integrate-azure-managed-service-identity

Jak utworzyć Key Vault:

https://docs.microsoft.com/azure/key-vault/general/quick-create-portal

Jak przeprowadzić uwierzytelnianie w Key Vault:

https://docs.microsoft.com/azure/key-vault/general/authentication

Jak przypisać zasady dostępu Key Vault:

https://docs.microsoft.com/azure/key-vault/general/assign-access-policy-portal

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

### <a name="712-manage-identities-securely-and-automatically"></a>7,12: bezpieczne i automatyczne zarządzanie tożsamościami

**Wskazówki**: w przypadku maszyn wirtualnych platformy Azure lub aplikacji sieci Web działających na Azure App Service używanym do uzyskiwania dostępu do pamięci podręcznej platformy Azure dla wystąpień Redis należy używać tożsamość usługi zarządzanej w połączeniu z Azure Key Vault, aby uprościć i zabezpieczyć pamięć podręczną systemu Azure na potrzeby zarządzania tajnymi Redis. Upewnij się, że Key Vault usuwanie trwałe jest włączone.

Użyj tożsamości zarządzanych, aby zapewnić usługom platformy Azure automatyczną tożsamość zarządzaną w Azure Active Directory. Tożsamości zarządzane umożliwiają uwierzytelnianie w dowolnej usłudze, która obsługuje uwierzytelnianie w usłudze AAD, w tym Azure Key Vault, bez żadnych poświadczeń w kodzie.

Jak skonfigurować tożsamości zarządzane:

https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/qs-configure-portal-windows-vm

Jak przeprowadzić integrację z tożsamościami zarządzanymi przez platformę Azure:

https://docs.microsoft.com/azure/azure-app-configuration/howto-integrate-azure-managed-service-identity

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

### <a name="713-eliminate-unintended-credential-exposure"></a>7,13: eliminowanie nieprzewidzianego narażenia na poświadczenia

**Wskazówki**: Implementuj skaner poświadczeń, aby identyfikować poświadczenia w kodzie. Skaner poświadczeń ułatwia również przenoszenie odnalezionych poświadczeń do bezpieczniejszych lokalizacji, takich jak usługa Azure Key Vault.

Jak skonfigurować skaner poświadczeń: https://secdevtools.azurewebsites.net/helpcredscan.html

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

## <a name="malware-defense"></a>Ochrona przed złośliwym oprogramowaniem

*Aby uzyskać więcej informacji, zobacz [Kontrola zabezpieczeń: Obrona złośliwego oprogramowania](../security/benchmarks/security-control-malware-defense.md).*

### <a name="81-use-centrally-managed-anti-malware-software"></a>8,1: Użyj centralnie zarządzanego oprogramowania chroniącego przed złośliwym oprogramowaniem

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych.

Oprogramowanie chroniące przed złośliwym oprogramowaniem firmy Microsoft jest włączone na podstawowym hoście, który obsługuje usługi platformy Azure (na przykład Azure App Service), ale nie jest uruchamiane w treści klienta.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

### <a name="82-pre-scan-files-to-be-uploaded-to-non-compute-azure-resources"></a>8,2: przeskanuj pliki przed przekazaniem do zasobów platformy Azure, które nie są obliczeniowe

**Wskazówki**: oprogramowanie chroniące przed złośliwym oprogramowaniem firmy Microsoft jest włączone na podstawowym hoście obsługującym usługi platformy Azure (na przykład Azure cache for Redis), ale nie jest uruchamiane na treści klienta.

Przed przeskanowaniem zawartość przekazywana do zasobów platformy Azure, które nie są obliczeniowe, takich jak App Service, Data Lake Storage, Blob Storage, Azure Database for PostgreSQL itp. Firma Microsoft nie może uzyskać dostępu do danych w tych wystąpieniach.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="83-ensure-anti-malware-software-and-signatures-are-updated"></a>8,3: Upewnij się, że oprogramowanie chroniące przed złośliwym oprogramowaniem i podpisy zostały zaktualizowane

**Wskazówki**: nie dotyczy; to zalecenie jest przeznaczone do zasobów obliczeniowych.

Oprogramowanie chroniące przed złośliwym oprogramowaniem firmy Microsoft jest włączone na podstawowym hoście, który obsługuje usługi platformy Azure (na przykład usługa Azure cache for Redis), ale nie jest uruchamiane na treści klienta.

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: nie dotyczy

## <a name="data-recovery"></a>Odzyskiwanie danych

*Aby uzyskać więcej informacji, zobacz [Kontrola zabezpieczeń: odzyskiwanie danych](../security/benchmarks/security-control-data-recovery.md).*

### <a name="91-ensure-regular-automated-back-ups"></a>9,1: Zapewnij regularne zautomatyzowane przywracanie awaryjne

**Wskazówki**: Włączanie trwałości Redis. Trwałość Redis umożliwia utrwalanie danych przechowywanych w Redis. Można również tworzyć migawki i tworzyć kopie zapasowe danych, które można ładować w przypadku awarii sprzętu. Jest to ogromna korzyść w porównaniu z warstwą podstawową lub standardową, w której wszystkie dane są przechowywane w pamięci i może istnieć potencjalna utrata danych w przypadku awarii, w której węzły pamięci podręcznej nie działają.

Możesz również użyć usługi Azure cache do eksportowania Redis. Eksport pozwala wyeksportować dane przechowywane w pamięci podręcznej platformy Azure dla Redis do Redis zgodnych plików RDB. Ta funkcja służy do przenoszenia danych z jednej pamięci podręcznej platformy Azure dla wystąpienia Redis do innego lub do innego serwera Redis. Podczas eksportowania plik tymczasowy jest tworzony na maszynie wirtualnej, która hostuje wystąpienie serwera usługi Azure cache for Redis, i plik zostanie przekazany do wskazanego konta magazynu. Po zakończeniu operacji eksportowania ze stanem powodzenie lub niepowodzenie plik tymczasowy zostanie usunięty.

Jak włączyć trwałość Redis:

https://docs.microsoft.com/azure/azure-cache-for-redis/cache-how-to-premium-persistence

Jak używać usługi Azure cache do eksportowania Redis:

https://docs.microsoft.com/azure/azure-cache-for-redis/cache-how-to-import-export-data

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: Klient

### <a name="92-perform-complete-system-backups-and-backup-any-customer-managed-keys"></a>9,2: wykonaj kompletne kopie zapasowe systemu i Utwórz kopię zapasową wszystkich kluczy zarządzanych przez klienta

**Wskazówki**: Włączanie trwałości Redis. Trwałość Redis umożliwia utrwalanie danych przechowywanych w Redis. Można również tworzyć migawki i tworzyć kopie zapasowe danych, które można ładować w przypadku awarii sprzętu. Jest to ogromna korzyść w porównaniu z warstwą podstawową lub standardową, w której wszystkie dane są przechowywane w pamięci i może istnieć potencjalna utrata danych w przypadku awarii, w której węzły pamięci podręcznej nie działają.

Możesz również użyć usługi Azure cache do eksportowania Redis. Eksport pozwala wyeksportować dane przechowywane w pamięci podręcznej platformy Azure dla Redis do Redis zgodnych plików RDB. Ta funkcja służy do przenoszenia danych z jednej pamięci podręcznej platformy Azure dla wystąpienia Redis do innego lub do innego serwera Redis. Podczas eksportowania plik tymczasowy jest tworzony na maszynie wirtualnej, która hostuje wystąpienie serwera usługi Azure cache for Redis, i plik zostanie przekazany do wskazanego konta magazynu. Po zakończeniu operacji eksportowania ze stanem powodzenie lub niepowodzenie plik tymczasowy zostanie usunięty.

W przypadku używania Azure Key Vault do przechowywania poświadczeń dla wystąpień usługi Azure cache for Redis należy zapewnić regularne automatyczne tworzenie kopii zapasowych kluczy.

Jak włączyć trwałość Redis:

https://docs.microsoft.com/azure/azure-cache-for-redis/cache-how-to-premium-persistence

Jak używać usługi Azure cache do eksportowania Redis:

https://docs.microsoft.com/azure/azure-cache-for-redis/cache-how-to-import-export-data

Jak utworzyć kopię zapasową kluczy Key Vault:

https://docs.microsoft.com/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey

**Monitorowanie usługi Azure Security Center**: Obecnie niedostępne

**Odpowiedzialność**: Klient

### <a name="93-validate-all-backups-including-customer-managed-keys"></a>9,3: Weryfikuj wszystkie kopie zapasowe, w tym klucze zarządzane przez klienta

**Wskazówki**: Użyj usługi Azure cache do importowania Redis. Import może służyć do przenoszenia plików RDB zgodnych z Redis z dowolnego serwera Redis działającego w dowolnej chmurze lub środowisku, w tym Redis działających w systemie Linux, Windows lub dowolnym dostawcy chmury, takim jak Amazon Web Services i inne. Importowanie danych to prosty sposób tworzenia pamięci podręcznej z wstępnie wypełnionymi danymi. Podczas procesu importowania usługa Azure cache for Redis ładuje pliki RDB z usługi Azure Storage do pamięci, a następnie wstawia klucze do pamięci podręcznej.

Okresowe testowanie przywracania danych tajnych Azure Key Vault.

Jak używać usługi Azure cache do importowania Redis:

https://docs.microsoft.com/azure/azure-cache-for-redis/cache-how-to-import-export-data

Jak przywrócić Key Vault wpisy tajne:

https://docs.microsoft.com/powershell/module/azurerm.keyvault/restore-azurekeyvaultsecret?view=azurermps-6.13.0

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="94-ensure-protection-of-backups-and-customer-managed-keys"></a>9,4: zapewnianie ochrony kopii zapasowych i kluczy zarządzanych przez klienta

**Wskazówki**: pamięć podręczna Azure dla Redis kopii zapasowych z Redis Export i Redis są przechowywane w ramach wybranego konta usługi Azure Storage. Dane w usłudze Azure Storage są szyfrowane i odszyfrowywane w sposób niewidoczny dla użytkownika przy użyciu 256-bitowego szyfrowania AES, jednego z najsilniejszych szyfrów blokowych i jest zgodny ze standardem FIPS 140-2. Nie można wyłączyć szyfrowania usługi Azure Storage. Możesz polegać na kluczach zarządzanych przez firmę Microsoft na potrzeby szyfrowania konta magazynu lub można zarządzać szyfrowaniem przy użyciu własnych kluczy.

Informacje o szyfrowaniu dla kont usługi Azure Storage: https://docs.microsoft.com/azure/storage/common/storage-service-encryption

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Microsoft

## <a name="incident-response"></a>Reagowanie na zdarzenia

*Aby uzyskać więcej informacji, zobacz [Kontrola zabezpieczeń: odpowiedź na zdarzenia](../security/benchmarks/security-control-incident-response.md).*

### <a name="101-create-an-incident-response-guide"></a>10,1: Tworzenie przewodnika odpowiedzi na zdarzenia

**Wskazówka**: Utwórz przewodnik odpowiedzi na zdarzenia dla swojej organizacji. Upewnij się, że istnieją zarejestrowane plany reakcji na zdarzenia, które definiują wszystkie role pracowników, a także etapy obsługi zdarzeń/zarządzania od wykrywania do oceny po zdarzeniu.

Jak skonfigurować automatyzację przepływu pracy w ramach Azure Security Center:

https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide

Wskazówki dotyczące tworzenia własnego procesu reagowania na zdarzenia zabezpieczeń:

https://msrc-blog.microsoft.com/2019/07/01/inside-the-msrc-building-your-own-security-incident-response-process/

Anatomia w centrum Microsoft Security Response:

https://msrc-blog.microsoft.com/2019/07/01/inside-the-msrc-building-your-own-security-incident-response-process/

Klient może także skorzystać z przewodnika obsługi zdarzeń związanych z bezpieczeństwem programu NIST, aby pomóc w tworzeniu własnego planu reagowania na zdarzenia:

https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="102-create-an-incident-scoring-and-prioritization-procedure"></a>10,2: Tworzenie oceny incydentu i procedury priorytetyzacji

**Wskazówki**: Security Center przypisuje ważność do każdego alertu, aby pomóc w ustaleniu, które alerty należy najpierw zbadać. Ważność jest oparta na tym, jak dobrze Security Center znajduje się w wyszukiwaniu lub analitycznym używanym do wystawiania alertu, a także poziom pewności, że istniało złośliwy wpływ na działanie, które prowadziło do alertu.

Dodatkowo jasno Oznacz subskrypcje (na przykład produkcyjny, nieprodukcyjny) i Utwórz system nazewnictwa, aby jasno identyfikować i klasyfikować zasoby platformy Azure.

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

### <a name="103-test-security-response-procedures"></a>10,3: procedury odpowiedzi na zabezpieczenia testowe

**Wskazówki**: przeprowadzanie ćwiczeń w celu przetestowania możliwości reagowania na zdarzenia systemu w regularnych erze. Zidentyfikuj słabe punkty i przerwy oraz popraw plan zgodnie z wymaganiami.

Zapoznaj się z publikacją NIST: Przewodnik dotyczący testowania, uczenia i ćwiczeń programów dla planów i możliwości IT:

https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-84.pdf

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="104-provide-security-incident-contact-details-and-configure-alert-notifications-for-security-incidents"></a>10,4: Podaj szczegóły kontaktu dotyczącego zabezpieczeń i Skonfiguruj powiadomienia dotyczące alertów dotyczących zdarzeń związanych z zabezpieczeniami

**Wskazówki**: informacje kontaktowe dotyczące zdarzenia zabezpieczeń będą używane przez firmę Microsoft do skontaktowania się z Tobą, jeśli firma Microsoft Security Response Center (MSRC) wykryje, że dostęp do danych klienta został uzyskany przez nielegalną lub nieautoryzowaną osobę.  Przejrzyj zdarzenia po fakcie, aby upewnić się, że problemy zostały rozwiązane.

Jak ustawić Azure Security Center kontaktu zabezpieczeń:

https://docs.microsoft.com/azure/security-center/security-center-provide-security-contact-details

**Monitorowanie usługi Azure Security Center**: Yes

**Odpowiedzialność**: Klient

### <a name="105-incorporate-security-alerts-into-your-incident-response-system"></a>10,5: Uwzględnij alerty zabezpieczeń w systemie odpowiedzi na zdarzenia

**Wskazówki**: eksportowanie alertów i zaleceń dotyczących Azure Security Center przy użyciu funkcji eksportu ciągłego. Eksport ciągły umożliwia wyeksportowanie alertów i zaleceń ręcznie lub w stały sposób ciągły. Możesz użyć łącznika danych Azure Security Center, aby przesłać strumieniowo wskaźnik do alertów.

Jak skonfigurować eksport ciągły:

https://docs.microsoft.com/azure/security-center/continuous-export

Jak przesłać strumieniowo alerty do usługi Azure wskaźnikowej:

https://docs.microsoft.com/azure/sentinel/connect-azure-security-center

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

### <a name="106-automate-the-response-to-security-alerts"></a>10,6: Automatyzowanie odpowiedzi na alerty zabezpieczeń

**Wskazówki**: Użyj funkcji automatyzacji przepływu pracy w programie Azure Security Center, aby automatycznie wyzwalać odpowiedzi za pośrednictwem "Logic Apps" na temat alertów zabezpieczeń i zaleceń.

Jak skonfigurować automatyzację przepływu pracy i Logic Apps:

https://docs.microsoft.com/azure/security-center/workflow-automation

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Klient

## <a name="penetration-tests-and-red-team-exercises"></a>Testy penetracyjne i ćwiczenia typu „red team”

*Aby uzyskać więcej informacji, zobacz [Kontrola zabezpieczeń: testy penetracji i czerwone ćwiczenia zespołu](../security/benchmarks/security-control-penetration-tests-red-team-exercises.md).*

### <a name="111-conduct-regular-penetration-testing-of-your-azure-resources-and-ensure-remediation-of-all-critical-security-findings-within-60-days"></a>11,1: Przeprowadź regularne testowanie penetracji zasobów platformy Azure i zadbaj o skorygowanie wszystkich krytycznych ustaleń dotyczących zabezpieczeń w ciągu 60 dni

**Wskazówki**: Postępuj zgodnie z zasadami firmy Microsoft dotyczącymi zaangażowania, aby upewnić się, że testy penetracji nie naruszają zasad firmy Microsoft:

https://www.microsoft.com/msrc/pentest-rules-of-engagement?rtc=1

Aby uzyskać więcej informacji na temat strategii i sposobu działania tworzenia zespołu Red-and-testowego na żywo w oparciu o infrastrukturę, usługi i aplikacje chmurowe zarządzane przez firmę Microsoft, należy tutaj: 

https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e

**Monitorowanie usługi Azure Security Center**: Nie dotyczy

**Odpowiedzialność**: Współużytkowane

## <a name="next-steps"></a>Następne kroki

- Zobacz [test porównawczy zabezpieczeń platformy Azure](../security/benchmarks/overview.md)
- Dowiedz się więcej o [punktach odniesienia zabezpieczeń platformy Azure](../security/benchmarks/security-baselines-overview.md)