---
title: Unterstützte Kubernetes-Versionen in Azure Kubernetes Service
description: Grundlegendes zur Richtlinie zur Unterstützung der Kubernetes-Version und zum Lebenszyklus von Clustern in Azure Kubernetes Service (AKS)
services: container-service
author: sauryadas
ms.service: container-service
ms.topic: article
ms.date: 05/20/2019
ms.author: saudas
ms.openlocfilehash: b6dd91dda559f778eaa8f5a17b46a22020dd8373
ms.sourcegitcommit: 8cf199fbb3d7f36478a54700740eb2e9edb823e8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/25/2019
ms.locfileid: "74484047"
---
# <a name="supported-kubernetes-versions-in-azure-kubernetes-service-aks"></a>Unterstützte Kubernetes-Versionen in Azure Kubernetes Service (AKS)

Die Kubernetes-Community veröffentlicht etwa alle drei Monate Nebenversionen. Diese Releases enthalten neue Features und Verbesserungen. Patchreleases kommen häufiger vor (manchmal wöchentlich) und sind nur für wichtige Fehlerbehebungen in einer Nebenversion gedacht. Diese Patchreleases beinhalten Behebungen von Sicherheitsrisiken oder größerer Fehler, die viele Kunden und Produkte betreffen, die in einer auf Kubernetes basierenden Produktionsumgebung ausgeführt werden.

AKS zielt darauf ab, neue Kubernetes-Versionen je nach Stabilität des Upstreamrelease innerhalb von 30 Tagen zu zertifizieren und zu veröffentlichen.

## <a name="kubernetes-versions"></a>Kubernetes-Versionen

Kubernetes verwendet als Standardversionierungsschema die [semantische Versionierung](https://semver.org/). Für jede Kubernetes-Version wird daher das folgende Nummerierungsschema verwendet:

```
[major].[minor].[patch]

Example:
  1.12.14
  1.12.15
```

Für jede Zahl in der Version gilt, dass allgemeine Kompatibilität mit der vorherigen Version besteht:

* Die Hauptversionen ändern sich, wenn nicht kompatible API-Änderungen vorgenommen werden oder möglicherweise keine Abwärtskompatibilität mehr gewährleistet wird.
* Nebenversionen ändern sich, wenn Änderungen an der Funktionalität vorgenommen werden, die zu den anderen Nebenreleases abwärtskompatibel sind.
* Patchversionen ändern sich, wenn abwärtskompatible Fehlerbehebungen vorgenommen werden.

Benutzer sollten nach Möglichkeit immer das neueste Patchrelease der aktuell verwendeten Nebenversion nutzen. Wenn Ihr Produktionscluster beispielsweise die Version *1.12.14* verwendet und *1.12.15* die neueste verfügbare Patchversion für die Nebenversion *1.12* ist, sollten Sie ein Upgrade auf die Version *1.12.15* durchführen, sobald Sie sicher sind, dass Ihr Cluster vollständig gepatcht und unterstützt wird.

## <a name="kubernetes-version-support-policy"></a>Richtlinie zur Unterstützung der Kubernetes-Version

> [!NOTE]
> Ab dem 9. Dezember 2019 unterstützt AKS die neuesten N–2 Versionen von Kubernetes. Diese Änderung soll dem Upstreamfenster der Unterstützung für Kubernetes-Versionen entsprechen und sicherstellen, dass die neuesten und sichersten Versionen verwendet werden. Weitere Informationen finden Sie in [dieser Ankündigung](https://azure.microsoft.com/updates/azure-kubernetes-service-will-be-retiring-support-for-kubernetes-versions-1-11-and-1-12/).

AKS unterstützt vier Nebenversionen von Kubernetes:

* Die aktuelle Nebenversion, die in AKS veröffentlicht wird (N).
* Die drei vorherigen Nebenversionen. Jede unterstützte Nebenversion unterstützt ebenfalls zwei stabile Patches.

Diese Richtlinie wird auch als „N-3“ bezeichnet, wobei „N“ für das neueste Release und die Zahl 3 für die Anzahl der Nebenversionen steht.

Wenn AKS beispielsweise die Version *1.13.a* einführt, werden die folgenden Versionen unterstützt:

Neue Nebenversion    |    Liste mit unterstützten Versionen
-----------------    |    ----------------------
1.13.a               |    1.12.a, 1.12.b, 1.11.a, 1.11.b, 1.10.a, 1.10.b

Hierbei stehen „.a“ und „.b“ für repräsentative Patchversionen. „a“ aus 1.13.a kann sich von 1.12.a unterscheiden. Beispiel: 1.13.9 und 1.12.8.

Informationen zu Benachrichtigungen, die Versionsänderungen und damit verbundene Auswirkungen betreffen, finden Sie im Abschnitt „Benachrichtigungen“ weiter unten.

Wenn eine neue Nebenversion eingeführt wird, werden die älteste Nebenversion und die unterstützten Patchreleases nicht mehr unterstützt und entfernt. Angenommen, die aktuelle Liste mit den unterstützten Versionen sieht wie folgt aus:

```
1.12.a
1.12.b
1.11.a
1.11.b
1.10.a
1.10.b
1.9.a
1.9.b
```

AKS veröffentlicht 1.13. *. Dies bedeutet, dass Version 1.9.* (alle 1.9-Versionen) entfernt wird und aus dem Support herausfällt.

> [!NOTE]
> Wenn Kunden eine nicht unterstützte Kubernetes-Version verwenden, werden sie aufgefordert, ein Upgrade vorzunehmen, sobald sie Support für den Cluster anfordern. Die [AKS-Supportrichtlinien](https://docs.microsoft.com/azure/aks/support-policies) gelten nicht für Cluster, auf denen nicht unterstützte Kubernetes-Releases ausgeführt werden.


Zusätzlich zur Unterstützung der oben genannten Nebenversionen unterstützt AKS auch die beiden neuesten *Patchreleases** für eine bestimmte Nebenversion. Angenommen, folgende Versionen werden unterstützt:

```
Current Supported Version List
------------------------------
1.12.1, 1.12.2, 1.11.4, 1.11.5
```

Wenn Upstream-Kubernetes die Patchversionen 1.12.3 und 1.11.6 veröffentlicht und AKS diese ebenfalls veröffentlicht, werden die ältesten Patchversionen nicht mehr unterstützt und entfernt. Die Liste mit den unterstützten Versionen ändert sich dann wie folgt:

```
New Supported Version List
----------------------
1.12.*2*, 1.12.*3*, 1.11.*5*, 1.11.*6*
```

> [!NOTE]
> Kunden sollten die Erstellung eines Clusters, CI oder andere automatisierte Aufträge nicht von bestimmten Patchreleases abhängig machen. 

### <a name="communications"></a>Benachrichtigungen

* Bei neuen **Nebenversionen** von Kubernetes:
  * Alle Benutzer werden öffentlich über die neue Version benachrichtigt. Außerdem wird mitgeteilt, welche Version entfernt wird.
  * Wenn eine neue Patchversion veröffentlicht wird, wird gleichzeitig die älteste Patchversion entfernt.
  * Kunden haben ab dem Datum der öffentlichen Benachrichtigung **60 Tage** Zeit, ein Upgrade auf ein unterstütztes Release der Nebenversion durchzuführen.
* Bei neuen **Patchversionen** von Kubernetes:
  * Alle Benutzer werden über die neue Patchversion benachrichtigt. Außerdem werden sie aufgefordert, ein Upgrade auf das neueste Patchrelease vorzunehmen.
  * Benutzer haben **30 Tage** Zeit, ein Upgrade auf ein neueres, unterstütztes Patchrelease durchzuführen, bevor das älteste Patchrelease entfernt wird.

In AKS wird „Veröffentlichung“ (Release) als allgemeine Verfügbarkeit definiert, die in allen Quality of Service-Messungen und Messungen von Servicelevelzielen (SLOs) sowie in allen Regionen verfügbar ist.

> [!NOTE]
> Kunden werden benachrichtigt, wenn Kubernetes-Versionen veröffentlicht oder nicht mehr unterstützt werden. Wenn eine Nebenversion nicht mehr unterstützt und entfernt wird, haben Benutzer 60 Tage Zeit, ein Upgrade auf ein unterstütztes Release vorzunehmen. Im Fall von Patchreleases haben Kunden 30 Tage Zeit, ein Upgrade auf ein unterstütztes Release vorzunehmen.

#### <a name="notification-channels-for-aks-changes"></a>Benachrichtigungskanäle für AKS-Änderungen

Für AKS wird ein wöchentliches Dienstupdate veröffentlicht, in dem neue Kubernetes-Versionen, Dienständerungen und Komponentenupdates zusammengefasst sind, die für den Dienst in [GitHub](https://github.com/Azure/AKS/releases) veröffentlicht wurden.

Diese Änderungen werden im Rahmen der regulären Wartung, die als Teil des verwalteten Diensts angeboten wird, an alle Kunden weitergegeben. Einige Änderungen erfordern explizite Upgrades, während für andere keine Maßnahmen erforderlich sind.

Benachrichtigungen werden außerdem an den folgenden Stellen veröffentlicht:

* in den [AKS-Versionshinweisen](https://aka.ms/aks/releasenotes)
* Benachrichtigungen im Azure-Portal
* im [Azure-Updatekanal][azure-update-channel]

### <a name="policy-exceptions"></a>Richtlinienausnahmen

AKS behält sich das Recht vor, ohne Vorankündigung neue oder bestehende Versionen hinzuzufügen oder zu entfernen, wenn in diesen kritische, die Produktion einschränkende Fehler oder Sicherheitsprobleme gefunden werden.

Bestimmte Patchreleases können übersprungen oder Rollouts je nach Schweregrad des Fehlers oder Sicherheitsproblems beschleunigt werden.

### <a name="azure-portal-and-cli-default-versions"></a>Standardversionen für das Azure-Portal und die Azure-CLI

Wenn Sie einen AKS-Cluster im Portal oder mit der Azure CLI bereitstellen, wird der Cluster immer auf die Nebenversion N-1 und den neuesten Patch festgelegt. Wenn AKS beispielsweise die Versionen *1.13.a*, *1.12.a* + *1.12.b*, *1.11.a* + *1.11.b* und *1.10.a* + *1.10b* unterstützt, ist die Standardversion für neue Cluster *1.12.b*.

AKS verwendet standardmäßig die Version N-1 (Nebenversion mit aktuellem Patch, beispielsweise 1.12.b), um Kunden eine bekannte, stabile und gepatchte Version bereitstellen zu können.

## <a name="list-currently-supported-versions"></a>Auflisten der derzeit unterstützten Versionen

Um herauszufinden, welche Versionen für Ihr Abonnement und Ihre Region derzeit verfügbar sind, verwenden Sie den Befehl [az aks get-versions][az-aks-get-versions]. Im folgenden Beispiel sind die verfügbaren Kubernetes-Versionen für die Region *EastUS* aufgelistet:

```azurecli-interactive
az aks get-versions --location eastus --output table
```

Die Ausgabe sieht ungefähr wie im folgenden Beispiel aus, in dem Kubernetes-Version *1.14.6* als aktuelle verfügbare Version angezeigt wird:

```
KubernetesVersion    Upgrades
-------------------  ------------------------
1.14.6               None available
1.14.5               1.14.6
1.13.10              1.14.5, 1.14.6
1.13.9               1.13.10, 1.14.5, 1.14.6
1.12.8               1.13.9, 1.13.10
1.12.7               1.12.8, 1.13.9, 1.13.10
1.11.10              1.12.7, 1.12.8
1.11.9               1.11.10, 1.12.7, 1.12.8
1.10.13              1.11.9, 1.11.10
1.10.12              1.10.13, 1.11.9, 1.11.10
```

## <a name="faq"></a>Häufig gestellte Fragen

**Was geschieht, wenn ein Kunde ein Upgrade eines Kubernetes-Clusters mit einer Nebenversion durchführt, die nicht unterstützt wird?**

Wenn Sie die Version *N-4* verwenden, wird diese nicht unterstützt, und Sie werden zu einem Upgrade aufgefordert. Wenn das Upgrade von der Version N-4 auf N-3 erfolgreich ist, können Sie den Support entsprechend der Supportrichtlinien wieder nutzen. Beispiel:

- Wenn die unterstützten AKS-Versionen *1.13.a*, *1.12.b* + *1.12.c*, *1.11.d* + *1.11.e* und *1.10.f* + *1.10.g* lauten und Sie *1.9.h* oder *1.9.i* verwenden, sind Sie aus dem Support herausgefallen.
- Falls das Upgrade von *1.9.h* oder *1.9.i* auf *1.10.f* oder *1.10.g* erfolgreich ist, befinden Sie sich wieder im Rahmen unserer Supportrichtlinien.

Upgrades auf ältere Versionen als *n-4* werden nicht unterstützt. In solchen Fällen wird empfohlen, dass die Kunden neue AKS-Cluster erstellen und ihre Workloads erneut bereitstellen.

**Was bedeutet „nicht unterstützt“?**

„Nicht unterstützt“ bedeutet, dass die verwendete Version nicht in der Liste mit den unterstützten Versionen enthalten ist und Sie aufgefordert werden, für den Cluster ein Upgrade auf eine unterstützte Version vorzunehmen, sobald Sie Support anfordern. Des Weiteren stellt AKS für Cluster, die nicht in der Liste der unterstützten Versionen aufgeführt sind, weder Laufzeitgarantien noch sonstige Garantien bereit.

**Was geschieht, wenn ein Kunde einen Kubernetes-Cluster mit einer Nebenversion skaliert, die nicht unterstützt wird?**

Bei Nebenversionen, die von AKS nicht unterstützt werden, funktioniert das Herunter- und Hochskalieren weiterhin einwandfrei.

**Kann ein Kunde für immer eine Kubernetes-Version verwenden?**

Ja. Wenn der Cluster jedoch keine der von AKS unterstützten Versionen verwendet, gelten die AKS-Supportrichtlinien nicht für den Cluster. Azure führt kein automatisches Upgrade Ihres Clusters durch und löscht ihn nicht.

**Welche Version wird vom Master unterstützt, wenn der Agent-Cluster keine der unterstützten AKS-Versionen verwendet?**

Der Master wird automatisch auf die neueste unterstützte Version aktualisiert.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum Upgrade Ihres Clusters finden Sie unter [Durchführen eines Upgrades für einen Azure Kubernetes Service-Cluster (AKS)][aks-upgrade].

<!-- LINKS - External -->
[aks-engine]: https://github.com/Azure/aks-engine
[azure-update-channel]: https://azure.microsoft.com/updates/?product=kubernetes-service

<!-- LINKS - Internal -->
[aks-upgrade]: upgrade-cluster.md
[az-aks-get-versions]: /cli/azure/aks#az-aks-get-versions
