---
title: Automatische Speichervergrößerung in Azure Database for MariaDB über das Azure-Portal
description: In diesem Artikel wird beschrieben, wie Sie die automatische Speichervergrößerung für Azure Database for MariaDB über das Azure-Portal aktivieren können.
author: ambhatna
ms.author: ambhatna
ms.service: mariadb
ms.topic: conceptual
ms.date: 5/29/2019
ms.openlocfilehash: 9d7b126b5c07cc8661cf50b4c4e13f78592b118e
ms.sourcegitcommit: d200cd7f4de113291fbd57e573ada042a393e545
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/29/2019
ms.locfileid: "70136679"
---
# <a name="auto-grow-storage-in-azure-database-for-mariadb-using-the-azure-portal"></a>Automatische Speichervergrößerung in Azure Database for MariaDB über das Azure-Portal
In diesem Artikel wird beschrieben, wie Sie die Speichervergrößerung für einen Azure Database for MariaDB-Server konfigurieren können, ohne die Workload zu beeinträchtigen.

Wenn ein Server das zugeordnete Speicherlimit erreicht, wird er als schreibgeschützt gekennzeichnet. Wenn Sie jedoch die automatische Speichervergrößerung aktivieren, wird der Speicher in Anpassung an die zunehmende Datenmenge erweitert. Bei Servern mit weniger als 100 GB bereitgestelltem Speicher wird die bereitgestellte Speichergröße um 5 GB erhöht, sobald der freie Speicher unter 1 GB oder zehn Prozent des bereitgestellten Speichers sinkt. Bei Servern mit mehr als 100 GB bereitgestelltem Speicher wird die bereitgestellte Speichergröße um fünf Prozent erhöht, sobald der freie Speicherplatz unter fünf Prozent der bereitgestellten Speichergröße sinkt. Dabei gelten die [hier](https://docs.microsoft.com/azure/mariadb/concepts-pricing-tiers#storage) beschriebenen Grenzwerte für maximalen Speicher.

## <a name="prerequisites"></a>Voraussetzungen
Zum Durcharbeiten dieses Leitfadens benötigen Sie Folgendes:
- [Azure Database for MariaDB-Server](./quickstart-create-mariadb-server-database-using-azure-portal.md)

## <a name="enable-storage-auto-grow"></a>Aktivieren der automatischen Speichervergrößerung 

Gehen Sie wie folgt vor, um die automatische Speichervergrößerung für MariaDB-Server zu aktivieren:

1. Wählen Sie im [Azure-Portal](https://portal.azure.com/) Ihren vorhandenen Azure Database for MariaDB-Server aus.

2. Klicken Sie auf der Seite des MariaDB-Servers unter der Überschrift **Einstellungen** auf **Tarif**, um die Seite mit Tarifen zu öffnen.

3. Wählen Sie im Abschnitt „Automatische Vergrößerung“ die Option **Ja** aus, um die automatische Speichervergrößerung zu aktivieren.

    ![Azure Database for MariaDB – Settings_Pricing_tier – Automatische Vergrößerung](./media/howto-auto-grow-storage-portal/3-auto-grow.png)

4. Klicken Sie zum Speichern der Änderungen auf **OK**.

5. In einer Benachrichtigung wird bestätigt, dass die automatische Vergrößerung erfolgreich aktiviert wurde.

    ![Azure Database for MariaDB – erfolgreiche automatische Vergrößerung](./media/howto-auto-grow-storage-portal/5-auto-grow-successful.png)

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie [Warnungen zu Metriken erstellen](howto-alert-metric.md).
