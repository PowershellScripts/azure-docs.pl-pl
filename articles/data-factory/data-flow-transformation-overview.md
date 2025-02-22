---
title: Mapowanie transformacji przepływu danych — omówienie
description: Przegląd różnych przekształceń dostępnych w mapowaniu przepływu danych
author: dcstwh
ms.author: weetok
manager: anandsub
ms.service: data-factory
ms.topic: conceptual
ms.date: 10/27/2020
ms.openlocfilehash: 9d44890e84e97a413543a4291d1331fee0f04841
ms.sourcegitcommit: d60976768dec91724d94430fb6fc9498fdc1db37
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/02/2020
ms.locfileid: "96490894"
---
# <a name="mapping-data-flow-transformation-overview"></a>Mapowanie transformacji przepływu danych — omówienie

[!INCLUDE[appliesto-adf-asa-md](includes/appliesto-adf-asa-md.md)] 

Poniżej znajduje się lista transformacji, które są obecnie obsługiwane w mapowaniu przepływu danych. Kliknij poszczególne przekształcenia, aby poznać jego szczegóły konfiguracji.

| Nazwa | Kategoria | Opis |
| ---- | -------- | ----------- |
| [Agregacja](data-flow-aggregate.md) | Modyfikator schematu | Zdefiniuj różne typy agregacji, takie jak SUM, MIN, MAX i COUNT pogrupowane według istniejących lub obliczanych kolumn. | 
| [Modyfikuj wiersz](data-flow-alter-row.md) | Modyfikator wiersza | Ustawianie zasad INSERT, DELETE, Update i upsert w wierszach. |
| [Podział warunkowy](data-flow-conditional-split.md) | Wiele danych wejściowych/wyjściowych | Kierowanie wierszy danych do różnych strumieni w oparciu o pasujące warunki. |
| [Kolumna pochodna](data-flow-derived-column.md) | Modyfikator schematu | Generuj nowe kolumny lub Modyfikuj istniejące pola przy użyciu języka wyrażeń przepływu danych. | 
| [Exists](data-flow-exists.md) | Wiele danych wejściowych/wyjściowych | Sprawdź, czy Twoje dane istnieją w innym źródle lub w strumieniu. | 
| [Filtr](data-flow-filter.md) | Modyfikator wiersza | Filtruj wiersz na podstawie warunku. |
| [Spłaszcz](data-flow-flatten.md) | Modyfikator schematu |  Należy zastosować wartości tablicowe w strukturach hierarchicznych, takich jak JSON, i odrzucić je w poszczególnych wierszach. |
| [Dołącz](data-flow-join.md) | Wiele danych wejściowych/wyjściowych |  Połącz dane z dwóch źródeł lub strumieni. |
| [Wyszukiwanie](data-flow-lookup.md) | Wiele danych wejściowych/wyjściowych | Dane referencyjne z innego źródła. |
| [Nowa gałąź](data-flow-new-branch.md) | Wiele danych wejściowych/wyjściowych | Zastosuj wiele zestawów operacji i transformacji dla tego samego strumienia danych. |
| [Przestawianie](data-flow-pivot.md) | Modyfikator schematu | Agregacja, w której co najmniej jedna kolumna grupowania ma swoje unikatowe wartości wierszy przekształcone w pojedyncze kolumny. |
| [Ranga](data-flow-rank.md) | Modyfikator schematu | Generowanie uporządkowanej klasyfikacji na podstawie warunków sortowania |
| [Wybierz](data-flow-select.md) | Modyfikator schematu | Kolumny aliasów i nazwy strumieni oraz upuszczanie lub zmiana kolejności kolumn |
| [Ujście](data-flow-sink.md) | - | Ostateczne miejsce docelowe dla danych |
| [Sortowanie](data-flow-sort.md) | Modyfikator wiersza | Sortuj wiersze przychodzące w bieżącym strumieniu danych |
| [Element źródłowy](data-flow-source.md) | - | Źródło danych dla przepływu danych |
| [Klucz zastępczy](data-flow-surrogate-key.md) | Modyfikator schematu | Dodaj przyrostową wartość klucza niezwiązanej z firmą |
| [Unii](data-flow-union.md) | Wiele danych wejściowych/wyjściowych | Łączenie wielu strumieni danych w pionie |
| [Anulowanie przestawiania](data-flow-unpivot.md) | Modyfikator schematu | Przestawianie kolumn na wartości wierszy |
| [Okno](data-flow-window.md) | Modyfikator schematu |  Zdefiniuj agregacje kolumn w strumieniach danych. |
