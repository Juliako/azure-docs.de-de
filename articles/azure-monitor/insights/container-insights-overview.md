---
title: Übersicht zu Azure Monitor für Container | Microsoft-Dokumentation
description: Dieser Artikel beschreibt Azure Monitor für Container, das die AKS Container Insights-Lösung überwacht, und den Wert, den es durch die Überwachung der Integrität Ihrer AKS-Cluster und Containerinstanzen in Azure bietet.
ms.service: azure-monitor
ms.subservice: ''
ms.topic: conceptual
author: mgoedtel
ms.author: magoedte
ms.date: 11/18/2019
ms.openlocfilehash: 12860d70cad2dbcfa3d06bf4df6939dd27ab3ab3
ms.sourcegitcommit: 653e9f61b24940561061bd65b2486e232e41ead4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2019
ms.locfileid: "74279630"
---
# <a name="azure-monitor-for-containers-overview"></a>Azure Monitor für Container – Übersicht

Azure Monitor für Container ist ein Feature zum Überwachen der Leistung von Containerworkloads,

- die in Managed Kubernetes-Clustern bereitgestellt und in Azure Kubernetes Service (AKS) gehostet sind.
- Azure Container Instances
- Selbstverwaltete Kubernetes-Cluster, die in Azure Stack oder lokal gehostet werden
- Azure Red Hat OpenShift

Die Überwachung Ihrer Container ist vor allem dann entscheidend, wenn Sie einen umfangreichen Produktionscluster mit mehreren Anwendungen ausführen.

Azure Monitor für Container visualisiert die Leistung, indem anhand der Metrik-API die in Kubernetes verfügbaren Speicher- und Prozessormetriken von Controllern, Knoten und Containern erfasst werden. Auch Containerprotokolle werden erfasst.  Nach der Aktivierung der Überwachung auf Kubernetes-Clustern werden Metriken und Protokolle für Sie automatisch mittels einer Containerversion des Log Analytics-Agents für Linux erfasst. Metriken werden in den Metrikspeicher geschrieben, und Protokolldaten werden in den Protokollspeicher geschrieben, der Ihrem [Log Analytics](../log-query/log-query-overview.md)-Arbeitsbereich zugeordnet ist. 

![Architektur von Azure Monitor für Container](./media/container-insights-overview/azmon-containers-architecture-01.png)
 
## <a name="what-does-azure-monitor-for-containers-provide"></a>Was bietet Azure Monitor für Container?

Azure Monitor für Container bietet umfassende Überwachung mithilfe verschiedener Funktionen von Azure Monitor, damit Sie Kenntnis über die Leistung und Integrität Ihres Kubernetes-Clusters und die Containerworkloads haben. Azure Monitor für Container bietet Ihnen folgende Möglichkeiten:

* Sie können auf dem Knoten ausgeführte AKS-Container sowie deren durchschnittliche Prozessor- und Speicherauslastung ermitteln. Mit diesem Wissen können Sie Ressourcenengpässe erkennen.
* Ermitteln Sie die Prozessor- und Arbeitsspeichernutzung von Containergruppen und den zugehörigen Containern, die in Azure Container Instances gehostet werden.  
* Sie können feststellen, wo im Controller bzw. im Pod sich der Container befindet. Dadurch können Sie die Gesamtleistung des Controllers bzw. Pods anzeigen. 
* Sie können die Ressourcenauslastung von Workloads überprüfen, die unabhängig von den Standardprozessen, die den Pod unterstützen, im Host ausgeführt werden.
* Sie bekommen Einblicke in das Verhalten des Clusters bei durchschnittlichen und schwersten Lasten. So können Sie benötigte Kapazitäten ermitteln und die maximale Last bestimmen, die der Cluster toleriert. 
* Konfigurieren Sie Warnungen so, dass Sie proaktiv benachrichtigt werden oder aufgezeichnet wird, wenn die CPU- und Arbeitsspeicherauslastung auf Knoten oder in Containern die Schwellenwerte überschreitet oder wenn eine Änderung des Integritätszustands im Cluster beim Integritätsrollup für Infrastruktur oder Knoten erfolgt.
* Über die Integration mit [Prometheus](https://prometheus.io/docs/introduction/overview/) können Sie Anwendungs- und Workloadmetriken anzeigen, die von Knoten und Kubernetes mithilfe von [Abfragen](container-insights-log-search.md) gesammelt werden, um benutzerdefinierte Warnungen und Dashboards zu erstellen und ausführliche Analysen durchzuführen.

    >[!NOTE]
    >Die Unterstützung für Prometheus ist zurzeit als Feature in der öffentlichen Vorschau verfügbar.
    >

* Überwachen Sie Containerworkloads, [die auf der AKS-Engine](https://github.com/microsoft/OMS-docker/tree/aks-engine) lokal und der [AKS-Engine in Azure Stack](https://docs.microsoft.com/azure-stack/user/azure-stack-kubernetes-aks-engine-overview?view=azs-1908) bereitgestellt werden.
* Überwachen von Containerworkloads, [die in Azure Red Hat OpenShift](../../openshift/intro-openshift.md) bereitgestellt sind.

    >[!NOTE]
    >Die Unterstützung für Azure Red Hat OpenShift ist zurzeit als Feature in der öffentlichen Vorschauversion verfügbar.
    >

Anhand des folgenden Videos für fortgeschrittene Benutzer können Sie sich ausführlicher mit der Überwachung Ihres AKS-Clusters mit Azure Monitor für Container vertraut machen.

> [!VIDEO https://www.youtube.com/embed/RjsNmapggPU]

## <a name="how-do-i-access-this-feature"></a>Wie greife ich auf dieses Feature zu?

Sie können auf zwei Arten auf Azure Monitor für Container zugreifen, aus Azure Monitor oder direkt aus dem ausgewählten AKS-Cluster. In Azure Monitor haben Sie eine globale Perspektive aller bereitgestellten Container, der überwachten wie auch der nicht überwachten, was es Ihnen ermöglicht, über Ihre Abonnements und Ressourcengruppen zu suchen und zu filtern und dann Drilldowns aus einem ausgewählten Container in Azure Monitor für Container auszuführen.  Andernfalls können Sie von der AKS-Seite aus einem ausgewählten AKS-Container auf das Feature direkt zugreifen.  

![Übersicht der Methoden für den Zugriff auf Azure Monitor für Container](./media/container-insights-overview/azmon-containers-experience.png)

Wenn Sie Ihre außerhalb von AKS ausgeführten Docker- und Windows-Containerhosts überwachen und verwalten möchten, um Informationen zur Konfiguration, Überwachung und Ressourcenverwendung anzuzeigen, lesen Sie den Artikel zur [Containerüberwachungslösung](../../azure-monitor/insights/containers.md).

## <a name="next-steps"></a>Nächste Schritte

Um in die Überwachung Ihrer Kubernetes-Cluster einzusteigen, lesen Sie [Aktivieren von Azure Monitor für Container](container-insights-onboard.md), um ein Verständnis für die Anforderungen und verfügbaren Methoden zum Aktivieren von Überwachung zu entwickeln. 
