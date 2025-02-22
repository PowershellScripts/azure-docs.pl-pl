---
author: cynthn
ms.service: virtual-machines
ms.topic: include
ms.date: 02/10/2020
ms.author: cynthn
ms.openlocfilehash: cd3ff3fce80e66d7cd61636b4416cb2fc28f5e77
ms.sourcegitcommit: 19ffdad48bc4caca8f93c3b067d1cf29234fef47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/06/2021
ms.locfileid: "97956575"
---
| Zasób | Limit |
| --- | --- |
| Maszyny wirtualne na [subskrypcję](https://azure.microsoft.com/pricing/) |25 000<sup>1</sup> na region. |
| Całkowita liczba rdzeni maszyn wirtualnych na [subskrypcję](https://azure.microsoft.com/pricing/) |20<sup>1</sup> na region. Skontaktuj się z pomocą techniczną, aby zwiększyć limit. |
| Łączna liczba rdzeni maszyn wirtualnych platformy Azure na [subskrypcję](https://azure.microsoft.com/pricing/) |20<sup>1</sup> na region. Skontaktuj się z pomocą techniczną, aby zwiększyć limit. |
| Maszyny wirtualne na serię, takie jak Dv2 i F, rdzenie na [subskrypcję](https://azure.microsoft.com/pricing/) |20<sup>1</sup> na region. Skontaktuj się z pomocą techniczną, aby zwiększyć limit. |
| [Zestawy dostępności](../articles/virtual-machines/manage-availability.md#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) na subskrypcję |2 500 na region. |
| Maszyny wirtualne na zestaw dostępności | 200 |
| [Grupy umieszczania zbliżeniowe](https://docs.microsoft.com/azure/virtual-machines/windows/proximity-placement-groups-portal) na [grupę zasobów](../articles/azure-resource-manager/management/overview.md#resource-groups) | 800 | 
| Certyfikaty według zestawu dostępności | 199<sup>2</sup> |
| Certyfikaty na subskrypcję |Bez ograniczeń<sup>3</sup> |

<sup>1</sup> domyślne limity różnią się w zależności od typu kategorii oferty, na przykład bezpłatnej wersji próbnej i płatnej zgodnie z rzeczywistym użyciem oraz według serii, takich jak Dv2, F i G. Na przykład domyślna wartość dla subskrypcji Umowa Enterprise to 350.

<sup>2</sup> właściwości, takie jak publiczne klucze SSH, są również wypychane jako certyfikaty i są wliczane do tego limitu. Aby ominąć ten limit, należy użyć [rozszerzenia Azure Key Vault dla systemu Windows](https://docs.microsoft.com/azure/virtual-machines/extensions/key-vault-windows) lub [rozszerzenia Azure Key Vault w systemie Linux](https://docs.microsoft.com/azure/virtual-machines/extensions/key-vault-linux) do zainstalowania certyfikatów.

<sup>3</sup> z Azure Resource Manager certyfikaty są przechowywane w Azure Key Vault. Liczba certyfikatów jest nieograniczona dla subskrypcji. Istnieje limit 1 MB certyfikatów na wdrożenie, które składa się z jednej maszyny wirtualnej lub zestawu dostępności.



> [!NOTE]
> Rdzenie maszyn wirtualnych mają limit regionalny dla regionu. Mają również limit dla regionalnych serii dla poszczególnych rozmiarów, takich jak Dv2 i F. Limity te są wykonywane osobno. Rozważmy na przykład subskrypcję z całkowitym limitem rdzeni maszyn wirtualnych dla regionu Wschodnie stany USA wynoszącym 30, limitem rdzeni dla serii A wynoszącym 30 i limitem rdzeni dla serii D wynoszącym 30. Ta subskrypcja może wdrażać 30 maszyn wirtualnych a1 lub 30 D1 maszyn wirtualnych albo kombinację tych dwóch, aby nie przekroczyć całkowitej liczby 30 rdzeni. Przykładem kombinacji są 10 maszyn wirtualnych a1 i 20 maszyn wirtualnych.  
> <!-- -->
>
