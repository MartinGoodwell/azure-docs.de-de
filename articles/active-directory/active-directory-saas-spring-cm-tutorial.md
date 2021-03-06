---
title: 'Tutorial: Azure Active Directory-Integration mit SpringCM | Microsoft Docs'
description: "Hier erfahren Sie, wie Sie Spring CM mit Azure Active Directory verwenden können, um einmaliges Anmelden, automatisierte Bereitstellung und vieles mehr zu ermöglichen."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/10/2017
ms.author: jeedes
translationtype: Human Translation
ms.sourcegitcommit: 07635b0eb4650f0c30898ea1600697dacb33477c
ms.openlocfilehash: 5600adfbc20fb499bdd206e966a9730f49a03e40
ms.lasthandoff: 03/28/2017


---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a>Tutorial: Azure Active Directory-Integration mit SpringCM
In diesem Tutorial wird erläutert, wie einmaliges Anmelden (SSO) für Azure Active Directory und SpringCM eingerichtet wird.

Das in diesem Lernprogramm verwendete Szenario setzt voraus, dass Sie bereits über die folgenden Elemente verfügen:

* Ein gültiges Azure-Abonnement
* Ein SpringCM-Abonnement, für das einmaliges Anmelden (SSO) aktiviert ist

Nach Abschluss dieses Tutorials können sich die Azure Active Directory-Benutzer, die Sie SpringCM zugewiesen haben, durch einmaliges Anmelden über den AAD-Zugriffsbereich anmelden.

1. Aktivieren der Anwendungsintegration für SpringCM
2. Konfigurieren des einmaligen Anmeldens (SSO)
3. Konfigurieren der Benutzerbereitstellung
4. Zuweisen von Benutzern

![Szenario](./media/active-directory-saas-spring-cm-tutorial/IC797044.png "Szenario")

## <a name="enabling-the-application-integration-for-springcm"></a>Aktivieren der Anwendungsintegration für SpringCM
In diesem Abschnitt wird beschrieben, wie Sie die Anwendungsintegration für SpringCM aktivieren.

**So aktivieren Sie die Anwendungsintegration für SpringCM**

1. Klicken Sie im klassischen Azure-Portal im linken Navigationsbereich auf **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-spring-cm-tutorial/IC700993.png "Active Directory")

2. Wählen Sie in der Liste **Verzeichnis** das Verzeichnis aus, für das Sie die Verzeichnisintegration aktivieren möchten.

3. Klicken Sie zum Öffnen der Anwendungsansicht in der oberen Menüleiste der Verzeichnisansicht auf **Anwendungen** .
   
    ![Anwendungen](./media/active-directory-saas-spring-cm-tutorial/IC700994.png "Anwendungen")

4. Klicken Sie unten auf der Seite auf **Hinzufügen** .
   
    ![Anwendung hinzufügen](./media/active-directory-saas-spring-cm-tutorial/IC749321.png "Anwendung hinzufügen")

5. Klicken Sie im Dialogfeld **Was möchten Sie tun?** auf **Anwendung aus dem Katalog hinzufügen**.
   
    ![Anwendung aus dem Katalog hinzufügen](./media/active-directory-saas-spring-cm-tutorial/IC749322.png "Anwendung aus dem Katalog hinzufügen")

6. Geben Sie im **Suchfeld** als Suchbegriff **SpringCM** ein.
   
    ![Anwendungskatalog](./media/active-directory-saas-spring-cm-tutorial/IC797045.png "Anwendungskatalog")

7. Wählen Sie im Ergebnisbereich **SpringCM** aus, und klicken Sie dann auf **Abschließen**, um die Anwendung hinzuzufügen.
   
    ![SpringCM](./media/active-directory-saas-spring-cm-tutorial/IC797046.png "SpringCM")

## <a name="configure-single-sign-on"></a>Configure single sign-on
In diesem Abschnitt wird erläutert, wie Sie es Benutzern mithilfe einer Verbundanmeldung auf Basis des SAML-Protokolls ermöglichen, sich mit ihrem Konto in Azure Active Directory bei SpringCM zu authentifizieren.

**So konfigurieren Sie einmaliges Anmelden**

1. Klicken Sie im klassischen Azure-Portal auf der Anwendungsintegrationsseite für **SpringCM** auf **Einmaliges Anmelden konfigurieren**, um das Dialogfeld **Einmaliges Anmelden konfigurieren** zu öffnen.
   
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-spring-cm-tutorial/IC797047.png "Einmaliges Anmelden konfigurieren")

2. Wählen Sie auf der Seite **Wie sollen sich Benutzer bei SpringCM anmelden?** die Option **Microsoft Azure AD – einmaliges Anmelden** aus, und klicken Sie dann auf **Weiter**.
   
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-spring-cm-tutorial/IC797048.png "Einmaliges Anmelden konfigurieren")

3. Geben Sie auf der Seite **App-URL konfigurieren** im Textfeld für die **SpringCM-Anmelde-URL** die von Ihren Benutzern für die Anmeldung bei Ihrer SpringCM-Anwendung verwendete URL ein, und klicken Sie dann auf **Weiter**. 
   
    Die App-URL ist Ihre SpringCM-Mandanten-URL (z.B.: *https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=16826*):
   
    ![App-URL konfigurieren](./media/active-directory-saas-spring-cm-tutorial/IC797049.png "App-URL konfigurieren")

4. Klicken Sie zum Herunterladen des Zertifikats auf der Seite **Einmaliges Anmelden konfigurieren für SpringCM** auf **Zertifikat herunterladen**, und speichern Sie die Zertifikatsdatei lokal auf Ihrem Computer.
   
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-spring-cm-tutorial/IC797050.png "Einmaliges Anmelden konfigurieren")

5. Melden Sie sich in einem anderen Webbrowserfenster bei der **SpringCM** -Unternehmenswebsite als Administrator an.

6. Klicken Sie im Menü oben auf **GEHE ZU**, anschließend auf **Voreinstellungen** und dann im Abschnitt **Kontovoreinstellungen** auf **SAML-SSO**.
   
    ![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/IC797051.png "SAML SSO")

7. Führen Sie im Abschnitt „Identitätsanbieterkonfiguration“ die folgenden Schritte aus:
   
    ![Identitätsanbieterkonfiguration](./media/active-directory-saas-spring-cm-tutorial/IC797052.png "Identitätsanbieterkonfiguration")   
  1. Zum Hochladen Ihres heruntergeladenen Azure Active Directory-Zertifikats klicken Sie auf **Ausstellerzertifikat auswählen** oder auf **Ausstellerzertifikat ändern**.
  2. Kopieren Sie im klassischen Azure-Portal auf der Dialogfeldseite **Einmaliges Anmelden konfigurieren für SpringCM** den Wert für **Aussteller-URL**, und fügen Sie ihn in das Textfeld **Aussteller** ein.
  3. Kopieren Sie im klassischen Azure-Portal auf der Seite **Einmaliges Anmelden konfigurieren für SpringCM** den Wert der **SSO-Dienst-URL**, und fügen Sie ihn in das Textfeld **Vom Dienstanbieter initiierter Endpunkt** ein.
  4. Wählen Sie für **SAML aktiviert** die Option **Aktivieren** aus.
  5. Klicken Sie auf **Speichern**.

8. Bestätigen Sie im klassischen Azure-Portal die Konfiguration der einmaligen Anmeldung, und klicken Sie dann auf **Abschließen**, um das Dialogfeld **Einmaliges Anmelden konfigurieren** zu schließen.
   
   ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-spring-cm-tutorial/IC797053.png "Einmaliges Anmelden konfigurieren")

## <a name="configure-user-provisioning"></a>Benutzerbereitstellung konfigurieren
Damit sich Azure Active Directory-Benutzer bei SpringCM anmelden können, müssen sie in SpringCM bereitgestellt werden.  

Im Fall von SpringCM ist die Bereitstellung eine manuelle Aufgabe.

>[!NOTE]
>Weitere Informationen finden Sie unter [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user) (Erstellen und Bearbeiten eines SpringCM-Benutzers). 
> 

**Führen Sie zum Bereitstellen eines Benutzerkontos in SpringCM die folgenden Schritte aus:**

1. Melden Sie sich bei der **SpringCM** -Unternehmenswebsite als Administrator an.

2. Klicken Sie auf **GEHE ZU** und dann auf **Adressbuch**.
   
    ![Benutzer erstellen](./media/active-directory-saas-spring-cm-tutorial/IC797054.png "Benutzer erstellen")

3. Klicken Sie auf **Benutzer erstellen**.

4. Wählen Sie eine **Benutzerrolle**aus.

5. Wählen Sie **Aktivierungs-E-Mail senden**.

6. Geben Sie die erforderlichen Angaben in die Textfelder „Vorname“, „Nachname“ und „E-Mail-Adresse“ eines gültigen Azure Active Directory-Kontos ein, das Sie bereitstellen möchten.

7. Fügen Sie den Benutzer zu einer **Sicherheitsgruppe**hinzu.

8. Klicken Sie auf **Speichern**.

  >[!NOTE]
  >Sie können AAD-Benutzerkonten auch mithilfe von anderen Tools zum Erstellen von SpringCM-Benutzerkonten oder mithilfe der von SpringCM bereitgestellten APIs erstellen.  
  > 

## <a name="assign-users"></a>Benutzer zuweisen
Um Ihre Konfiguration zu testen, müssen Sie den Azure AD-Benutzern, denen Sie die Verwendung Ihrer Anwendung ermöglichen möchten, Zugriff auf die Anwendung gewähren. Weisen Sie dazu der Anwendung Benutzer zu.

**So weisen Sie SpringCM Benutzer zu**

1. Erstellen Sie im klassischen Azure-Portal ein Testkonto.

2. Klicken Sie auf der Anwendungsintegrationsseite für **SpringCM** auf **Benutzer zuweisen**.
   
    ![Zuweisen von Benutzern](./media/active-directory-saas-spring-cm-tutorial/IC797055.png "Zuweisen von Benutzern")

3. Wählen Sie den Testbenutzer aus, klicken Sie auf **Zuweisen** und anschließend auf **Ja**, um die Zuweisung zu bestätigen.
   
    ![Ja](./media/active-directory-saas-spring-cm-tutorial/IC767830.png "Ja")

Wenn Sie die SSO-Einstellungen testen möchten, öffnen Sie den Zugriffsbereich. Weitere Informationen zum Zugriffsbereich finden Sie unter [Einführung in den Zugriffsbereich](active-directory-saas-access-panel-introduction.md).


