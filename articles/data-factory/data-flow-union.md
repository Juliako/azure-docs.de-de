---
title: 'Azure Data Factory Mapping Data Flow: Transformation für neue Verzweigung'
description: 'Azure Data Factory Mapping Data Flow: Transformation für neue Verzweigung'
author: kromerm
ms.author: makromer
ms.reviewer: douglasl
ms.service: data-factory
ms.topic: conceptual
ms.date: 02/12/2019
ms.openlocfilehash: 4832cd2036f615d1e90d5e7a21c1a9832c2fa837
ms.sourcegitcommit: bb65043d5e49b8af94bba0e96c36796987f5a2be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/16/2019
ms.locfileid: "72387132"
---
# <a name="mapping-data-flow-union-transformation"></a>Mapping Data Flow: Vereinigungstransformation



Union kombiniert mehrere Datenströme zu einem einzigen, wobei die SQL Union dieser Datenströme die neue Ausgabe der Union-Transformation ist. Alle Schemas aus jedem Eingabestream werden innerhalb Ihres Datenflusses kombiniert, ohne dass Sie einen Joinschlüssel benötigen.

Sie können die n-Anzahl von Streams in der Einstellungstabelle kombinieren, indem Sie neben jeder konfigurierten Zeile auf das Symbol „+“ klicken, einschließlich sowohl Quelldaten als auch Streams aus vorhandenen Transformationen in Ihrem Datenfluss.

![Vereinigungstransformation](media/data-flow/union.png "Vereinigung")

In diesem Fall können Sie unterschiedliche Metadaten aus mehreren Quellen (in diesem Beispiel drei verschiedene Quelldateien) zusammenführen und zu einem einzigen Stream kombinieren:

![Vereinigungstransformation: Übersicht](media/data-flow/union111.png "Vereinigung 1")

Um dies zu erreichen, fügen Sie zusätzliche Zeilen in „Union Settings“ (Vereinigungseinstellungen) hinzu, indem Sie alle Quellen einbeziehen, die Sie hinzufügen möchten. Ein allgemeiner Verweis oder Joinschlüssel ist nicht notwendig:

![Vereinigungstransformation: Einstellungen](media/data-flow/unionsettings.png "Vereinigungseinstellungen")

Wenn Sie nach Ihrer Vereinigung eine Auswahltransformation festlegen, können Sie überlappende Felder oder Felder umbenennen, die in Quellen ohne Kopfzeilen nicht benannt wurden. Klicken Sie auf „Inspekt“ (Überprüfen), um die kombinierten Metadaten mit insgesamt 132 Spalten in diesem Beispiel aus drei verschiedenen Quellen anzuzeigen:

![Endgültige Vereinigungstransformation](media/data-flow/union333.png "Vereinigung 3")

## <a name="name-and-position"></a>Name und Position

Wenn Sie „Union by name“ (Vereinigung anhand des Namens) wählen, wird jeder Spaltenwert mit einem neuen verketteten Metadatenschema aus jeder Quelle in die entsprechende Spalte übernommen.

Wenn Sie "Union by position" (Vereinigung anhand der Position) wählen, wird jeder Spaltenwert aus jeder entsprechenden Quelle an der ursprünglichen Position abgelegt, was zu einem neuen kombinierten Stream aus Daten führt, bei dem die Daten aus jeder Quelle zum gleichen Stream hinzugefügt werden:

![Vereinigungsausgabe](media/data-flow/unionoutput.png "Vereinigungsausgabe")

## <a name="next-steps"></a>Nächste Schritte

Erkunden Sie ähnliche Transformationen, einschließlich [Join](data-flow-join.md) und [Exists](data-flow-exists.md).
