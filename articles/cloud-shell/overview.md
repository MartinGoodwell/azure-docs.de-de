---
title: "Übersicht über Azure Cloud Shell (Vorschau) | Microsoft-Dokumentation"
description: "Übersicht über Azure Cloud Shell."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: 
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: juluk
ms.translationtype: Human Translation
ms.sourcegitcommit: e7da3c6d4cfad588e8cc6850143112989ff3e481
ms.openlocfilehash: 63f1c468b5f8f4b0bb298cb67adea8c01b065427
ms.contentlocale: de-de
ms.lasthandoff: 05/16/2017

---
# <a name="overview-of-azure-cloud-shell-preview"></a>Übersicht über Azure Cloud Shell (Vorschau)
Azure Cloud Shell ist eine interaktive, über den Browser zugängliche Shell für die Verwaltung von Azure-Ressourcen.

![](media/startup.gif)

## <a name="features"></a>Features
### <a name="browser-based-shell-experience"></a>Browserbasierte Shelloberfläche
Cloud Shell ermöglicht den Zugriff auf eine browserbasierte Befehlszeilenumgebung, die extra auf Azure-Verwaltungsaufgaben ausgerichtet ist. Nutzen Sie Cloud Shell, um unabhängig von einem lokalen Computer in einer Weise zu arbeiten, die Ihnen nur die Cloud bieten kann.

### <a name="pre-configured-azure-workstation"></a>Vorkonfigurierte Azure-Arbeitsstation
In Cloud Shell sind gängige Befehlszeilentools und Sprachunterstützung vorinstalliert, damit Sie schneller arbeiten können.

[Hier können Sie die vollständige Toolliste für Azure Cloud Shell anzeigen.](features.md#tools)

### <a name="automatic-authentication"></a>Automatische Authentifizierung
Cloud Shell führt in jeder Sitzung eine sichere Authentifizierung durch, sodass Sie über die Azure CLI 2.0 sofort auf Ihre Ressourcen zugreifen können.

### <a name="connect-your-azure-file-storage"></a>Herstellen einer Verbindung mit Ihrem Azure-Dateispeicher
Cloud Shell-Computer sind temporär und erfordern folglich das Einbinden einer Azure-Dateifreigabe als `clouddrive`, um Ihr $Home-Verzeichnis dauerhaft bereitzustellen.
Beim ersten Start werden Sie von Cloud Shell darauf hingewiesen, dass eine Ressourcengruppe, ein Speicherkonto und eine Dateifreigabe in Ihrem Namen erstellt werden. Dieser Schritt ist nur einmal erforderlich. Diese Komponenten werden für alle Sitzungen automatisch angefügt. 

![](media/storage-prompt.png)

In Ihrem Namen wird ein LRS-Speicherkonto mit einer Azure-Dateifreigabe erstellt, die standardmäßig ein 5-GB-Datenträgerimage umfasst. Die Dateifreigabe wird zum Zweck der Interaktion mit dem Datenträgerimage, das zum Synchronisieren und dauerhaften Bereitstellen Ihres $Home-Verzeichnisses verwendet wird, als `clouddrive` eingebunden. Es gelten die üblichen Speicherkosten.

Drei Ressourcen werden in Ihrem Namen erstellt:
1. Eine Ressourcengruppe namens `cloud-shell-storage-<region>`
2. Ein Speicherkonto namens `cs-uniqueGuid`
3. Eine Dateifreigabe namens `cs-<user>-<domain>-com-uniqueGuid`

> [!Note]
> Alle Dateien in Ihrem $Home-Verzeichnis, wie etwa SSH-Schlüssel, werden beständig in Ihrem Datenträgerimage gespeichert, das in der eingebundenen Dateitreigabe gespeichert ist. Wenden Sie beim Speichern von Dateien in Ihrem $Home-Verzeichnis und der eingebundenen Dateifreigabe bewährte Methoden an.

[Weitere Informationen zu Cloud Shell-Speicher, dem Aktualisieren von Dateifreigaben und dem Upload/Download von Dateien.] (persisting-shell-storage.md).

## <a name="concepts"></a>Konzepte
* Cloud Shell wird auf einem temporären Computer ausgeführt, der pro Sitzung und pro Benutzer bereitgestellt wird.
* Nach 10 Minuten ohne interaktive Aktivitäten tritt für Cloud Shell ein Timeout ein.
* Der Zugriff auf Cloud Shell ist nur möglich, wenn eine Dateifreigabe angefügt ist.
* Cloud Shell wird ein Computer pro Benutzerkonto zugewiesen.
* Berechtigungen werden auf einen normalen Linux-Benutzer festgelegt.

[Weitere Informationen zu allen Cloud Shell-Features.](features.md)

## <a name="examples"></a>Beispiele
* Erstellen oder Bearbeiten von Skripts zum Verwalten von Azure-Ressourcen über einen beliebigen Browser
* Gleichzeitiges Verwalten von Ressourcen über das Azure-Portal und die Azure CLI 2.0
* Testen der Azure CLI 2.0

[Probieren Sie all diese Beispiele beim Cloud Shell-Schnellstart aus.](quickstart.md)

## <a name="pricing"></a>Preise
Der Computer, auf dem Cloud Shell gehostet wird, ist kostenlos. Als Voraussetzung muss eine Azure-Dateifreigabe eingebunden sein, um Ihr $Home-Verzeichnis dauerhaft zu speichern. Es gelten die üblichen Speicherkosten.

## <a name="supported-browsers"></a>Unterstützte Browser
Cloud Shell wird für Chrome, Edge und Safari empfohlen. Cloud Shell wird zwar für Chrome, Firefox, Safari, Internet Explorer und Edge unterstützt, unterliegt jedoch bestimmten Browsereinstellungen.
Informationen zu bestimmten bekannten Einschränkungen finden Sie unter [Einschränkungen von Cloud Shell](limitations.md).
