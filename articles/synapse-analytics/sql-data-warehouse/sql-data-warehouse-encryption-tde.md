---
title: Transparent Data Encryption (Portal) dla dedykowanej puli SQL (dawniej SQL DW)
description: Transparent Data Encryption (TDE) dla dedykowanej puli SQL (dawniej SQL DW) w usłudze Azure Synapse Analytics
services: synapse-analytics
author: julieMSFT
manager: craigg
ms.service: synapse-analytics
ms.topic: conceptual
ms.subservice: sql-dw
ms.date: 04/30/2019
ms.author: jrasnick
ms.reviewer: rortloff
ms.custom: seo-lt-2019
ms.openlocfilehash: 45c7b53d3bbe0c57e96fc5435650c4e86b0cb032
ms.sourcegitcommit: 6a350f39e2f04500ecb7235f5d88682eb4910ae8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2020
ms.locfileid: "96455264"
---
# <a name="get-started-with-transparent-data-encryption-tde-for-dedicated-sql-pool-formerly-sql-dw-in-azure-synapse-analytics"></a>Wprowadzenie do Transparent Data Encryption (TDE) dla dedykowanej puli SQL (dawniej SQL DW) w usłudze Azure Synapse Analytics

> [!div class="op_single_selector"]
>
> * [Przegląd zabezpieczeń](sql-data-warehouse-overview-manage-security.md)
> * [Authentication](sql-data-warehouse-authentication.md)
> * [Szyfrowanie (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Szyfrowanie (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)

## <a name="required-permissions"></a>Wymagane uprawnienia

Aby włączyć Transparent Data Encryption (TDE), musisz być administratorem lub członkiem roli dbmanager.

## <a name="enabling-encryption"></a>Włączanie szyfrowania

Aby włączyć TDE, wykonaj następujące czynności:

1. Otwórz bazę danych w [Azure Portal](https://portal.azure.com)
2. W bloku baza danych kliknij przycisk **Ustawienia**
3. Wybierz ustawienia portalu dla opcji **przezroczystego szyfrowania danych** ![](./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png)
4. Wybierz ustawienie **On** ![ Ustawienia portalu na](./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png)
5. Wybierz pozycję **Zapisz** 
    ![ Ustawienia portalu Zapisz](./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png)  

## <a name="disabling-encryption"></a>Wyłączanie szyfrowania

Aby wyłączyć TDE, wykonaj następujące czynności:

1. Otwórz bazę danych w [Azure Portal](https://portal.azure.com)
2. W bloku baza danych kliknij przycisk **Ustawienia**
3. Wybierz ustawienia portalu dla opcji **przezroczystego szyfrowania danych** ![](./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png)
4. Wybierz wyłączone **Off** ![ Ustawienia portalu](./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png)
5. Wybierz pozycję **Zapisz** 
    ![ ustawienie portalu Zapisz 2](./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png)  

## <a name="encryption-dmvs"></a>Szyfrowanie widoków DMV

Szyfrowanie można potwierdzić przy użyciu następujących widoków DMV:

* [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest)
* [sys.dm_pdw_nodes_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest)
