---
title: Ankündigungen neuer Features
titleSuffix: Azure Cognitive Search
description: Ankündigungen neuer und erweiterter Features, einschließlich der Umbenennung des Diensts von Azure Search in kognitive Azure-Suche.
manager: nitinme
author: HeidiSteen
ms.author: heidist
ms.service: cognitive-search
ms.topic: conceptual
ms.date: 11/04/2019
ms.openlocfilehash: 247378461a99d42f21a67a2c0aebc7019727f3a0
ms.sourcegitcommit: 428fded8754fa58f20908487a81e2f278f75b5d0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2019
ms.locfileid: "74555141"
---
# <a name="whats-new-in-azure-cognitive-search"></a>Neuerungen in der kognitiven Azure-Suche

Informieren Sie sich über die Neuerungen im Dienst. Legen Sie ein Lesezeichen für diese Seite an, um über den Dienst auf dem Laufenden zu bleiben.

<a name="new-service-name"></a>

## <a name="new-service-name-for-azure-search"></a>Neuer Dienstname für Azure Search

Azure Search wurde jetzt in **kognitive Azure-Suche** umbenannt, um die erweiterte Verwendung von kognitiven Qualifikationen und KI-Verarbeitung bei wichtigen Vorgängen widerzuspiegeln. Während durch kognitive Qualifikationen neue Funktionen hinzugefügt werden, ist die Verwendung von KI ausschließlich optional. Sie können Azure Cognitive Search weiterhin ohne KI verwenden, um umfassende Lösungen für die Volltextsuche zu erstellen, die über private, heterogene, textbasierte Inhalte in einem Index ausgeführt wird, den Sie in der Cloud erstellen und verwalten. 

API-Versionen, NuGet-Pakete, Namespaces und Endpunkte sind unverändert. Ihre vorhandenen Suchlösungen sind von der Änderung des Dienstnamens nicht betroffen.

## <a name="feature-announcements"></a>Featureankündigungen

4\. November 2019 – Ignite-Konferenz

+ Mit der [inkrementellen Indizierung (Vorschau)](cognitive-search-incremental-indexing-conceptual.md) können Sie beim Ändern einer Anreicherungspipeline auswählen, welche Schritte erneut verarbeitet werden sollen. Die inkrementelle Indizierung ist besonders nützlich, wenn Sie über Bildinhalte verfügen, die Sie zuvor analysiert haben. Die Ausgabe der kostenintensiven Analyse wird gespeichert und dann als Grundlage für die zusätzliche Indizierung oder Anreicherung verwendet.

<!-- 
+ Custom Entity Lookup is a cognitive skill used during indexing that allows you to provide a list of custom entities (such as part numbers, diseases, or names of locations you care about) that should be found within the text. It supports fuzzy matching, case-insensitive matching, and entity synonyms. -->

+ Die [Dokumentextrahierung (Vorschauversion)](cognitive-search-skill-document-extraction.md) ist eine kognitive Qualifikation, die während der Indizierung verwendet wird und es Ihnen ermöglicht, den Inhalt einer Datei aus einem Skillset zu extrahieren. Bisher fand die Dokumententschlüsselung nur vor der Ausführung von Qualifikationsgruppen statt. Durch diese zusätzliche Qualifikation können Sie diesen Vorgang auch bei der Ausführung von Qualifikationsgruppen durchführen.

+ Die [Textübersetzung (Vorschauversion)](cognitive-search-skill-text-translation.md) ist eine kognitive Qualifikation, die während der Indizierung zum Auswerten von Text verwendet wird und für jeden Datensatz Text zurückgibt, der in die angegebene Zielsprache übersetzt wurde.

+ [Power BI-Vorlagen](https://github.com/Azure-Samples/cognitive-search-templates/blob/master/README.md) können Ihren Visualisierungen und Analysen von angereicherten Inhalten in einem Wissensspeicher in Power BI Desktop neue Impulse verleihen. Diese Vorlage ist für Azure-Tabellenprojektionen konzipiert, die mithilfe des [Assistenten zum Importieren von Daten](knowledge-store-create-portal.md) erstellt wurden.

+ [Azure Data Lake Storage Gen2 (Vorschauversion)](search-howto-index-azure-data-lake-storage.md), die [Cosmos DB-Gremlin-API (Vorschauversion)](search-howto-index-cosmosdb.md) und die [Cosmos DB-Cassandra-API (Vorschauversion)](search-howto-index-cosmosdb.md) werden nun in Indexern unterstützt. Füllen Sie [dieses Formular](https://aka.ms/azure-cognitive-search/indexer-preview) aus, um sich zu registrieren. Sie erhalten eine Bestätigungs-E-Mail, sobald Sie in das Vorschauprogramm aufgenommen wurden.

24. Juli 2019

+ In der [Azure Government-Cloud](../azure-government/documentation-government-services-webandmobile.md#azure-cognitive-search) allgemein verfügbar.

## <a name="service-updates"></a>Dienstupdates

[Ankündigungen von Dienstupdates](https://azure.microsoft.com/updates/?product=search&status=all) für die kognitive Azure-Suche finden Sie auf der Azure-Website.