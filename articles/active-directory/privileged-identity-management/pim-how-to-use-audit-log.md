---
title: Anzeigen des Überwachungsberichts für Azure AD-Rollen in PIM – Azure AD | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie den Überwachungsverlauf für Azure AD-Rollen in Azure AD Privileged Identity Management (PIM) anzeigen.
services: active-directory
documentationcenter: ''
author: curtand
manager: daveba
editor: ''
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.subservice: pim
ms.date: 10/22/2019
ms.author: curtand
ms.custom: pim
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c4a157d8d5bcd281ca9fee488e58c455034e898
ms.sourcegitcommit: 49cf9786d3134517727ff1e656c4d8531bbbd332
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2019
ms.locfileid: "74022061"
---
# <a name="view-audit-history-for-azure-ad-roles-in-pim"></a>Anzeigen des Überwachungsverlaufs für Azure AD-Rollen in PIM

Im Überwachungsverlauf von Privileged Identity Management (PIM) können Sie alle Rollenzuweisungen und -aktivierungen für alle privilegierten Rollen in den letzten 30 Tagen anzeigen. Wenn Sie den vollständigen Überwachungsverlauf von Aktivitäten in Ihrer Azure Active Directory-Organisation (Azure AD-Organisation) einschließlich der Aktivitäten von Administratoren, Endbenutzern und Synchronisierungen anzeigen möchten, können Sie die [Azure Active Directory-Sicherheits- und Aktivitätsberichte](../reports-monitoring/overview-reports.md) verwenden.

## <a name="view-audit-history"></a>Anzeigen des Überwachungsverlaufs

Führen Sie die folgenden Schritte aus, um den Überwachungsverlauf für Azure AD-Rollen anzuzeigen.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/) mit einem Benutzer an, der ein Mitglied der Rolle [Administrator für privilegierte Rollen](../users-groups-roles/directory-assign-admin-roles.md#privileged-role-administrator) ist.

1. Öffnen Sie **Azure AD Privileged Identity Management**.

1. Klicken Sie auf **Azure AD-Rollen**.

1. Klicken Sie auf **Verlauf der Verzeichnisrollenüberwachung**.

    Abhängig von Ihrem Überwachungsverlauf wird ein Säulendiagramm zusammen mit der Gesamtzahl der Aktivierungen, der maximalen Aktivierungen pro Tag und der durchschnittlichen Aktivierungen pro Tag angezeigt.

    ![Verlauf der Verzeichnisrollenüberwachung](media/pim-how-to-use-audit-log/directory-roles-audit-history.png)

    Am unteren Rand der Seite wird eine Tabelle mit Informationen zu jeder Aktion im verfügbaren Überwachungsverlauf angezeigt. Die Spalten haben die folgende Bedeutung:

    | Column | BESCHREIBUNG |
    | --- | --- |
    | Time | Der Zeitpunkt, zu dem die Aktion erfolgt ist. |
    | Anforderer | Der Benutzer, der die Rollenaktivierung oder -änderung angefordert hat. Wenn der Wert **Azure System**lautet, suchen Sie im Azure-Überwachungsverlauf nach weiteren Informationen. |
    | Aktion | Die vom Anforderer ausgeführten Aktionen. Aktionen können „Assign“, „Unassign“, „Activate“, „Deactivate“ oder „AddedOutsidePIM“ umfassen. |
    | Member | Der Benutzer, der eine Rolle aktiviert oder einer Rolle zugewiesen ist. |
    | Role | Die Rolle, die dem Benutzer zugewiesen ist oder die durch den Benutzer aktiviert wurde. |
    | Erläuterung | Text, der während der Aktivierung in das Feld „Grund“ eingegeben wurde. |
    | Ablauf | Zeitpunkt, an dem die aktivierte Rolle abläuft. Gilt nur für berechtigte Rollenzuweisungen. |

1. Um den Überwachungsverlauf zu sortieren, klicken Sie auf **Zeit**, **Aktion** und **Rolle**.

## <a name="filter-audit-history"></a>Filtern des Überwachungsverlaufs

1. Klicken Sie am oberen Rand der Seite mit dem Überwachungsverlauf auf die Schaltfläche **Filter**.

    Der Bereich **Diagrammparameter aktualisieren** wird angezeigt.

1. Wählen Sie in **Zeitbereich** einen Zeitraum aus.

1. Aktivieren Sie unter **Rollen** die Kontrollkästchen für die Rollen, die Sie anzeigen möchten.

    ![Bereich „Diagrammparameter aktualisieren“](media/pim-how-to-use-audit-log/update-chart-parameters.png)

1. Klicken Sie auf **Fertig**, um den gefilterten Überwachungsverlauf anzuzeigen.

## <a name="next-steps"></a>Nächste Schritte

- [Anzeigen von Aktivitäten und des Überwachungsverlaufs für Azure-Ressourcenrollen in Privileged Identity Management](azure-pim-resource-rbac.md)
