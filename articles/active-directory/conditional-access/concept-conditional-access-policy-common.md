---
title: Allgemeine Richtlinien für bedingten Zugriff – Azure Active Directory
description: Häufig verwendete Richtlinien für bedingten Zugriff für Unternehmen
services: active-directory
ms.service: active-directory
ms.subservice: conditional-access
ms.topic: conceptual
ms.date: 12/03/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: calebb, rogoya
ms.collection: M365-identity-device-management
ms.openlocfilehash: bf338ad0c555038cd99c3604d69ab80371d6ea22
ms.sourcegitcommit: 5aefc96fd34c141275af31874700edbb829436bb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/04/2019
ms.locfileid: "74804973"
---
# <a name="common-conditional-access-policies"></a>Allgemeine Richtlinien für bedingten Zugriff

Grundlegende Schutzrichtlinien sind großartig, aber viele Unternehmen benötigen mehr Flexibilität als diese bieten. Viele Unternehmen benötigen z. B. die Möglichkeit, bestimmte Konten wie ihr Notfallzugriffskonto von den Richtlinien für bedingten Zugriff auszuschließen, die eine mehrstufige Authentifizierung erfordern. Für diese Unternehmen können die in diesem Artikel genannten allgemeinen Richtlinien hilfreich sein.

![Richtlinien für bedingten Zugriff im Azure-Portal](./media/concept-conditional-access-policy-common/conditional-access-policies-azure-ad-listing.png)

## <a name="emergency-access-accounts"></a>Konten für den Notfallzugriff

Weitere Informationen zu Notfallzugriffskonten und warum sie wichtig sind, finden Sie in den folgenden Artikeln: 

* [Verwalten von Konten für den Notfallzugriff in Azure AD](../users-groups-roles/directory-emergency-access.md)
* [Erstellen einer robusten Verwaltungsstrategie für die Zugriffssteuerung in Azure Active Directory](../authentication/concept-resilient-controls.md)

## <a name="typical-policies-deployed-by-organizations"></a>Typische Richtlinien, die von Unternehmen bereitgestellt werden

* [Vorschreiben der MFA für Administratoren](howto-conditional-access-policy-admin-mfa.md)
* [Vorschreiben der MFA für die Azure-Verwaltung](howto-conditional-access-policy-azure-management.md)
* [Erzwingen der MFA für alle Benutzer](howto-conditional-access-policy-all-users-mfa.md)
* [Blockieren älterer Authentifizierungsmethoden](howto-conditional-access-policy-block-legacy.md)
* [Risikobasierter bedingter Zugriff (erfordert Azure AD Premium P2)](howto-conditional-access-policy-risk.md)
* [Vorschreiben eines vertrauenswürdigen Standorts für die MFA-Registrierung](howto-conditional-access-policy-registration.md)
* [Blockieren des Zugriffs nach Standort](howto-conditional-access-policy-location.md)
* [Erzwingen eines kompatiblen Geräts](howto-conditional-access-policy-compliant-device.md)

## <a name="next-steps"></a>Nächste Schritte

[Simulieren des Anmeldeverhaltens mit dem Was-wäre-wenn-Tool für den bedingten Zugriff](troubleshoot-conditional-access-what-if.md)
