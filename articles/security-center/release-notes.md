---
title: Informacje o wersji Azure Security Center
description: Opis nowości i zmian w programie Azure Security Center.
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.service: security-center
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/07/2021
ms.author: memildin
ms.openlocfilehash: 86da6c0a3393dd3f47143355597cd9ccdec9928d
ms.sourcegitcommit: fc23b4c625f0b26d14a5a6433e8b7b6fb42d868b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/17/2021
ms.locfileid: "98539943"
---
# <a name="whats-new-in-azure-security-center"></a>Co nowego w Azure Security Center?

Security Center jest aktywnym programowaniem i od bieżąco otrzymuje ulepszenia. Ta strona zawiera informacje o nowych funkcjach, poprawkach błędów i przestarzałych funkcjach, aby zachować aktualność.

Ta strona jest często aktualizowana, więc często należy ją ponownie odwiedzać. 

Aby dowiedzieć się o *planowanych* zmianach, które wkrótce zostaną udostępnione Security Center, zobacz [Ważne zmiany nadchodzące Azure Security Center](upcoming-changes.md). 

> [!TIP]
> Jeśli szukasz elementów starszych niż sześć miesięcy, znajdziesz je w [archiwum, co nowego w programie Azure Security Center](release-notes-archive.md).


## <a name="january-2021"></a>Styczeń 2021 r.

### <a name="vulnerability-assessment-for-on-premise-and-multi-cloud-machines-is-generally-available"></a>Ocena luk w zabezpieczeniach dla maszyn lokalnych i wielochmurowych jest ogólnie dostępna

W październiku ogłoszono w wersji zapoznawczej skanowanie serwerów z obsługą usługi Azure ARC przy użyciu [usługi Azure Defender na potrzeby](defender-for-servers-introduction.md)zintegrowanego skanera oceny luk w zabezpieczeniach serwerów (obsługiwanego przez Qualys).

Jest ona teraz ogólnie dostępna. 

Gdy usługa Azure Arc została włączona na maszynach spoza platformy Azure, Security Center będzie oferować ręczne wdrażanie skanera zintegrowanej luki w zabezpieczeniach.

Dzięki tej aktualizacji można wyłączyć **usługę Azure Defender dla serwerów** , aby skonsolidować program do zarządzania lukami w zabezpieczeniach dla wszystkich zasobów platformy Azure i spoza platformy Azure.

Główne możliwości:

- Monitorowanie stanu aprowizacji skanera (ocena luk w zabezpieczeniach) na maszynach usługi Azure Arc
- Inicjowanie obsługi zintegrowanego agenta VA do niechronionych maszyn z systemem Windows i Linux na platformie Azure (ręcznie i w skali)
- Otrzymywanie i analizowanie wykrytych luk w zabezpieczeniach wdrożonych agentów (ręcznie i w skali)
- Ujednolicone środowisko dla maszyn wirtualnych platformy Azure i usługi Azure Arc

[Dowiedz się więcej o wdrażaniu zintegrowanego skanera luk w zabezpieczeniach na maszynach hybrydowych](deploy-vulnerability-assessment-vm.md#deploy-the-integrated-scanner-to-your-azure-and-hybrid-machines).

[Dowiedz się więcej o serwerach z obsługą usługi Azure Arc](../azure-arc/servers/index.yml).


## <a name="december-2020"></a>Grudzień 2020 r.

Aktualizacje w grudniu obejmują:

- [Usługa Azure Defender dla serwerów SQL na maszynach jest ogólnie dostępna](#azure-defender-for-sql-servers-on-machines-is-generally-available)
- [Usługa Azure Defender for SQL dla dedykowanej puli SQL usługi Azure Synapse Analytics jest ogólnie dostępna](#azure-defender-for-sql-support-for-azure-synapse-analytics-dedicated-sql-pool-is-generally-available)
- [Administratorzy globalni mogą teraz udzielić sobie uprawnień na poziomie dzierżawy](#global-administrators-can-now-grant-themselves-tenant-level-permissions)
- [Dwa nowe plany usługi Azure Defender: usługa Azure Defender dla systemu DNS i usługi Azure Defender dla Menedżer zasobów (w wersji zapoznawczej)](#two-new-azure-defender-plans-azure-defender-for-dns-and-azure-defender-for-resource-manager-in-preview)
- [Nowa strona alertów zabezpieczeń w Azure Portal (wersja zapoznawcza)](#new-security-alerts-page-in-the-azure-portal-preview)
- [Security Center środowisko w Azure SQL Database & wystąpieniu zarządzanym SQL](#revitalized-security-center-experience-in-azure-sql-database--sql-managed-instance)
- [Zaktualizowano narzędzia i filtry spisu zasobów](#asset-inventory-tools-and-filters-updated)
- [Zalecenie dotyczące aplikacji sieci Web żądających certyfikatów SSL, które nie są już częścią bezpiecznego wyniku](#recommendation-about-web-apps-requesting-ssl-certificates-no-longer-part-of-secure-score)
- [Strona zalecenia zawiera nowe filtry dotyczące środowiska, ważności i dostępnych odpowiedzi](#recommendations-page-has-new-filters-for-environment-severity-and-available-responses)
- [Eksport ciągły pobiera nowe typy danych i udoskonalone zasady deployifnotexist](#continuous-export-gets-new-data-types-and-improved-deployifnotexist-policies)


### <a name="azure-defender-for-sql-servers-on-machines-is-generally-available"></a>Usługa Azure Defender dla serwerów SQL na maszynach jest ogólnie dostępna

Azure Security Center oferuje dwa plany usługi Azure Defender dla serwerów SQL:

- **Usługa Azure Defender dla serwerów usługi Azure SQL Database** — obrona natywnych serwerów SQL platformy Azure 
- **Usługa Azure Defender dla serwerów SQL na maszynach** — rozszerza te same zabezpieczenia na serwery SQL w środowiskach hybrydowych, wielochmurowych i lokalnych

Za pomocą tego anonsu **usługa Azure Defender dla programu SQL zapewnia** teraz ochronę baz danych i ich danych, wszędzie tam, gdzie się znajdują.

Usługa Azure Defender dla programu SQL zawiera funkcje oceny luk w zabezpieczeniach. Narzędzie do oceny luk w zabezpieczeniach obejmuje następujące funkcje zaawansowane:

- **Konfiguracja linii bazowej** (New!), aby inteligentnie udoskonalać wyniki skanowania luk w zabezpieczeniach, które mogą reprezentować rzeczywiste problemy z zabezpieczeniami. Po ustaleniu stanu zabezpieczeń linii bazowej narzędzie do oceny luk w zabezpieczeniach zgłasza odchylenia od tego stanu linii bazowej. Wyniki, które pasują do linii bazowej, są uznawane za przekazanie kolejnych skanów. Dzięki temu możesz i analitykom skupić uwagę na miejscu.
- **Szczegółowe informacje na temat testów porównawczych** ułatwiające *zrozumienie* odnalezionych wyników i przyczyn związanych z zasobami.
- **Skrypty korygowania** pomagające ograniczyć określone zagrożenia.

Dowiedz się więcej o [usłudze Azure Defender dla języka SQL](defender-for-sql-introduction.md).


### <a name="azure-defender-for-sql-support-for-azure-synapse-analytics-dedicated-sql-pool-is-generally-available"></a>Usługa Azure Defender for SQL dla dedykowanej puli SQL usługi Azure Synapse Analytics jest ogólnie dostępna

Azure Synapse Analytics (dawniej SQL DW) to Usługa analityczna, która łączy magazyn danych w przedsiębiorstwie i analizy danych Big Data. Dedykowane pule SQL to funkcje magazynowania danych przedsiębiorstwa w usłudze Azure Synapse. Dowiedz się więcej w temacie [co to jest usługa Azure Synapse Analytics (wcześniej SQL DW)?](../synapse-analytics/sql-data-warehouse/sql-data-warehouse-overview-what-is.md).

Usługa Azure Defender dla programu SQL chroni dedykowane pule SQL przy użyciu:

- **Zaawansowana ochrona przed zagrożeniami** w celu wykrywania zagrożeń i ataków 
- **Możliwości oceny luk** w zabezpieczeniach w celu identyfikowania i rozwiązywania problemów z konfiguracją zabezpieczeń

Usługa Azure Defender for SQL dla usług Azure Synapse Analytics jest automatycznie dodawana do pakietu baz danych SQL Azure w Azure Security Center. Nowa karta "Azure Defender for SQL" znajduje się na stronie obszaru roboczego Synapse w Azure Portal.

Dowiedz się więcej o [usłudze Azure Defender dla języka SQL](defender-for-sql-introduction.md).


### <a name="global-administrators-can-now-grant-themselves-tenant-level-permissions"></a>Administratorzy globalni mogą teraz udzielić sobie uprawnień na poziomie dzierżawy

Użytkownik z rolą Azure Active Directory **administrator globalny** może korzystać z obowiązków obejmujących dzierżawę, ale nie ma uprawnień platformy Azure do wyświetlania informacji o całej organizacji w Azure Security Center. 

Aby przypisać własne uprawnienia na poziomie dzierżawy, postępuj zgodnie z instrukcjami podanymi w temacie [Przyznawanie uprawnień dla całej dzierżawy](security-center-management-groups.md#grant-tenant-wide-permissions-to-yourself).


### <a name="two-new-azure-defender-plans-azure-defender-for-dns-and-azure-defender-for-resource-manager-in-preview"></a>Dwa nowe plany usługi Azure Defender: usługa Azure Defender dla systemu DNS i usługi Azure Defender dla Menedżer zasobów (w wersji zapoznawczej)

Dodaliśmy dwie nowe funkcje natywnej ochrony przed zagrożeniami w chmurze dla środowiska platformy Azure.

Te nowe zabezpieczenia znacznie rozszerzają odporność na ataki od aktorów zagrożeń i znacząco zwiększają liczbę zasobów platformy Azure chronionych przez usługę Azure Defender.

- **Usługa Azure Defender dla Menedżer zasobów** — automatycznie monitoruje wszystkie operacje zarządzania zasobami wykonywane w organizacji. Aby uzyskać więcej informacji, zobacz:
    - [Wprowadzenie do usługi Azure Defender dla Menedżer zasobów](defender-for-resource-manager-introduction.md)
    - [Reagowanie na alerty usługi Azure Defender dla usługi Resource Manager](defender-for-resource-manager-usage.md)
    - [Lista alertów dostarczonych przez usługę Azure Defender dla Menedżer zasobów](alerts-reference.md#alerts-resourcemanager)

- **Usługa Azure Defender dla systemu DNS** — stale monitoruje wszystkie zapytania DNS z zasobów platformy Azure. Aby uzyskać więcej informacji, zobacz:
    - [Wprowadzenie do usługi Azure Defender dla systemu DNS](defender-for-dns-introduction.md)
    - [Reagowanie na alerty usługi Azure Defender dla usługi DNS](defender-for-dns-usage.md)
    - [Lista alertów udostępnianych przez usługę Azure Defender dla systemu DNS](alerts-reference.md#alerts-dns)


### <a name="new-security-alerts-page-in-the-azure-portal-preview"></a>Nowa strona alertów zabezpieczeń w Azure Portal (wersja zapoznawcza)

Strona alertów zabezpieczeń Azure Security Center została przeprojektowana w celu zapewnienia:

- **Udoskonalone środowisko Klasyfikacja dla alertów** — pomaga zmniejszyć zmęczenie alertów i skupić się na najważniejszych zagrożeniach, a lista zawiera dostosowywalne filtry i opcje grupowania
- **Więcej informacji na liście alertów** — takich jak MITRE ATT&ACK taktykę
- **Przycisk umożliwiający tworzenie przykładowych alertów** — aby oszacować możliwości usługi Azure Defender i przetestować konfigurację alertów (na potrzeby integracji Siem, powiadomień e-mail i automatyzacji przepływu pracy), możesz utworzyć przykładowe alerty ze wszystkich planów usługi Azure Defender
- **Wyrównywanie za pomocą doświadczenia ze zdarzeniami platformy Azure** — w przypadku klientów, którzy korzystają z obu tych produktów, przełączenie między nimi jest teraz bardziej prostym doświadczeniem i można łatwo poznać jeden z nich.
- **Lepsza wydajność** dla list z dużymi alertami
- **Nawigacja** przy użyciu klawiatury przez listę alertów
- **Alerty z grafu zasobów platformy Azure** — możesz wysyłać zapytania dotyczące alertów na wykresie zasobów platformy Azure, interfejsu API przypominającego Kusto dla wszystkich zasobów. Jest to przydatne również w przypadku tworzenia własnych pulpitów nawigacyjnych alertów. [Dowiedz się więcej o usłudze Azure Resource Graph](../governance/resource-graph/index.yml).

Aby uzyskać dostęp do nowego środowiska, Użyj linku "Wypróbuj teraz" na transparencie w górnej części strony alertów zabezpieczeń.

:::image type="content" source="media/security-center-managing-and-responding-alerts/preview-alerts-experience-banner.png" alt-text="Transparent z linkiem do nowego środowiska obsługi alertów w wersji zapoznawczej":::

Aby utworzyć przykładowe alerty z nowego środowiska alertów, zobacz [generowanie przykładowych alertów usługi Azure Defender](security-center-alert-validation.md#generate-sample-azure-defender-alerts).


### <a name="revitalized-security-center-experience-in-azure-sql-database--sql-managed-instance"></a>Security Center środowisko w Azure SQL Database & wystąpieniu zarządzanym SQL 

Security Center środowisko w programie SQL zapewnia dostęp do następujących Security Center i usługi Azure Defender dla funkcji SQL:

- **Zalecenia dotyczące zabezpieczeń** — Security Center okresowo analizuje stan zabezpieczeń wszystkich połączonych zasobów platformy Azure w celu zidentyfikowania potencjalnych problemów z konfiguracją zabezpieczeń. Następnie zawiera zalecenia dotyczące sposobu korygowania tych luk w zabezpieczeniach i ulepszania stan zabezpieczeń organizacji.
- **Alerty zabezpieczeń** — usługa wykrywania, która stale monitoruje działania usługi Azure SQL pod kątem zagrożeń, takich jak iniekcja kodu SQL, ataki z wymuszeniem i nadużycie uprawnień. Ta usługa wyzwala szczegółowe i zorientowane na działania alerty zabezpieczeń w Security Center i oferuje opcje dla kontynuowania badań za pomocą platformy Azure — natywnego rozwiązania SIEM firmy Microsoft.
- **Ustalenia** — usługa oceny luk w zabezpieczeniach, która stale monitoruje konfiguracje SQL platformy Azure i pomaga skorygować luki w zabezpieczeniach. Przeglądy oceny zawierają omówienie stanów zabezpieczeń usługi Azure SQL wraz ze szczegółowymi ustaleniami w zakresie zabezpieczeń.     

:::image type="content" source="media/release-notes/azure-security-center-experience-in-sql.png" alt-text="Funkcje zabezpieczeń Azure Security Center dla programu SQL są dostępne w ramach usługi Azure SQL":::


### <a name="asset-inventory-tools-and-filters-updated"></a>Zaktualizowano narzędzia i filtry spisu zasobów

Strona spisu w Azure Security Center została odświeżona z następującymi zmianami:

- **Przewodniki i opinie** dodane do paska narzędzi. Spowoduje to otwarcie okienka z linkami do powiązanych informacji i narzędzi. 
- **Filtr subskrypcje** został dodany do domyślnych filtrów dostępnych dla Twoich zasobów.
- **Otwórz link zapytania** , aby otworzyć bieżące opcje filtru jako zapytanie wykresu zasobów platformy Azure (dawniej "widok w Eksploratorze grafu zasobów").
- **Opcje operatora** dla każdego filtru. Teraz można wybrać spośród dodatkowych operatorów logicznych innych niż "=". Na przykład możesz chcieć znaleźć wszystkie zasoby z aktywnymi zaleceniami, których tytuły zawierają ciąg "Szyfruj". 

    :::image type="content" source="media/release-notes/inventory-filter-operators.png" alt-text="Kontrolki dla opcji operatora w filtrach spisu zasobów":::

Dowiedz się więcej na temat spisu w temacie [Eksplorowanie zasobów i zarządzanie nimi za pomocą spisu](asset-inventory.md)zasobów.


### <a name="recommendation-about-web-apps-requesting-ssl-certificates-no-longer-part-of-secure-score"></a>Zalecenie dotyczące aplikacji sieci Web żądających certyfikatów SSL, które nie są już częścią bezpiecznego wyniku

Zalecenie "aplikacje sieci Web powinno zażądać certyfikatu SSL dla wszystkich żądań przychodzących" zostało przeniesione z kontroli zabezpieczeń **Zarządzanie dostępem i uprawnieniami** (wartość maksymalna wynosząca 4) do **implementacji najlepszych** rozwiązań w zakresie zabezpieczeń (które nie uwzględnia żadnych punktów). 

Zapewnienie, aby aplikacje sieci Web żądały certyfikatu, co sprawia, że są bezpieczniejsze. Jednak dla publicznych aplikacji sieci Web jest to nieistotne. Jeśli uzyskujesz dostęp do witryny za pośrednictwem protokołu HTTP, a nie HTTPS, nie otrzymasz żadnych certyfikatów klienta. Dlatego jeśli aplikacja wymaga certyfikatów klienta, nie należy zezwalać na żądania do aplikacji za pośrednictwem protokołu HTTP. Dowiedz się więcej w temacie [Konfigurowanie wzajemnego uwierzytelniania TLS dla Azure App Service](../app-service/app-service-web-configure-tls-mutual-auth.md).

W przypadku tej zmiany zalecenie jest teraz zalecanym najlepszym rozwiązaniem, które nie ma wpływu na ocenę. 

Dowiedz się, które zalecenia znajdują się w każdej kontroli zabezpieczeń w obszarze kontrola [zabezpieczeń i ich zalecenia](secure-score-security-controls.md#security-controls-and-their-recommendations).


### <a name="recommendations-page-has-new-filters-for-environment-severity-and-available-responses"></a>Strona zalecenia zawiera nowe filtry dotyczące środowiska, ważności i dostępnych odpowiedzi

Azure Security Center monitoruje wszystkie połączone zasoby i generuje zalecenia dotyczące zabezpieczeń. Skorzystaj z tych zaleceń, aby wzmocnić chmurę hybrydową stan i śledzić zgodność z zasadami i normami istotnymi dla Twojej organizacji, branży i kraju.

Ponieważ Security Center w dalszym ciągu rozszerza swój zakres i funkcje, lista zaleceń dotyczących zabezpieczeń rośnie co miesiąc. Na przykład zapoznaj [się z artykułem 29 zaleceń dotyczących wersji zapoznawczych, aby zwiększyć zakres testów zabezpieczeń platformy Azure](#29-preview-recommendations-added-to-increase-coverage-of-azure-security-benchmark).

Mając listę rozwijaną, należy mieć możliwość filtrowania do zaleceń o największym znaczeniu. W listopadzie dodaliśmy filtry do strony zalecenia (zobacz [Lista zaleceń zawiera teraz filtry](#recommendations-list-now-includes-filters)).

Filtry dodane w tym miesiącu zapewniają opcje, aby uściślić listę zaleceń zgodnie z:

- **Środowisko** — zapoznaj się z zaleceniami dotyczącymi zasobów AWS, GCP lub Azure (lub dowolnej kombinacji)
- **Ważność** — Wyświetl zalecenia zgodnie z klasyfikacją ważności ustawioną przez Security Center
- **Akcje odpowiedzi** — wyświetlanie zaleceń zgodnie z dostępnością Security Center opcje odpowiedzi: szybka naprawa, odmowa i wymuszanie

    > [!TIP]
    > Filtr akcje odpowiedzi zastępuje filtr **dostępne szybkie poprawki (tak/nie)** . 
    > 
    > Dowiedz się więcej na temat każdej z tych opcji odpowiedzi:
    > - [Szybkie rozwiązywanie problemów](security-center-remediate-recommendations.md#quick-fix-remediation)
    > - [Zapobieganie błędom konfiguracji za pomocą wymuszania/odmawiania — zalecenia](prevent-misconfigurations.md)

:::image type="content" source="./media/release-notes/added-recommendations-filters.png" alt-text="Zalecenia pogrupowane według kontroli zabezpieczeń" lightbox="./media/release-notes/added-recommendations-filters.png":::

### <a name="continuous-export-gets-new-data-types-and-improved-deployifnotexist-policies"></a>Eksport ciągły pobiera nowe typy danych i udoskonalone zasady deployifnotexist

Narzędzia eksportu ciągłego Azure Security Center umożliwiają eksportowanie zaleceń i alertów Security Center do użycia z innymi narzędziami do monitorowania w środowisku.

Eksport ciągły pozwala w pełni dostosować zawartość, która zostanie wyeksportowana, oraz miejsce, w której zostanie ono przeszukane. Aby uzyskać szczegółowe informacje, zobacz  [ciągły eksport danych Security Center](continuous-export.md).

Te narzędzia zostały ulepszone i rozszerzane w następujący sposób:

- **Ulepszone zaawansowane zasady deployifnotexistymi eksportu**. Zasady teraz:

    - **Sprawdź, czy konfiguracja jest włączona.** Jeśli tak nie jest, zasady będą widoczne jako niezgodne i tworzą zgodne zasoby. Dowiedz się więcej o dostarczonych szablonach Azure Policy na karcie "wdrażanie w skali przy użyciu Azure Policy" w temacie [Konfigurowanie eksportu ciągłego](continuous-export.md#set-up-a-continuous-export).

    - **Obsługa eksportowania wyników dotyczących zabezpieczeń.** Korzystając z szablonów Azure Policy, można skonfigurować eksport ciągły w taki sposób, aby zawierał wyniki. Jest to istotne w przypadku eksportowania zaleceń, które mają zalecenia "Sub", takie jak wyniki z skanerów oceny luk w zabezpieczeniach lub aktualizacje systemu dla zaleceń "nadrzędnej", należy zainstalować na swoich maszynach.
    
    - **Obsługa eksportowania zabezpieczonych danych oceny.**

- **Dodano dane oceny zgodności z przepisami (w wersji zapoznawczej).** Teraz możesz ciągle eksportować aktualizacje do oceny zgodności z przepisami, w tym dla dowolnych inicjatyw niestandardowych, do Log Analytics obszaru roboczego lub centrum zdarzeń. Ta funkcja jest niedostępna w chmurach narodowych/suwerennych.

    :::image type="content" source="media/release-notes/continuous-export-regulatory-compliance-option.png" alt-text="Opcje w celu uwzględnienia informacji o ocenie zgodności z przepisami w przypadku danych eksportu ciągłego.":::


## <a name="november-2020"></a>Listopad 2020 r.

Aktualizacje w listopadzie obejmują:

- [29 zaleceń dotyczących wersji zapoznawczej dodanych w celu zwiększenia zakresu testów zabezpieczeń platformy Azure](#29-preview-recommendations-added-to-increase-coverage-of-azure-security-benchmark)
- [NIST SP 800 171 R2 dodano do Security Center pulpitu nawigacyjnego zgodności z przepisami](#nist-sp-800-171-r2-added-to-security-centers-regulatory-compliance-dashboard)
- [Lista rekomendacji zawiera teraz filtry](#recommendations-list-now-includes-filters)
- [Ulepszone i rozszerzone środowisko aprowizacji](#auto-provisioning-experience-improved-and-expanded)
- [Ocena zabezpieczeń jest teraz dostępna w przypadku eksportu ciągłego (wersja zapoznawcza)](#secure-score-is-now-available-in-continuous-export-preview)
- [Zalecenie "aktualizacje systemu powinny być zainstalowane na Twoich komputerach" obejmuje teraz zalecenia podrzędne](#system-updates-should-be-installed-on-your-machines-recommendation-now-includes-sub-recommendations)
- [Na stronie Zarządzanie zasadami w Azure Portal teraz jest wyświetlany stan domyślnych przypisań zasad](#policy-management-page-in-the-azure-portal-now-shows-status-of-default-policy-assignments)

### <a name="29-preview-recommendations-added-to-increase-coverage-of-azure-security-benchmark"></a>29 zaleceń dotyczących wersji zapoznawczej dodanych w celu zwiększenia zakresu testów zabezpieczeń platformy Azure

Usługa Azure Security test to zestaw wytycznych dotyczących zabezpieczeń i zgodności opartych na platformie Azure, które są stosowane do najlepszych rozwiązań w zakresie bezpieczeństwa i zapewniających zgodność. [Dowiedz się więcej o teście porównawczym zabezpieczeń platformy Azure](../security/benchmarks/introduction.md).

Do Security Center dodano następujące zalecenia dotyczące wersji zapoznawczej w celu zwiększenia zakresu tego testu porównawczego.

Zalecenia dotyczące wersji zapoznawczej nie powodują złej kondycji zasobu i nie są uwzględniane w obliczeniach bezpiecznego wyniku. Skoryguj je wszędzie tam, gdzie to możliwe, aby po zakończeniu okresu korzystania z wersji zapoznawczej doczyniły się do oceny. Dowiedz się więcej o tym, jak odpowiedzieć na te zalecenia w temacie [Koryguj zalecenia w Azure Security Center](security-center-remediate-recommendations.md).

| Kontrola zabezpieczeń                     | Nowe rekomendacje                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Szyfruj dane podczas przesyłania              | -Wymuszaj połączenie SSL powinno być włączone dla serwerów bazy danych PostgreSQL<br>-Wymuś połączenie SSL dla serwerów baz danych MySQL<br>-TLS należy zaktualizować do najnowszej wersji dla aplikacji interfejsu API<br>-TLS należy zaktualizować do najnowszej wersji aplikacji funkcji<br>-TLS należy zaktualizować do najnowszej wersji aplikacji sieci Web<br>-FTPS powinna być wymagana w aplikacji interfejsu API<br>-FTPS powinna być wymagana w aplikacji funkcji<br>-FTPS powinna być wymagana w aplikacji sieci Web                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Zarządzanie dostępem i uprawnieniami        | -Aplikacje sieci Web powinny zażądać certyfikatu SSL dla wszystkich żądań przychodzących<br>— Tożsamość zarządzana powinna być używana w aplikacji interfejsu API<br>— Tożsamość zarządzana powinna być używana w aplikacji funkcji<br>— Tożsamość zarządzana powinna być używana w aplikacji sieci Web                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Ogranicz nieautoryzowany dostęp do sieci | -Prywatny punkt końcowy powinien być włączony dla serwerów PostgreSQL<br>-Prywatny punkt końcowy powinien być włączony dla serwerów MariaDB<br>-Prywatny punkt końcowy powinien być włączony dla serwerów MySQL                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Włącz inspekcję i rejestrowanie          | -Należy włączyć dzienniki diagnostyczne w App Services                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Implementowanie najlepszych rozwiązań w zakresie zabezpieczeń    | -Azure Backup powinna być włączona dla maszyn wirtualnych<br>-Geograficznie nadmiarowe kopie zapasowe powinny być włączone dla Azure Database for MariaDB<br>-Geograficznie nadmiarowe kopie zapasowe powinny być włączone dla Azure Database for MySQL<br>-Geograficznie nadmiarowe kopie zapasowe powinny być włączone dla Azure Database for PostgreSQL<br>-PHP należy zaktualizować do najnowszej wersji dla aplikacji interfejsu API<br>-PHP należy zaktualizować do najnowszej wersji aplikacji sieci Web<br>-Java należy zaktualizować do najnowszej wersji dla aplikacji interfejsu API<br>— Środowisko Java należy zaktualizować do najnowszej wersji aplikacji funkcji<br>-Java należy zaktualizować do najnowszej wersji aplikacji sieci Web<br>-Python należy zaktualizować do najnowszej wersji dla aplikacji interfejsu API<br>-Python należy zaktualizować do najnowszej wersji aplikacji funkcji<br>-Python należy zaktualizować do najnowszej wersji aplikacji sieci Web<br>-Inspekcja przechowywania dla serwerów SQL powinna wynosić co najmniej 90 dni |
|                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

Powiązane linki:

- [Dowiedz się więcej o teście zabezpieczeń Azure](../security/benchmarks/introduction.md)
- [Dowiedz się więcej o usłudze Azure API Apps](../app-service/app-service-web-tutorial-rest-api.md)
- [Dowiedz się więcej na temat aplikacji funkcji platformy Azure](../azure-functions/functions-overview.md)
- [Dowiedz się więcej o usłudze Azure Web Apps](../app-service/overview.md)
- [Dowiedz się więcej o Azure Database for MariaDB](../mariadb/overview.md)
- [Dowiedz się więcej o Azure Database for MySQL](../mysql/overview.md)
- [Dowiedz się więcej o Azure Database for PostgreSQL](../postgresql/overview.md)


### <a name="nist-sp-800-171-r2-added-to-security-centers-regulatory-compliance-dashboard"></a>NIST SP 800 171 R2 dodano do Security Center pulpitu nawigacyjnego zgodności z przepisami

Standard NIST SP 800-171 R2 jest teraz dostępny jako wbudowana inicjatywa do używania z pulpitem nawigacyjnym zgodności z przepisami Azure Security Center. Mapowania dla formantów są opisane [szczegółowo w artykule NIST SP 800-171 R2 zgodność z przepisami](../governance/policy/samples/nist-sp-800-171-r2.md). 

Aby zastosować Standard do subskrypcji i stale monitorować stan zgodności, użyj instrukcji w temacie [Dostosowywanie zestawu standardów na pulpicie nawigacyjnym zgodności z przepisami](update-regulatory-compliance-packages.md).

:::image type="content" source="media/release-notes/nist-sp-800-171-r2-standard.png" alt-text="Standard NIST SP 800 171 R2 na pulpicie nawigacyjnym zgodności z przepisami Security Center":::

Aby uzyskać więcej informacji na temat tego standardu zgodności, zobacz [NIST SP 800-171 R2](https://csrc.nist.gov/publications/detail/sp/800-171/rev-2/final).


### <a name="recommendations-list-now-includes-filters"></a>Lista rekomendacji zawiera teraz filtry

Teraz można filtrować listę zaleceń dotyczących zabezpieczeń zgodnie z zakresem kryteriów. W poniższym przykładzie lista zaleceń została przefiltrowana w celu wyświetlenia zaleceń, które:

- są **ogólnie dostępne** (to nie jest wersja zapoznawcza)
- dotyczy **kont magazynu**
- Pomoc techniczna dotycząca **szybkiego rozwiązywania problemów**

:::image type="content" source="media/release-notes/recommendations-filters.png" alt-text="Filtry listy rekomendacji":::


### <a name="auto-provisioning-experience-improved-and-expanded"></a>Ulepszone i rozszerzone środowisko aprowizacji

Funkcja autoaprowizacji pozwala zmniejszyć obciążenie związane z zarządzaniem przez zainstalowanie wymaganych rozszerzeń na nowych maszynach wirtualnych platformy Azure, które mogą korzystać z ochrony Security Center. 

W miarę zwiększania Azure Security Center, opracowano więcej rozszerzeń i Security Center może monitorować większą listę typów zasobów. Narzędzia do samoobsługowego udostępniania zostały teraz rozwinięte w celu obsługi dodatkowych rozszerzeń i typów zasobów, wykorzystując możliwości Azure Policy.

Teraz można skonfigurować funkcję samoobsługowego udostępniania:

- Agent usługi Log Analytics
- Nowy Dodatek Azure Policy dla Kubernetes
- Nowy Agent zależności firmy Microsoft

Dowiedz się więcej w temacie [Inicjowanie obsługi administracyjnej agentów i rozszerzeń z Azure Security Center](security-center-enable-data-collection.md).


### <a name="secure-score-is-now-available-in-continuous-export-preview"></a>Ocena zabezpieczeń jest teraz dostępna w przypadku eksportu ciągłego (wersja zapoznawcza)

Za pomocą ciągłego eksportowania zabezpieczeń można przesyłać strumieniowo zmiany do oceny w czasie rzeczywistym do usługi Azure Event Hubs lub do Log Analytics obszaru roboczego. Użyj tej funkcji, aby:

- Śledź swój Bezpieczny wynik w czasie dzięki dynamicznym raportom
- Eksportuj dane dotyczące danych oceny do platformy Azure (lub innych SIEM)
- Integruj te dane z dowolnymi procesami, które mogą już być używane do monitorowania bezpiecznego wyniku w organizacji

Dowiedz się więcej o tym, jak [ciągle eksportować Security Center dane](continuous-export.md).


### <a name="system-updates-should-be-installed-on-your-machines-recommendation-now-includes-sub-recommendations"></a>Zalecenie "aktualizacje systemu powinny być zainstalowane na Twoich komputerach" obejmuje teraz zalecenia podrzędne

**Aktualizacje systemu powinny być zainstalowane na** zalecanych komputerach. Nowa wersja zawiera zalecenia podrzędne dla każdej brakującej aktualizacji i oferuje następujące udoskonalenia:

- Ponownie zaprojektowane środowisko na Azure Security Center stronach Azure Portal. **Na swoich maszynach należy zainstalować na** stronie Szczegóły rekomendacji zawierającej listę wyników, jak pokazano poniżej. Po wybraniu pojedynczego wyszukiwania zostanie otwarte okienko Szczegóły z linkiem do informacji o korygowaniu oraz z listą zasobów, których to dotyczy.

    :::image type="content" source="./media/upcoming-changes/system-updates-should-be-installed-subassessment.png" alt-text="Otwieranie jednego z zaleceń w portalu w celu uzyskania zaktualizowanego zalecenia":::

- Wzbogacone dane dla zalecenia z grafu zasobów platformy Azure (ARG). ARG to usługa platformy Azure, która została zaprojektowana w celu zapewnienia wydajnej eksploracji zasobów. Za pomocą argumentu ARG można wykonywać zapytania na dużą skalę w ramach danego zestawu subskrypcji, dzięki czemu można efektywnie zarządzać środowiskiem. 

    Aby uzyskać Azure Security Center, można użyć ARG i [Kusto Query Language (KQL)](/azure/data-explorer/kusto/query/) do wykonywania zapytań o szeroki zakres danych stan zabezpieczeń.

    Wcześniej, jeśli zbadasz to zalecenie w ARG, jedynymi dostępnymi informacjami było to, że zalecenie należy skorygować na komputerze. Poniższe zapytanie o wersję rozszerzoną zwróci wszystkie brakujące aktualizacje systemu pogrupowane według maszyn.

    ```kusto
    securityresources
    | where type =~ "microsoft.security/assessments/subassessments"
    | where extract(@"(?i)providers/Microsoft.Security/assessments/([^/]*)", 1, id) == "4ab6e3c5-74dd-8b35-9ab9-f61b30875b27"
    | where properties.status.code == "Unhealthy"
    ```

### <a name="policy-management-page-in-the-azure-portal-now-shows-status-of-default-policy-assignments"></a>Na stronie Zarządzanie zasadami w Azure Portal teraz jest wyświetlany stan domyślnych przypisań zasad

Teraz możesz sprawdzić, czy subskrypcje mają przypisane domyślne zasady Security Center na stronie **zasady zabezpieczeń** Security Center w Azure Portal.

:::image type="content" source="media/release-notes/policy-assignment-info-per-subscription.png" alt-text="Strona Zarządzanie zasadami Azure Security Center wyświetlania domyślnych przypisań zasad":::

## <a name="october-2020"></a>Październik 2020 r.

Aktualizacje w październiku obejmują:
- [Ocena luk w zabezpieczeniach dla maszyn lokalnych i wielochmurowych (wersja zapoznawcza)](#vulnerability-assessment-for-on-premise-and-multi-cloud-machines-preview)
- [Dodane zalecenie dotyczące zapory platformy Azure (wersja zapoznawcza)](#azure-firewall-recommendation-added-preview)
- [Autoryzowane zakresy adresów IP powinny być zdefiniowane w zaleceniu usług Kubernetes Services zaktualizowanym z opcją szybkie rozwiązanie.](#authorized-ip-ranges-should-be-defined-on-kubernetes-services-recommendation-updated-with-quick-fix)
- [Pulpit nawigacyjny zgodności z przepisami zawiera teraz opcję usuwania standardów](#regulatory-compliance-dashboard-now-includes-option-to-remove-standards)
- [Tabela Microsoft. Security/securityStatuses została usunięta z grafu zasobów platformy Azure (ARG)](#microsoftsecuritysecuritystatuses-table-removed-from-azure-resource-graph-arg)

### <a name="vulnerability-assessment-for-on-premise-and-multi-cloud-machines-preview"></a>Ocena luk w zabezpieczeniach dla maszyn lokalnych i wielochmurowych (wersja zapoznawcza)

Program [Azure Defender dla serwerów](defender-for-servers-introduction.md)"zintegrowany skaner do oceny luk w zabezpieczeniach (obsługiwany przez Qualys) skanuje teraz serwery z włączonym rozwiązaniem Azure Arc.

Gdy usługa Azure Arc została włączona na maszynach spoza platformy Azure, Security Center będzie oferować ręczne wdrażanie skanera zintegrowanej luki w zabezpieczeniach.

Dzięki tej aktualizacji można wyłączyć **usługę Azure Defender dla serwerów** , aby skonsolidować program do zarządzania lukami w zabezpieczeniach dla wszystkich zasobów platformy Azure i spoza platformy Azure.

Główne możliwości:

- Monitorowanie stanu aprowizacji skanera (ocena luk w zabezpieczeniach) na maszynach usługi Azure Arc
- Inicjowanie obsługi zintegrowanego agenta VA do niechronionych maszyn z systemem Windows i Linux na platformie Azure (ręcznie i w skali)
- Otrzymywanie i analizowanie wykrytych luk w zabezpieczeniach wdrożonych agentów (ręcznie i w skali)
- Ujednolicone środowisko dla maszyn wirtualnych platformy Azure i usługi Azure Arc

[Dowiedz się więcej o wdrażaniu zintegrowanego skanera luk w zabezpieczeniach na maszynach hybrydowych](deploy-vulnerability-assessment-vm.md#deploy-the-integrated-scanner-to-your-azure-and-hybrid-machines).

[Dowiedz się więcej o serwerach z obsługą usługi Azure Arc](../azure-arc/servers/index.yml).


### <a name="azure-firewall-recommendation-added-preview"></a>Dodane zalecenie dotyczące zapory platformy Azure (wersja zapoznawcza)

Dodano nowe zalecenie umożliwiające ochronę wszystkich sieci wirtualnych za pomocą zapory platformy Azure.

Zalecenie, **sieci wirtualne powinny być chronione przez zaporę platformy Azure** , zaleca się ograniczyć dostęp do sieci wirtualnych i uniemożliwić potencjalne zagrożenia za pomocą zapory platformy Azure.

Dowiedz się więcej o [zaporze platformy Azure](https://azure.microsoft.com/services/azure-firewall/).


### <a name="authorized-ip-ranges-should-be-defined-on-kubernetes-services-recommendation-updated-with-quick-fix"></a>Autoryzowane zakresy adresów IP powinny być zdefiniowane w zaleceniu usług Kubernetes Services zaktualizowanym z opcją szybkie rozwiązanie.

**Zatwierdzone zakresy adresów IP powinny być zdefiniowane w usługach Kubernetes** teraz mają opcję Szybkie rozwiązanie.

Aby uzyskać więcej informacji na temat tego zalecenia i wszystkie inne zalecenia dotyczące Security Center, zobacz [zalecenia dotyczące zabezpieczeń — Podręcznik referencyjny](recommendations-reference.md).

:::image type="content" source="./media/release-notes/authorized-ip-ranges-recommendation.png" alt-text="Autoryzowane zakresy adresów IP należy zdefiniować w rekomendacji usług Kubernetes Services z opcją szybkie rozwiązanie":::


### <a name="regulatory-compliance-dashboard-now-includes-option-to-remove-standards"></a>Pulpit nawigacyjny zgodności z przepisami zawiera teraz opcję usuwania standardów

Pulpit nawigacyjny zgodności z przepisami Security Center zapewnia wgląd w stan zgodności w zależności od tego, jak spełniasz określone wymagania kontroli zgodności.

Pulpit nawigacyjny zawiera domyślny zestaw standardów prawnych. Jeśli którekolwiek z podanych standardów nie są odpowiednie dla Twojej organizacji, to teraz prosty proces, po prostu usunąć go z interfejsu użytkownika dla subskrypcji. Standardy można usuwać tylko na poziomie *subskrypcji* . to nie jest zakres grupy zarządzania.

Dowiedz się więcej w temacie [usuwanie standardu z pulpitu nawigacyjnego](update-regulatory-compliance-packages.md#removing-a-standard-from-your-dashboard).


### <a name="microsoftsecuritysecuritystatuses-table-removed-from-azure-resource-graph-arg"></a>Tabela Microsoft. Security/securityStatuses została usunięta z grafu zasobów platformy Azure (ARG)

Azure Resource Graph to usługa platformy Azure, która została zaprojektowana w celu zapewnienia wydajnej eksploracji zasobów dzięki możliwości wykonywania zapytań na dużą skalę w ramach danego zestawu subskrypcji, dzięki czemu możesz efektywnie zarządzać środowiskiem. 

Aby uzyskać Azure Security Center, można użyć ARG i [Kusto Query Language (KQL)](/azure/data-explorer/kusto/query/) do wykonywania zapytań o szeroki zakres danych stan zabezpieczeń. Na przykład:

- Wykorzystanie spisu zasobów (ARG)
- Zarejestrowano przykładowe zapytanie ARG dotyczące [identyfikowania kont bez włączonej usługi uwierzytelniania wieloskładnikowego (MFA)](security-center-identity-access.md#identify-accounts-without-multi-factor-authentication-mfa-enabled)

W ciągu ARG istnieją tabele danych, których można używać w zapytaniach.

:::image type="content" source="./media/release-notes/azure-resource-graph-tables.png" alt-text="Eksplorator usługi Azure Resource Graph i dostępne tabele":::

> [!TIP]
> W dokumentacji ARG znajdują się wszystkie dostępne tabele w [tabeli grafów zasobów platformy Azure i odwołania do typu zasobu](../governance/resource-graph/reference/supported-tables-resources.md).

W ramach tej aktualizacji tabela **Microsoft. Security/securityStatuses** została usunięta. Interfejs API securityStatuses jest nadal dostępny.

Wymiana danych może być używana przez tabelę Microsoft. Security/Assessments.

Główna różnica między elementami Microsoft. Security/securityStatuses i Microsoft. Security/Assessments polega na tym, że podczas pierwszego wyświetlania agregacji ocen w sekundach są przechowywane pojedyncze rekordy.

Na przykład firma Microsoft. Security/securityStatuses zwróci wynik z tablicą dwóch policyAssessments:

```
{
id: "/subscriptions/449bcidd-3470-4804-ab56-2752595 felab/resourceGroups/mico-rg/providers/Microsoft.Network/virtualNetworks/mico-rg-vnet/providers/Microsoft.Security/securityStatuses/mico-rg-vnet",
name: "mico-rg-vnet",
type: "Microsoft.Security/securityStatuses",
properties:  {
    policyAssessments: [
        {assessmentKey: "e3deicce-f4dd-3b34-e496-8b5381bazd7e", category: "Networking", policyName: "Azure DDOS Protection Standard should be enabled",...},
        {assessmentKey: "sefac66a-1ec5-b063-a824-eb28671dc527", category: "Compute", policyName: "",...}
    ],
    securitystateByCategory: [{category: "Networking", securityState: "None" }, {category: "Compute",...],
    name: "GenericResourceHealthProperties",
    type: "VirtualNetwork",
    securitystate: "High"
}
```
W związku z tym firma Microsoft. Security/Assessments będzie przechowywać rekord dla każdej takiej oceny zasad w następujący sposób:

```
{
type: "Microsoft.Security/assessments",
id:  "/subscriptions/449bc1dd-3470-4804-ab56-2752595f01ab/resourceGroups/mico-rg/providers/Microsoft. Network/virtualNetworks/mico-rg-vnet/providers/Microsoft.Security/assessments/e3delcce-f4dd-3b34-e496-8b5381ba2d70",
name: "e3deicce-f4dd-3b34-e496-8b5381ba2d70",
properties:  {
    resourceDetails: {Source: "Azure", Id: "/subscriptions/449bc1dd-3470-4804-ab56-2752595f01ab/resourceGroups/mico-rg/providers/Microsoft.Network/virtualNetworks/mico-rg-vnet"...},
    displayName: "Azure DDOS Protection Standard should be enabled",
    status: (code: "NotApplicable", cause: "VnetHasNOAppGateways", description: "There are no Application Gateway resources attached to this Virtual Network"...}
}

{
type: "Microsoft.Security/assessments",
id:  "/subscriptions/449bc1dd-3470-4804-ab56-2752595f01ab/resourcegroups/mico-rg/providers/microsoft.network/virtualnetworks/mico-rg-vnet/providers/Microsoft.Security/assessments/80fac66a-1ec5-be63-a824-eb28671dc527",
name: "8efac66a-1ec5-be63-a824-eb28671dc527",
properties: {
    resourceDetails: (Source: "Azure", Id: "/subscriptions/449bc1dd-3470-4804-ab56-2752595f01ab/resourcegroups/mico-rg/providers/microsoft.network/virtualnetworks/mico-rg-vnet"...),
    displayName: "Audit diagnostic setting",
    status:  {code: "Unhealthy"}
}
```

**Przykład konwersji istniejącego zapytania ARG przy użyciu securityStatuses, aby teraz korzystać z tabeli ocen:**

Zapytanie odwołujące się do SecurityStatuses:

```kusto
SecurityResources 
| where type == 'microsoft.security/securitystatuses' and properties.type == 'virtualMachine'
| where name in ({vmnames}) 
| project name, resourceGroup, policyAssesments = properties.policyAssessments, resourceRegion = location, id, resourceDetails = properties.resourceDetails
```

Zastępowanie zapytania dla tabeli ocen:

```kusto
securityresources
| where type == "microsoft.security/assessments" and id contains "virtualMachine"
| extend resourceName = extract(@"(?i)/([^/]*)/providers/Microsoft.Security/assessments", 1, id)
| extend source = tostring(properties.resourceDetails.Source)
| extend resourceId = trim(" ", tolower(tostring(case(source =~ "azure", properties.resourceDetails.Id,
source =~ "aws", properties.additionalData.AzureResourceId,
source =~ "gcp", properties.additionalData.AzureResourceId,
extract("^(.+)/providers/Microsoft.Security/assessments/.+$",1,id)))))
| extend resourceGroup = tolower(tostring(split(resourceId, "/")[4]))
| where resourceName in ({vmnames}) 
| project resourceName, resourceGroup, resourceRegion = location, id, resourceDetails = properties.additionalData
```

Dowiedz się więcej na następujące linki:
- [Jak tworzyć zapytania za pomocą eksploratora usługi Azure Resource Graph](../governance/resource-graph/first-query-portal.md)
- [Kusto Query Language (KQL)](/azure/data-explorer/kusto/query/)


## <a name="september-2020"></a>Wrzesień 2020

Aktualizacje we wrześniu obejmują:
- [Security Center Pobiera nowy wygląd!](#security-center-gets-a-new-look)
- [Wydano usługę Azure Defender](#azure-defender-released)
- [Usługa Azure Defender dla Key Vault jest ogólnie dostępna](#azure-defender-for-key-vault-is-generally-available)
- [Usługa Azure Defender do ochrony magazynu dla plików i ADLS Gen2 jest ogólnie dostępna](#azure-defender-for-storage-protection-for-files-and-adls-gen2-is-generally-available)
- [Narzędzia spisu zasobów są teraz ogólnie dostępne](#asset-inventory-tools-are-now-generally-available)
- [Wyłączenie konkretnej luki w zabezpieczeniach w poszukiwaniu skanów rejestrów kontenerów i maszyn wirtualnych](#disable-a-specific-vulnerability-finding-for-scans-of-container-registries-and-virtual-machines)
- [Wykluczanie zasobu z rekomendacji](#exempt-a-resource-from-a-recommendation)
- [Łączniki AWS i GCP w Security Center zapewniają środowisko z obsługą chmury](#aws-and-gcp-connectors-in-security-center-bring-a-multi-cloud-experience)
- [Pakiet rekomendacji ochrony obciążeń Kubernetes](#kubernetes-workload-protection-recommendation-bundle)
- [Wyniki oceny luk w zabezpieczeniach są teraz dostępne w przypadku eksportu ciągłego](#vulnerability-assessment-findings-are-now-available-in-continuous-export)
- [Zapobiegaj błędom konfiguracji zabezpieczeń, wymuszając zalecenia podczas tworzenia nowych zasobów](#prevent-security-misconfigurations-by-enforcing-recommendations-when-creating-new-resources)
- [Ulepszone zalecenia dotyczące sieciowej grupy zabezpieczeń](#network-security-group-recommendations-improved)
- [Przestarzałe zalecenie dotyczące wersji zapoznawczej AKS "pod kątem zasad zabezpieczeń należy zdefiniować w usługach Kubernetes Services"](#deprecated-preview-aks-recommendation-pod-security-policies-should-be-defined-on-kubernetes-services)
- [Ulepszona wiadomość e-mail z powiadomieniem Azure Security Center](#email-notifications-from-azure-security-center-improved)
- [Wynik zabezpieczony nie obejmuje zaleceń dotyczących wersji zapoznawczej](#secure-score-doesnt-include-preview-recommendations)
- [Zalecenia zawierają teraz wskaźnik ważności i interwał Aktualności](#recommendations-now-include-a-severity-indicator-and-the-freshness-interval)


### <a name="security-center-gets-a-new-look"></a>Security Center Pobiera nowy wygląd!

Opublikowano odświeżony interfejs użytkownika dla stron portalu Security Center. Nowe strony zawierają nową stronę przeglądu, a także pulpity nawigacyjne do zabezpieczania oceny, spisu zasobów i usługi Azure Defender.

Przeprojektowana Strona przeglądu zawiera teraz kafelek umożliwiające dostęp do usług pulpitu nawigacyjnego bezpiecznego oceny, spisu zasobów i usługi Azure Defender. Zawiera również kafelek łączący pulpit nawigacyjny zgodności z przepisami.

Dowiedz się więcej o [stronie Przegląd](overview-page.md).


### <a name="azure-defender-released"></a>Wydano usługę Azure Defender

**Usługa Azure Defender** to platforma ochrony obciążeń w chmurze (CWPP) zintegrowana w ramach Security Center na potrzeby zaawansowanej, inteligentnej, chronionej platformy Azure i obciążeń hybrydowych. Zastępuje Security Center opcję warstwy cenowej standardowa. 

Po włączeniu usługi Azure Defender w obszarze **cennika i ustawienia** Azure Security Center następujące plany usługi Defender są dostępne jednocześnie i zapewniają kompleksowe zabezpieczenia dla warstw obliczeniowych, danych i usług w środowisku:

- [Usługa Azure Defender dla serwerów](defender-for-servers-introduction.md)
- [Usługa Azure Defender dla usługi App Service](defender-for-app-service-introduction.md)
- [Usługa Azure Defender dla usługi Storage](defender-for-storage-introduction.md)
- [Azure Defender for SQL](defender-for-sql-introduction.md)
- [Usługa Azure Defender dla usługi Key Vault](defender-for-key-vault-introduction.md)
- [Usługa Azure Defender dla platformy Kubernetes](defender-for-kubernetes-introduction.md)
- [Usługa Azure Defender dla rejestrów kontenerów](defender-for-container-registries-introduction.md)

Każdy z tych planów został opisany osobno w dokumentacji Security Center.

Dzięki dedykowanemu pulpitowi nawigacyjnemu usługa Azure Defender udostępnia alerty zabezpieczeń i zaawansowaną ochronę przed zagrożeniami dla maszyn wirtualnych, baz danych SQL, kontenerów, aplikacji sieci Web, sieci i innych.

[Dowiedz się więcej o usłudze Azure Defender](azure-defender.md)

### <a name="azure-defender-for-key-vault-is-generally-available"></a>Usługa Azure Defender dla Key Vault jest ogólnie dostępna

Azure Key Vault to usługa w chmurze, która chroni klucze szyfrowania i wpisy tajne, takie jak certyfikaty, ciągi połączeń i hasła. 

**Usługa Azure Defender dla Key Vault** zapewnia platformę Azure — natywną, zaawansowaną ochronę przed zagrożeniami dla Azure Key Vault, zapewniając dodatkową warstwę analizy zabezpieczeń. Dzięki rozszerzeniu usługa Azure Defender dla Key Vault chroni wiele zasobów zależnych od kont Key Vault.

Plan opcjonalny jest teraz rozpowszechny. Ta funkcja była dostępna w wersji zapoznawczej jako "Zaawansowana ochrona przed zagrożeniami dla Azure Key Vault".

Ponadto strony Key Vault w Azure Portal zawierają teraz dedykowaną stronę **zabezpieczeń** dla **Security Center** zaleceń i alertów.

Dowiedz się więcej w [usłudze Azure Defender dla Key Vault](defender-for-key-vault-introduction.md).


### <a name="azure-defender-for-storage-protection-for-files-and-adls-gen2-is-generally-available"></a>Usługa Azure Defender do ochrony magazynu dla plików i ADLS Gen2 jest ogólnie dostępna 

**Usługa Azure Defender for Storage** wykrywa potencjalnie szkodliwe działanie na kontach usługi Azure Storage. Dane można chronić, niezależnie od tego, czy są przechowywane jako kontenery obiektów blob, udziały plików czy jeziora danych.

Obsługa [Azure Files](../storage/files/storage-files-introduction.md) i [Azure Data Lake Storage Gen2](../storage/blobs/data-lake-storage-introduction.md) jest teraz ogólnie dostępna.

Od 1 października 2020 rozpocznie się naliczanie opłat za ochronę zasobów w tych usługach.

Dowiedz się więcej w [usłudze Azure Defender dla magazynu](defender-for-storage-introduction.md).


### <a name="asset-inventory-tools-are-now-generally-available"></a>Narzędzia spisu zasobów są teraz ogólnie dostępne

Strona spisu zasobów Azure Security Center udostępnia pojedynczą stronę do wyświetlania stan zabezpieczeń zasobów, z którymi nawiązano połączenie Security Center.

Security Center okresowo analizuje stan zabezpieczeń zasobów platformy Azure w celu zidentyfikowania potencjalnych luk w zabezpieczeniach. Następnie zawiera zalecenia dotyczące sposobu korygowania tych luk w zabezpieczeniach.

Jeśli którykolwiek z zasobów ma zaległe zalecenia, zostaną one wyświetlone w spisie.

Dowiedz się więcej w temacie [Eksplorowanie zasobów i zarządzanie nimi przy użyciu spisu](asset-inventory.md)zasobów.



### <a name="disable-a-specific-vulnerability-finding-for-scans-of-container-registries-and-virtual-machines"></a>Wyłączenie konkretnej luki w zabezpieczeniach w poszukiwaniu skanów rejestrów kontenerów i maszyn wirtualnych

Usługa Azure Defender zawiera skanery luk w zabezpieczeniach do skanowania obrazów w Azure Container Registry i maszynach wirtualnych.

Jeśli istnieje organizacja, która ma być ignorowana, zamiast skorygować ją, możesz ją wyłączyć. Wyłączone wyniki nie wpływają na swój Bezpieczny wynik ani nie generują niechcianych szumów.

Gdy wyszukiwanie jest zgodne z kryteriami zdefiniowanymi w regułach wyłączania, nie będą wyświetlane na liście wyników.

Ta opcja jest dostępna na stronie Szczegóły zaleceń dla:

- **Luki w zabezpieczeniach Azure Container Registry obrazów należy skorygować**
- **Luki w zabezpieczeniach maszyn wirtualnych należy skorygować**

Dowiedz się więcej w temacie [wyłączanie określonych wyników dla obrazów kontenerów](defender-for-container-registries-usage.md#disable-specific-findings-preview) i [wyłączanie określonych wyników dla maszyn wirtualnych](remediate-vulnerability-findings-vm.md#disable-specific-findings-preview).


### <a name="exempt-a-resource-from-a-recommendation"></a>Wykluczanie zasobu z rekomendacji

Czasami zasób będzie wyświetlany jako w złej kondycji w odniesieniu do konkretnego zalecenia (i w związku z tym obniżenie bezpiecznego wyniku), nawet jeśli nie będzie to możliwe. Być może został skorygowany przez proces, który nie jest śledzony przez Security Center. Lub być może Twoja organizacja zdecydowała się zaakceptować ryzyko związane z tym konkretnym zasobem. 

W takich przypadkach można utworzyć regułę wykluczania i upewnić się, że zasób nie znajduje się na liście zasobów w złej kondycji w przyszłości. Te reguły mogą zawierać udokumentowane uzasadnienia, jak opisano poniżej.

Dowiedz się więcej na temat [wykluczania zasobu z rekomendacji i bezpiecznego oceny](exempt-resource.md).


### <a name="aws-and-gcp-connectors-in-security-center-bring-a-multi-cloud-experience"></a>Łączniki AWS i GCP w Security Center zapewniają środowisko z obsługą chmury

W przypadku obciążeń w chmurze zwykle obejmujących wiele platform w chmurze usługi zabezpieczeń w chmurze muszą być takie same.

Azure Security Center teraz chroni obciążenia na platformie Azure, Amazon Web Services (AWS) i Google Cloud Platform (GCP).

Dołączanie kont AWS i GCP do Security Center integruje się z usługą AWS Security Hub, GCP Security Command i Azure Security Center. 

Więcej informacji znajduje się w temacie [Łączenie kont AWS w celu Azure Security Center](quickstart-onboard-aws.md) i [łączenia kont GCP z Azure Security Center](quickstart-onboard-gcp.md).


### <a name="kubernetes-workload-protection-recommendation-bundle"></a>Pakiet rekomendacji ochrony obciążeń Kubernetes

Aby zapewnić, że obciążenia Kubernetes są zabezpieczone domyślnie, Security Center dodaje zalecenia dotyczące ograniczania poziomu Kubernetes, w tym opcje wymuszania z Kubernetes Admission Control.

Po zainstalowaniu dodatku Azure Policy dla Kubernetes w klastrze AKS, każde żądanie do serwera interfejsu API Kubernetes zostanie monitorowane względem wstępnie zdefiniowanego zestawu najlepszych rozwiązań przed utrwaleniem w klastrze. Następnie można skonfigurować w celu wymuszenia najlepszych rozwiązań i ich upoważnienia do przyszłych obciążeń.

Na przykład można przystąpić do tego, że kontenery uprzywilejowane nie powinny być tworzone, a wszystkie przyszłe żądania, które należy wykonać, zostaną zablokowane.

Dowiedz się więcej o [najlepszych rozwiązaniach dotyczących ochrony obciążeń przy użyciu funkcji Kubernetes Admission Control](container-security.md#workload-protection-best-practices-using-kubernetes-admission-control).


### <a name="vulnerability-assessment-findings-are-now-available-in-continuous-export"></a>Wyniki oceny luk w zabezpieczeniach są teraz dostępne w przypadku eksportu ciągłego

Używaj eksportu ciągłego do przesyłania strumieniowego alertów i zaleceń w czasie rzeczywistym do usługi Azure Event Hubs, Log Analytics obszarów roboczych lub Azure Monitor. Z tego miejsca możesz zintegrować te dane z rozwiązań Siem (np. na platformie Azure, Power BI, na platformie Azure Eksplorator danych i nie tylko.

Narzędzia do oceny luk w zabezpieczeniach Security Center zwracają informacje o zasobach jako zalecenia z możliwością działania w ramach zalecenia "nadrzędny", takie jak "luki w zabezpieczeniach w maszynach wirtualnych, należy skorygować". 

W przypadku wybrania opcji zalecenia dotyczące zabezpieczeń można eksportować za pomocą eksportu ciągłego, a także włączyć opcję **Uwzględnij wnioski dotyczące zabezpieczeń** .

:::image type="content" source="./media/continuous-export/include-security-findings-toggle.png" alt-text="Uwzględnij w konfiguracji eksportu ciągłego funkcję przełączania zabezpieczeń" :::

Powiązane strony:

- [Security Center rozwiązanie do oceny luk w zabezpieczeniach dla usługi Azure Virtual Machines](deploy-vulnerability-assessment-vm.md)
- [Security Center rozwiązanie do oceny luk w zabezpieczeniach dla Azure Container Registry obrazów](defender-for-container-registries-usage.md)
- [Eksport ciągły](continuous-export.md)

### <a name="prevent-security-misconfigurations-by-enforcing-recommendations-when-creating-new-resources"></a>Zapobiegaj błędom konfiguracji zabezpieczeń, wymuszając zalecenia podczas tworzenia nowych zasobów

Błędy konfiguracji zabezpieczeń są główną przyczyną zdarzeń zabezpieczeń. Security Center teraz ma możliwość *zapobiegania* błędom konfiguracji nowych zasobów w odniesieniu do określonych zaleceń. 

Ta funkcja może pomóc w zabezpieczeniu obciążeń i stabilizacji bezpiecznego wyniku.

Wymuszanie bezpiecznej konfiguracji w oparciu o określone zalecenie jest oferowane w dwóch trybach:

- Przy użyciu efektu **odmowy** Azure Policy można zatrzymać tworzenie zasobów w złej kondycji

- Przy użyciu opcji **Wymuszaj** można korzystać z **DeployIfNotExist** i automatycznego korygowania niezgodnych zasobów podczas tworzenia
 
Jest to dostępne dla wybranych zaleceń dotyczących zabezpieczeń i można je znaleźć w górnej części strony Szczegóły zasobu.

Dowiedz się więcej w temacie [zapobieganie błędom konfiguracji z zaleceń Wymuszaj/Odmów](prevent-misconfigurations.md).

###  <a name="network-security-group-recommendations-improved"></a>Ulepszone zalecenia dotyczące sieciowej grupy zabezpieczeń

Udoskonalono następujące zalecenia dotyczące zabezpieczeń dotyczące sieciowych grup zabezpieczeń, aby zmniejszyć liczbę wystąpień fałszywie dodatnich.

- Wszystkie porty sieciowe powinny być ograniczone do sieciowej grupy zabezpieczeń skojarzonych z maszyną wirtualną
- Porty zarządzania powinny być zamknięte na maszynach wirtualnych
- Maszyny wirtualne dostępne z Internetu powinny być chronione za pomocą sieciowych grup zabezpieczeń
- Podsieci powinny być skojarzone z sieciową grupą zabezpieczeń


### <a name="deprecated-preview-aks-recommendation-pod-security-policies-should-be-defined-on-kubernetes-services"></a>Przestarzałe zalecenie dotyczące wersji zapoznawczej AKS "pod kątem zasad zabezpieczeń należy zdefiniować w usługach Kubernetes Services"

Zalecenia dotyczące wersji zapoznawczej muszą być zdefiniowane w usługach Kubernetes Services są przestarzałe zgodnie z opisem w dokumentacji [usługi Azure Kubernetes](../aks/use-pod-security-policies.md) .

Funkcja zasad zabezpieczeń (wersja zapoznawcza) jest ustawiana jako przestarzała i nie będzie już dostępna po 15 października Azure Policy 2020 AKS.

Gdy zasady zabezpieczeń (wersja zapoznawcza) są przestarzałe, należy wyłączyć tę funkcję w przypadku wszystkich istniejących klastrów przy użyciu przestarzałej funkcji w celu przeprowadzania przyszłych uaktualnień klastra i pozostawania w ramach pomocy technicznej systemu Azure.


### <a name="email-notifications-from-azure-security-center-improved"></a>Ulepszona wiadomość e-mail z powiadomieniem Azure Security Center

Ulepszono następujące obszary wiadomości e-mail dotyczące alertów zabezpieczeń: 

- Dodano możliwość wysyłania powiadomień e-mail o alertach dotyczących wszystkich poziomów ważności
- Dodano możliwość powiadamiania użytkowników z różnymi rolami platformy Azure w ramach subskrypcji
- Aktywnie Powiadamiamy właścicieli subskrypcji domyślnie o alertach o wysokiej ważności (które mają wysokie prawdopodobieństwo naruszenia oryginalnego oprogramowania)
- Usunięto pole numeru telefonu ze strony konfiguracji powiadomień e-mail

Dowiedz się więcej w temacie [Konfigurowanie powiadomień e-mail dla alertów zabezpieczeń](security-center-provide-security-contact-details.md).


### <a name="secure-score-doesnt-include-preview-recommendations"></a>Wynik zabezpieczony nie obejmuje zaleceń dotyczących wersji zapoznawczej 

Security Center stale ocenia zasoby, subskrypcje i organizację pod kątem problemów z zabezpieczeniami. Następnie agreguje wszystkie wyniki w postaci pojedynczego wyniku, dzięki czemu można szybko powiedzieć, że aktualna sytuacja zabezpieczeń: wyższy wynik, tym niższy poziom ryzyka.

Po odnalezieniu nowych zagrożeń nowe porady dotyczące zabezpieczeń są udostępniane w Security Center przez nowe zalecenia. Aby zapobiec niezależnym zmianom i poznawać okres prolongaty, w którym można poznać nowe zalecenia, zanim wpłyną one na Twoje wyniki, zalecenia oflagowane jako **Podgląd** nie są już uwzględniane w obliczeniach bezpiecznego wyniku. Powinny być nadal korygowane wszędzie tam, gdzie jest to możliwe, więc po zakończeniu okresu korzystania z wersji zapoznawczej będą one wchodzić w skład Twojego wyniku.

Ponadto zalecenia dotyczące **wersji zapoznawczej** nie renderują zasobu w złej kondycji.

Przykład zalecenia dotyczącego wersji zapoznawczej:

:::image type="content" source="./media/secure-score-security-controls/example-of-preview-recommendation.png" alt-text="Zalecenie z flagą wersji zapoznawczej":::

[Dowiedz się więcej na temat bezpiecznego oceny](secure-score-security-controls.md).


### <a name="recommendations-now-include-a-severity-indicator-and-the-freshness-interval"></a>Zalecenia zawierają teraz wskaźnik ważności i interwał Aktualności

Strona szczegóły dotyczące rekomendacji zawiera teraz wskaźnik czasu świeżości (jeśli dotyczy) oraz jasne wyświetlanie ważności zalecenia.

:::image type="content" source="./media/release-notes/recommendations-severity-freshness-indicators.png" alt-text="Strona rekomendacja przedstawiająca aktualność i ważność":::



## <a name="august-2020"></a>Sierpień 2020 r.

Aktualizacje w sierpniu obejmują:

- [Spis zasobów — zaawansowany nowy widok stan zabezpieczeń zasobów](#asset-inventory---powerful-new-view-of-the-security-posture-of-your-assets)
- [Dodano obsługę domyślnych ustawień zabezpieczeń Azure Active Directory (w przypadku uwierzytelniania wieloskładnikowego)](#added-support-for-azure-active-directory-security-defaults-for-multi-factor-authentication)
- [Dodano zalecenie dotyczące jednostek usługi](#service-principals-recommendation-added)
- [Ocena luk w zabezpieczeniach maszyn wirtualnych — zaleceń i zasad skonsolidowanych](#vulnerability-assessment-on-vms---recommendations-and-policies-consolidated)
- [Nowe zasady zabezpieczeń AKS dodane do inicjatywy ASC_default — wyłącznie do użytku przez klientów prywatnej wersji zapoznawczej](#new-aks-security-policies-added-to-asc_default-initiative--for-use-by-private-preview-customers-only)


### <a name="asset-inventory---powerful-new-view-of-the-security-posture-of-your-assets"></a>Spis zasobów — zaawansowany nowy widok stan zabezpieczeń zasobów

Security Center spisu zasobów (obecnie w wersji zapoznawczej) umożliwia wyświetlenie stan zabezpieczeń zasobów, z którymi nawiązano połączenie Security Center.

Security Center okresowo analizuje stan zabezpieczeń zasobów platformy Azure w celu zidentyfikowania potencjalnych luk w zabezpieczeniach. Następnie zawiera zalecenia dotyczące sposobu korygowania tych luk w zabezpieczeniach. Jeśli którykolwiek z zasobów ma zaległe zalecenia, zostaną one wyświetlone w spisie.

Widok i jego Filtry umożliwiają Eksplorowanie danych stan zabezpieczeń i podejmowanie dalszych działań w oparciu o Twoje wyniki.

Dowiedz się więcej na temat [spisu zasobów](asset-inventory.md).


### <a name="added-support-for-azure-active-directory-security-defaults-for-multi-factor-authentication"></a>Dodano obsługę domyślnych ustawień zabezpieczeń Azure Active Directory (w przypadku uwierzytelniania wieloskładnikowego)

Security Center dodaliśmy pełną obsługę [zabezpieczeń domyślnych](../active-directory/fundamentals/concept-fundamentals-security-defaults.md), bezpłatna ochrona zabezpieczeń firmy Microsoft.

Wartości domyślne zabezpieczeń zapewniają wstępnie skonfigurowane ustawienia zabezpieczeń tożsamości, aby chronić organizację przed typowymi atakami związanymi z tożsamościami. Zabezpieczenia domyślne chronią już więcej niż 5 000 000 dzierżawców; dzierżawy 50 000 są również chronione przez Security Center.

Security Center teraz zawiera zalecenie dotyczące zabezpieczeń, za każdym razem, gdy zidentyfikuje subskrypcję platformy Azure bez włączonej wartości domyślnej zabezpieczeń. Do tej pory Security Center zalecane włączenie uwierzytelniania wieloskładnikowego przy użyciu dostępu warunkowego, który jest częścią licencji Premium Azure Active Directory (AD). W przypadku klientów korzystających bezpłatnie z usługi Azure AD zalecamy włączenie ustawień domyślnych zabezpieczeń. 

Naszym celem jest zachęcanie większej liczby klientów do zabezpieczania środowisk w chmurze za pomocą usługi MFA i łagodzenie jednego z największych zagrożeń, które są również najbardziej wpływem na [bezpieczny wynik](secure-score-security-controls.md).

Dowiedz się więcej o [domyślnych ustawieniach zabezpieczeń](../active-directory/fundamentals/concept-fundamentals-security-defaults.md).


### <a name="service-principals-recommendation-added"></a>Dodano zalecenie dotyczące jednostek usługi

Dodano nowe zalecenie, aby zalecić Security Center klientom używającym certyfikatów zarządzania do zarządzania swoimi subskrypcjami przełączać się do podmiotów usługi.

Zaleca się, **Aby Ochrona Twoich subskrypcji zamiast certyfikatów zarządzania była chroniona** przy użyciu jednostek usługi lub Azure Resource Manager do bezpieczniejszego zarządzania subskrypcjami. 

Więcej informacji o [obiektach głównych aplikacji i usług znajduje się w Azure Active Directory](../active-directory/develop/app-objects-and-service-principals.md#service-principal-object).


### <a name="vulnerability-assessment-on-vms---recommendations-and-policies-consolidated"></a>Ocena luk w zabezpieczeniach maszyn wirtualnych — zaleceń i zasad skonsolidowanych

Security Center przeprowadza inspekcję maszyn wirtualnych w celu wykrycia, czy są uruchomione rozwiązanie do oceny luk w zabezpieczeniach. Jeśli nie zostanie odnalezione rozwiązanie do oceny luk w zabezpieczeniach, Security Center zapewnia zalecenie upraszczające wdrożenie.

Po znalezieniu luk w zabezpieczeniach Security Center zawiera zalecenia podsumowujące wyniki, które należy zbadać i skorygować w razie potrzeby.

Aby zapewnić spójne środowisko dla wszystkich użytkowników, niezależnie od używanego typu skanera, zostały ujednolicone cztery zalecenia w następujących dwóch:

|Ujednolicone zalecenie|Zmień opis|
|----|:----|
|**Rozwiązanie do oceny luk w zabezpieczeniach powinno być włączone na maszynach wirtualnych**|Zastępuje dwa następujące zalecenia:<br> **•** Włącz wbudowane rozwiązanie do oceny luk w zabezpieczeniach na maszynach wirtualnych (obsługiwane przez Qualys (obecnie przestarzałe) (dołączone do warstwy Standardowa)<br> **•** Rozwiązanie do oceny luk w zabezpieczeniach powinno być zainstalowane na maszynach wirtualnych (obecnie przestarzałe) (warstwy Standardowa i bezpłatna)|
|**Luki w zabezpieczeniach maszyn wirtualnych należy skorygować**|Zastępuje dwa następujące zalecenia:<br>**•** Koryguj luki w zabezpieczeniach na maszynach wirtualnych (obsługiwane przez Qualys) (obecnie przestarzałe)<br>**•** Usterki należy skorygować przez rozwiązanie do oceny luk w zabezpieczeniach (obecnie przestarzałe)|
|||

Teraz użyjesz tego samego zalecenia do wdrożenia rozszerzenia oceny luk w zabezpieczeniach Security Center lub rozwiązania z licencją prywatną ("BYOL") od partnera, takiego jak Qualys lub Rapid7.

Ponadto po znalezieniu luk w zabezpieczeniach i zaraportowaniu ich do Security Center, jedno zalecenie będzie powiadamiać o wynikach niezależnie od rozwiązania do oceny luk w zabezpieczeniach, które je określiło.

#### <a name="updating-dependencies"></a>Aktualizowanie zależności

Jeśli masz skrypty, zapytania lub automatyzacje odwołujące się do poprzednich zaleceń lub kluczy zasad/nazw, Użyj poniższych tabel, aby zaktualizować odwołania:

##### <a name="before-august-2020"></a>Przed 2020 sierpnia

|Zalecenie|Zakres|
|----|:----|
|**Włącz wbudowane rozwiązanie do oceny luk w zabezpieczeniach na maszynach wirtualnych (obsługiwane przez Qualys)**<br>Klucz: 550e890b-e652-4d22-8274-60b3bdb24c63|Wbudowane|
|**Koryguj luki w zabezpieczeniach na maszynach wirtualnych (obsługiwane przez Qualys)**<br>Klucz: 1195afff-c881-495e-9bc5-1486211ae03f|Wbudowane|
|**Rozwiązanie do oceny luk w zabezpieczeniach powinno być zainstalowane na maszynach wirtualnych**<br>Klucz: 01b1ed4c-b733-4fee-b145-f23236e70cf3|BYOL|
|**Usterki należy skorygować przez rozwiązanie do oceny luk w zabezpieczeniach**<br>Klucz: 71992a2a-D168-42e0-b10e-6b45fa2ecddb|BYOL|
||||


|Zasady|Zakres|
|----|:----|
|**Ocena luk w zabezpieczeniach powinna być włączona na maszynach wirtualnych**<br>Identyfikator zasad: 501541f7-f7e7-4cd6-868c-4190fdad3ac9|Wbudowane|
|**Usterki należy skorygować przez rozwiązanie do oceny luk w zabezpieczeniach**<br>Identyfikator zasad: 760a85ff-6162-42b3-8d70-698e268f648c|BYOL|
||||


##### <a name="from-august-2020"></a>Od sierpnia 2020

|Zalecenie|Zakres|
|----|:----|
|**Rozwiązanie do oceny luk w zabezpieczeniach powinno być włączone na maszynach wirtualnych**<br>Klucz: ffff0522-1e88-47fc-8382-2a80ba848f5d|Wbudowane + BYOL|
|**Luki w zabezpieczeniach maszyn wirtualnych należy skorygować**<br>Klucz: 1195afff-c881-495e-9bc5-1486211ae03f|Wbudowane + BYOL|
||||

|Zasady|Zakres|
|----|:----|
|[**Ocena luk w zabezpieczeniach powinna być włączona na maszynach wirtualnych**](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f501541f7-f7e7-4cd6-868c-4190fdad3ac9)<br>Identyfikator zasad: 501541f7-f7e7-4cd6-868c-4190fdad3ac9 |Wbudowane + BYOL|
||||


### <a name="new-aks-security-policies-added-to-asc_default-initiative--for-use-by-private-preview-customers-only"></a>Nowe zasady zabezpieczeń AKS dodane do inicjatywy ASC_default — wyłącznie do użytku przez klientów prywatnej wersji zapoznawczej

Aby zapewnić, że obciążenia Kubernetes są zabezpieczone domyślnie, Security Center dodaje zasady na poziomie Kubernetes i zalecenia dotyczące ograniczania funkcjonalności, w tym opcje wymuszania z Kubernetes Admission Control.

Wczesna Faza tego projektu obejmuje prywatną wersję zapoznawczą oraz dodanie nowych (domyślnie wyłączonych) zasad do inicjatywy ASC_default.

Można bezpiecznie zignorować te zasady i nie będzie to miało wpływu na Twoje środowisko. Jeśli chcesz je włączyć, Utwórz konto w wersji zapoznawczej, https://aka.ms/SecurityPrP a następnie wybierz jedną z następujących opcji:

1. **Pojedynczej wersji zapoznawczej** — aby dołączyć tylko do tej prywatnej wersji zapoznawczej. Jawnie wskaż "ciągłe skanowanie ASC" jako wersję zapoznawczą, do której chcesz dołączyć.
1. **Program** będący w toku — zostanie dodany do tego i przyszłych wersji zapoznawczych. Konieczne będzie ukończenie profilu i umowy dotyczącej ochrony prywatności.