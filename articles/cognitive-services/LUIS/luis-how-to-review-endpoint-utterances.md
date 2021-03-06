---
title: Überprüfen von Benutzeräußerungen – LUIS
titleSuffix: Azure Cognitive Services
description: Überprüfen Sie die beim aktiven Lernen erfassten Äußerungen, um die Absicht auszuwählen und Entitäten für reale Äußerungen zu markieren. Akzeptieren Sie die Änderungen, und führen Sie das Training und die Veröffentlichung durch.
services: cognitive-services
author: diberry
manager: nitinme
ms.custom: seodec18
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: conceptual
ms.date: 11/15/2019
ms.author: diberry
ms.openlocfilehash: 67953f552b5b2bcdd7d13253548227e57dab8548
ms.sourcegitcommit: 2d3740e2670ff193f3e031c1e22dcd9e072d3ad9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/16/2019
ms.locfileid: "74132653"
---
# <a name="how-to-improve-the-luis-app-by-reviewing-endpoint-utterances"></a>Verbessern der LUIS-App durch Überprüfen der Endpunktäußerungen

Der Prozess der Überprüfung von Endpunktäußerungen auf korrekte Vorhersagen wird als [Aktives Lernen](luis-concept-review-endpoint-utterances.md) bezeichnet. Beim aktiven Lernen werden Endpunktabfragen erfasst und die Äußerungen des Benutzers ausgewählt, bei denen es sich nicht sicher ist. Sie überprüfen diese Äußerungen, um die Absicht auszuwählen und Entitäten für diese realen Äußerungen zu markieren. Akzeptieren Sie diese Änderungen in Ihren Beispieläußerungen, dann trainieren und veröffentlichen Sie sie. Dann werden Äußerungen von LUIS genauer identifiziert.

Wenn viele Personen an einer LUIS-App beteiligt sind, 

[!INCLUDE [Uses preview portal](includes/uses-portal-preview.md)]

## <a name="enable-active-learning"></a>Aktivieren des aktiven Lernens

Um das aktive Lernen zu aktivieren, müssen Sie Benutzerabfragen protokollieren. Dies wird durch Aufrufen der [Endpunktabfrage](luis-get-started-create-app.md#query-the-v3-api-prediction-endpoint) mit dem `log=true`-Abfragezeichenfolgenparameter und -wert erreicht.

## <a name="correct-intent-predictions-to-align-utterances"></a>Korrigieren von Absichtsvorhersagen zum Ausrichten von Äußerungen

Für jede Äußerung wird eine vorgeschlagene Absicht in der Spalte **Aligned intent** (Zugeordnete Absicht) angezeigt. 

> [!div class="mx-imgBorder"]
> [![Überprüfen der Endpunktäußerungen, bei denen LUIS unsicher ist](./media/label-suggested-utterances/review-endpoint-utterances.png)](./media/label-suggested-utterances/review-endpoint-utterances.png#lightbox)

Wenn Sie dieser Absicht zustimmen, aktivieren Sie das Kontrollkästchen. Wenn Sie mit dem Vorschlag nicht einverstanden sind, wählen Sie die richtige Absicht in der Dropdownliste der zugeordneten Absichten aus, und aktivieren Sie dann rechts neben der zugeordneten Absicht das Kontrollkästchen. Nachdem Sie das Kontrollkästchen aktiviert haben, wird die Äußerung zu der Absicht verschoben und aus der Liste **Endpunktäußerungen überprüfen** entfernt. 

> [!TIP]
> Es ist wichtig, zur Seite mit den Absichtsdetails zu wechseln, um die Entitätsvorhersagen aus allen Beispieläußerungen aus der Liste **Endpunktäußerungen überprüfen** zu überprüfen und zu korrigieren.

## <a name="delete-utterance"></a>Löschen einer Äußerung

Jede Äußerung kann aus der Überprüfungsliste gelöscht werden. Nach dem Löschen wird sie nicht mehr in der Liste angezeigt. Dies gilt auch dann, wenn der Benutzer die gleiche Äußerung am Endpunkt eingibt. 

Wenn Sie nicht wissen, ob Sie die Äußerung löschen sollten, verschieben Sie sie zur Absicht „None“, oder erstellen Sie eine neue Absicht, z. B. `miscellaneous`, und verschieben Sie die Äußerung in diese Absicht. 

## <a name="disable-active-learning"></a>Deaktivieren des aktiven Lernens

Um das aktive Lernen zu deaktivieren, protokollieren Sie keine Benutzerabfragen. Dies wird erreicht, indem die [Endpunktabfrage](luis-get-started-create-app.md#query-the-v2-api-prediction-endpoint) mit dem QueryString-Parameter `log=false` und dem Wert oder nicht mit dem QueryString-Wert festgelegt wird, da der Standardwert „false“ ist.

## <a name="next-steps"></a>Nächste Schritte

Um zu testen, wie die Leistung nach dem Bezeichnen der vorgeschlagenen Äußerungen verbessert wird, können Sie auf die Testkonsole zugreifen, die Sie im oberen Bereich **Test** auswählen. Anleitungen zum Testen Ihrer App mit der Testkonsole finden Sie unter [Trainieren und Testen Ihrer App](luis-interactive-test.md).
