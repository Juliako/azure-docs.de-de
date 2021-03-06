---
title: include file
description: include file
services: container-service
author: dlepow
ms.service: container-service
ms.topic: include
ms.date: 11/22/2019
ms.author: danlep
ms.custom: include file
ms.openlocfilehash: 0695416c65eed2bbf0a19d5ed1ea0c53a7ece332
ms.sourcegitcommit: 8cf199fbb3d7f36478a54700740eb2e9edb823e8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/25/2019
ms.locfileid: "74485445"
---
| Resource | Standardlimit |
| --- | :--- |
| Maximale Anzahl Cluster pro Abonnement | 100 |
| Maximale Knoten pro Cluster mit VM-Verfügbarkeitsgruppen und der Load Balancer Basic-SKU  | 100 |
| Maximale Knoten pro Cluster mit VM-Skalierungsgruppen und der [Load Balancer Standard-SKU][standard-load-balancer] | 800 (100 Knoten pro [Knotenpool][node-pool]) |
| Maximale Anzahl Pods pro Knoten: [Basisnetzwerke][basic-networking] mit Kubenet | 110 |
| Maximale Anzahl Pods pro Knoten: [Erweiterte Netzwerkunterstützung][advanced-networking] mit Azure Container Networking Interface | Bereitstellung mithilfe der Azure CLI: 30<sup>1</sup><br />Azure Resource Manager-Vorlage: 30<sup>1</sup><br />Bereitstellung über das Portal: 30 |

<sup>1</sup>Wenn Sie einen AKS-Cluster (Azure Kubernetes Service) über die Azure-Befehlszeilenschnittstelle oder über eine Resource Manager-Vorlage bereitstellen, kann dieser Wert auf bis zu 250 Pods pro Knoten festgelegt werden. Wenn Sie bereits einen AKS-Cluster bereitgestellt haben oder einen Cluster über das Azure-Portal bereitstellen, kann die maximale Anzahl von Pods pro Knoten nicht konfiguriert werden.<br />

<!-- LINKS - Internal -->
[basic-networking]: ../articles/aks/concepts-network.md#kubenet-basic-networking
[advanced-networking]: ../articles/aks/concepts-network.md#azure-cni-advanced-networking
[standard-load-balancer]: ../articles/load-balancer/load-balancer-standard-overview.md
[node-pool]: ../articles/aks/use-multiple-node-pools.md

<!-- LINKS - External -->
[azure-support]: https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest
