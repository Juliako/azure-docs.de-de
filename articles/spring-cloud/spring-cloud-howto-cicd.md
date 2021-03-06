---
title: CI/CD für Azure Spring Cloud
description: CI/CD für Azure Spring Cloud
author: jpconnock
ms.service: spring-cloud
ms.topic: conceptual
ms.date: 10/04/2019
ms.author: jeconnoc
ms.openlocfilehash: c19d32f0be2eb817f9f7d73e6c6eaad8d90ce350
ms.sourcegitcommit: c62a68ed80289d0daada860b837c31625b0fa0f0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2019
ms.locfileid: "73607800"
---
# <a name="cicd-for-azure-spring-cloud"></a>CI/CD für Azure Spring Cloud

Continuous Integration- und Continuous Delivery-Tools (CI/CD) ermöglichen Entwicklern die schnelle Bereitstellung von Updates für vorhandene Anwendungen mit minimalem Aufwand und Risiko. Mit Azure DevOps können Sie diese wichtigen Aufträge organisieren und steuern. Derzeit bietet Azure Spring Cloud kein bestimmtes Azure DevOps-Plug-In.  Sie können jedoch Ihre Spring Cloud-Anwendungen mit DevOps integrieren, indem Sie eine [Azure CLI-Aufgabe](https://docs.microsoft.com/azure/devops/pipelines/tasks/deploy/azure-cli?view=azure-devops) verwenden. In diesem Artikel erfahren Sie, wie Sie eine Azure CLI-Aufgabe mit Azure Spring Cloud für die Integration mit Azure DevOps verwenden.

## <a name="create-an-azure-resource-manager-service-connection"></a>Erstellen einer Azure Resource Manager-Dienstverbindung

Lesen Sie [diesen Artikel](https://docs.microsoft.com/azure/devops/pipelines/library/connect-to-azure?view=azure-devops), um zu erfahren, wie Sie eine Azure Resource Manager-Dienstverbindung mit Ihrem Azure DevOps-Projekt herstellen. Achten Sie darauf, dasselbe Abonnement auszuwählen, das Sie für Ihre Azure Spring Cloud-Dienstinstanz verwenden.

## <a name="azure-cli-task-templates"></a>Vorlagen für Azure CLI-Aufgaben

### <a name="deploy-artifacts"></a>Bereitstellen von Artefakten

Sie können Ihre Projekte mit einer Reihe von `tasks` erstellen und bereitstellen. In diesem Codeausschnitt wird zunächst eine Maven-Aufgabe zum Erstellen der Anwendung definiert, gefolgt von einer zweiten Aufgabe, die die JAR-Datei mithilfe der Azure CLI-Erweiterung für Azure Spring Cloud bereitstellt.

```yaml
steps:
- task: Maven@3
  inputs:
    mavenPomFile: 'pom.xml'
- task: AzureCLI@1
  inputs:
    azureSubscription: <your service connection name>
    scriptLocation: inlineScript
    inlineScript: |
      az extension add -y --source https://azureclitemp.blob.core.windows.net/spring-cloud/spring_cloud-0.1.0-py2.py3-none-any.whl
      az spring-cloud app deploy --resource-group <your-resource-group> --service <your-spring-cloud-service> --name <app-name> --jar-path ./target/your-result-jar.jar
      # deploy other app
```

### <a name="deploy-from-source"></a>Bereitstellen aus der Quelle

Es ist möglich, die Bereitstellung direkt in Azure durchzuführen, ohne einen separaten Buildschritt auszuführen.

```yaml
- task: AzureCLI@1
  inputs:
    azureSubscription: <your service connection name>
    scriptLocation: inlineScript
    inlineScript: |
      az extension add -y --source https://azureclitemp.blob.core.windows.net/spring-cloud/spring_cloud-0.1.0-py2.py3-none-any.whl
      az spring-cloud app deploy --resource-group <your-resource-group> --service <your-spring-cloud-service> --name <app-name>

      # or if it is a multi-module project
      az spring-cloud app deploy --resource-group <your-resource-group> --service <your-spring-cloud-service> --name <app-name> --target-module relative/path/to/module
```
