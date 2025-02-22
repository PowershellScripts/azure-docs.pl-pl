---
author: alkohli
ms.service: databox
ms.topic: include
ms.date: 12/09/2020
ms.author: alkohli
ms.openlocfilehash: 9ea5fb26a52c967c5296f1a83976e748c86c9e18
ms.sourcegitcommit: 799f0f187f96b45ae561923d002abad40e1eebd6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/24/2020
ms.locfileid: "97763880"
---
Rozmiar maszyny wirtualnej określa ilość zasobów obliczeniowych, takich jak procesor CPU, procesor GPU i pamięć, które są dostępne dla maszyny wirtualnej. Tworzone maszyny wirtualne powinny mieć rozmiar odpowiadający obciążeniu. Mimo że wszystkie maszyny będą uruchomione na tym samym sprzęcie, rozmiary maszyn mają różne limity dostępu do dysku, co ułatwia zarządzanie ogólnym dostępem do dysku na maszynach wirtualnych. Jeśli obciążenie zwiększy się, można również zmienić rozmiar istniejącej maszyny wirtualnej.

Następujące maszyny wirtualne są obsługiwane do tworzenia na Azure Stack urządzeniu brzegowym.

### <a name="dv2-series"></a>Seria Dv2
|Rozmiar     |Procesor wirtualny     |Pamięć (GiB) | Rozmiar dysku zasobu (GiB)  | Rozmiar dysku systemu operacyjnego (GiB) | Maks. liczba dysków danych | Maksymalna liczba kart sieciowych |
|-------------------|----|----|-----|----|------|------------|
|**Standardowa_D1_v2** |1   |3,5 |50   |1000| 4    |2 |
|**Standardowa_D2_v2** |2   |7   |100  |1000| 8    |4 |
|**Standardowa_D3_v2** |4   |14  |200  |1000| 16  |4 |
|**Standardowa_D4_v2** |8   |28  |400  |1000| 32  |8 |
|**Standardowa_D5_v2** |16  |56  |800  |1000| 64  |8 |
|**Standardowa_D11_v2** |2   |14  |100  |1000| 8     |2 |
|**Standardowa_D12_v2** |4   |28  |200  |1000| 16   |4 |
|**Standardowa_D13_v2** |8   |56  |400  |1000| 32  |8 |

### <a name="dsv2-series"></a>Seria DSv2
|Rozmiar     |Procesor wirtualny     |Pamięć (GiB) |  Rozmiar dysku zasobu (GiB)  | Rozmiar dysku systemu operacyjnego (GiB) | Maks. liczba dysków danych| Maksymalna liczba kart sieciowych |
|--------------------|----|----|----|-----|------|-------------|
|**Standardowa_DS1_v2** |1   |3,5 |7  |4000  |1000 |4  |2 |
|**Standard_DS2_v2** |2   |7   |14 |8000  |1000 |8  |4 |
|**Standardowa_DS3_v2** |4   |14  |28 |16000 |1000 |16 |4 |
|**Standardowa_DS4_v2** |8   |28  |56 |32000 |1000 |32 |8 |
|**Standard_DS5_v2** |16  |56  |112|64000 |1000 |64 |8 |
|**Standardowa_DS11_v2**|2   |14  |28 |8000  |1000 |4  |2 |
|**Standardowa_DS12_v2**|4   |28  |56 |16000 |1000 |8  |4 |
|**Standardowa_DS13_v2**|8   |56  |112|32000 |1000 |16 |8 |


Aby uzyskać więcej informacji, przejdź do [serii Dv2 na ogólnego przeznaczenia rozmiary maszyn wirtualnych](../articles/virtual-machines/dv2-dsv2-series.md#dv2-series).

### <a name="ncast4_v3-series-preview"></a>Seria NCasT4_v3 (wersja zapoznawcza)

Te rozmiary są obsługiwane w przypadku maszyn wirtualnych procesora GPU na urządzeniu i są zoptymalizowane pod kątem aplikacji z przyspieszeniem procesora GPU intensywnie korzystających z mocy obliczeniowej. Ta seria koncentruje się na obciążeniach wnioskowania z procesorem GPU Tesla T4 firmy NVIDIA. 

|Rozmiar     |Procesor wirtualny     |Pamięć (GiB) | Rozmiar dysku zasobu (GiB)  |Rozmiar dysku systemu operacyjnego (GiB)| Procesory GPU | Pamięć procesora GPU (GiB) | Maksymalna liczba kart sieciowych |
|---------------------|----|----|-----|-----|-------|--------------|
|**Standard_NC4as_T4_v3** |4   |28  |180   |1000|1 |16   |4 |
|**Standard_NC8as_T4_v3** |8   |56  |360   |1000|1 |16  |8 |

Aby uzyskać więcej informacji, przejdź do [serii NCasT4_v3 na rozmiarach maszyn wirtualnych zoptymalizowanych pod kątem procesora GPU](../articles/virtual-machines/nct4-v3-series.md).

### <a name="f-series"></a>Seria F

Te serie są zoptymalizowane pod kątem obciążeń obliczeniowych i uruchamianych na procesorach Intel Xeon. 

| Rozmiar | vCPU | Pamięć: GiB |Rozmiar dysku zasobu (GiB) |Rozmiar dysku systemu operacyjnego (GiB)|  Maks. liczba dysków danych | Maksymalna liczba kart sieciowych |
|---|---|---|---|---|---|---|---|---|
| Standardowa_F1  | 1  | 2   |16      |1000| 4  |  2 |
| Standardowa_F2 | 2  | 4 |32      |1000| 8  |  4 |
| Standardowa_F4  | 4  | 8 |64   |1000| 16 |  4 |
| Standardowa_F8 | 8 | 16  |132    |1000| 32 |  8 |
| Standardowa_F16 | 16 | 32  |262   |1000| 64 |  8 |
| Standardowa_F1s | 1 | 2  | 4  |1000| 4 | 1 |
| Standardowa_F2s | 2 | 4 |8   |1000| 8 | 4 |
| Standardowa_F4s | 4 | 8 |16 |1000| 16 |  4 |
| Standardowa_F8s | 8 | 16 |32 |1000| 32 |  8 |
| Standardowa_F16s | 16 | 32 |64 |1000| 64 |  8 |

Aby uzyskać więcej informacji, przejdź do [serii Fsv2 w obszarze rozmiary maszyn wirtualnych zoptymalizowanych pod kątem obliczeń](../articles/virtual-machines/fsv2-series.md).

