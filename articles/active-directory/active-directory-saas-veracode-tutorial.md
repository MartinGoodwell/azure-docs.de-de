---
title: 'Tutorial: Azure Active Directory-Integration mit Veracode | Microsoft Docs'
description: "Erfahren Sie, wie Sie Veracode mit Azure Active Directory verwenden können, um einmaliges Anmelden, automatisierte Bereitstellung und vieles mehr zu aktivieren."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
translationtype: Human Translation
ms.sourcegitcommit: 1c22e4fc17226578aaaf272fdf79178da65c63c2
ms.openlocfilehash: 8c8ac0af8a39afdd9755040d21585185ceca890e
ms.lasthandoff: 02/23/2017


---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a>Tutorial: Azure Active Directory-Integration mit Veracode
In diesem Tutorial wird die Integration von Azure und Veracode erläutert. Das in diesem Tutorial verwendete Szenario setzt voraus, dass Sie bereits über die folgenden Elemente verfügen:

* Ein gültiges Azure-Abonnement
* Ein Veracode-Abonnement, für das einmaliges Anmelden aktiviert ist

Nach Abschluss dieses Tutorials können sich die Veracode zugewiesenen Azure AD-Benutzer wie unter [Einführung in den Zugriffsbereich](active-directory-saas-access-panel-introduction.md)beschrieben mittels einmaliger Anmeldung bei der Anwendung anmelden.

Das in diesem Tutorial beschriebene Szenario besteht aus den folgenden Bausteinen:

1. Aktivieren der Anwendungsintegration für Veracode
2. Konfigurieren der einmaligen Anmeldung
3. Konfigurieren der Benutzerbereitstellung
4. Zuweisen von Benutzern

![Szenario](./media/active-directory-saas-veracode-tutorial/IC802903.png "Szenario")

## <a name="enabling-the-application-integration-for-veracode"></a>Aktivieren der Anwendungsintegration für Veracode
In diesem Abschnitt wird beschrieben, wie Sie die Anwendungsintegration für Veracode aktivieren.

### <a name="to-enable-the-application-integration-for-veracode-perform-the-following-steps"></a>So aktivieren Sie die Anwendungsintegration für Veracode
1. Klicken Sie im klassischen Azure-Portal im linken Navigationsbereich auf **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-veracode-tutorial/IC700993.png "Active Directory")

2. Wählen Sie in der Liste **Verzeichnis** das Verzeichnis aus, für das Sie die Verzeichnisintegration aktivieren möchten.

3. Klicken Sie zum Öffnen der Anwendungsansicht in der oberen Menüleiste der Verzeichnisansicht auf **Anwendungen** .
   
    ![Anwendungen](./media/active-directory-saas-veracode-tutorial/IC700994.png "Anwendungen")

4. Klicken Sie unten auf der Seite auf **Hinzufügen** .
   
    ![Anwendung hinzufügen](./media/active-directory-saas-veracode-tutorial/IC749321.png "Anwendung hinzufügen")

5. Klicken Sie im Dialogfeld **Was möchten Sie tun?** auf **Anwendung aus dem Katalog hinzufügen**.
   
    ![Anwendung aus dem Katalog hinzufügen](./media/active-directory-saas-veracode-tutorial/IC749322.png "Anwendung aus dem Katalog hinzufügen")

6. Geben Sie im **Suchfeld** als Suchbegriff **Veracode** ein.
   
    ![Anwendungskatalog](./media/active-directory-saas-veracode-tutorial/IC802904.png "Anwendungskatalog")

7. Wählen Sie im Ergebnisbereich **Veracode** aus, und klicken Sie dann auf **Abschließen**, um die Anwendung hinzuzufügen.
   
    ![Veracode](./media/active-directory-saas-veracode-tutorial/IC802905.png "Veracode")

## <a name="configuring-single-sign-on"></a>Konfigurieren der einmaligen Anmeldung
In diesem Abschnitt wird erläutert, wie Sie es Benutzern mithilfe einer Verbundanmeldung auf Basis des SAML-Protokolls ermöglichen, sich mit ihrem Azure AD-Konto bei Veracode zu authentifizieren.  
Die Veracode-Anwendung erwartet die SAML-Assertionen in einem bestimmten Format. Daher müssen Sie Ihrer Konfiguration der **SAML-Tokenattribute** benutzerdefinierte Attributzuordnungen hinzufügen.  
Der folgende Screenshot zeigt ein Beispiel für diese Attributzuordnungen:

![Attribute](./media/active-directory-saas-veracode-tutorial/IC802906.png "Attribute")

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a>So konfigurieren Sie einmaliges Anmelden
1. Klicken Sie im klassischen Azure-Portal auf der Anwendungsintegrationsseite für **Veracode** auf **Einmaliges Anmelden konfigurieren**, um das Dialogfeld **Einmaliges Anmelden konfigurieren** zu öffnen.
   
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-veracode-tutorial/IC802907.png "Einmaliges Anmelden konfigurieren")

2. Wählen Sie auf der Seite **Wie sollen sich Benutzer bei Veracode anmelden?** die Option **Microsoft Azure AD – einmaliges Anmelden** aus, und klicken Sie dann auf **Weiter**.
   
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-veracode-tutorial/IC802908.png "Einmaliges Anmelden konfigurieren")

3. Klicken Sie auf der Seite **App-Einstellungen konfigurieren** auf **Weiter**.
   
    ![App-Einstellungen konfigurieren](./media/active-directory-saas-veracode-tutorial/IC802909.png "App-Einstellungen konfigurieren")

4. Klicken Sie zum Herunterladen des Zertifikats auf der Seite **Einmaliges Anmelden konfigurieren für Veracode** auf **Zertifikat herunterladen**, und speichern Sie die Zertifikatsdatei lokal auf Ihrem Computer.
   
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-veracode-tutorial/IC802910.png "Einmaliges Anmelden konfigurieren")

5. Melden Sie sich in einem anderen Webbrowserfenster bei der Veracode-Unternehmenswebsite als Administrator an.

6. Klicken Sie oben im Menü auf **Einstellungen** und dann auf **Administration**.
   
    ![Verwaltung](./media/active-directory-saas-veracode-tutorial/IC802911.png "Verwaltung")

7. Klicken Sie auf die Registerkarte **SAML** .

8. Führen Sie im Abschnitt für die **SAML-Einstellungen der Organisation** die folgenden Schritte aus:
   
    ![Verwaltung](./media/active-directory-saas-veracode-tutorial/IC802912.png "Verwaltung")
   
    a. Kopieren Sie im klassischen Azure-Portal auf der Dialogfeldseite **Einmaliges Anmelden konfigurieren für Veracode** den Wert für **Aussteller-URL**, und fügen Sie ihn in das Textfeld **Aussteller** ein.
   
    b. Klicken Sie auf **Datei auswählen**, um das heruntergeladene Zertifikat hochzuladen.
   
    c. Wählen Sie **Selbstregistrierung aktivieren**.

9. Führen Sie im Abschnitt **Selbstregistrierungseinstellungen** die folgenden Schritte aus. Klicken Sie dann auf **Speichern**:
   
    ![Verwaltung](./media/active-directory-saas-veracode-tutorial/IC802913.png "Verwaltung")
   
    a. Wählen Sie für **Aktivierung neuer Benutzer** die Option **Keine Aktivierung erforderlich** aus.
   
    b. Wählen Sie für **Benutzerdaten-Aktualisierungen** die Option **Veracode-Benutzerdaten bevorzugen** aus.
   
    c. Wählen Sie für die **SAML-Attributdetails**Folgendes aus:
      * **Benutzerrollen**
      * **Richtlinien-Administrator**
      * **Prüfer**
      * **Leiter der Sicherheitsabteilung**
      * **Geschäftsleitung**
      * **Absender**
      * **Ersteller**
      * **Alle Scantypen**
      * **Teammitgliedschaften**
      * **Standardteam**

10. Bestätigen Sie im klassischen Azure-Portal die Konfiguration der einmaligen Anmeldung, und klicken Sie dann auf **Abschließen**, um das Dialogfeld **Einmaliges Anmelden konfigurieren** zu schließen.
    
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-veracode-tutorial/IC802914.png "Einmaliges Anmelden konfigurieren")

11. Klicken Sie oben im Menü auf **Attribute** to open the **SAML Token Attribute** zu öffnen.
    
    ![Attribute](./media/active-directory-saas-veracode-tutorial/IC795920.png "Attribute")

12. So fügen Sie die erforderlichen Attributzuordnungen hinzu:
    
    ![Attribute](./media/active-directory-saas-veracode-tutorial/IC802906.png "Attribute")
    
    | Attributname | Attributwert |
    |:--- |:--- |
    | firstname |User.givenname |
    | lastname |User.surname |
    | E-Mail |User.mail |
    
    a. Klicken Sie für jede Datenzeile in der obigen Tabelle auf **Benutzerattribut hinzufügen**.

    b. Geben Sie im Textfeld **Attribute Name** den für die Zeile angezeigten Attributnamen ein.

    c. Geben Sie im Textfeld **Attribute Value** den für die Zeile angezeigten Attributwert ein.

    d. Klicken Sie auf **Fertig stellen**.

13. Klicken Sie auf **Apply Changes**.

## <a name="configuring-user-provisioning"></a>Konfigurieren der Benutzerbereitstellung
Damit sich Azure AD-Benutzer bei Veracode anmelden können, müssen sie in Veracode bereitgestellt werden.  
Im Fall von Veracode ist die Bereitstellung eine automatisierte Aufgabe.  
Für Sie steht kein Aktionselement zur Verfügung.

Benutzer werden beim Versuch des einmaligen Anmeldens bei Bedarf automatisch erstellt.

> [!NOTE]
> Sie können AAD-Benutzerkonten auch mithilfe anderer Tools zum Erstellen von Veracode-Benutzerkonten oder mithilfe der von Veracode bereitgestellten APIs erstellen.
> 
> 

## <a name="assigning-users"></a>Zuweisen von Benutzern
Um Ihre Konfiguration zu testen, müssen Sie den Azure AD-Benutzern, denen Sie die Verwendung Ihrer Anwendung ermöglichen möchten, Zugriff auf die Anwendung gewähren. Weisen Sie dazu der Anwendung Benutzer zu.

### <a name="to-assign-users-to-veracode-perform-the-following-steps"></a>So weisen Sie Veracode Benutzer zu:
1. Erstellen Sie im klassischen Azure-Portal ein Testkonto.

2. Klicken Sie auf der Anwendungsintegrationsseite für **Veracode** auf **Benutzer zuweisen**.
   
    ![Zuweisen von Benutzern](./media/active-directory-saas-veracode-tutorial/IC802915.png "Zuweisen von Benutzern")

3. Wählen Sie den Testbenutzer aus, klicken Sie auf **Zuweisen** und anschließend auf **Ja**, um die Zuweisung zu bestätigen.
   
    ![Ja](./media/active-directory-saas-veracode-tutorial/IC767830.png "Ja")

Wenn Sie die SSO-Einstellungen testen möchten, öffnen Sie den Zugriffsbereich. Weitere Informationen zum Zugriffsbereich finden Sie unter [Einführung in den Zugriffsbereich](active-directory-saas-access-panel-introduction.md).


