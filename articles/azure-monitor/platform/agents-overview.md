---
title: Omówienie agentów monitorowania platformy Azure | Microsoft Docs
description: Ten artykuł zawiera szczegółowe omówienie dostępnych agentów platformy Azure, które obsługują monitorowanie maszyn wirtualnych hostowanych na platformie Azure lub w środowisku hybrydowym.
services: azure-monitor
ms.subservice: ''
ms.topic: conceptual
author: bwren
ms.author: bwren
ms.date: 11/21/2020
ms.openlocfilehash: 8b9a79ee32d7a81fee64e40b85272877b7d87589
ms.sourcegitcommit: d79513b2589a62c52bddd9c7bd0b4d6498805dbe
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2020
ms.locfileid: "97674202"
---
# <a name="overview-of-azure-monitor-agents"></a>Omówienie agentów Azure Monitor

Maszyny wirtualne i inne zasoby obliczeniowe wymagają od agenta zebrania danych monitorowania wymaganych do mierzenia wydajności i dostępności systemu operacyjnego gościa oraz obciążeń. W tym artykule opisano agentów używanych przez Azure Monitor i można określić, które z nich muszą spełniać wymagania dotyczące konkretnego środowiska.

> [!NOTE]
> Azure Monitor ma obecnie wielu agentów z powodu ostatniej konsolidacji Azure Monitor i Log Analytics. Chociaż może się nakładać na swoje funkcje, każdy z nich ma unikatowe możliwości. W zależności od wymagań może być potrzebny co najmniej jeden Agent na maszynach wirtualnych. 

Może istnieć określony zestaw wymagań, które nie mogą być w pełni spełnione przy użyciu jednego agenta dla określonej maszyny wirtualnej. Można na przykład użyć alertów metryk, które wymagają rozszerzenia diagnostyki platformy Azure, ale również skorzystać z funkcjonalności Azure Monitor dla maszyn wirtualnych, która wymaga agenta Log Analytics i agenta zależności. W takich przypadkach można używać wielu agentów i jest to typowy scenariusz dla klientów, którzy wymagają funkcjonalności z każdego z nich.

## <a name="summary-of-agents"></a>Podsumowanie agentów

W poniższych tabelach przedstawiono krótkie porównanie Azure Monitor agentów dla systemów Windows i Linux. Więcej szczegółowych informacji na ten temat znajduje się w sekcji poniżej.

> [!NOTE]
> Agent Azure Monitor jest obecnie w wersji zapoznawczej z ograniczonymi możliwościami. Ta tabela zostanie zaktualizowana 

### <a name="windows-agents"></a>Agenci dla systemu Windows

| | Agent Azure Monitor (wersja zapoznawcza) | Diagnostyka<br>rozszerzenie (funkcji wad) | Log Analytics<br>agent | Zależność<br>agent |
|:---|:---|:---|:---|:---|
| **Obsługiwane środowiska** | Azure<br>Inna chmura (Azure ARC)<br>Lokalna (łuk systemu Azure)  | Azure | Azure<br>Inna chmura<br>Lokalnie | Azure<br>Inna chmura<br>Magazyn lokalny | 
| **Wymagania dotyczące agenta**  | Brak | Brak | Brak | Wymaga agenta Log Analytics |
| **Zbierane dane** | Dzienniki zdarzeń<br>Wydajność | Dzienniki zdarzeń<br>zdarzenia ETW<br>Wydajność<br>Dzienniki na podstawie plików<br>Dzienniki usług IIS<br>Dzienniki aplikacji .NET<br>Zrzuty awaryjne<br>Dzienniki diagnostyki agentów | Dzienniki zdarzeń<br>Wydajność<br>Dzienniki na podstawie plików<br>Dzienniki usług IIS<br>Szczegółowe informacje i rozwiązania<br>Inne usługi | Zależności procesów<br>Metryki połączenia sieciowego |
| **Dane wysyłane do** | Dzienniki usługi Azure Monitor<br>Metryki usługi Azure Monitor | Azure Storage<br>Metryki usługi Azure Monitor<br>Centrum zdarzeń | Dzienniki usługi Azure Monitor | Dzienniki usługi Azure Monitor<br>(za poorednictwem agenta Log Analytics) |
| **Usługi i**<br>**oferowanych**<br>**obsługiwał** | Log Analytics<br>Eksplorator metryk | Eksplorator metryk | Usługa Azure Monitor dla maszyn wirtualnych<br>Log Analytics<br>Azure Automation<br>Azure Security Center<br>Usługa Azure Sentinel | Usługa Azure Monitor dla maszyn wirtualnych<br>Mapa usługi |

### <a name="linux-agents"></a>Agenci dla systemu Linux

| | Agent Azure Monitor (wersja zapoznawcza) | Diagnostyka<br>rozszerzenie (LAD) | Telegraf<br>agent | Log Analytics<br>agent | Zależność<br>agent |
|:---|:---|:---|:---|:---|:---|
| **Obsługiwane środowiska** | Azure<br>Inna chmura (Azure ARC)<br>Lokalna (łuk łuku) | Azure | Azure<br>Inna chmura<br>Lokalnie | Azure<br>Inna chmura<br>Lokalnie | Azure<br>Inna chmura<br>Magazyn lokalny |
| **Wymagania dotyczące agenta**  | Brak | Brak | Brak | Brak | Wymaga agenta Log Analytics |
| **Zbierane dane** | Dziennik systemu<br>Wydajność | Dziennik systemu<br>Wydajność | Wydajność | Dziennik systemu<br>Wydajność| Zależności procesów<br>Metryki połączenia sieciowego |
| **Dane wysyłane do** | Dzienniki usługi Azure Monitor<br>Metryki usługi Azure Monitor | Azure Storage<br>Centrum zdarzeń | Metryki usługi Azure Monitor | Dzienniki usługi Azure Monitor | Dzienniki usługi Azure Monitor<br>(za poorednictwem agenta Log Analytics) |
| **Usługi i**<br>**oferowanych**<br>**obsługiwał** | Log Analytics<br>Eksplorator metryk | | Eksplorator metryk | Usługa Azure Monitor dla maszyn wirtualnych<br>Log Analytics<br>Azure Automation<br>Azure Security Center<br>Usługa Azure Sentinel | Usługa Azure Monitor dla maszyn wirtualnych<br>Mapa usługi |


## <a name="azure-monitor-agent-preview"></a>Agent Azure Monitor (wersja zapoznawcza)
[Agent Azure monitor](azure-monitor-agent-overview.md) jest obecnie w wersji zapoznawczej i zastąpi agenta log Analytics i agenta telegraf dla maszyn wirtualnych z systemami Windows i Linux. Można wysyłać dane do dzienników Azure Monitor i metryk Azure Monitor i używać [zasad zbierania danych (DCR)](data-collection-rule-overview.md) , które zapewniają bardziej skalowalną metodę konfigurowania zbierania i lokalizacji docelowych danych dla każdego agenta.

Użyj agenta Azure Monitor, jeśli zachodzi taka potrzeba:

- Zbierz dzienniki gościa i metryki z dowolnej maszyny wirtualnej na platformie Azure, w innych chmurach lub lokalnie. (Usługa Azure Arc jest wymagana w przypadku maszyn wirtualnych poza platformą Azure). 
- Wysyłaj dane do dzienników Azure Monitor i Azure Monitor metryki analizy za pomocą Azure Monitor. 
- Wyślij dane do usługi Azure Storage w celu archiwizacji.
- Wyślij dane do narzędzi innych firm przy użyciu [usługi Azure Event Hubs](diagnostics-extension-stream-event-hubs.md).
- Zarządzaj zabezpieczeniami maszyn wirtualnych przy użyciu [Azure Security Center](../../security-center/security-center-introduction.md)  lub [platformy Azure](../../sentinel/overview.md). (Niedostępne w wersji zapoznawczej).

Ograniczenia Azure Monitor agenta obejmują:

- Obecnie w publicznej wersji zapoznawczej. Zobacz [bieżące ograniczenia](azure-monitor-agent-overview.md#current-limitations) dotyczące listy ograniczeń w ramach publicznej wersji zapoznawczej.

## <a name="log-analytics-agent"></a>Agent usługi Log Analytics

[Agent log Analytics](log-analytics-agent.md) zbiera dane monitorowania z systemu operacyjnego gościa i obciążeń maszyn wirtualnych na platformie Azure, innych dostawców chmury i lokalnie. Wysyła dane do obszaru roboczego Log Analytics. Agent Log Analytics jest tym samym agentem, który jest używany przez System Center Operations Manager, i można korzystać z agentów wieloznacznych, aby komunikować się z grupą zarządzania i Azure Monitor jednocześnie. Ten agent jest również wymagany przez niektóre szczegółowe informacje w Azure Monitor i innych usługach platformy Azure.


> [!NOTE]
> Agent Log Analytics dla systemu Windows jest często określany jako Microsoft Monitoring Agent (MMA). Agent Log Analytics dla systemu Linux jest często nazywany agentem pakietu OMS.



Użyj agenta Log Analytics, jeśli zachodzi taka potrzeba:

* Zbieraj dzienniki i dane wydajności z maszyn wirtualnych lub fizycznych z platformy Azure lub poza nią. 
* Wyślij dane do obszaru roboczego Log Analytics, aby korzystać z funkcji obsługiwanych przez [dzienniki Azure monitor](data-platform-logs.md) , takie jak [zapytania dziennika](../log-query/log-query-overview.md).
* Użyj [Azure monitor dla maszyn wirtualnych](../insights/vminsights-overview.md) , która pozwala monitorować maszyny wirtualne w odpowiedniej skali i monitoruje ich procesy oraz zależności od innych zasobów i procesów zewnętrznych.  
* Zarządzaj zabezpieczeniami maszyn wirtualnych przy użyciu [Azure Security Center](../../security-center/security-center-introduction.md)  lub [platformy Azure](../../sentinel/overview.md).
* Użyj [Azure Automation zarządzania aktualizacjami](../../automation/update-management/overview.md), [Azure Automation konfiguracji stanu](../../automation/automation-dsc-overview.md)lub [Azure Automation Change Tracking i spisu](../../automation/change-tracking/overview.md) , aby zapewnić kompleksowe zarządzanie maszynami wirtualnymi platformy Azure
* Użyj różnych [rozwiązań](../monitor-reference.md#insights-and-core-solutions) do monitorowania określonej usługi lub aplikacji.

Ograniczenia Log Analytics agenta obejmują:

- Nie można wysyłać danych do metryk Azure Monitor, usługi Azure Storage ani Event Hubs platformy Azure.
- Trudne skonfigurowanie unikatowych definicji monitorowania dla poszczególnych agentów.
- Trudno zarządzać na dużą skalę, ponieważ każda maszyna wirtualna ma unikatową konfigurację.

## <a name="azure-diagnostics-extension"></a>Rozszerzenie diagnostyki platformy Azure

[Rozszerzenie Diagnostyka Azure](diagnostics-extension-overview.md) zbiera dane monitorowania z systemu operacyjnego gościa oraz obciążeń maszyn wirtualnych platformy Azure i innych zasobów obliczeniowych. Polega ona głównie na zbieraniu danych do usługi Azure Storage, ale również umożliwia zdefiniowanie ujścia danych w celu wysyłania danych do innych miejsc docelowych, takich jak metryki Azure Monitor i Event Hubs platformy Azure.

Użyj rozszerzenia diagnostyki platformy Azure, jeśli zachodzi taka potrzeba:

- Wyślij dane do usługi Azure Storage w celu archiwizacji lub Przeanalizuj je za pomocą narzędzi, takich jak [Eksplorator usługi Azure Storage](../../vs-azure-tools-storage-manage-with-storage-explorer.md).
- Wyślij dane do [metryk Azure monitor](data-platform-metrics.md) , aby przeanalizować je za pomocą [Eksploratora metryk](metrics-getting-started.md) i korzystać z funkcji, takich jak [alerty metryk](./alerts-metric-overview.md) niemal w czasie rzeczywistym i [Automatyczne skalowanie](autoscale-overview.md) (tylko system Windows).
- Wyślij dane do narzędzi innych firm przy użyciu [usługi Azure Event Hubs](diagnostics-extension-stream-event-hubs.md).
- Zbierz [diagnostykę rozruchu](../../virtual-machines/troubleshooting/boot-diagnostics.md) , aby zbadać problemy z rozruchem maszyny wirtualnej.

Ograniczenia rozszerzenia usługi Azure Diagnostics obejmują:

- Może być używany tylko z zasobami platformy Azure.
- Ograniczona możliwość wysyłania danych do dzienników Azure Monitor.

## <a name="telegraf-agent"></a>Agent telegraf

[Agent InfluxData telegraf](collect-custom-metrics-linux-telegraf.md) jest używany do zbierania danych wydajności z komputerów z systemem Linux do metryk Azure monitor.

Użyj agenta telegraf, jeśli chcesz:

* Wyślij dane do [metryk Azure monitor](data-platform-metrics.md) , aby przeanalizować je za pomocą [Eksploratora metryk](metrics-getting-started.md) i korzystać z funkcji, takich jak [alerty metryk](./alerts-metric-overview.md) niemal w czasie rzeczywistym i [Automatyczne skalowanie](autoscale-overview.md) (tylko system Linux). 



## <a name="dependency-agent"></a>Agent zależności

Agent zależności zbiera odnalezione dane dotyczące procesów uruchomionych na maszynie wirtualnej i zewnętrznych zależności procesów. 

Użyj agenta zależności, jeśli zachodzi taka potrzeba:

* Użyj funkcji map [Azure monitor dla maszyn wirtualnych](../insights/vminsights-overview.md) lub [Service map](../insights/service-map.md) rozwiązanie.

Podczas korzystania z agenta zależności należy wziąć pod uwagę następujące kwestie:

- Agent zależności wymaga zainstalowania agenta Log Analytics na tej samej maszynie wirtualnej.
- Na maszynach wirtualnych z systemem Linux należy zainstalować agenta Log Analytics przed rozszerzeniem diagnostyki platformy Azure.

## <a name="virtual-machine-extensions"></a>Rozszerzenia maszyny wirtualnej

Log Analytics rozszerzenie dla [systemów Windows](../../virtual-machines/extensions/oms-windows.md) i [Linux](../../virtual-machines/extensions/oms-linux.md) Zainstaluj agenta log Analytics na maszynach wirtualnych platformy Azure. Rozszerzenie zależności Azure Monitor dla [systemu Windows](../../virtual-machines/extensions/agent-dependency-windows.md) i [Linux](../../virtual-machines/extensions/agent-dependency-linux.md) Zainstaluj agenta zależności na maszynach wirtualnych platformy Azure. Są to te same agenci, ale umożliwiają zarządzanie nimi za pomocą [rozszerzeń maszyny wirtualnej](../../virtual-machines/extensions/overview.md). Jeśli to możliwe, należy używać rozszerzeń do instalowania agentów i zarządzania nimi.


## <a name="supported-operating-systems"></a>Obsługiwane systemy operacyjne
W poniższej tabeli wymieniono systemy operacyjne, które są obsługiwane przez agentów Azure Monitor. Zapoznaj się z dokumentacją dla każdego agenta, aby uzyskać unikatowe uwagi i proces instalacji. Zapoznaj się z dokumentacją telegraf dla obsługiwanych systemów operacyjnych. Przyjmuje się, że wszystkie systemy operacyjne są w wersji x64. Architektura x86 nie jest obsługiwana dla żadnego systemu operacyjnego.

### <a name="windows"></a>Windows

| System operacyjny | Agent usługi Azure Monitor | Agent usługi Log Analytics | Agent zależności | Rozszerzenie diagnostyki | 
|:---|:---:|:---:|:---:|:---:|
| Windows Server 2019                                      | X | X | X | X |
| Windows Server 2016                                      | X | X | X | X |
| System Windows Server 2016 Core                                 |   |   |   | X |
| Windows Server 2012 z dodatkiem R2                                   | X | X | X | X |
| Windows Server 2012                                      | X | X | X | X |
| Windows Server 2008 z dodatkiem R2                                   |   | X | X | X |
| Windows 10 Enterprise<br>(w tym wiele sesji) i Pro<br>(Tylko scenariusze serwera)  | X | X | X | X |
| Windows 8 Enterprise i Pro<br>(Tylko scenariusze serwera)  |   | X | X |   |
| Windows 7 z dodatkiem SP1<br>(Tylko scenariusze serwera)                 |   | X | X |   |


### <a name="linux"></a>Linux

| System operacyjny | Agent usługi Azure Monitor | Agent usługi Log Analytics | Agent zależności | Rozszerzenie diagnostyki | 
|:---|:---:|:---:|:---:|:---:
| Amazon Linux 2017,09                                     |   | X |   |   |
| CentOS Linux 8                                           |   | X |   |   |
| CentOS Linux 7                                           | X | X |   | X |
| CentOS Linux 7,8                                         | X | X | X | X |
| CentOS Linux 7,6                                         | X | X | X | X |
| CentOS Linux 6                                           |   | X |   |   |
| CentOS Linux 6.5 +                                        |   | X |   | X |
| Debian 10                                                | X |   |   |   |
| Debian 9                                                 | X | X | x | X |
| Debian 8                                                 |   | X | X | X |
| Debian 7                                                 |   |   |   | X |
| OpenSUSE 13.1 +                                           |   |   |   | X |
| Oracle Linux 8                                           |   | X |   |   |
| Oracle Linux 7                                           | X | X |   | X |
| Oracle Linux 6                                           |   | X |   |   |
| Oracle Linux 6.4 +                                        |   | X |   | X |
| Red Hat Enterprise Linux Server 8                        |   | X |   |   |
| Red Hat Enterprise Linux Server 7                        | X | X | X | X |
| Red Hat Enterprise Linux Server 6                        |   | X | X |   |
| Red Hat Enterprise Linux Server 6.7 +                     |   | X | X | X |
| SUSE Linux Enterprise Server 15,1                        |   | X |   |   |
| SUSE Linux Enterprise Server 15                          | X | X |   |   |
| SUSE Linux Enterprise Server 12                          | X | X | X | X |
| Ubuntu 20,04 LTS                                         |   | X |   |   |
| Ubuntu 18.04 LTS                                         | X | X | X | X |
| Ubuntu 16.04 LTS                                         | X | X | X | X |
| Ubuntu 14,04 LTS                                         |   | X |   | X |


#### <a name="dependency-agent-linux-kernel-support"></a>Obsługa jądra dla agenta zależności
Ponieważ agent zależności działa na poziomie jądra, pomoc techniczna jest również zależna od wersji jądra. W poniższej tabeli wymieniono główne i pomocnicze wersje systemu operacyjnego Linux, które są obsługiwane przez agenta zależności.

| Dystrybucja | Wersja systemu operacyjnego | Wersja jądra |
|:---|:---|:---|
|  Red Hat Linux 7   | 7,6     | 3.10.0-957  |
|                    | 7,5     | 3.10.0-862  |
|                    | 7,4     | 3.10.0-693  |
| Red Hat Linux 6    | 6,10    | 2.6.32 — 754 |
|                    | 6,9     | 2.6.32-696  |
| CentOSPlus         | 6,10    | 2.6.32-754.3.5<br>2.6.32-696.30.1 |
|                    | 6,9     | 2.6.32-696.30.1<br>2.6.32-696.18.7 |
| Ubuntu Server      | 18,04   | 5.3.0-1020<br>5,0 (obejmuje jądro dostosowane do platformy Azure)<br>4,18 *<br> 4,15* |
|                    | 16.04.3 | 4,15. * |
|                    | 16,04   | 4,13.\*<br>4,11.\*<br>4,10.\*<br>4,8.\*<br>4,4.\* |
| SUSE Linux 12 Enterprise Server | 12 SP4 | 4,12. * (obejmuje jądro dostosowane do platformy Azure) |
|                                 | 12 SP3 | 4,4. * |
|                                 | 12 Z DODATKIEM SP2 | 4,4. * |
| Debian                          | 9      | 4,9  | 


## <a name="next-steps"></a>Następne kroki

Więcej informacji na temat każdego z agentów znajduje się w następujących tematach:

- [Przegląd agenta Log Analytics](log-analytics-agent.md)
- [Omówienie rozszerzenia Diagnostyki Azure](diagnostics-extension-overview.md)
- [Zbieranie niestandardowych metryk dla maszyny wirtualnej z systemem Linux za pomocą agenta InfluxData telegraf](collect-custom-metrics-linux-telegraf.md)
