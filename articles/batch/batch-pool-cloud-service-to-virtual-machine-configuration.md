---
title: Migruj konfigurację puli partii z Cloud Services do Virtual Machines
description: Dowiedz się, jak zaktualizować konfigurację puli do najnowszej i zalecanej konfiguracji
ms.topic: how-to
ms.date: 1/6/2021
ms.openlocfilehash: d987a185efb6593fd541dd14fa74b6c4d3ca41be
ms.sourcegitcommit: c7153bb48ce003a158e83a1174e1ee7e4b1a5461
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/15/2021
ms.locfileid: "98234311"
---
# <a name="migrate-batch-pool-configuration-from-cloud-services-to-virtual-machines"></a>Migruj konfigurację puli partii z Cloud Services do Virtual Machines

Pule usługi Batch można tworzyć przy użyciu [cloudServiceConfiguration](https://docs.microsoft.com/rest/api/batchservice/pool/add#cloudserviceconfiguration) lub [virtualMachineConfiguration](https://docs.microsoft.com/rest/api/batchservice/pool/add#virtualmachineconfiguration). "virtualMachineConfiguration" jest zalecaną konfiguracją, ponieważ obsługuje ona wszystkie możliwości partii. pule "cloudServiceConfiguration" nie obsługują wszystkich funkcji i nie są planowane żadne nowe funkcje.

W przypadku używania pul "cloudServiceConfiguration" zdecydowanie zaleca się przechodzenie do korzystania z pul "virtualMachineConfiguration". Dzięki temu można korzystać ze wszystkich możliwości usługi Batch, takich jak Rozszerzona funkcja [wybierania maszyn](batch-pool-vm-sizes.md)wirtualnych, maszyn wirtualnych z systemem Linux, [kontenerów](batch-docker-container-workloads.md), [Azure Resource Manager sieci wirtualnych](batch-virtual-network.md)i [szyfrowania dysków węzłowych](disk-encryption.md).

W tym artykule opisano sposób migracji do programu "virtualMachineConfiguration".

## <a name="new-pools-are-required"></a>Wymagane są nowe pule

Istniejących aktywnych pul nie można zaktualizować z "cloudServiceConfiguration" do "virtualMachineConfiguration", należy utworzyć nowe pule. Tworzenie pul przy użyciu "virtualMachineConfiguration" jest obsługiwane przez wszystkie interfejsy API usługi Batch, narzędzia wiersza polecenia, Azure Portal i Batch Explorer interfejs użytkownika.

**Samouczki dotyczące [platformy .NET](tutorial-parallel-dotnet.md) i języka [Python](tutorial-parallel-python.md) zawierają przykłady tworzenia puli przy użyciu elementu "virtualMachineConfiguration".**

## <a name="pool-configuration-differences"></a>Różnice konfiguracji puli

Podczas aktualizowania konfiguracji puli należy wziąć pod uwagę następujące kwestie:

- węzły puli "cloudServiceConfiguration" to zawsze system operacyjny Windows, a pule "virtualMachineConfiguration" mogą być systemami OPERACYJNYmi Linux lub Windows.
- W porównaniu do pul "cloudServiceConfiguration" pule "virtualMachineConfiguration" mają bogatszy zestaw funkcji, takich jak obsługa kontenerów, dyski danych i szyfrowanie dysków.
- węzły puli "virtualMachineConfiguration" wykorzystują zarządzane dyski systemu operacyjnego. [Typ dysku zarządzanego](../virtual-machines/disks-types.md) , który jest używany dla każdego węzła, zależy od rozmiaru maszyny wirtualnej wybranego dla puli. Jeśli dla puli zostanie określony rozmiar maszyny wirtualnej, na przykład "Standard_D2s_v3" zostanie użyty dysk SSD w warstwie Premium. Jeśli jest określony rozmiar maszyny wirtualnej "inny niż s", na przykład "Standard_D2_v3", zostanie użyty standardowy dysk twardy.

   > [!IMPORTANT]
   > Podobnie jak w przypadku Virtual Machines i Virtual Machine Scale Sets, dysk zarządzany systemu operacyjnego używany dla każdego węzła wiąże się z kosztem, który jest dodatkowym kosztem maszyn wirtualnych. Nie ma kosztu dysku systemu operacyjnego dla węzłów "cloudServiceConfiguration", ponieważ dysk systemu operacyjnego jest tworzony na lokalnym dysku SSD.

- Czasy uruchamiania i usuwania puli i węzła mogą się nieco różnić między pulami "cloudServiceConfiguration" i "virtualMachineConfiguration".

## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [konfiguracjach puli](nodes-and-pools.md#configurations).
- Dowiedz się więcej o [najlepszych rozwiązaniach dotyczących puli](best-practices.md#pools).
- Dokumentacja interfejsu API REST dla [dodawania puli](https://docs.microsoft.com/rest/api/batchservice/pool/add) i [virtualMachineConfiguration](https://docs.microsoft.com/rest/api/batchservice/pool/add#virtualmachineconfiguration).
