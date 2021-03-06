---
title: Schützen Ihrer Computer und Anwendungen
description: In diesem Dokument werden Empfehlungen in Security Center erläutert, die zum Schutz Ihrer virtuellen und physischen Computer sowie Ihrer Web-Apps und App Service-Umgebungen beitragen.
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.assetid: 47fa1f76-683d-4230-b4ed-d123fef9a3e8
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/20/2019
ms.author: memildin
ms.openlocfilehash: 4a6d733b490edd892136f6febcc90c29a5a865e1
ms.sourcegitcommit: 6bb98654e97d213c549b23ebb161bda4468a1997
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2019
ms.locfileid: "74766802"
---
# <a name="protect-your-machines-and-applications"></a>Schützen Ihrer Computer und Anwendungen
Wenn potenzielle Sicherheitslücken erkannt werden, erstellt Security Center Empfehlungen, die Sie beim Konfigurieren der erforderlichen Kontrollen unterstützen. 

In diesem Artikel wird die Seite **Compute und Apps** des Abschnitts „Ressourcensicherheit“ von Azure Security Center erläutert. Außerdem werden einige der Empfehlungen beschrieben, die dort angezeigt werden.

Eine vollständige Liste der Empfehlungen für Compute- und App-Dienste finden Sie unter [Compute- und App-Empfehlungen](recommendations-compute-and-apps.md).

## <a name="view-the-security-of-your-compute-and-apps-resources"></a>Anzeigen der Sicherheit Ihrer Compute- und App-Ressourcen

![Security Center-Dashboard](./media/security-center-virtual-machine-recommendations/overview.png)

Wenn Sie den Status Ihrer Compute- und App-Ressourcen anzeigen möchten, wählen Sie **Compute und Apps** unter **Ressourcen** in der Randleiste von Security Center aus. Die folgenden Registerkarten sind verfügbar:

* **Übersicht**: Listet die Empfehlungen für alle Compute- und App-Ressourcen sowie deren aktuellen Sicherheitsstatus auf. 

* [**VMs und Computer**](#vms-and-computers): Listet die Empfehlungen für Ihre VMs und Computer sowie deren aktuellen Sicherheitsstatus auf.

* [**VM-Skalierungsgruppen**](#vmscale-sets): Listet die Empfehlungen für Ihre Skalierungsgruppen auf. 

* [**Clouddienste**](#cloud-services): Listet die Empfehlungen für die von Security Center überwachten Web- und Workerrollen auf.

* [**App Services**](#app-services): Listet die Empfehlungen für Ihre App Service-Umgebungen und deren jeweiligen Sicherheitsstatus auf.

* **Container**: Listet die Empfehlungen für Ihre Container und die Sicherheitsbewertung ihrer Konfigurationen auf.

* **Computeressourcen**: Listet die Empfehlungen für Ihre Computeressourcen wie Service Fabric-Cluster und Event Hubs auf.

### <a name="whats-in-each-tab"></a>Was befindet sich auf jeder Registerkarte?

Jede Registerkarte enthält mehrere Abschnitte, und in jedem Abschnitt können Sie einen Drilldown ausführen, um weitere Details zum angezeigten Element anzuzeigen.

Auf jeder Registerkarte finden Sie außerdem Empfehlungen für die relevanten Ressourcen in Ihrer überwachten Umgebung. In der ersten Spalte wird die Empfehlung aufgelistet, die zweite zeigt die Gesamtzahl der betroffenen Ressourcen an, und die dritte zeigt den Schweregrad des Problems an.

Jeder Empfehlung ist eine Reihe von Aktionen zugeordnet, die ausgeführt werden können, nachdem Sie sie ausgewählt haben. Wenn Sie beispielsweise **Fehlende Systemupdates** auswählen, werden die Anzahl der virtuellen und physischen Computer, auf denen Patches fehlen, und der Schweregrad des fehlenden Updates angezeigt.

> [!NOTE]
> Die Sicherheitsempfehlungen sind identisch mit denen auf der Seite **Empfehlungen**, aber hier werden sie nach dem von Ihnen ausgewählten Ressourcentyp gefiltert. Weitere Informationen zur Anwendung von Empfehlungen finden Sie unter [Implementieren von Sicherheitsempfehlungen in Azure Security Center](security-center-recommendations.md).
>

### <a name="vms-and-computers"></a>VMs und Computer
Der Abschnitt „VMs und Computer“ enthält eine Übersicht über alle Sicherheitsempfehlungen für Ihre VMs und Computer. Es sind vier Arten von Computern enthalten:

![Nicht-Azure-Computer](./media/security-center-virtual-machine-recommendations/security-center-monitoring-icon1.png) Azure-fremder Computer

![Virtueller Azure Resource Manager-Computer](./media/security-center-virtual-machine-recommendations/security-center-monitoring-icon2.png) Virtueller Azure Resource Manager-Computer

![Klassischer virtueller Azure-Computer](./media/security-center-virtual-machine-recommendations/security-center-monitoring-icon3.png) Klassischer virtueller Azure-Computer

![Virtuelle Computer, die anhand des Arbeitsbereichs identifiziert werden](./media/security-center-virtual-machine-recommendations/security-center-monitoring-icon4.png) Virtuelle Computer, die nur anhand des Arbeitsbereichs identifiziert werden, der dem angezeigten Abonnement angehört. Dazu zählen virtuelle Computer aus anderen Abonnements, die dem Arbeitsbereich in diesem Abonnement unterstellt sind, sowie virtuelle Computer, die mit dem direkten Operations Manager-Agent installiert wurden und über keine Ressourcen-ID verfügen.

Anhand des Symbols unter der jeweiligen Empfehlung sehen Sie sofort, bei welchem virtuellen oder physischen Computer eine Aktion erforderlich ist und um welche Art von Empfehlung es sich handelt. Sie können auch die Filter verwenden, um die Liste nach **Ressourcentyp** und **Schweregrad** zu durchsuchen.

Um einen Drilldown in die Sicherheitsempfehlungen für jeden virtuellen Computer durchzuführen, klicken Sie auf den virtuellen Computer.
Hier finden Sie die Sicherheitsdetails für den virtuellen oder physischen Computer. Im unteren Bereich des Blatts werden die empfohlene Aktion und der Schweregrad des jeweiligen Problems angezeigt.
![Clouddienste](./media/security-center-virtual-machine-recommendations/recommendation-list.png)

### <a name="cloud-services"></a>Clouddienste
Für Clouddienste wird eine Empfehlung erstellt, wenn die Betriebssystemversion nicht mehr aktuell ist.

![Clouddienste](./media/security-center-virtual-machine-recommendations/security-center-monitoring-fig1-new006-2017.png)

In einem Szenario, in dem eine Empfehlung vorliegt, befolgen Sie die Schritte in der Empfehlung zum Aktualisieren des Betriebssystems. Ist ein Update verfügbar, erhalten Sie eine Warnung (rot oder orange, je nach Schweregrad des Problems). Eine vollständige Erläuterung der Empfehlung erhalten Sie, wenn Sie in der Spalte **BESCHREIBUNG** auf **Betriebssystemversion aktualisieren** klicken.

### <a name="app-services"></a>App Services
Um die App Service-Informationen anzuzeigen, müssen Sie den Tarif „Standard“ von Security Center verwenden und App Service in Ihrem Abonnement aktivieren. Anweisungen zum Aktivieren dieses Features finden Sie unter [Schützen von App Services in Azure Security Center](security-center-app-services.md).


Unter **App Services** wird eine Liste Ihrer App Service-Umgebungen und die Integritätszusammenfassung basierend auf der von Security Center ausgeführten Bewertung angezeigt.

![App Services](./media/security-center-virtual-machine-recommendations/app-services.png)

Es werden drei Arten von Anwendungsdiensten angezeigt:

![App Service-Umgebung](./media/security-center-virtual-machine-recommendations/ase.png) App Service-Umgebung

![Webanwendung](./media/security-center-virtual-machine-recommendations/web-app.png) Webanwendung

![Funktionsanwendung](./media/security-center-virtual-machine-recommendations/function-app.png) Funktionsanwendung

Wenn Sie eine Webanwendung auswählen, wird eine Zusammenfassungsansicht mit drei Registerkarten geöffnet:

   - **Empfehlungen**: Basiert auf von Security Center ausgeführten Bewertungen, bei denen ein Fehler aufgetreten ist.
   - **Bestandene Bewertungen**: Liste der vom Security Center ausgeführten Bewertungen, die bestanden wurden.
   - **Nicht verfügbare Bewertungen:** Liste der Bewertungen, die aufgrund eines Fehlers nicht ausgeführt wurden, oder bei denen die Empfehlung für den jeweiligen Service nicht relevant ist.

   Unter **Empfehlungen** finden Sie eine Liste der Empfehlungen für die ausgewählte Webanwendung und den Schweregrad der einzelnen Empfehlungen.

   ![Empfehlungen für App Services](./media/security-center-virtual-machine-recommendations/app-services-rec.png)

Wählen Sie eine Empfehlung aus, um eine Beschreibung der Empfehlung und eine Liste von fehlerhaften und fehlerfreien sowie nicht überprüften Ressourcen anzuzeigen.

   - In der Spalte **Bestandene Bewertungen** wird eine Liste der bestandenen Bewertungen angezeigt. Der Schweregrad dieser Bewertungen wird immer in Grün angezeigt.

   - Wählen Sie eine bestandene Bewertung in der Liste aus, um eine Beschreibung der Bewertung, eine Liste von fehlerhaften und fehlerfreien Ressourcen und eine Liste von nicht überprüften Ressourcen anzuzeigen. Zwar ist eine Registerkarte für fehlerhafte Ressourcen vorhanden, diese Liste ist aber immer leer, da die Bewertung bestanden wurde.

### <a name="vmscale-sets"></a>VM-Skalierungsgruppen
Security Center erkennt automatisch, ob Sie über Skalierungsgruppen verfügen und empfiehlt, Microsoft Monitoring Agent auf diesen installieren.

So installieren Sie den Microsoft Monitoring Agent: 

1. Wählen Sie die Empfehlung **Überwachungs-Agent für VM-Skalierungsgruppen installieren** aus. Sie erhalten eine Liste der nicht überwachten Skalierungsgruppen.

1. Wählen Sie eine Skalierungsgruppe in fehlerhaftem Zustand aus. Führen Sie die Anweisungen zum Installieren des Überwachungs-Agents mit einem vorhandenen aufgefüllten Arbeitsbereich aus, oder erstellen Sie einen neuen. Stellen Sie unbedingt den [Tarif](security-center-pricing.md) des Arbeitsbereichs ein, wenn er nicht festgelegt ist.

   ![Installieren von MMS](./media/security-center-virtual-machine-recommendations/install-mms.png)

Festlegen einer neuen Skalierungsgruppen, um automatisch Microsoft Monitoring Agent zu installieren:
1. Wechseln Sie zu Azure Policy, und klicken Sie auf **Definitionen**.

1. Suchen Sie nach der Richtlinie **Bereitstellen von Log Analytics-Agent für Windows-VM-Skalierungsgruppen**, und klicken Sie darauf.

1. Klicken Sie auf **Zuweisen**.

1. Legen Sie **Bereich** und **Log Analytics-Arbeitsbereich** fest, und klicken Sie auf **Zuweisen**.

Wenn Sie die Installation des Microsoft Monitoring Agent in Azure Policy für alle vorhandenen Skalierungsgruppen festlegen möchten, wenden Sie unter **Wiederherstellung** die vorhandene Richtlinie auf die vorhandenen Skalierungsgruppen an.


## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zu Empfehlungen für andere Arten von Azure-Ressourcen finden Sie in den folgenden Artikeln:

* [Überwachen von Identität und Zugriff in Azure Security Center](security-center-identity-access.md)
* [Schützen Ihres Netzwerks in Azure Security Center](security-center-network-recommendations.md)
* [Schützen Ihres Azure SQL-Diensts in Azure Security Center](security-center-sql-service-recommendations.md)
