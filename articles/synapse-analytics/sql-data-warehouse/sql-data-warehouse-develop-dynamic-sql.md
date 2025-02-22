---
title: Korzystanie z dynamicznego języka SQL
description: Porady dotyczące rozwiązań programistycznych korzystających z dynamicznego języka SQL dla dedykowanych pul SQL w usłudze Azure Synapse Analytics.
services: synapse-analytics
author: MSTehrani
manager: craigg
ms.service: synapse-analytics
ms.topic: conceptual
ms.subservice: sql-dw
ms.date: 04/17/2018
ms.author: emtehran
ms.reviewer: igorstan
ms.custom: seo-lt-2019, azure-synapse
ms.openlocfilehash: 52bc7bdc63f754d52bf4a69097c1dd309a6dc3ec
ms.sourcegitcommit: 6a350f39e2f04500ecb7235f5d88682eb4910ae8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96462775"
---
# <a name="dynamic-sql-for-dedicated-sql-pools-in-azure-synapse-analytics"></a>Dynamiczne SQL dla dedykowanych pul SQL w usłudze Azure Synapse Analytics

W tym artykule przedstawiono wskazówki dotyczące rozwiązań programistycznych korzystających z dynamicznego języka SQL w dedykowanych pulach SQL.

## <a name="dynamic-sql-example"></a>Dynamiczny przykład SQL

Podczas tworzenia kodu aplikacji dla dedykowanych pul SQL może być konieczne użycie dynamicznego SQL w celu zapewnienia elastycznych, ogólnych i modularnych rozwiązań. Dedykowane pule SQL nie obsługują w tym momencie typów danych obiektów BLOB.

Nieobsługiwane typy danych obiektów BLOB mogą ograniczać rozmiar ciągów, ponieważ typy danych obiektów BLOB zawierają zarówno typy varchar (max), jak i nvarchar (max).

Jeśli w kodzie aplikacji użyto tych typów do kompilowania dużych ciągów, należy podzielić kod na fragmenty i zamiast tego użyć instrukcji EXEC.

Prosty przykład:

```sql
DECLARE @sql_fragment1 VARCHAR(8000)=' SELECT name '
,       @sql_fragment2 VARCHAR(8000)=' FROM sys.system_views '
,       @sql_fragment3 VARCHAR(8000)=' WHERE name like ''%table%''';

EXEC( @sql_fragment1 + @sql_fragment2 + @sql_fragment3);
```

Jeśli ciąg jest krótki, można użyć [sp_executesql](/sql/relational-databases/system-stored-procedures/sp-executesql-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest) jak zwykle.

> [!NOTE]
> Instrukcje wykonane jako dynamiczny kod SQL będą nadal podlegać wszystkim regułom walidacji T-SQL.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej porad programistycznych, zobacz [Omówienie projektowania](sql-data-warehouse-overview-develop.md).
