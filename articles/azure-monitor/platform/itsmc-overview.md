---
title: Przegląd łącznik zarządzania usługami IT
description: Ten artykuł zawiera omówienie łącznik zarządzania usługami IT (ITSMC).
ms.subservice: logs
ms.topic: conceptual
author: nolavime
ms.author: v-jysur
ms.date: 12/16/2020
ms.custom: references_regions
ms.openlocfilehash: 93b6160b495b609e23e10b3f709d130792067423
ms.sourcegitcommit: 7e97ae405c1c6c8ac63850e1b88cf9c9c82372da
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/29/2020
ms.locfileid: "97803786"
---
# <a name="it-service-management-connector-overview"></a>Przegląd łącznik zarządzania usługami IT

:::image type="icon" source="media/itsmc-overview/itsmc-symbol.png":::

Łącznik zarządzania usługami IT (ITSMC) umożliwia połączenie platformy Azure z obsługiwanym produktem lub usługą zarządzania usługami IT (narzędzia ITSM).

Usługi platformy Azure, takie jak Azure Log Analytics i Azure Monitor, udostępniają narzędzia umożliwiające wykrywanie, analizowanie i rozwiązywanie problemów z zasobami platformy Azure i spoza niej. Jednak elementy robocze związane z problemem zwykle znajdują się w narzędzia ITSM produktu lub usłudze. ITSMC zapewnia dwukierunkową połączenie między narzędziami platformy Azure i narzędzia ITSM, które ułatwiają szybsze rozwiązywanie problemów.

## <a name="configuration-steps"></a>Kroki konfiguracji

ITSMC obsługuje połączenia z następującymi narzędziami narzędzia ITSM:

-   ServiceNow
-   System Center Service Manager
-   Provance
-   Cherwell

   >[!NOTE]
> Firma Microsoft proponuje naszym klientom Cherwell i Provance użycie [akcji elementu webhook](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups#webhook) w Cherwell i Provance Endpoint jako innego rozwiązania do integracji.

Za pomocą ITSMC można:

-  Utwórz elementy robocze w narzędziu narzędzia ITSM na podstawie alertów platformy Azure (alertów metryk, alertów dziennika aktywności i alertów Log Analytics).
-  Opcjonalnie możesz zsynchronizować zdarzenie i dane żądania zmiany z narzędzia Narzędzia ITSM w obszarze roboczym usługi Azure Log Analytics.

Aby uzyskać informacje na temat warunków prawnych i zasad zachowania poufności informacji, zobacz zasady [zachowania poufności informacji firmy Microsoft](https://go.microsoft.com/fwLink/?LinkID=522330&clcid=0x9).

Możesz rozpocząć korzystanie z ITSMC, wykonując następujące czynności:

1. [Skonfiguruj środowisko narzędzia ITSM, aby akceptować alerty z platformy Azure.](./itsmc-connections.md)
1. [Skonfiguruj rozwiązanie Azure narzędzia ITSM](./itsmc-definition.md#add-it-service-management-connector)
1. [Skonfiguruj łącznik usługi Azure narzędzia ITSM dla środowiska narzędzia ITSM.](./itsmc-definition.md#create-an-itsm-connection)
1. [Skonfiguruj grupę akcji, aby korzystać z łącznika narzędzia ITSM.](./itsmc-definition.md#use-itsmc)

## <a name="next-steps"></a>Następne kroki

* [Rozwiązywanie problemów w łączniku ITSM](./itsmc-resync-servicenow.md)