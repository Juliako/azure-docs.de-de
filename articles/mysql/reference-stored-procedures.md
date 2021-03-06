---
title: Gespeicherte Prozeduren für die Azure Database for MySQL-Verwaltung
description: Erfahren Sie, welche gespeicherten Prozeduren in Azure Database for MySQL hilfreich sind, um Datenreplikation zu konfigurieren, die Zeitzone festzulegen und Abfragen abzubrechen.
author: ajlam
ms.author: andrela
ms.service: mysql
ms.topic: conceptual
ms.date: 09/19/2019
ms.openlocfilehash: 34598278ac7f432c5976de86eaf5dcf477c7e81a
ms.sourcegitcommit: c2e7595a2966e84dc10afb9a22b74400c4b500ed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2019
ms.locfileid: "71970337"
---
# <a name="azure-database-for-mysql-management-stored-procedures"></a>Gespeicherte Prozeduren für die Azure Database for MySQL-Verwaltung

Gespeicherte Prozeduren sind auf Azure Database for MySQL-Servern verfügbar, um die Verwaltung Ihres MySQL-Servers zu erleichtern. Dies schließt die Verwaltung der Verbindungen und Abfragen Ihres Servers sowie das Einrichten von Datenreplikation ein.  

## <a name="data-in-replication-stored-procedures"></a>Gespeicherte Prozeduren für die Datenreplikation

Mithilfe der Replikation eingehender Daten können Sie Daten von einem MySQL-Server, der lokal, auf virtuellen Computern oder von Datenbankdiensten ausgeführt wird, die von anderen Cloudanbietern gehostet werden, mit dem Azure Database for MySQL-Dienst synchronisieren.

Mit den folgenden gespeicherten Prozeduren wird die Datenreplikation zwischen einem Master und einem Replikat eingerichtet oder entfernt.

|**Name der gespeicherten Prozedur**|**Eingabeparameter**|**Ausgabeparameter**|**Hinweis zur Verwendung**|
|-----|-----|-----|-----|
|*mysql.az_replication_change_master*|master_host<br/>master_user<br/>master_password<br/>master_port<br/>master_log_file<br/>master_log_pos<br/>master_ssl_ca|–|Um Daten im SSL-Modus zu übertragen, übergeben Sie im Parameter „master_ssl_ca“ den Kontext des Zertifizierungsstellenzertifikats. </br><br>Um Daten ohne SSL zu übertragen, übergeben Sie im Parameter „master_ssl_ca“ eine leere Zeichenfolge.|
|*mysql.az_replication _start*|–|–|Startet die Replikation.|
|*mysql.az_replication _stop*|–|–|Beendet die Replikation.|
|*mysql.az_replication _remove_master*|–|–|Entfernt die Replikationsbeziehung zwischen dem Master und dem Replikat|
|*mysql.az_replication_skip_counter*|–|–|Überspringt einen Replikationsfehler.|

Informationen zum Einrichten der Datenreplikation zwischen einem Master und einem Replikat in Azure Database for MySQL finden Sie unter [Konfigurieren der Datenreplikation](howto-data-in-replication.md).

## <a name="other-stored-procedures"></a>Andere gespeicherte Prozeduren

Die folgenden gespeicherten Prozeduren sind in Azure Database for MySQL zum Verwalten Ihres Servers verfügbar.

|**Name der gespeicherten Prozedur**|**Eingabeparameter**|**Ausgabeparameter**|**Hinweis zur Verwendung**|
|-----|-----|-----|-----|
|*mysql.az_kill*|processlist_id|–|Entspricht dem Befehl [`KILL CONNECTION`](https://dev.mysql.com/doc/refman/8.0/en/kill.html). Beendet die der angegebenen „processlist_id“ zugeordnete Verbindung nach dem Beenden einer beliebigen Anweisung, die von der Verbindung ausgeführt wird.|
|*mysql.az_kill_query*|processlist_id|–|Entspricht dem Befehl [`KILL QUERY`](https://dev.mysql.com/doc/refman/8.0/en/kill.html). Beendet die Anweisung, die derzeit von der Verbindung ausgeführt wird. Die Verbindung bleibt unverändert erhalten.|
|*mysql.az_load_timezone*|–|–|Lädt Zeitzonentabellen, damit der `time_zone`-Parameter auf benannte Werte festgelegt werden kann (z.B. „USA/Pazifik“).|

## <a name="next-steps"></a>Nächste Schritte
- Erfahren Sie, wie Sie die [Datenreplikation einrichten](howto-data-in-replication.md).
- Erfahren Sie, wie Sie die [Zeitzonentabellen](howto-server-parameters.md#working-with-the-time-zone-parameter) verwenden.
