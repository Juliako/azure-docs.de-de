---
title: Kopieren und Transformieren von Daten in Azure Cosmos DB (SQL-API) mithilfe von Data Factory
description: Hier erfahren Sie, wie Sie mithilfe von Data Factory Daten in und aus Azure Cosmos DB (SQL-API) kopieren sowie Daten in Azure Cosmos DB (SQL-API) transformieren.
services: data-factory, cosmosdb
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: conceptual
ms.date: 11/13/2019
ms.author: jingwang
ms.openlocfilehash: 5e9db7c63e1493e1de5593262515040f071186e8
ms.sourcegitcommit: a107430549622028fcd7730db84f61b0064bf52f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/14/2019
ms.locfileid: "74076798"
---
# <a name="copy-and-transform-data-in-azure-cosmos-db-sql-api-by-using-azure-data-factory"></a>Kopieren und Transformieren von Daten in Azure Cosmos DB (SQL-API) mithilfe von Azure Data Factory

> [!div class="op_single_selector" title1="Wählen Sie die von Ihnen verwendete Version des Data Factory-Diensts aus:"]
> * [Version 1](v1/data-factory-azure-documentdb-connector.md)
> * [Aktuelle Version](connector-azure-cosmos-db.md)

In diesem Artikel wird beschrieben, wie Sie Daten mithilfe der Kopieraktivität in Azure Data Factory aus und in Azure Cosmos DB (SQL-API) kopieren sowie Daten mithilfe von Datenfluss in Azure Cosmos DB (SQL API) transformieren. Informationen zu Azure Data Factory finden Sie im [Einführungsartikel](introduction.md).

>[!NOTE]
>Dieser Connector unterstützt nur Cosmos DB SQL-API. Informationen zur MongoDB-API finden Sie unter [Connector für Azure Cosmos DB-API für MongoDB](connector-azure-cosmos-db-mongodb-api.md). Andere API-Typen werden derzeit nicht unterstützt.

## <a name="supported-capabilities"></a>Unterstützte Funktionen

Dieser Connector für Azure Cosmos DB (SQL API) wird für die folgenden Aktivitäten unterstützt:

- [Kopieraktivität](copy-activity-overview.md) mit [unterstützter Quellen/Senken-Matrix](copy-activity-overview.md)
- [Mapping Data Flow](concepts-data-flow-overview.md)
- [Lookup-Aktivität](control-flow-lookup-activity.md)

Im Rahmen der Kopieraktivität unterstützt dieser Azure Cosmos DB (SQL-API)-Connector folgende Aktivitäten:

- Kopieren von Daten in die oder aus der [SQL-API](https://docs.microsoft.com/azure/cosmos-db/documentdb-introduction) von Azure Cosmos DB.
- Schreiben in Azure Cosmos DB als **insert** oder **upsert**.
- Importieren und Exportieren von JSON-Dokumenten in ihrem jeweiligen Zustand oder Kopieren von Daten aus einem tabellarischen Dataset oder in ein tabellarisches Dataset. Die Beispiele zeigen eine SQL-Datenbank und eine CSV-Datei. Informationen zum Kopieren von Dokumenten in ihrem jeweiligen Zustand in bzw. aus JSON-Dateien oder in eine andere bzw. aus einer anderen Azure Cosmos DB-Sammlung finden Sie unter „Importieren oder Exportieren von JSON-Dokumenten“.

Data Factory wird in die [Azure Cosmos DB-BuklExecutor-Bibliothek](https://github.com/Azure/azure-cosmosdb-bulkexecutor-dotnet-getting-started) integriert, um beim Schreiben in Azure Cosmos DB die beste Leistung zu erzielen.

> [!TIP]
> Das Video [Datenmigration](https://youtu.be/5-SRNiC_qOU) führt Sie schrittweise durch das Kopieren von Daten aus Azure Blob Storage in Azure Cosmos DB. Das Video beschreibt auch Überlegungen zur Leistungsoptimierung beim Erfassen von Daten in Azure Cosmos DB im Allgemeinen.

## <a name="get-started"></a>Erste Schritte

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

Die folgenden Abschnitte enthalten Details zu Eigenschaften, die Sie zum Definieren von Data Factory-Entitäten verwenden können, die spezifisch für Azure Cosmos DB (SQL-API) sind.

## <a name="linked-service-properties"></a>Eigenschaften des verknüpften Diensts

Folgende Eigenschaften werden für den verknüpften Azure Cosmos DB-Dienst (SQL-API) unterstützt:

| Eigenschaft | BESCHREIBUNG | Erforderlich |
|:--- |:--- |:--- |
| type | Die **type**-Eigenschaft muss auf **CosmosDb** festgelegt werden. | Ja |
| connectionString |Geben Sie die zum Herstellen einer Verbinden mit der Azure Cosmos DB-Datenbank erforderlichen Informationen an.<br />**Hinweis**: Sie müssen Datenbankinformationen in der Verbindungszeichenfolge angeben, wie in den folgenden Beispielen gezeigt. <br/>Markieren Sie dieses Feld als „SecureString“, um es sicher in Data Factory zu speichern. Sie können auch den Kontoschlüssel in Azure Key Vault speichern und die `accountKey`-Konfiguration aus der Verbindungszeichenfolge pullen. Ausführlichere Informationen finden Sie in den folgenden Beispielen und im Artikel [Speichern von Anmeldeinformationen in Azure Key Vault](store-credentials-in-key-vault.md). |Ja |
| connectVia | Die [Integration Runtime](concepts-integration-runtime.md), die zum Herstellen einer Verbindung mit dem Datenspeicher verwendet werden soll. Sie können die Azure Integration Runtime oder eine selbstgehostete Integration Runtime verwenden (sofern sich Ihr Datenspeicher in einem privaten Netzwerk befindet). Wenn diese Eigenschaft nicht angegeben ist, wird die standardmäßige Azure Integration Runtime verwendet. |Nein |

**Beispiel**

```json
{
    "name": "CosmosDbSQLAPILinkedService",
    "properties": {
        "type": "CosmosDb",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

**Beispiel: Speichern des Kontoschlüssels in Azure Key Vault**

```json
{
    "name": "CosmosDbSQLAPILinkedService",
    "properties": {
        "type": "CosmosDb",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "AccountEndpoint=<EndpointUrl>;Database=<Database>"
            },
            "accountKey": { 
                "type": "AzureKeyVaultSecret", 
                "store": { 
                    "referenceName": "<Azure Key Vault linked service name>", 
                    "type": "LinkedServiceReference" 
                }, 
                "secretName": "<secretName>" 
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a>Dataset-Eigenschaften

Eine vollständige Liste mit den Abschnitten und Eigenschaften, die zum Definieren von Datasets zur Verfügung stehen, finden Sie unter [Datasets und verknüpfte Dienste](concepts-datasets-linked-services.md).

Folgende Eigenschaften werden für das Azure Cosmos DB (SQL-API)-Dataset unterstützt: 

| Eigenschaft | BESCHREIBUNG | Erforderlich |
|:--- |:--- |:--- |
| type | Die Eigenschaft **type** des Datasets muss auf **CosmosDbSqlApiCollection** festgelegt werden. |Ja |
| collectionName |Der Name der Azure Cosmos DB-Dokumentsammlung. |Ja |

Wenn Sie ein Dataset vom Typ „DocumentDbCollection“ verwenden, wird es aus Gründen der Abwärtskompatibilität für die Kopier- und Lookup-Aktivität weiterhin unverändert unterstützt. Für Datenfluss wird es nicht unterstützt. Es wird jedoch empfohlen, in Zukunft das neue Modell zu verwenden.

**Beispiel**

```json
{
    "name": "CosmosDbSQLAPIDataset",
    "properties": {
        "type": "CosmosDbSqlApiCollection",
        "linkedServiceName":{
            "referenceName": "<Azure Cosmos DB linked service name>",
            "type": "LinkedServiceReference"
        },
        "schema": [],
        "typeProperties": {
            "collectionName": "<collection name>"
        }
    }
}
```

### <a name="schema-by-data-factory"></a>Schema per Data Factory

Für schemafreie Datenspeicher wie Azure Cosmos DB leitet die Kopieraktivität das Schema auf eine der in der folgenden Liste beschriebenen Arten ab. Die bewährte Methode besteht darin, die Struktur der Daten im Abschnitt **structure** anzugeben, es sei denn, Sie möchten [JSON-Dokumente in ihrem jeweiligen Zustand importieren oder exportieren](#import-or-export-json-documents).

Data Factory berücksichtigt die Zuordnung, die Sie in der Aktivität angegeben haben. Wenn eine Zeile keinen Wert für eine Spalte enthält, wird ein NULL-Wert als Spaltenwert angegeben.

Wenn Sie keine Zuordnung angeben, leitet der Data Factory-Dienst das Schema anhand der ersten Zeile in den Daten ab. Wenn die erste Zeile nicht das vollständige Schema enthält, fehlen im Ergebnis der Aktivität einige Spalten.

## <a name="copy-activity-properties"></a>Eigenschaften der Kopieraktivität

Dieser Abschnitt enthält eine Liste der Eigenschaften, die von der Azure Cosmos DB-Quelle und -Senke (SQL-API) unterstützt werden.

Eine vollständige Liste mit den verfügbaren Abschnitten und Eigenschaften zum Definieren von Aktivitäten finden Sie unter [Pipelines](concepts-pipelines-activities.md).

### <a name="azure-cosmos-db-sql-api-as-source"></a>Azure Cosmos DB (SQL API) als Quelle

Legen Sie zum Kopieren von Daten aus Azure Cosmos DB (SQL-API) den **Quelltyp** in der Copy-Aktivität auf **DocumentDbCollectionSource** fest. 

Die folgenden Eigenschaften werden im Abschnitt **source** der Kopieraktivität unterstützt:

| Eigenschaft | BESCHREIBUNG | Erforderlich |
|:--- |:--- |:--- |
| type | Die Eigenschaft **type** der Quelle für die Kopieraktivität muss auf **CosmosDbSqlApiSource** festgelegt werden. |Ja |
| query |Geben Sie die Azure Cosmos DB-Abfrage an, um Daten zu lesen.<br/><br/>Beispiel:<br /> `SELECT c.BusinessEntityID, c.Name.First AS FirstName, c.Name.Middle AS MiddleName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |Nein <br/><br/>Falls nicht angegeben, wird die folgende SQL-Anweisung ausgeführt: `select <columns defined in structure> from mycollection` |
| preferredRegions | Die bevorzugte Liste der Regionen, mit denen beim Abrufen von Daten aus Cosmos DB eine Verbindung hergestellt werden soll. | Nein |
| pageSize | Die Anzahl der Dokumente pro Seite des Abfrageergebnisses. Der Standardwert ist „-1“. Dies bedeutet, dass im Ergebnis die dienstseitige dynamische Seitengröße bis zu 1000 verwendet wird. | Nein |

Wenn Sie eine Quelle vom Typ „DocumentDbCollectionSource“ verwenden, wird sie aus Gründen der Abwärtskompatibilität weiterhin unverändert unterstützt. Es wird empfohlen, in Zukunft das neue Modell zu verwenden, das umfangreichere Funktionen zum Kopieren von Daten aus Cosmos DB enthält.

**Beispiel**

```json
"activities":[
    {
        "name": "CopyFromCosmosDBSQLAPI",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Cosmos DB SQL API input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "CosmosDbSqlApiSource",
                "query": "SELECT c.BusinessEntityID, c.Name.First AS FirstName, c.Name.Middle AS MiddleName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"",
                "preferredRegions": [
                    "East US"
                ]
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

### <a name="azure-cosmos-db-sql-api-as-sink"></a>Azure Cosmos DB (SQL API) als Senke

Legen Sie zum Kopieren von Daten in Azure Cosmos DB (SQL-API) den **Senkentyp** in der Copy-Aktivität auf **DocumentDbCollectionSink** fest. 

Die folgenden Eigenschaften werden im Abschnitt **source** der Kopieraktivität unterstützt:

| Eigenschaft | BESCHREIBUNG | Erforderlich |
|:--- |:--- |:--- |
| type | Die Eigenschaft **type**der Senke für die Kopieraktivität muss auf **CosmosDbSqlApiSink** festgelegt werden. |Ja |
| writeBehavior |Beschreibt, wie Daten in Azure Cosmos DB geschrieben werden. Zulässige Werte: **insert** und **upsert**.<br/><br/>Das Verhalten von **upsert** besteht darin, das Dokument zu ersetzen, wenn ein Dokument mit der gleichen ID bereits vorhanden ist. Andernfalls wird das Dokument eingefügt.<br /><br />**Hinweis**: Data Factory generiert automatisch eine ID für ein Dokument, wenn eine ID weder im Originaldokument noch durch Spaltenzuordnung angegeben wird. Dies bedeutet, dass Sie sicherstellen müssen, dass Ihr Dokument eine ID besitzt, damit **upsert** wie erwartet funktioniert. |Nein<br />(der Standardwert ist **insert**) |
| writeBatchSize | Data Factory verwendet die [Azure Cosmos DB-BulkExecutor-Bibliothek](https://github.com/Azure/azure-cosmosdb-bulkexecutor-dotnet-getting-started) zum Schreiben von Daten in Azure Cosmos DB. Die Eigenschaft **writeBatchSize** steuert die Größe der von der Anwendungsdefinitionsdatei in der Bibliothek bereitgestellten Dokumente. Sie können versuchen, den Wert für **writeBatchSize** zu erhöhen, um die Leistung zu verbessern, oder den Wert verringern, falls Ihre Dokumente groß sind. Weitere Tipps finden Sie weiter unten. |Nein<br />(der Standardwert ist **10.000**) |
| disableMetricsCollection | Data Factory sammelt Metriken wie Cosmos DB-Anforderungseinheiten für die Leistungsoptimierung von Kopiervorgängen und Empfehlungen. Wenn Sie sich wegen dieses Verhaltens Gedanken machen, geben Sie `true` an, um es zu deaktivieren. | Nein (Standard = `false`) |

>[!TIP]
>Cosmos DB begrenzt die Größe der einzelnen Anforderung auf 2 MB. Die Formel lautet: Anforderungsgröße = Einzeldokumentgröße * Schreibbatchgröße. Sollte ein Fehler mit dem Hinweis auftreten, dass die **Anforderung zu groß ist**, **verringern Sie den `writeBatchSize`-Wert** in der Kopiersenkenkonfiguration.

Wenn Sie eine Quelle vom Typ „DocumentDbCollectionSink“ verwenden, wird sie aus Gründen der Abwärtskompatibilität weiterhin unverändert unterstützt. Es wird empfohlen, in Zukunft das neue Modell zu verwenden, das umfangreichere Funktionen zum Kopieren von Daten aus Cosmos DB enthält.

**Beispiel**

```json
"activities":[
    {
        "name": "CopyToCosmosDBSQLAPI",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Document DB output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "CosmosDbSqlApiSink",
                "writeBehavior": "upsert"
            }
        }
    }
]
```

## <a name="mapping-data-flow-properties"></a>Eigenschaften von Mapping Data Flow

Ausführliche Informationen hierzu finden Sie unter [Quellentransformation](data-flow-source.md) und [Senkentransformation](data-flow-sink.md) in Mapping Data Flow.

## <a name="lookup-activity-properties"></a>Eigenschaften der Lookup-Aktivität

Ausführliche Informationen zu den Eigenschaften finden Sie unter [Lookup-Aktivität](control-flow-lookup-activity.md).

## <a name="import-or-export-json-documents"></a>Importieren oder Exportieren von JSON-Dokumenten

Sie können diesen Azure Cosmos DB-Connector (SQL-API) verwenden, um die folgenden Aufgaben auf einfache Weise zu erledigen:

* Importieren von JSON-Dokumenten aus verschiedenen Quellen in Azure Cosmos DB, z.B. aus Azure Blob Storage, Azure Data Lake Storage und anderen dateibasierten Speichern, die von Azure Data Factory unterstützt werden.
* Exportieren von JSON-Dokumenten aus einer Azure Cosmos DB-Sammlung in verschiedene dateibasierte Speicher.
* Kopieren von Dokumenten in ihrem jeweiligen Zustand zwischen zwei Azure Cosmos DB-Sammlungen.

So erhalten Sie eine vom Schema unabhängige Kopie:

* Aktivieren Sie bei Verwendung des Tools zum Kopieren von Daten die Option **Export as-is to JSON files or Cosmos DB collection** (Wie vorhanden in JSON-Dateien oder Cosmos DB-Sammlung exportieren).
* Wenn Sie die Aktivität „Dokumenterstellung“ verwenden, wählen Sie das JSON-Format mit dem entsprechenden Dateispeicher für Quelle oder Senke aus.

## <a name="next-steps"></a>Nächste Schritte

Eine Liste der Datenspeicher, die von der Kopieraktivität als Quellen und Senken in Azure Data Factory unterstützt werden, finden Sie unter [Unterstützte Datenspeicher](copy-activity-overview.md##supported-data-stores-and-formats).
