---
title: Benutzeroberflächenelement StorageAccountSelector in Azure | Microsoft-Dokumentation
description: Hier wird das Benutzeroberflächenelement Microsoft.Storage.StorageAccountSelector für das Azure-Portal beschrieben.
services: managed-applications
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: managed-applications
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2018
ms.author: tomfitz
ms.openlocfilehash: e1f96b42e58bcb09cfc2836c993626a889669fc0
ms.sourcegitcommit: 5cfe977783f02cd045023a1645ac42b8d82223bd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2019
ms.locfileid: "74151459"
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a>Benutzeroberflächenelement „Microsoft.Storage.StorageAccountSelector“

Ein Steuerelement zum Auswählen eines neuen oder vorhandenen Speicherkontos.

## <a name="ui-sample"></a>Benutzeroberflächenbeispiel

Das Steuerelement zeigt den Standardwert an.

![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

Das Steuerelement ermöglicht es dem Benutzer, ein neues Speicherkonto zu erstellen oder ein bereits vorhandenes Speicherkonto auszuwählen.

![Microsoft.Storage.StorageAccountSelector neu](./media/managed-application-elements/microsoft.storage.storageaccountselector-new.png)

## <a name="schema"></a>Schema

```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="sample-output"></a>Beispielausgabe

```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="remarks"></a>Anmerkungen

- Wird `defaultValue.name` angegeben, wird das Element automatisch auf Eindeutigkeit überprüft. Wenn der Name des Speicherkontos nicht eindeutig ist, muss der Benutzer einen anderen Namen angeben oder ein vorhandenes Speicherkonto auswählen.
- Der Standardwert für `defaultValue.type` lautet **Premium_LRS**.
- Alle nicht in `constraints.allowedTypes` angegebenen Typen werden ausgeblendet, und nicht in `constraints.excludedTypes` angegebene Typen werden angezeigt. `constraints.allowedTypes` und `constraints.excludedTypes` sind optional, können jedoch nicht gleichzeitig angegeben werden.
- Wenn **true** für `options.hideExisting` angegeben ist, kann der Benutzer kein vorhandenes Speicherkonto auswählen. Der Standardwert ist **false**.

## <a name="next-steps"></a>Nächste Schritte
* Eine Einführung zum Erstellen von Benutzeroberflächendefinitionen finden Sie unter [Erste Schritte mit „CreateUiDefinition“](create-uidefinition-overview.md).
* Eine Beschreibung der allgemeinen Eigenschaften in Benutzeroberflächenelementen finden Sie unter [CreateUiDefinition-Elemente](create-uidefinition-elements.md).
