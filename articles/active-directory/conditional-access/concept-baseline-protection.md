---
title: Basisrichtlinien für den bedingten Zugriff – Azure Active Directory
description: Basisrichtlinien für den bedingten Zugriff zum Schutz von Organisationen vor gängigen Angriffen
services: active-directory
ms.service: active-directory
ms.subservice: conditional-access
ms.topic: conceptual
ms.date: 11/21/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: calebb, rogoya
ms.collection: M365-identity-device-management
ms.openlocfilehash: a9bb384045c8b2e0a5743fdc301a829792639b7e
ms.sourcegitcommit: 4c831e768bb43e232de9738b363063590faa0472
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/23/2019
ms.locfileid: "74420566"
---
# <a name="what-are-baseline-policies"></a>Was sind Basisrichtlinien?

Basisrichtlinien sind vordefinierte Richtlinien, die dabei helfen, Organisationen vor vielen gängigen Angriffen zu schützen. Zu diesen gängigen Angriffen zählen Kennwortspray, Wiedergabe und Phishing. Basisrichtlinien sind in allen Editionen von Azure AD verfügbar. Microsoft stellt diese Basisschutzrichtlinien für alle Benutzer zur Verfügung, da auf Identitäten basierende Angriffe in den letzten Jahren zugenommen haben. Das Ziel dieser vier Richtlinien ist sicherzustellen, dass bei allen Organisationen eine Basissicherheitsebene ohne zusätzliche Kosten aktiviert ist.  

Für die Verwaltung von Richtlinien für den bedingten Zugriff ist eine Azure AD Premium-Lizenz erforderlich.

## <a name="baseline-policies"></a>Basisrichtlinien

![Basisrichtlinien für bedingten Zugriff im Azure-Portal](./media/concept-baseline-protection/conditional-access-policies.png)

Es gibt vier Basisrichtlinien:

* Benötigt MFA für Admins (Vorschau)
* Endbenutzerschutz (Vorschau)
* Blockieren der Legacyauthentifizierung (Vorschau)
* Anfordern von MFA für die Dienstverwaltung (Vorschau)

Alle vier genannten Basisrichtlinien betreffen bekannte Authentifizierungsabläufe wie POP, IMAP oder ältere Office-Desktopclients.

### <a name="require-mfa-for-admins-preview"></a>Benötigt MFA für Admins (Vorschau)

Aufgrund der Befugnisse und des Zugriffs, über die Administratorkonten verfügen, sollten sie mit Bedacht verwaltet werden. Eine gängige Methode zur Verbesserung des Schutzes von privilegierten Konten ist eine stärkere Form der Kontoüberprüfung bei der Anmeldung. In Azure Active Directory können Sie eine striktere Kontoüberprüfung erreichen, indem Sie fordern, dass Administratoren sich für Azure Multi-Factor Authentication registrieren und die mehrstufige Authentifizierung verwenden.

Das Erfordern der mehrstufigen Authentifizierung für Administratoren (Vorschau) stellt eine Basisrichtlinie dar, bei der für die folgenden Verzeichnisrollen, die als die Azure AD-Rollen mit den höchsten Berechtigungen angesehen werden, mehrstufige Authentifizierung erforderlich ist:

* Globaler Administrator
* SharePoint-Administrator
* Exchange-Administrator
* Administrator für den bedingten Zugriff
* Sicherheitsadministrator
* Helpdeskadministrator/Kennwortadministrator
* Rechnungsadministrator
* Benutzeradministrator

Wenn Ihre Organisation diese Konten in Skripts oder Code verwendet, sollten Sie in Betracht ziehen, diese durch [verwaltete Identitäten](../managed-identities-azure-resources/overview.md) zu ersetzen.

### <a name="end-user-protection-preview"></a>Endbenutzerschutz (Vorschau)

Administratoren mit erhöhten Rechten sind nicht das einzige Ziel bei Angriffen. Angreifer konzentrieren sich im Allgemeinen auf Endbenutzer. Sobald Angreifer Zugang zum System haben, können sie im Namen des ursprünglichen Kontobesitzers auf vertrauliche Informationen zugreifen oder das vollständige Verzeichnis herunterladen und einen Phishing-Angriff auf die gesamte Organisation einleiten. Eine gängige Methode zum besseren Schutz aller Benutzer besteht in einer restriktiveren Kontoüberprüfung, wenn eine risikobehaftete Anmeldung erkannt wird.

Der **Endbenutzerschutz (Vorschau)** stellt eine Basisrichtlinie dar, die alle Benutzer in einem Verzeichnis schützt. Wenn Sie diese Richtlinie aktivieren, müssen sich alle Benutzer innerhalb von 14 Tagen für Azure Multi-Factor Authentication registrieren. Nachdem sie sich für MFA registriert haben, werden Benutzer nur während risikobehafteter Anmeldeversuche zur mehrstufigen Authentifizierung aufgefordert. Kompromittierte Benutzerkonten werden gesperrt, bis das Kennwort zurückgesetzt und Risiken ausgeschlossen werden. 

[!NOTE]
Alle Benutzer, die zuvor mit Risiko gekennzeichnet wurden, werden blockiert, bis das Kennwort durch Aktivierung der Richtlinie zurückgesetzt und das Risiko beseitigt wird.

### <a name="block-legacy-authentication-preview"></a>Blockieren der Legacyauthentifizierung (Vorschau)

Legacyauthentifizierungsprotokolle (z. B. IMAP, SMTP, POP3) sind Protokolle, die normalerweise von älteren E-Mail-Clients für die Authentifizierung verwendet werden. Legacyprotokolle unterstützen keine mehrstufige Authentifizierung. Selbst wenn Sie über eine Richtlinie verfügen, die mehrstufige Authentifizierung für Ihr Verzeichnis erfordert, kann ein Angreifer sich mit einem dieser Legacyprotokolle authentifizieren und die mehrstufige Authentifizierung umgehen.

Die beste Möglichkeit zum Schutz Ihres Kontos vor böswilligen Authentifizierungsanforderungen durch ältere Protokolle ist, diese zu blockieren.

Die Basisrichtlinie zum **Blockieren der Legacyauthentifizierung (Vorschau)** blockiert alle Authentifizierungsanforderungen mit Legacyprotokollen. Die erfolgreiche Anmeldung aller Benutzer setzt moderne Authentifizierung voraus. In Verbindung mit den anderen Basisrichtlinien werden alle Anfragen von Legacyprotokollen blockiert. Darüber hinaus müssen alle Benutzer die mehrstufige Authentifizierung verwenden, wenn dies erforderlich ist. Diese Richtlinie blockiert nicht Exchange ActiveSync.

### <a name="require-mfa-for-service-management-preview"></a>Anfordern von MFA für die Dienstverwaltung (Vorschau)

Organisationen verwenden verschiedenste Azure-Dienste und verwalten diese mit Azure Resource Manager-basierten Tools wie:

* Azure-Portal
* Azure PowerShell
* Azure-Befehlszeilenschnittstelle

Das Verwalten von Ressourcen mit diesen Tools ist eine Aktion, die weitreichende Berechtigungen erfordert. Diese Tools können mandantenweite Konfigurationen wie Diensteinstellungen und die Abonnementabrechnung ändern.

Um privilegierte Aktionen zu schützen, fordert die Richtlinie zum **Erfordern von MFA für die Dienstverwaltung (Vorschau)** eine mehrstufige Authentifizierung von allen Benutzern, die auf das Azure-Portal, Azure PowerShell oder die Azure-Befehlszeilenschnittstelle zugreifen möchten.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen finden Sie unter

* [Allgemeine Richtlinien für bedingten Zugriff](concept-conditional-access-policy-common.md)
* [Fünf Schritte zum Sichern Ihrer Identitätsinfrastruktur](../../security/fundamentals/steps-secure-identity.md)
* [Was ist bedingter Zugriff?](overview.md)
