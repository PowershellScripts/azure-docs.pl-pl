---
title: Co nowego w usłudze Azure Backup
description: Dowiedz się więcej o nowych funkcjach w Azure Backup.
ms.topic: conceptual
ms.date: 11/11/2020
ms.openlocfilehash: ba29ddea5d5f096640f2bfc012c44ab06bb3e131
ms.sourcegitcommit: ac7029597b54419ca13238f36f48c053a4492cb6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/29/2020
ms.locfileid: "96309668"
---
# <a name="whats-new-in-azure-backup"></a>Co nowego w usłudze Azure Backup

Azure Backup ciągle ulepsza i zwalnia nowe funkcje, które rozszerzają ochronę danych na platformie Azure. Te nowe funkcje rozszerzają ochronę danych na nowe typy obciążeń, zwiększają bezpieczeństwo i zwiększają dostępność danych kopii zapasowej. Dodaje również nowe możliwości zarządzania, monitorowania i automatyzacji.

Więcej informacji o nowych wersjach można uzyskać, zaznaczając je na tej stronie lub [subskrybując je tutaj](https://azure.microsoft.com/updates/?query=backup).

## <a name="updates-summary"></a>Podsumowanie aktualizacji

- Listopad 2020 r.
  - [Szablon Azure Resource Manager dla kopii zapasowej udziału plików platformy Azure (AFS)](#azure-resource-manager-template-for-afs-backup)
  - [Przyrostowe kopie zapasowe baz danych SAP HANA na maszynach wirtualnych platformy Azure](#incremental-backups-for-sap-hana-databases)
- Wrzesień 2020
  - [Centrum kopii zapasowych](#backup-center)
  - [Tworzenie kopii zapasowej usługi Azure Database for PostgreSQL](#backup-azure-database-for-postgresql)
  - [Selektywne tworzenie kopii zapasowych i przywracanie dysków](#selective-disk-backup-and-restore)
  - [Przywracanie między regionami dla baz danych SQL Server i SAP HANA na maszynach wirtualnych platformy Azure](#cross-region-restore-for-sql-server-and-sap-hana)
  - [Obsługa tworzenia kopii zapasowych maszyn wirtualnych z maksymalnie 32 dyskami](#support-for-backup-of-vms-with-up-to-32-disks)
  - [Uproszczone środowisko konfiguracji kopii zapasowej dla programu SQL na maszynach wirtualnych platformy Azure](#simpler-backup-configuration-for-sql-in-azure-vms)
  - [SAP HANA kopii zapasowych w usłudze RHEL Azure Virtual Machines](#backup-sap-hana-in-rhel-azure-virtual-machines)
  - [Magazyn strefowo nadmiarowy (ZRS) dla danych kopii zapasowej](#zone-redundant-storage-zrs-for-backup-data)
  - [Usuwanie nietrwałe dla obciążeń SQL Server i SAP HANA na maszynach wirtualnych platformy Azure](#soft-delete-for-sql-server-and-sap-hana-workloads)

## <a name="azure-resource-manager-template-for-afs-backup"></a>Szablon Azure Resource Manager dla kopii zapasowej AFS

Azure Backup teraz obsługuje Konfigurowanie kopii zapasowej istniejących udziałów plików platformy Azure przy użyciu szablonu Azure Resource Manager (ARM). Szablon konfiguruje ochronę istniejącego udziału plików platformy Azure, określając odpowiednie szczegóły dotyczące magazynu Recovery Services i zasad tworzenia kopii zapasowych. Opcjonalnie tworzy nowy magazyn Recovery Services i zasady tworzenia kopii zapasowych oraz rejestruje konto magazynu zawierające udział plików w magazynie Recovery Services.

Aby uzyskać więcej informacji, zobacz [Azure Resource Manager szablonów dla Azure Backup](backup-rm-template-samples.md).

## <a name="incremental-backups-for-sap-hana-databases"></a>Przyrostowe kopie zapasowe baz danych SAP HANA

Azure Backup teraz obsługuje przyrostowe kopie zapasowe dla SAP HANA baz danych hostowanych na maszynach wirtualnych platformy Azure. Pozwala to na szybsze i wydajniejsze wykonywanie kopii zapasowych danych SAP HANA.

Aby uzyskać więcej informacji, zobacz [różne opcje dostępne podczas tworzenia zasad tworzenia kopii zapasowych](sap-hana-faq-backup-azure-vm.md#policy) i [tworzenia zasad tworzenia kopii zapasowych dla SAP HANA baz danych](tutorial-backup-sap-hana-db.md#creating-a-backup-policy).

## <a name="backup-center"></a>Centrum kopii zapasowych

Azure Backup włączyła nową natywną funkcję zarządzania do zarządzania całej kopii zapasowej z poziomu konsoli centralnej. Usługa Backup Center umożliwia monitorowanie, obsługę, zarządzanie i optymalizowanie ochrony danych w odpowiedniej skali w jednolity sposób spójny z natywnymi środowiskami zarządzania platformy Azure.

Usługa Backup Center pozwala uzyskać Zagregowany widok spisu między subskrypcjami, lokalizacjami, grupami zasobów, magazynami, a nawet dzierżawcami przy użyciu usługi Azure Lighthouse. Centrum kopii zapasowych to również centrum akcji, z którego można wyzwolić działania związane z tworzeniem kopii zapasowych, takie jak konfigurowanie kopii zapasowej, przywracanie, tworzenie zasad lub magazynów, a wszystko to w jednym miejscu. Ponadto z bezproblemową integracją Azure Policy można teraz zarządzać środowiskiem i śledzić zgodność z perspektywy tworzenia kopii zapasowych. Wbudowane zasady platformy Azure specyficzne dla Azure Backup umożliwiają również konfigurowanie kopii zapasowych na dużą skalę.

Aby uzyskać więcej informacji, zobacz [Omówienie centrum kopii zapasowych](backup-center-overview.md).

## <a name="backup-azure-database-for-postgresql"></a>Tworzenie kopii zapasowej usługi Azure Database for PostgreSQL

Azure Backup i usługi Azure Database zostały połączone w celu utworzenia rozwiązania do tworzenia kopii zapasowych klasy korporacyjnej dla usługi Azure PostgreSQL (teraz w wersji zapoznawczej). Teraz można spełnić wymagania dotyczące ochrony danych i zgodności z zasadami tworzenia kopii zapasowych kontrolowanymi przez klienta, które umożliwiają przechowywanie kopii zapasowych przez maksymalnie 10 lat. Dzięki temu masz szczegółową kontrolę nad zarządzaniem operacjami tworzenia kopii zapasowych i przywracania na poziomie poszczególnych baz danych. Podobnie można przywrócić wiele wersji PostgreSQL lub do magazynu obiektów BLOB.

Aby uzyskać więcej informacji, zobacz [Azure Database for PostgreSQL Backup](backup-azure-database-postgresql.md).

## <a name="selective-disk-backup-and-restore"></a>Selektywne tworzenie kopii zapasowych i przywracanie dysków

Azure Backup obsługuje tworzenie kopii zapasowych wszystkich dysków (systemu operacyjnego i danych) w maszynie wirtualnej przy użyciu rozwiązania do tworzenia kopii zapasowych maszyn wirtualnych. Teraz korzystając z funkcji tworzenia kopii zapasowych i przywracania dysków selektywnych, można utworzyć kopię zapasową podzbioru dysków danych w maszynie wirtualnej. Zapewnia to wydajne i ekonomiczne rozwiązanie dla potrzeb tworzenia kopii zapasowych i przywracania. Każdy punkt odzyskiwania zawiera tylko te dyski, które są uwzględnione w operacji tworzenia kopii zapasowej.

Aby uzyskać więcej informacji, zobacz [selektywne tworzenie kopii zapasowych i przywracanie dysków dla maszyn wirtualnych platformy Azure](selective-disk-backup-restore.md).

## <a name="cross-region-restore-for-sql-server-and-sap-hana"></a>Przywracanie między regionami dla SQL Server i SAP HANA

Po wprowadzeniu operacji przywracania między regionami można teraz zainicjować przywracanie w regionie pomocniczym w systemie, aby ograniczyć rzeczywiste problemy przestoju w regionie podstawowym środowiska. Dzięki temu region pomocniczy jest przywracany całkowicie przez klienta. Azure Backup używa kopii zapasowych replikowanych do regionu pomocniczego na potrzeby takich operacji przywracania.

Teraz oprócz obsługi przywracania między regionami dla usługi Azure Virtual Machines funkcja została rozszerzona o przywracanie baz danych SQL i SAP HANA na maszynach wirtualnych platformy Azure.

Aby uzyskać więcej informacji, zobacz [przywracanie między regionami dla baz danych SQL](restore-sql-database-azure-vm.md#cross-region-restore) i [przywracanie między regionami dla baz danych SAP HANA](sap-hana-db-restore.md#cross-region-restore).

## <a name="support-for-backup-of-vms-with-up-to-32-disks"></a>Obsługa tworzenia kopii zapasowych maszyn wirtualnych z maksymalnie 32 dyskami

Do tej pory Azure Backup obsługiwał 16 dysków zarządzanych na maszynę wirtualną. Teraz Azure Backup obsługuje tworzenie kopii zapasowych do 32 dysków zarządzanych na maszynę wirtualną.

Aby uzyskać więcej informacji, zobacz [Macierz obsługi magazynu maszyn wirtualnych](backup-support-matrix-iaas.md#vm-storage-support).

## <a name="simpler-backup-configuration-for-sql-in-azure-vms"></a>Prostsze Konfigurowanie kopii zapasowych dla bazy danych SQL na maszynach wirtualnych platformy Azure

Konfigurowanie kopii zapasowych SQL Server na maszynach wirtualnych platformy Azure jest teraz jeszcze łatwiejsze dzięki konfiguracji wbudowanej kopii zapasowej zintegrowanej z okienkiem maszyny wirtualnej w Azure Portal. W zaledwie kilku krokach można włączyć tworzenie kopii zapasowej SQL Server w celu ochrony wszystkich istniejących baz danych, a także tych, które zostaną dodane w przyszłości.

Aby uzyskać więcej informacji, zobacz [Tworzenie kopii zapasowej SQL Server z okienka maszyny wirtualnej](backup-sql-server-vm-from-vm-pane.md).

## <a name="backup-sap-hana-in-rhel-azure-virtual-machines"></a>SAP HANA kopii zapasowych w usłudze Azure Virtual Machines RHEL

Azure Backup to natywne rozwiązanie do tworzenia kopii zapasowych dla systemu Azure i jest BackInt z certyfikatem SAP. Azure Backup dodano teraz obsługę Red Hat Enterprise Linux (RHEL), jednego z najczęściej używanych systemów operacyjnych Linux, na których działa SAP HANA.

Aby uzyskać więcej informacji, zobacz [Macierz obsługi scenariusza tworzenia kopii zapasowej bazy danych SAP HANA](sap-hana-backup-support-matrix.md#scenario-support).

## <a name="zone-redundant-storage-zrs-for-backup-data"></a>Magazyn strefowo nadmiarowy (ZRS) dla danych kopii zapasowej

Usługa Azure Storage zapewnia wysoką wydajność, wysoką dostępność i wysoką odporność na dane przy użyciu różnych opcji nadmiarowości. Azure Backup pozwala na rozciągnięcie tych korzyści na kopie zapasowe danych, a także opcje przechowywania kopii zapasowych w magazynie lokalnie nadmiarowy (LRS) i magazyn Geograficznie nadmiarowy (GRS). Teraz dostępne są dodatkowe opcje trwałości z dodatkową obsługą magazynu Strefowo nadmiarowego (ZRS).

Aby uzyskać więcej informacji, zobacz [Ustawianie nadmiarowości magazynu dla magazynu Recovery Services](backup-create-rs-vault.md#set-storage-redundancy).

## <a name="soft-delete-for-sql-server-and-sap-hana-workloads"></a>Usuwanie nietrwałe dla obciążeń SQL Server i SAP HANA

Problemy dotyczące zabezpieczeń, takie jak złośliwe oprogramowanie, programy wymuszającego okup i wtargnięcie, zwiększają się. Te problemy z zabezpieczeniami mogą być kosztowne, w odniesieniu do pieniędzy i danych. Aby ochronić przed takimi atakami, Azure Backup zapewnia funkcje zabezpieczeń, które ułatwiają ochronę danych kopii zapasowej nawet po usunięciu.

Jedną z tych funkcji jest usuwanie nietrwałe. W przypadku usuwania nietrwałego, nawet jeśli złośliwy aktor usuwa kopię zapasową (lub przypadkowo usunięto dane kopii zapasowej), dane kopii zapasowej są przechowywane przez 14 dodatkowych dni, umożliwiając odzyskanie tego elementu kopii zapasowej bez utraty danych. Dodatkowe 14 dni przechowywania danych kopii zapasowej w stanie "usuwanie nietrwałe" nie wiążą się z pozostałymi kosztami.

Teraz oprócz obsługi usuwania nietrwałego dla maszyn wirtualnych platformy Azure SQL Server i SAP HANA obciążenia na maszynach wirtualnych platformy Azure są również chronione za pomocą usuwania nietrwałego.

Aby uzyskać więcej informacji, zobacz [usuwanie nietrwałe dla programu SQL Server na maszynie wirtualnej platformy Azure i SAP HANA w obciążeniach maszyn wirtualnych platformy Azure](soft-delete-sql-saphana-in-azure-vm.md).

## <a name="next-steps"></a>Następne kroki

- [Wskazówki i najlepsze rozwiązania Azure Backup](guidance-best-practices.md)
