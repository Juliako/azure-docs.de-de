---
title: 'VPN Gateway: Ändern der Einstellungen für die Gateway-IP-Adresse: Azure PowerShell'
description: In diesem Artikel wird erläutert, wie Sie die IP-Adresspräfixe für Ihr lokales Netzwerkgateway mithilfe von PowerShell ändern können.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 8c7db48f-d09a-44e7-836f-1fb6930389df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 6aae2c87615ae0e250d7f9460bde483e3448c46e
ms.sourcegitcommit: ae8b23ab3488a2bbbf4c7ad49e285352f2d67a68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2019
ms.locfileid: "74014904"
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a>Ändern der Einstellungen des lokalen Netzwerkgateways mit PowerShell

Manchmal ändern sich die Einstellungen für „AddressPrefix“ oder „GatewayIPAddress“ Ihres lokalen Netzwerkgateways. In diesem Artikel wird gezeigt, wie Sie die Einstellungen Ihres lokalen Netzwerkgateways ändern. Sie können diese Einstellungen auch über eine andere Option aus der folgenden Liste ändern:

> [!div class="op_single_selector"]
> * [Azure-Portal](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Azure-Befehlszeilenschnittstelle](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>Voraussetzungen

Installieren Sie die aktuelle Version der PowerShell-Cmdlets für Azure Resource Manager. Weitere Informationen zum Installieren der PowerShell-Cmdlets finden Sie unter [Installieren und Konfigurieren von Azure PowerShell](/powershell/azureps-cmdlets-docs) .

## <a name="ipaddprefix"></a>Ändern von IP-Adresspräfixen

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="gwip"></a>Ändern der Gateway-IP-Adresse

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Nächste Schritte

Sie können die Gatewayverbindung überprüfen. Informationen finden Sie unter [Überprüfen einer Gatewayverbindung](vpn-gateway-verify-connection-resource-manager.md).