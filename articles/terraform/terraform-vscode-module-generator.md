---
title: 'Tutorial: Erstellen einer Terraform-Basisvorlage in Azure mithilfe von Yeoman'
description: Hier erfahren Sie, wie Sie eine Terraform-Basisvorlage in Azure mithilfe von Yeoman erstellen.
ms.topic: tutorial
ms.date: 10/26/2019
ms.openlocfilehash: ba81d0ee797fd879fdadc3a6b25ca8f310383f61
ms.sourcegitcommit: 28688c6ec606ddb7ae97f4d0ac0ec8e0cd622889
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2019
ms.locfileid: "74159168"
---
# <a name="tutorial-create-a-terraform-base-template-in-azure-using-yeoman"></a>Tutorial: Erstellen einer Terraform-Basisvorlage in Azure mithilfe von Yeoman

In diesem Tutorial erfahren Sie, wie Sie eine Kombination aus [Terraform](/azure/terraform/) und [Yeoman](https://yeoman.io/) verwenden. Terraform ist ein Tool für die Infrastrukturerstellung in Azure. Yeoman erleichtert die Erstellung von Terraform-Modulen.

In diesem Artikel lernen Sie Folgendes:
> [!div class="checklist"]
> * Erstellen Sie eine Terraform-Basisvorlage mithilfe des Yeoman-Modulgenerators
> * Testen der Terraform-Vorlage mit zwei verschiedenen Methoden
> * Ausführen des Terraform-Moduls unter Verwendung einer Docker-Datei
> * Natives Ausführen des Terraform-Moduls in Azure Cloud Shell

## <a name="prerequisites"></a>Voraussetzungen

- **Azure-Abonnement**: Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/) erstellen, bevor Sie beginnen.
- **Visual Studio Code**: Laden Sie [hier](https://code.visualstudio.com/download) Visual Studio Code für Ihre Plattform herunter.
- **Terraform**: [Installieren Sie Terraform](/azure/virtual-machines/linux/terraform-install-configure ), um das von Yeoman erstellte Modul auszuführen.
- **Docker**: [Installieren Sie Docker](https://www.docker.com/get-started), um das vom Yeoman-Generator erstellte Modul auszuführen.
- **Programmiersprache Go**: [Installieren Sie Go](https://golang.org/), da es sich bei den von Yeoman generierten Testfällen um Code in der Sprache Go handelt.

>[!NOTE]
>Bei den meisten der in diesem Tutorial beschriebenen Verfahren wird die Befehlszeilenschnittstelle verwendet. Die beschriebenen Schritte gelten für alle Betriebssysteme und Befehlszeilentools. In den Beispielen wird PowerShell für die lokale Umgebung und Git Bash für die Cloud Shell-Umgebung verwendet.

## <a name="prepare-your-environment"></a>Vorbereiten der Umgebung

### <a name="install-nodejs"></a>Installieren von Node.js

Sie müssen [Node.js 6.0 oder höher](https://nodejs.org/en/download/) installieren, um Terraform in Cloud Shell zu verwenden.

>[!NOTE]
>Wenn Sie überprüfen möchten, ob Node.js installiert ist, öffnen Sie ein Terminalfenster, und geben Sie `node --version` ein.

### <a name="install-yeoman"></a>Installieren von Yeoman

Führen Sie den folgenden Befehl aus:

```bash
npm install -g yo
```

![Installieren von Yeoman](media/terraform-vscode-module-generator/ymg-npm-install-yo.png)

### <a name="install-the-yeoman-template-for-terraform-module"></a>Installieren der Yeoman-Vorlage für das Terraform-Modul

Führen Sie den folgenden Befehl aus:

```bash
npm install -g generator-az-terra-module
```

![Installieren von generator-az-terra-module](media/terraform-vscode-module-generator/ymg-pm-install-generator-module.png)

Führen Sie den folgenden Befehl aus, um sich zu vergewissern, dass Yeoman installiert ist:

```bash
yo --version
```

### <a name="create-a-directory-for-the-yeoman-generated-module"></a>Erstellen eines Verzeichnisses für das von Yeoman generierte Modul

Die Yeoman-Vorlage generiert Dateien im aktuellen Verzeichnis. Aus diesem Grund müssen Sie ein Verzeichnis erstellen.

Dieses leere Verzeichnis muss unter „$GOPATH/src“ erstellt werden. Weitere Informationen zu diesem Pfad finden Sie im Artikel [Festlegen von GOPATH](https://github.com/golang/go/wiki/SettingGOPATH).

1. Navigieren Sie zu dem Verzeichnis, unter dem ein neues Verzeichnis erstellt werden soll.

1. Führen Sie den folgenden Befehl aus, und ersetzen Sie dabei den Platzhalter. In diesem Beispiel wird der Verzeichnisname `GeneratorDocSample` verwendet.

    ```bash
    mkdir <new-directory-name>
    ```

    ![mkdir](media/terraform-vscode-module-generator/ymg-mkdir-GeneratorDocSample.png)

1. Navigieren Sie zu dem neuen Verzeichnis:

    ```bash
    cd <new-directory-name>
    ```

    ![Navigieren Sie zu Ihrem neuen Verzeichnis.](media/terraform-vscode-module-generator/ymg-cd-GeneratorDocSample.png)

## <a name="create-a-base-module-template"></a>Erstellen einer Basismodulvorlage

1. Führen Sie den folgenden Befehl aus:

    ```bash
    yo az-terra-module
    ```

1. Führen Sie die Anweisungen auf dem Bildschirm aus, um die folgenden Informationen anzugeben:

    - **Terraform module project Name** (Name des Terraform-Modulprojekts): In diesem Beispiel wird `doc-sample-module` verwendet.

        ![Projektname](media/terraform-vscode-module-generator/ymg-project-name.png)       


    - **Möchten Sie die Docker-Imagedatei einbeziehen?** Geben Sie `y` ein. Wenn Sie `n` auswählen, unterstützt der generierte Modulcode nur die Ausführung im nativen Modus.

        ![Docker-Imagedatei einbeziehen?](media/terraform-vscode-module-generator/ymg-include-docker-image-file.png) 

1. Listen Sie die Verzeichnisinhalte auf, um die erstellten resultierenden Dateien anzuzeigen:

    ```bash
    ls
    ```

    ![Erstellte Dateien auflisten](media/terraform-vscode-module-generator/ymg-ls-GeneratorDocSample-files.png)

## <a name="review-the-generated-module-code"></a>Überprüfen des generierte Modulcodes

1. Starten Sie Visual Studio Code.

1. Wählen Sie in der Menüleiste **Datei > Ordner öffnen** aus, und wählen Sie den Ordner aus, den Sie erstellt haben.

    ![Visual Studio Code](media/terraform-vscode-module-generator/ymg-open-in-vscode.png)

Vom Yeoman-Modulgenerator wurden folgende Dateien erstellt. Weitere Informationen zu diesen Dateien und zu ihrer Verwendung finden Sie unter [Terratest in Terraform-Modulen](https://mseng.visualstudio.com/VSJava/_git/Terraform?path=%2FTerratest%20Introduction.md&version=GBmaster).

- `main.tf`: Definiert ein Modul namens `random-shuffle`. Die Eingabe ist eine Zeichenfolgenliste (`string_list`). Die Ausgabe ist die Anzahl der Permutationen.
- `variables.tf`: Definiert die vom Modul verwendeten Eingabe- und Ausgabevariablen.
- `outputs.tf`: Definiert die Ausgabe des Moduls. Hier ist es der von `random_shuffle` zurückgegebene Wert (ein integriertes Terraform-Modul).
- `Rakefile`: Definiert die Schritte im Buildprozess. Diese Schritte umfassen:
    - `build`: Überprüft die Formatierung der Datei „main.tf“.
    - `unit`: Das generierte Modulgerüst enthält keinen Code für einen Komponententest. Wenn Sie ein Komponententestszenario angeben möchten, fügen Sie diesen Code hier hinzu.
    - `e2e`: Führt einen End-to-End-Test des Moduls aus.
- `test`
    - Testfälle werden in Go geschrieben.
    - Alle Codes im Test sind End-to-End-Tests.
    - Bei End-to-End-Tests wird versucht, alle unter `fixture`definierten Elemente bereitzustellen. Die Ergebnisse in der Datei `template_output.go` werden mit den vordefinierten erwarteten Werten verglichen.
    - `Gopkg.lock` und `Gopkg.toml`: Definieren die Abhängigkeiten. 

## <a name="test-your-new-terraform-module-using-a-docker-file"></a>Testen Ihres neuen Terraform-Moduls mithilfe einer Docker-Datei

In diesem Abschnitt erfahren Sie, wie Sie ein Terraform-Modul mithilfe einer Docker-Datei testen.

>[!NOTE]
>Das Modul wird in diesem Beispiel nicht in Azure, sondern lokal ausgeführt.

### <a name="confirm-docker-is-installed-and-running"></a>Bestätigen, dass Docker installiert ist und ausgeführt wird

Geben Sie an einer Befehlszeile `docker version` ein.

![Docker-Version](media/terraform-vscode-module-generator/ymg-docker-version.png)

Die resultierende Ausgabe bestätigt, dass Docker installiert ist.

Um zu bestätigen, dass Docker wirklich ausgeführt wird, geben Sie `docker info` ein.

![Docker-Info](media/terraform-vscode-module-generator/ymg-docker-info.png)

### <a name="set-up-a-docker-container"></a>Einrichten eines Docker-Containers

1. Geben Sie an einer Eingabeaufforderung Folgendes ein:

    `docker build --build-arg BUILD_ARM_SUBSCRIPTION_ID= --build-arg BUILD_ARM_CLIENT_ID= --build-arg BUILD_ARM_CLIENT_SECRET= --build-arg BUILD_ARM_TENANT_ID= -t terra-mod-example .`.

    Die Nachricht **Erfolgreich erstellt** wird angezeigt.

    ![Meldung bei erfolgreicher Erstellung](media/terraform-vscode-module-generator/ymg-successfully-built.png)

1. Geben Sie an der Eingabeaufforderung `docker image ls` ein. Daraufhin wird das erstellte Modul `terra-mod-example` aufgelistet.

    ![Liste mit dem neuen Modul](media/terraform-vscode-module-generator/ymg-repository-results.png)

1. Geben Sie `docker run -it terra-mod-example /bin/sh` ein. Nachdem Sie den `docker run` Befehl ausgeführt haben, befinden Sie sich in der Docker-Umgebung. Nun können Sie die Datei mithilfe des Befehls `ls` ermitteln.

    ![Dateiliste in Docker](media/terraform-vscode-module-generator/ymg-list-docker-file.png)

### <a name="build-the-module"></a>Erstellen des Moduls

1. Führen Sie den folgenden Befehl aus:

    ```bash
    bundle install
    ```

1. Führen Sie den folgenden Befehl aus:

    ```bash
    rake build
    ```

    ![Rake build](media/terraform-vscode-module-generator/ymg-rake-build.png)

### <a name="run-the-end-to-end-test"></a>Durchführen des End-to-End-Tests

1. Führen Sie den folgenden Befehl aus:

    ```bash
    rake e2e
    ```

1. Nach einigen Augenblicken wird die Meldung **ERFOLGREICH** angezeigt.

    ![ERFOLGREICH](media/terraform-vscode-module-generator/ymg-pass.png)

1. Geben Sie `exit` ein, um den Test abzuschließen und die Docker-Umgebung zu beenden.

## <a name="use-yeoman-generator-to-create-and-test-a-module-in-cloud-shell"></a>Verwenden des Yeoman-Generators zum Erstellen und Testen eines Moduls in Cloud Shell

In diesem Abschnitt wird zum Erstellen und Testen eines Moduls in Cloud Shell der Yeoman-Generator verwendet. Die Verwendung von Cloud Shell anstelle einer Docker-Datei vereinfacht den Prozess erheblich. Bei Verwendung von Cloud Shell sind die folgenden Produkte bereits vorinstalliert:

- Node.js
- Yeoman
- Terraform

### <a name="start-a-cloud-shell-session"></a>Starten einer Cloud Shell-Sitzung.

1. Starten Sie eine Azure Cloud Shell-Sitzung entweder über das [Azure-Portal](https://portal.azure.com/), über [shell.azure.com](https://shell.azure.com) oder über die [mobile Azure-App](https://azure.microsoft.com/features/azure-portal/mobile-app/).

1. Die Seite **Willkommen bei Azure Cloud Shell** wird geöffnet. Wählen Sie **Bash (Linux)** aus.

    ![Willkommen bei Azure Cloud Shell](media/terraform-vscode-module-generator/ymg-welcome-to-azure-cloud-shell.png)

1. Wenn Sie noch kein Azure-Speicherkonto eingerichtet haben, wird folgender Bildschirm angezeigt. Klicken Sie auf **Speicher erstellen**.

    ![Für Sie wurde kein Speicher bereitgestellt.](media/terraform-vscode-module-generator/ymg-you-have-no-storage-mounted.png)

1. Azure Cloud Shell wird in der Shell gestartet, die Sie zuvor ausgewählt haben, und zeigt Informationen zu dem Cloudlaufwerk an, das gerade für Sie erstellt wurde.

    ![Cloudlaufwerk wurde erstellt](media/terraform-vscode-module-generator/ymg-your-cloud-drive-has-been-created-in.png)

### <a name="prepare-a-directory-to-hold-your-terraform-module"></a>Vorbereiten eines Verzeichnisses für Ihr Terraform-Modul

1. Zu diesem Zeitpunkt wurde GOPATH in Ihren Umgebungsvariablen bereits von Cloud Shell für Sie konfiguriert. Geben Sie zum Anzeigen des Pfads `go env` ein.

1. Erstellen Sie das Verzeichnis „$GOPATH“, sofern es noch nicht vorhanden ist: Geben Sie `mkdir ~/go` ein.

1. Erstellen Sie ein Verzeichnis innerhalb des Verzeichnisses „$GOPATH“. In diesem Verzeichnis werden die verschiedenen Projektverzeichnisse platziert, die in diesem Beispiel erstellt werden. 

    ```bash
    mkdir ~/go/src
    ```

1. Erstellen Sie ein Verzeichnis für Ihr Terraform-Modul, und ersetzen Sie dabei den Platzhalter. In diesem Beispiel wird der Verzeichnisname `my-module-name` verwendet.

    ```bash
    mkdir ~/go/src/<your-module-name>
    ```

1. Navigieren Sie zu Ihrem Modulverzeichnis: 

    ```bash
    cd ~/go/src/<your-module-name>
    ```

### <a name="create-and-test-your-terraform-module"></a>Erstellen und Testen Ihres Terraform-Moduls

1. Führen Sie den folgenden Befehl aus, und befolgen Sie die Anweisungen. Wenn Sie gefragt werden, ob Sie die Docker-Dateien erstellen möchten, geben Sie `N` ein.

    ```bash
    yo az-terra-module
    ```

1. Führen Sie den folgenden Befehl aus, um die Abhängigkeiten zu installieren:

    ```bash
    bundle install
    ```

1. Führen Sie den folgenden Befehl aus, um das Modul zu erstellen:

    ```bash
    rake build
    ```

    ![Rake build](media/terraform-vscode-module-generator/ymg-rake-build.png)

1. Führen Sie den folgenden Befehl aus, um den Test auszuführen:

    ```bash
    rake e2e
    ```

    ![Ergebnisse des Testdurchlaufs](media/terraform-vscode-module-generator/ymg-pass.png)

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Tutorial: Konfigurieren der Azure Terraform-Erweiterung für Visual Studio Code](/azure/terraform/terraform-vscode-extension)