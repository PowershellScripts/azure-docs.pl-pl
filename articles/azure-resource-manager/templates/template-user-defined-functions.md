---
title: Funkcje zdefiniowane przez użytkownika w szablonach
description: Opisuje sposób definiowania i używania funkcji zdefiniowanych przez użytkownika w szablonie Azure Resource Manager (szablon ARM).
ms.topic: conceptual
ms.date: 03/09/2020
ms.openlocfilehash: f428fa3bc827af3820ad9f928f4f92b881c9c84c
ms.sourcegitcommit: 2aa52d30e7b733616d6d92633436e499fbe8b069
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/06/2021
ms.locfileid: "97934683"
---
# <a name="user-defined-functions-in-arm-template"></a>Funkcje zdefiniowane przez użytkownika w szablonie ARM

W ramach szablonu można tworzyć własne funkcje. Te funkcje są dostępne do użycia w szablonie. Funkcje zdefiniowane przez użytkownika są niezależne od [standardowych funkcji szablonów](template-functions.md) , które są automatycznie dostępne w ramach szablonu. Utwórz własne funkcje, jeśli masz skomplikowane wyrażenia, które są wielokrotnie używane w szablonie.

W tym artykule opisano sposób dodawania funkcji zdefiniowanych przez użytkownika w szablonie Azure Resource Manager (szablon ARM).

## <a name="define-the-function"></a>Zdefiniuj funkcję

Funkcje wymagają wartości przestrzeni nazw, aby uniknąć konfliktów nazw z funkcjami szablonu. Poniższy przykład pokazuje funkcję, która zwraca unikatową nazwę:

```json
"functions": [
  {
    "namespace": "contoso",
    "members": {
      "uniqueName": {
        "parameters": [
          {
            "name": "namePrefix",
            "type": "string"
          }
        ],
        "output": {
          "type": "string",
          "value": "[concat(toLower(parameters('namePrefix')), uniqueString(resourceGroup().id))]"
        }
      }
    }
  }
],
```

## <a name="use-the-function"></a>Korzystanie z funkcji

Poniższy przykład pokazuje szablon, który zawiera funkcję zdefiniowaną przez użytkownika. Używa tej funkcji, aby uzyskać unikatową nazwę konta magazynu. Szablon ma parametr o nazwie `storageNamePrefix` , który przekazuje jako parametr do funkcji.

```json
{
 "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "parameters": {
   "storageNamePrefix": {
     "type": "string",
     "maxLength": 11
   }
 },
 "functions": [
  {
    "namespace": "contoso",
    "members": {
      "uniqueName": {
        "parameters": [
          {
            "name": "namePrefix",
            "type": "string"
          }
        ],
        "output": {
          "type": "string",
          "value": "[concat(toLower(parameters('namePrefix')), uniqueString(resourceGroup().id))]"
        }
      }
    }
  }
],
 "resources": [
   {
     "type": "Microsoft.Storage/storageAccounts",
     "apiVersion": "2019-04-01",
     "name": "[contoso.uniqueName(parameters('storageNamePrefix'))]",
     "location": "South Central US",
     "sku": {
       "name": "Standard_LRS"
     },
     "kind": "StorageV2",
     "properties": {
       "supportsHttpsTrafficOnly": true
     }
   }
 ]
}
```

## <a name="limitations"></a>Ograniczenia

Podczas definiowania funkcji użytkownika istnieją pewne ograniczenia:

* Funkcja nie może uzyskać dostępu do zmiennych.
* Funkcja może używać tylko parametrów, które są zdefiniowane w funkcji. Gdy używana jest funkcja [Parameters](template-functions-deployment.md#parameters) w funkcji zdefiniowanej przez użytkownika, są ograniczone do parametrów tej funkcji.
* Funkcja nie może wywoływać innych funkcji zdefiniowanych przez użytkownika.
* Funkcja nie może używać funkcji [Reference](template-functions-resource.md#reference) ani żadnej z funkcji [list](template-functions-resource.md#list) .
* Parametry funkcji nie mogą mieć wartości domyślnych.

## <a name="next-steps"></a>Następne kroki

* Aby dowiedzieć się więcej o dostępnych właściwościach funkcji zdefiniowanych przez użytkownika, zobacz [Omówienie struktury i składni szablonów usługi ARM](template-syntax.md).
* Listę dostępnych funkcji szablonu można znaleźć w temacie [funkcje szablonu ARM](template-functions.md).
