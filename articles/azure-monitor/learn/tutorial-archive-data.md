---
title: Archivieren von Azure-Metriken und -Protokolldaten mithilfe von Azure Storage
description: Es wird beschrieben, wie Sie von Azure-Ressourcen generierte Protokoll- und Metrikdaten in einem Speicherkonto archivieren.
author: johnkemnetz
services: azure-monitor
ms.service: azure-monitor
ms.topic: tutorial
ms.date: 09/25/2017
ms.author: johnkem
ms.custom: mvc
ms.subservice: metrics
ms.openlocfilehash: 4d150a1f6793cc20d58bebc67d5c6b58c03139d4
ms.sourcegitcommit: 8a2949267c913b0e332ff8675bcdfc049029b64b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2019
ms.locfileid: "74304711"
---
# <a name="archive-azure-metric-and-log-data-using-azure-storage"></a>Archivieren von Azure-Metriken und -Protokolldaten mithilfe von Azure Storage

Auf mehreren Ebenen Ihrer Azure-Umgebung werden Protokoll- und Metrikdaten generiert, die in einem Azure Storage-Konto archiviert werden können. Dies bietet sich an, um einen Verlauf von Überwachungsdaten über einen längeren Zeitraum in einem preiswerten, nicht durchsuchbaren Speicher beizubehalten, nachdem die Daten die Aufbewahrungsfrist überschritten haben. 

- Metriken werden auf der Azure Monitor-Plattform 93 Tage lang aufbewahrt. 
- Ressourcendiagnoseprotokolle werden nur angezeigt, wenn sie an Log Analytics weitergeleitet werden. Dort verfügen sie über einen konfigurierbaren Aufbewahrungszeitraum von mindestens 30 Tagen. 
- Aktivitätsprotokolleinträge werden 90 Tage lang aufbewahrt.  

In diesem Tutorial durchlaufen Sie die Schritte zum Konfigurieren Ihrer Azure-Umgebung für das Archivieren von Daten in einem Speicherkonto.

> [!div class="checklist"]
> * Erstellen eines Speicherkontos zum Speichern der Überwachungsdaten
> * Weiterleiten von Abonnementprotokollen an dieses Konto
> * Weiterleiten von Ressourcen an dieses Konto
> * Weiterleiten von Daten des virtuellen Computers (Gastbetriebssystems) an das Konto
> * Anzeigen der Überwachungsdaten im Konto
> * Bereinigen von Ressourcen

Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/) erstellen, bevor Sie beginnen.

## <a name="sign-in-to-the-azure-portal"></a>Melden Sie sich auf dem Azure-Portal an.

Melden Sie sich beim [Azure-Portal](https://portal.azure.com/) an.

## <a name="create-a-storage-account"></a>Speicherkonto erstellen

Zunächst müssen Sie ein Speicherkonto einrichten, in dem die Überwachungsdaten archiviert werden sollen. Führen Sie dazu [die hier beschriebenen Schritte](../../storage/common/storage-quickstart-create-account.md) aus.

## <a name="route-subscription-logs-to-the-storage-account"></a>Weiterleiten von Abonnementprotokollen an das Speicherkonto

Sie können nun beginnen, Ihre Azure-Umgebung für das Weiterleiten von Überwachungsdaten an ein Speicherkonto einzurichten. Zunächst konfigurieren wir Daten auf Abonnementebene (die im Azure-Aktivitätsprotokoll enthalten sind) so, dass sie an das Speicherkonto weitergeleitet werden. Das [**Azure-Aktivitätsprotokoll**](../../azure-monitor/platform/activity-logs-overview.md) bietet einen Verlauf der Ereignisse auf Abonnementebene in Azure. Sie können diesen im Azure-Portal durchsuchen, um zu bestimmen, *welche* Ressourcen *wann* von *wem* erstellt, aktualisiert oder gelöscht wurden.

1. Klicken Sie im Navigationsbereich auf der linken Seite auf die Schaltfläche **Überwachen** und dann auf **Aktivitätsprotokoll**.

   ![Abschnitt „Aktivitätsprotokoll“](media/tutorial-archive-data/activity-log-home.png)

2. Klicken Sie im eingeblendeten Abschnitt „Aktivitätsprotokoll“ auf die Schaltfläche **Exportieren**.

3. Aktivieren Sie im angezeigten Abschnitt **Aktivitätsprotokoll exportieren** das Kontrollkästchen **In ein Speicherkonto exportieren**, und klicken Sie dann auf **Speicherkonto auswählen**.

   ![Exportieren des Aktivitätsprotokolls](media/tutorial-archive-data/activity-log-export.png)

4. Wählen Sie im angezeigten Abschnitt in der Dropdownliste **Speicherkonto** den Namen des Speicherkontos aus, das Sie im vorherigen Schritt **Erstellen eines Speicherkontos** erstellt haben, und klicken Sie dann auf **OK**.

   ![Auswählen eines Speicherkontos](media/tutorial-archive-data/activity-log-storage.png)

5. Legen Sie den Schieberegler **Aufbewahrung (Tage)** auf 30 fest. Mit diesem Schieberegler legen Sie die Anzahl von Tagen fest, die Überwachungsdaten im Speicherkonto aufbewahrt werden sollen. Azure Monitor löscht automatisch Daten, die älter als die angegebene Anzahl von Tagen sind. Bei einer Aufbewahrungsdauer von 0 Tagen werden die Daten dauerhaft gespeichert.

6. Klicken Sie auf **Speichern**, und schließen Sie diesen Abschnitt.

Zu Ihrem Abonnement gehörige Überwachungsdaten werden nun in das Speicherkonto übertragen.

## <a name="route-resource-data-to-the-storage-account"></a>Weiterleiten von Ressourcendaten an das Speicherkonto

Jetzt konfigurieren wir Daten auf Ressourcenebene (Ressourcenmetriken und Diagnoseprotokolle), die an das Speicherkonto weitergeleitet werden sollen, indem wir **Diagnoseeinstellungen für Ressourcen** vornehmen.

1. Klicken Sie im Navigationsbereich auf der linken Seite auf die Schaltfläche **Überwachen** und dann auf **Diagnoseeinstellungen**. Es wird eine Liste aller Ressourcen in Ihrem Abonnement eingeblendet, die mithilfe von Azure Monitor Überwachungsdaten generieren. Wenn diese Liste keine Ressourcen enthält, können Sie, bevor Sie fortfahren, [eine Logik-App erstellen](../../logic-apps/quickstart-create-first-logic-app-workflow.md), damit Sie über eine Ressource verfügen, für die Sie eine Diagnoseeinstellung konfigurieren können.

2. Klicken Sie auf eine Ressource in der Liste und dann auf **Diagnose aktivieren**.

   ![Aktivieren der Diagnose](media/tutorial-archive-data/diagnostic-settings-turn-on.png)

   Wenn bereits eine Einstellung konfiguriert ist, sehen Sie stattdessen die vorhandenen Einstellungen und die Schaltfläche **Diagnoseeinstellung hinzufügen**. Klicken Sie auf diese Schaltfläche.

   Eine Diagnoseeinstellung für eine Ressource ist eine Definition, *welche* Überwachungsdaten von einer bestimmten Ressource weitergeleitet werden und *wo* diese Überwachungsdaten landen sollen.

3. Geben Sie im eingeblendeten Abschnitt der Einstellung einen **Namen**, und aktivieren Sie das Kontrollkästchen **In einem Speicherkonto archivieren**.

   ![Abschnitt „Diagnoseeinstellungen“](media/tutorial-archive-data/diagnostic-settings-home.png)

4. Klicken Sie unter **In einem Speicherkonto archivieren** auf die Schaltfläche **Konfigurieren**, und wählen Sie das im vorherigen Abschnitt angelegte Speicherkonto aus. Klicken Sie auf **OK**.

   ![Diagnoseeinstellungen und Speicherkonto](media/tutorial-archive-data/diagnostic-settings-storage.png)

5. Aktivieren Sie alle Kontrollkästchen unter **Protokoll** und **Metrik**. Je nach Ressourcentyp wird Ihnen nur eine dieser Optionen angeboten. Diese Kontrollkästchen steuern, welche Kategorien von Protokoll- und Metrikdaten, die für den jeweiligen Ressourcentyp verfügbar sind, an das ausgewählte Ziel, in diesem Fall ein Speicherkonto, gesendet werden.

   ![Kategorien von Diagnoseeinstellungen](media/tutorial-archive-data/diagnostic-settings-categories.png)

6. Legen Sie den Schieberegler **Aufbewahrung (Tage)** auf 30 fest. Mit diesem Schieberegler legen Sie die Anzahl von Tagen fest, die Überwachungsdaten im Speicherkonto aufbewahrt werden sollen. Azure Monitor löscht automatisch Daten, die älter als die angegebene Anzahl von Tagen sind. Bei einer Aufbewahrungsdauer von 0 Tagen werden die Daten dauerhaft gespeichert.

7. Klicken Sie auf **Speichern**.

Zu Ihrer Ressource gehörige Überwachungsdaten werden nun in das Speicherkonto übertragen.

> [!NOTE]
> Das Senden mehrdimensionaler Metriken über die Diagnoseeinstellungen wird derzeit nicht unterstützt. Metriken mit Dimensionen werden als vereinfachte eindimensionale Metriken exportiert und dimensionswertübergreifend aggregiert.
>
> *Beispiel*: Die Metrik „Eingehende Nachrichten“ in einem Event Hub kann auf Warteschlangenebene untersucht und in einem Diagramm dargestellt werden. Wenn Sie die Metrik allerdings über die Diagnoseeinstellungen exportieren, umfasst die Darstellung alle eingehenden Nachrichten für alle Warteschlangen im Event Hub.
>
>

## <a name="route-virtual-machine-guest-os-data-to-the-storage-account"></a>Weiterleiten von Daten des virtuellen Computers (Gastbetriebssystems) an das Speicherkonto

1. Falls in Ihrem Abonnement noch kein virtueller Computer vorhanden ist, [erstellen Sie einen virtuellen Computer](../../virtual-machines/windows/quick-create-portal.md).

2. Klicken Sie im Portal im Navigationsbereich auf der linken Seite auf **Virtual Machines**.

3. Klicken Sie in der Liste der virtuellen Computer, die angezeigt wird, auf die VM, die Sie erstellt haben.

4. Klicken Sie im eingeblendeten Abschnitt im linken Navigationsbereich auf **Diagnoseeinstellungen**. In diesem Abschnitt erfahren Sie, wie Sie die standardmäßige Überwachungserweiterung von Azure Monitor auf Ihrem virtuellen Computer einrichten und von Windows oder Linux erzeugte Daten an ein Speicherkonto weiterleiten.

   ![Navigieren zu Diagnoseeinstellungen](media/tutorial-archive-data/guest-navigation.png)

5. Klicken Sie im eingeblendeten Abschnitt auf **Überwachung auf Gastebene aktivieren**.

   ![Aktivieren von Diagnoseeinstellungen](media/tutorial-archive-data/guest-enable.png)

6. Sobald die Diagnoseeinstellung richtig gespeichert wurde, wird auf der Registerkarte **Übersicht** eine Liste der erfassten Daten und ihrer Speicherorte angezeigt. Klicken Sie auf den Abschnitt **Leistungsindikatoren**, um die erfassten Windows-Leistungsindikatoren zu überprüfen.

   ![Einstellungen von Leistungsindikatoren](media/tutorial-archive-data/guest-perf-counters.png)

7. Klicken Sie auf die Registerkarte **Protokolle**, und aktivieren Sie in „Anwendungs- und Systemprotokolle“ die Kontrollkästchen für Protokolle auf der Ebene **Informationen**.

   ![Protokolleinstellungen](media/tutorial-archive-data/guest-logs.png)

8. Klicken Sie auf die Registerkarte **Agent** und unter **Speicherkonto** auf den Namen des angezeigten Speicherkontos.

   ![Aktualisieren des Speicherkontos](media/tutorial-archive-data/guest-storage-home.png)

9. Wählen Sie im eingeblendeten Abschnitt das Speicherkonto aus, das Sie im vorhergehenden Schritt **Speicherkonto erstellen** angelegt haben.

10. Klicken Sie auf **Speichern**.

Zu Ihren virtuellen Computern gehörige Überwachungsdaten werden nun in das Speicherkonto übertragen.

## <a name="view-the-monitoring-data-in-the-storage-account"></a>Anzeigen der Überwachungsdaten im Speicherkonto

> [!WARNING]
> Das Format der Protokolldaten im Speicherkonto wird am 1. November 2018 in JSON Lines geändert. [Dieser Artikel enthält eine Beschreibung der Auswirkungen und der Aktualisierung Ihrer Tools zur Verarbeitung des neuen Formats.](./../../azure-monitor/platform/diagnostic-logs-append-blobs.md) 
>
> 

Wenn Sie die vorherigen Schritte ausgeführt haben, wurde begonnen, die Daten in Ihr Speicherkonto zu übertragen.

1. Für einige Datentypen, z.B. das Aktivitätsprotokoll, muss es eine Aktivität geben, die ein Ereignis im Speicherkonto erzeugt. Um Aktivität im Aktivitätsprotokoll zu generieren, befolgen Sie [diese Anweisungen](./../../azure-monitor/platform/quick-audit-notify-action-subscription.md). Unter Umständen müssen Sie bis zu fünf Minuten warten, bis das Ereignis im Speicherkonto erscheint.

2. Navigieren Sie im Portal auf der linken Navigationsleiste zum Abschnitt **Speicherkonten**.

3. Bestimmen Sie das Speicherkonto, das Sie im vorherigen Abschnitt erstellt haben, und klicken Sie darauf.

4. Klicken Sie auf **Blobs**, dann auf den Container mit der Bezeichnung **insights-operational-logs** und schließlich auf den Container mit der Bezeichnung **name=default**. Dieser Container enthält Ihr Aktivitätsprotokoll. Überwachungsdaten werden anhand der Ressourcen-ID (für das Aktivitätsprotokoll lediglich die Abonnement-ID) in Container und dann nach Datum und Uhrzeit unterteilt. Das vollständige Format dieser Blobs ist wie folgt:

   insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{Abonnement-ID}/y={Jahr (vierstellige Zahl)}/m={Monat (zweistellige Zahl)}/d={Tag (zweistellige Zahl)}/h={Stunde im 24-Stunden-Format (zweistellige Zahl)}/m=00/PT1H.json

5. Navigieren Sie zur Datei „PT1H.json“, indem Sie auf die Container für Ressourcen-ID, Datum und Uhrzeit klicken. Klicken Sie auf die Datei „PT1H.json“ und dann auf **Herunterladen**. Jedes Blob vom Typ „PT1H.json“ enthält ein JSON-Blob mit Ereignissen, die innerhalb der in der Blob-URL angegebenen Stunde (Beispiel: h=12) aufgetreten sind. Während der aktuellen Stunde werden Ereignisse an die Datei „PT1H.json“ angefügt, sobald sie auftreten. Der Minutenwert (m=00) ist immer „00“, da Protokollereignisse stundenweise in einzelne Blobs unterteilt werden.

   Sie können jetzt das JSON-Ereignis anzeigen, das im Speicherkonto gespeichert wurde. Für Diagnoseprotokolle von Ressourcen ist das Format der Blobs wie folgt:

   insights-logs-{Name der Protokollkategorie}/resourceId=/{Ressourcen-ID}/y={Jahr (vierstellige Zahl)}/m={Monat (zweistellige Zahl)}/d={Tag (zweistellige Zahl)}/h={Stunde im 24-Stunden-Format (zweistellige Zahl)}/m=00/PT1H.json

6. Überwachungsdaten für das Gastbetriebssystem werden in Tabellen gespeichert. Navigieren Sie zurück zur Startseite des Speicherkontos, und klicken Sie auf **Tabellen**. Es gibt Tabellen für Metriken, Leistungsindikatoren und Ereignisprotokolle.

Sie haben das Archivieren von Überwachungsdaten in einem Speicherkonto erfolgreich eingerichtet.

## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

1. Navigieren Sie im vorherigen Schritt **Weiterleiten von Abonnementprotokollen an das Speicherkonto** zurück zum Abschnitt **Aktivitätsprotokoll exportieren**, und klicken Sie auf **Zurücksetzen**.

2. Navigieren Sie zum Abschnitt **Diagnoseeinstellungen**. Klicken Sie auf die Ressource, für die Sie im vorherigen Schritt **Weiterleiten von Ressourcendaten an das Speicherkonto** eine Diagnoseeinstellung erstellt haben. Wechseln Sie zur Einstellung, die Sie erstellt haben. Klicken Sie auf die Schaltfläche **Einstellung bearbeiten** und dann auf **Löschen**.

3. Navigieren Sie auf dem virtuellen Computer, den Sie im vorherigen Schritt **Weiterleiten von Daten des virtuellen Computers (Gastbetriebssystems) an das Speicherkonto** zum Abschnitt **Diagnoseeinstellungen**. Klicken Sie unter der Registerkarte **Agent** (unter dem Abschnitt **Azure-Diagnose-Agent entfernen**) auf **Entfernen**.

4. Navigieren Sie zum Speicherkonto, das Sie im vorhergehenden Schritt **Erstellen eines Speicherkontos** angelegt haben, und klicken Sie auf **Speicherkonto löschen**. Geben Sie den Namen des Kontos ein, und klicken Sie dann auf **Löschen**.

5. Wenn Sie in den vorherigen Schritten einen virtuellen Computer oder eine Logik-App erstellt haben, löschen Sie diese ebenfalls.

## <a name="next-steps"></a>Nächste Schritte

In diesem Tutorial haben Sie gelernt, wie Sie die Archivierung von Überwachungsdaten aus Ihrer Azure-Umgebung (Abonnement, Ressource und Gastbetriebssystem) in einem Speicherkonto einrichten.


> [!div class="checklist"]
> * Erstellen eines Speicherkontos zum Speichern der Überwachungsdaten
> * Weiterleiten von Abonnementprotokollen an dieses Konto
> * Weiterleiten von Ressourcen an dieses Konto
> * Weiterleiten von Daten des virtuellen Computers (Gastbetriebssystems) an das Konto
> * Anzeigen der Überwachungsdaten im Konto
> * Bereinigen von Ressourcen

Um Ihre Daten optimal auszunutzen und zusätzliche Erkenntnisse zu gewinnen, übermitteln Sie Ihre Daten an Log Analytics.

> [!div class="nextstepaction"]
> [Erste Schritte mit Log Analytics](../../azure-monitor/log-query/log-query-overview.md)

