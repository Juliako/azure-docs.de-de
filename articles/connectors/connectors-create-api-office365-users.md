---
title: Herstellen einer Verbindung mit Office 365-Benutzern
description: Verwalten von Benutzerprofilen mit Office 365-Benutzer-REST-APIs und Azure Logic Apps
services: logic-apps
ms.suite: integration
ms.reviewer: klam, logicappspm
ms.date: 08/18/2016
ms.topic: article
tags: connectors
ms.openlocfilehash: addb64a9b43c51af8363caa6f0fb3261a618e893
ms.sourcegitcommit: 76b48a22257a2244024f05eb9fe8aa6182daf7e2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2019
ms.locfileid: "74789517"
---
# <a name="get-started-with-the-office-365-users-connector"></a>Erste Schritte mit dem Office 365-Benutzer-Connector
Stellen Sie eine Verbindung mit der Office 365-Benutzer-API her, um Profile abzurufen, Benutzer zu suchen und vieles mehr. Mit der Office 365-Benutzer-API können Sie folgende Aktionen ausführen:

* Erstellen eines Geschäftsworkflows basierend auf den Daten, die aus der Office 365-Benutzer-API abgerufen werden. 
* Verwenden von Aktionen zum Abrufen von direkt unterstellten Mitarbeitern oder Benutzerprofilen von Vorgesetzten und vieles mehr. Diese Aktionen erhalten eine Antwort und stellen anschließend die Ausgabe anderen Aktionen zur Verfügung. Rufen Sie beispielsweise die direkt unterstellten Mitarbeiter einer Person ab, und aktualisieren Sie mit diesen Informationen eine Azure SQL-Datenbank. 

Erstellen Sie zu Beginn eine Logik-App, wie unter [Erstellen einer Logik-App](../logic-apps/quickstart-create-first-logic-app-workflow.md) beschrieben.

## <a name="create-a-connection-to-office-365-users"></a>Herstellen einer Verbindung mit Office 365-Benutzern
Wenn Sie Ihren Logik-Apps diesen Connector hinzufügen, müssen Sie sich bei Ihrem Office 365-Benutzer-Konto anmelden und den Logik-Apps das Herstellen einer Verbindung mit Ihrem Konto erlauben.

> [!INCLUDE [Steps to create a connection to Office 365 Users](../../includes/connectors-create-api-office365users.md)]
> 
> 

Nachdem Sie eine Verbindung hergestellt haben, geben Sie die Eigenschaften für die Office 365-Benutzer-API ein, z. B. die Benutzer-ID. Diese Eigenschaften werden in diesem Artikel in der **REST-API-Referenz** beschrieben.

## <a name="connector-specific-details"></a>Connectorspezifische Details

Zeigen Sie die in Swagger definierten Trigger und Aktionen sowie mögliche Beschränkungen in den [Connectordetails](/connectors/officeusers/) an.

## <a name="more-connectors"></a>Weitere Connectors
Gehen Sie zur [Liste der APIs](apis-list.md)zurück.