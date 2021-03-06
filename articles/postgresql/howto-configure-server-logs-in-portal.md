---
title: Konfigurieren von Serverprotokollen in Azure Database for PostgreSQL (Einzelserver) und Zugreifen auf diese über das Azure-Portal
description: In diesem Artikel wird beschrieben, wie Sie über das Azure-Portal die Serverprotokolle in Azure Database for PostgreSQL (Einzelserver) konfigurieren und auf diese zugreifen.
author: rachel-msft
ms.author: raagyema
ms.service: postgresql
ms.topic: conceptual
ms.date: 5/6/2019
ms.openlocfilehash: c77e708e14d34545754ca38095aedb63ff0172a1
ms.sourcegitcommit: 15e3bfbde9d0d7ad00b5d186867ec933c60cebe6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/03/2019
ms.locfileid: "71841518"
---
# <a name="configure-and-access-azure-database-for-postgresql---single-server-logs-from-the-azure-portal"></a>Konfigurieren von Protokollen für Azure Database for PostgreSQL (Einzelserver) und Zugreifen auf diese über das Azure-Portal

Sie können die [Azure Database for PostgreSQL-Protokolle](concepts-server-logs.md) im Azure-Portal konfigurieren und auflisten sowie über dieses herunterladen.

## <a name="prerequisites"></a>Voraussetzungen
Für die Schritte in diesem Artikel ist es erforderlich, dass Sie über [Azure Database for PostgreSQL Server](quickstart-create-server-database-portal.md) verfügen.

## <a name="configure-logging"></a>Konfigurieren der Protokollierung
Konfigurieren Sie den Zugriff auf die Abfrage- und Fehlerprotokolle. 

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/) an.

2. Wählen Sie Ihre Azure Database for PostgreSQL-Server aus.

3. Wählen Sie im Abschnitt **Überwachung** in der Randleiste die Option **Serverprotokolle** aus. 

   ![Screenshot der Optionen für Serverprotokolle](./media/howto-configure-server-logs-in-portal/1-select-server-logs-configure.png)

4. Um die Serverparameter anzuzeigen, wählen Sie **Klicken Sie hier, um Protokolle zu aktivieren und Protokollparameter zu konfigurieren** aus.

5. Ändern Sie die Parameter, die Sie anpassen müssen. Alle in dieser Sitzung vorgenommenen Änderungen werden in violett hervorgehoben.

   Wählen Sie **Speichern** aus, nachdem Sie die Parameter geändert haben. Sie können Ihre Änderungen auch verwerfen. 

   ![Screenshot der Optionen für Serverparameter](./media/howto-configure-server-logs-in-portal/3-save-discard.png)

Von der Seite **Serverparameter** können Sie zur Liste der Protokolle zurückkehren, indem Sie die Seite schließen.

## <a name="view-list-and-download-logs"></a>Anzeigen der Liste und Herunterladen von Protokollen
Nachdem die Protokollierung begonnen hat, können Sie eine Liste der verfügbaren Protokolle anzeigen und einzelne Protokolldateien herunterladen. 

1. Öffnen Sie das Azure-Portal.

2. Wählen Sie Ihre Azure Database for PostgreSQL-Server aus.

3. Wählen Sie im Abschnitt **Überwachung** in der Randleiste die Option **Serverprotokolle** aus. Die Seite zeigt eine Liste der Protokolldateien an.

   ![Screenshot der Seite „Serverprotokolle“ mit hervorgehobener Liste der Protokolle](./media/howto-configure-server-logs-in-portal/4-server-logs-list.png)

   > [!TIP]
   > Die Namenskonvention des Protokolls ist **postgresql-jjjj-mm-tt_hh0000.log**. Das im Dateinamen verwendete Datum und die Uhrzeit geben den Zeitpunkt an, zu dem das Protokoll ausgestellt wurde. Die Protokolldateien rotieren jede Stunde bzw. bei einer Größe von 100 MB, wenn diese Größe früher erreicht wird.

4. Verwenden Sie bei Bedarf das Suchfeld, um schnell ein spezifisches Protokoll basierend auf Datum und Uhrzeit einzugrenzen. Die Suche erfolgt anhand des Namens des Protokolls.

   ![Screenshot der Seite „Serverprotokolle“ mit hervorgehobenem Suchfeld und Ergebnissen](./media/howto-configure-server-logs-in-portal/5-search.png)

5. Um einzelne Protokolldateien herunterzuladen, wählen Sie das Pfeilsymbol nach unten neben den einzelnen Protokolldateien in der Tabellenzeile aus.

   ![Screenshot der Seite „Serverprotokolle“ mit hervorgehobenem Pfeilsymbol nach unten](./media/howto-configure-server-logs-in-portal/6-download.png)

## <a name="next-steps"></a>Nächste Schritte
- Lesen Sie [Zugriff auf Serverprotokolle in der CLI](howto-configure-server-logs-using-cli.md), um weitere Informationen zum programmgesteuerten Herunterladen von Protokollen zu erhalten.
- Erhalten Sie weitere Informationen zu [Serverprotokollen](concepts-server-logs.md) in Azure Database for PostgreSQL. 
- Weitere Informationen zu den Parameterdefinitionen und der PostgreSQL-Protokollierung finden Sie in der PostgreSQL-Dokumentation unter [Fehlerberichterstellung und Protokollierung](https://www.postgresql.org/docs/current/static/runtime-config-logging.html).

