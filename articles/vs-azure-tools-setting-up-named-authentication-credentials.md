---
title: Einrichten benannter Authentifizierungsanmeldeinformationen | Microsoft Docs
description: "Erfahren Sie, wie Sie die Anmeldeinformationen angeben, mit denen Visual Studio Anforderungen für Azure authentifizieren kann, um eine Anwendung von Visual Studio aus in Azure zu veröffentlichen oder einen vorhandenen Clouddienst zu überwachen. "
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: tarcher
translationtype: Human Translation
ms.sourcegitcommit: 01623fa76175091439d5a571fb8b8f96aee01c4c
ms.openlocfilehash: 03875b4215943a8bbabeb15610776a221cbf7b71


---
# <a name="setting-up-named-authentication-credentials"></a>Einrichten benannter Authentifizierungsanmeldeinformationen
Geben Sie die Anmeldeinformationen an, mit denen Visual Studio Anforderungen für Azure authentifizieren kann, um eine Anwendung von Visual Studio aus in Azure zu veröffentlichen oder einen vorhandenen Clouddienst zu überwachen. Es gibt verschiedene Stellen in Visual Studio, an denen Sie sich anmelden können, um diese Anmeldeinformationen bereitzustellen. Beispielsweise können Sie im Server-Explorer das Kontextmenü des Knotens **Azure** öffnen und **Mit Azure verbinden** auswählen. Wenn Sie sich anmelden, stehen die Abonnementinformationen, die dem Azure-Konto zugeordnet sind, in Visual Studio zur Verfügung. Sie müssen keine weiteren Schritte ausführen.

Die Azure-Tools unterstützen auch eine ältere Möglichkeit zum Bereitstellen von Anmeldeinformationen mithilfe der Abonnementdatei (.publishsettings). In diesem Thema wird diese Methode beschrieben, die in Azure SDK 2.2 weiterhin unterstützt wird.

Die folgenden Elemente sind für die Authentifizierung bei Azure erforderlich.

* Ihre Abonnement-ID
* Ein gültiges X.509 v3-Zertifikat

> [!NOTE]
> Der Schlüssel für das X.509 v3-Zertifikat muss mindestens 2048 Bit lang sein. Von Azure werden alle Zertifikate abgelehnt, die diese Anforderung nicht erfüllen oder ungültig sind.
>
>

Visual Studio verwendet die Abonnement-ID zusammen mit den Zertifikatdaten als Anmeldeinformationen. Die entsprechenden Anmeldeinformationen werden in der Abonnementdatei (.publishsettings) verwiesen wird, enthält einen öffentlichen Schlüssel für das Zertifikat. Die Abonnementdatei kann Anmeldeinformationen für mehrere Abonnements enthalten.

Im Dialogfeld **Neues Abonnement/Abonnement bearbeiten** können Sie die Abonnementinformationen bearbeiten, wie weiter unten in diesem Thema erläutert.

Wenn Sie ein Zertifikat selbst erstellen möchten, finden Sie die entsprechenden Anweisungen unter [Erstellen und Hochladen eines Verwaltungszertifikats für Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx). Laden Sie anschließend das Zertifikat manuell in das [klassische Azure-Portal](http://go.microsoft.com/fwlink/?LinkID=213885) hoch.

> [!NOTE]
> Diese Anmeldeinformationen, die Visual Studio zum Verwalten Ihrer Clouddienste benötigt, müssen nicht den Anmeldeinformationen entsprechen, die zum Authentifizieren einer Anforderung für die Azure-Speicherdienste erforderlich sind.
>
>

## <a name="modify-or-export-authentication-credentials-in-visual-studio"></a>Ändern oder Exportieren von Authentifizierungsinformationen in Visual Studio
Sie können die Authentifizierungsinformationen auch im Dialogfeld **Neues Abonnement** einrichten, ändern oder exportieren. Dieses Dialogfeld wird angezeigt, wenn Sie eine der folgenden Aktionen ausführen:

* Öffnen Sie im **Server-Explorer** das Kontextmenü des Knotens **Azure**, und wählen Sie **Abonnements verwalten** aus. Wählen Sie die Registerkarte **Zertifikate** aus, und klicken Sie dann auf die Schaltfläche **Neu** bzw. **Bearbeiten**.
* Wenn Sie einen Azure-Clouddienst mit dem **Assistenten zum Veröffentlichen einer Azure-Anwendung** veröffentlichen, wählen Sie in der Liste **Abonnement auswählen** den Eintrag **Verwalten** aus. Wählen Sie dann die Registerkarte „Zertifikate“ aus, und klicken Sie anschließend auf die Schaltfläche **Neu** oder **Bearbeiten**.

Bei der folgenden Vorgehensweise wird davon ausgegangen, dass das Dialogfeld **Neues Abonnement** geöffnet ist.

### <a name="to-set-up-authentication-credentials-in-visual-studio"></a>So richten Sie Anmeldeinformationen für die Authentifizierung in Visual Studio ein
1. Wählen Sie in der Liste **Wählen Sie ein vorhandenes Zertifikat für die Authentifizierung aus** ein vorhandenes Zertifikat aus.
2. Klicken Sie auf die Schaltfläche **Vollständigen Pfad kopieren**. Der Pfad des Zertifikats (CER-Datei) wird in die Zwischenablage kopiert.

   > [!IMPORTANT]
   > Laden Sie dieses Zertifikat in das [klassische Azure-Portal](http://go.microsoft.com/fwlink/?LinkID=213885)hoch, um die Azure-Anwendung aus Visual Studio zu veröffentlichen.
   >
   >
3. So laden Sie das Zertifikat in das [klassische Azure-Portal](http://go.microsoft.com/fwlink/?LinkID=213885)hoch

   1. Klicken Sie auf den Link für das Azure-Portal.

        Das [klassische Azure-Portal](http://go.microsoft.com/fwlink/?LinkID=213885) wird geöffnet.
   2. Melden Sie sich beim [klassischen Azure-Portal](http://go.microsoft.com/fwlink/?LinkID=213885)an, und klicken Sie dann auf die Schaltfläche **Clouddienste** .
   3. Wählen Sie den gewünschten Clouddienst aus.

       Die Seite für diesen Dienst wird geöffnet.
   4. Klicken Sie auf der Registerkarte **Zertifikate** auf die Schaltfläche **Hochladen**.
   5. Fügen Sie den vollständigen Pfad der erstellten CER-Datei ein, und geben Sie dann das festgelegte Kennwort ein.



<!--HONumber=Dec16_HO2-->


