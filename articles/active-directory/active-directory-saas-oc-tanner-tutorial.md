---
title: "Tutorial: Azure Active Directory-Integration mit O. C. Tanner – AppreciateHub | Microsoft-Dokumentation"
description: "Erfahren Sie, wie Sie einmaliges Anmelden zwischen Azure Active Directory und O. C. Tanner – AppreciateHub konfigurieren."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.translationtype: Human Translation
ms.sourcegitcommit: 1b5527090a41c274b590ed9d1ac7b561b6f4ed14
ms.openlocfilehash: 10faa27e0c82e59c35e00258a2d90bea977dc28f
ms.contentlocale: de-de
ms.lasthandoff: 02/15/2017


---
# Tutorial: Azure Active Directory-Integration mit O. C. Tanner – AppreciateHub Zugriff hat.
<a id="tutorial-azure-active-directory-integration-with-o-c-tanner---appreciatehub" class="xliff"></a>
In diesem Lernprogramm wird die Integration von O.C. Tanner – AppreciateHub mit Azure Active Directory (Azure AD).  
Integration von O.C. Tanner – AppreciateHub mit Azure AD bietet die folgenden Vorteile: 

* Sie können in Azure AD steuern, wer auf O.C. Tanner – AppreciateHub Zugriff hat. 
* Sie können für die Benutzer die automatische Anmeldung bei O.C. Tanner – AppreciateHub (einmaliges Anmelden) mit ihren Azure AD-Konten einrichten.
* Sie können Ihre Konten an einem zentralen Ort verwalten – im klassischen Azure-Portal.

Weitere Informationen zur Integration von SaaS-Apps in Azure AD finden Sie unter [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## Voraussetzungen
<a id="prerequisites" class="xliff"></a>
Für das Konfigurieren der Azure AD-Integration mit O.C. Tanner – AppreciateHub benötigen Sie die folgenden Elemente:

* Ein Azure AD-Abonnement
* Ein O.C. Tanner – AppreciateHub-Abonnement, für das einmaliges Anmelden aktiviert ist

> [!NOTE]
> Um die Schritte in diesem Tutorial zu testen, wird empfohlen, keine Produktionsumgebung zu verwenden.
> 
> 

Um die Schritte in diesem Tutorial zu testen, sollten Sie folgende Empfehlungen beachten:

* Sie sollten keine Produktionsumgebung verwenden, sofern dies nicht erforderlich ist.
* Wenn Sie keine Azure AD-Testumgebung haben, können Sie [hier](https://azure.microsoft.com/pricing/free-trial/)eine einmonatige Testversion anfordern. 

## Beschreibung des Szenarios
<a id="scenario-description" class="xliff"></a>
Ziel dieses Tutorials ist es, das einmalige Anmelden von Azure AD in einer Testumgebung zu testen.  
Das in diesem Tutorial beschriebene Szenario besteht aus drei großen Bausteinen:

1. Hinzufügen von O.C. Tanner – AppreciateHub aus dem Katalog 
2. Konfigurieren und Testen der einmaligen Anmeldung von Azure AD

## Hinzufügen von O.C. Tanner – AppreciateHub aus dem Katalog
<a id="adding-oc-tanner---appreciatehub-from-the-gallery" class="xliff"></a>
Für das Konfigurieren der Integration von O.C. Tanner – AppreciateHub in Azure AD müssen Sie O.C. Tanner – AppreciateHub aus dem Katalog der Liste der verwalteten SaaS-Apps hinzufügen.

**Befolgen Sie folgende Schritte, um O.C. Tanner – AppreciateHub aus dem Katalog hinzuzufügen:**

1. Klicken Sie im linken Navigationsbereich des **klassischen Azure-Portals** auf **Active Directory**. 
   
    ![Active Directory][1] 
2. Wählen Sie in der Liste **Verzeichnis** das Verzeichnis aus, für das Sie die Verzeichnisintegration aktivieren möchten.
3. Klicken Sie zum Öffnen der Anwendungsansicht in der oberen Menüleiste der Verzeichnisansicht auf **Anwendungen** .
   
    ![Anwendungen][2] 
4. Klicken Sie unten auf der Seite auf **Hinzufügen** .
   
    ![Anwendungen][3] 
5. Klicken Sie im Dialogfeld **Was möchten Sie tun?** auf **Anwendung aus dem Katalog hinzufügen**.
   
    ![Anwendungen][4] 
6. Geben Sie im Suchfeld den Suchbegriff **O.C. Tanner – AppreciateHub**.
   
    ![Anwendungen][5] 
7. Wählen Sie im Ergebnisbereich **O.C. Tanner – AppreciateHub** aus, und klicken Sie dann auf **Abschließen**, um die Anwendung hinzuzufügen.
   
    ![Anwendungen][25] 

## Konfigurieren und Testen der einmaligen Anmeldung von Azure AD
<a id="configuring-and-testing-azure-ad-single-sign-on" class="xliff"></a>
In diesem Abschnitt soll veranschaulicht werden, wie basierend auf einem Testbenutzer namens "Britta Simon" das einmalige Anmelden mit Azure AD in O.C. Tanner – AppreciateHub konfiguriert und getestet werden kann.

Damit einmaliges Anmelden funktioniert, muss Azure AD wissen, wer der entsprechende Gegenbenutzer in O.C. Tanner – AppreciateHub zu einem Benutzer in Azure AD ist. Anders ausgedrückt: Zwischen einem Azure AD-Benutzer und dem entsprechenden Benutzer in O.C. Tanner – AppreciateHub muss eine Linkbeziehung eingerichtet werden.  
Diese Linkbeziehung wird hergestellt, indem Sie den **Benutzernamen** in Azure AD als **Benutzernamen** in O.C. Tanner – AppreciateHub zuweisen.

Für das Konfigurieren und Testen des einmaligen Anmeldens in Azure AD mit O.C. Tanner – AppreciateHub, sind folgende Bausteine erforderlich:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** , um Ihren Benutzern das Verwenden dieser Funktion zu ermöglichen.
2. **[Erstellen eines Azure AD-Testbenutzers](#creating-an-azure-ad-test-user)** , um das einmalige Anmelden mit Azure AD mit dem Testbenutzer Britta Simon zu testen.
3. **[Erstellen eines O.C. Tanner – AppreciateHub-Testbenutzers](#creating-a-halogen-software-test-user)** – um eine Entsprechung von Britta Simon in O.C. Tanner – AppreciateHub zu haben, die mit ihrer Azure AD-Darstellung verknüpft ist.
4. **[Zuweisen des Azure AD-Testbenutzers](#assigning-the-azure-ad-test-user)** , um Britta Simon für das einmalige Anmelden von Azure AD zu aktivieren.
5. **[Testen der einmaligen Anmeldung](#testing-single-sign-on)** , um zu überprüfen, ob die Konfiguration funktioniert.

### Konfigurieren des einmaligen Anmeldens von Azure AD
<a id="configuring-azure-ad-single-sign-on" class="xliff"></a>
Das Ziel dieses Abschnitts besteht darin, das einmalige Anmelden von Azure AD im klassischen Azure-Portal zu aktivieren und das einmalige Anmelden in der O.C. Tanner – AppreciateHub-Anwendung angemeldet werden.

**Für das Konfigurieren und Testen des einmaligen Anmeldens in Azure AD mit O.C. Tanner – AppreciateHub sind folgende Schritte erforderlich:**

1. Klicken Sie im klassischen Azure-Portal auf der Anwendungsintegrationsseite für **O.C. Tanner – AppreciateHub** auf **Einmaliges Anmelden konfigurieren**, um das Dialogfeld **Einmaliges Anmelden konfigurieren** zu öffnen.
   
    ![Einmaliges Anmelden konfigurieren][6]
2. Wählen Sie auf der Seite **Wie sollen sich Benutzer bei O.C. Tanner – AppreciateHub anmelden?** die Option **Azure AD – einmaliges Anmelden**, und klicken Sie dann auf **Weiter**.
   
    ![Azure AD – einmaliges Anmelden][7]
3. Führen Sie auf der Dialogseite **App-Einstellungen konfigurieren** die folgenden Schritte aus:
   
    ![App-Einstellungen konfigurieren][8]
   
     a. Öffnen Sie die Metadatendatei mithilfe des folgenden Links: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).
   
     b. Suchen Sie den Knoten **Md:AssertionConsumerService** . 
   
     c. Kopieren Sie den Wert des **Location** -Attributs. 
   
     ![App-Einstellungen konfigurieren][12]
   
     d. Fügen Sie im Textfeld **Anmelde-URL** den im vorherigen Schritt abgerufenen Wert ein.
   
    > [!NOTE]
    > Wenden Sie sich bei Problemen beim Auffinden der Antwort-URL in der Metadatendatei an das O.C. Tanner – AppreciateHub-Supportteam unter [sso@octanner.com](mailto:sso@octanner.com).
    > 
    > 
   
    e. Klicken Sie auf **Weiter**.

4. Klicken Sie auf der Seite **Einmaliges Anmelden konfigurieren für O.C. Tanner – AppreciateHub** auf **Metadaten herunterladen**, und speichern Sie die Metadatendatei dann lokal auf Ihrem Computer.
   
    ![Was ist Azure AD Connect?][9]
5. Kontaktieren Sie das O.C. Tanner – AppreciateHub-Supportteam, stellen Sie ihm die Metadatendatei bereit, und bitten Sie es, SSO für Sie zu aktivieren.
6. Wählen Sie im klassischen Azure-Portal die Bestätigung zur Konfiguration des einmaligen Anmeldens aus, und klicken Sie dann auf **Weiter**. 
   
    ![Was ist Azure AD Connect?][10]
7. Klicken Sie auf der Seite **Bestätigung zur einmaligen Anmeldung** auf **Fertig stellen**.  
   
    ![Was ist Azure AD Connect?][11]

### Erstellen eines Azure AD-Testbenutzers
<a id="creating-an-azure-ad-test-user" class="xliff"></a>
In diesem Abschnitt wird im klassischen Azure-Portal eine Testbenutzerin namens Britta Simon erstellt.  

![Azure AD-Benutzer erstellen][20]

**Um einen Testbenutzer in Azure AD zu erstellen, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im linken Navigationsbereich des **klassischen Azure-Portals** auf **Active Directory**.
   
    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 
2. Wählen Sie in der Liste **Verzeichnis** das Verzeichnis aus, für das Sie die Verzeichnisintegration aktivieren möchten.
3. Klicken Sie zum Anzeigen der Liste der Benutzer im Menü oben auf **Benutzer**.
   
    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 
4. Um das Dialogfeld **Benutzer hinzufügen** zu öffnen, klicken Sie auf der Symbolleiste unten auf **Benutzer hinzufügen**. 
   
    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 
5. Führen Sie auf der Dialogfeldseite **Informationen über diesen Benutzer** die folgenden Schritte aus: 
   
    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_05.png) 
   
    a. Wählen Sie als „Benutzertyp“ die Option „Neuer Benutzer in Ihrer Organisation“ aus.
   
    b. Geben Sie in das Textfeld **Benutzername** den Namen **BrittaSimon** ein.
   
    c. Klicken Sie auf **Weiter**.
6. Führen Sie auf der Dialogfeldseite **Benutzerprofil** die folgenden Schritte aus: 
   
    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_06.png)
   
    a. Geben Sie in das Textfeld **Vorname** den Namen **Britta** ein.  
   
    b. Geben Sie in das Textfeld **Nachname** den Namen **Simon** ein.
   
    c. Geben Sie in das Textfeld **Anzeigename** den Namen **Britta Simon** ein.
   
    d. Wählen Sie in der Liste **Rolle** die Option **Benutzer** aus.
    e. Klicken Sie auf **Weiter**.

7. Klicken Sie auf der Dialogfeldseite **Vorübergehendes Kennwort abrufen** auf **Erstellen**.
   
    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_07.png) 
8. Führen Sie auf der Dialogfeldseite **Vorübergehendes Kennwort abrufen** die folgenden Schritte aus:
   
    ![Erstellen eines Azure AD-Testbenutzers](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_08.png) 
   
    a. Notieren Sie den Wert von **Neues Kennwort**.
   
    b. Klicken Sie auf **Fertig stellen**.   

### Erstellen eines O.C. C. Tanner – AppreciateHub-Testbenutzers
<a id="creating-a-oc-tanner---appreciatehub-test-user" class="xliff"></a>
Das Ziel dieses Abschnitts ist das Erstellen eines Benutzers namens Britta Simon in O.C. Tanner – AppreciateHub.

**Für das Erstellen eines Benutzers namens Britta Simon in O.C. Tanner – AppreciateHub sind folgende Schritte erforderlich:**

Bitten Sie das O.C. Tanner-Supportteam, einen Benutzer zu erstellen, dessen nameID-Attribut dem Benutzernamen von Britta Simon in Azure AD entspricht.

### Zuweisen des Azure AD-Testbenutzers
<a id="assigning-the-azure-ad-test-user" class="xliff"></a>
Das Ziel dieses Abschnitts ist, Britta Simon für das einmalige Anmelden bei Azure zu aktivieren, indem sie Zugriff auf O.C. Tanner – AppreciateHub konfigurieren.

![Benutzer zuweisen][200]

**Für das Zuweisen von Britta Simon an O.C. Tanner – AppreciateHub sind folgende Schritte erforderlich:**

1. Klicken Sie zum Öffnen der Anwendungsansicht im klassischen Azure-Portal in der oberen Menüleiste der Verzeichnisansicht auf **Anwendungen** .
   
    ![Benutzer zuweisen][201]
2. Wählen Sie in der Anwendungsliste **O.C. Tanner – AppreciateHub**.
   
    ![Benutzer zuweisen][202]
3. Klicken Sie im oberen Menü auf **Benutzer**.
   
    ![Benutzer zuweisen][203]
4. Wählen Sie in der Benutzerliste **Britta Simon**aus.
5. Klicken Sie auf der Symbolleiste unten auf **Zuweisen**.
   
    ![Benutzer zuweisen][205]

### Testen der einmaligen Anmeldung
<a id="testing-single-sign-on" class="xliff"></a>
Das Ziel dieses Abschnitts ist das Testen Ihrer Azure AD-Konfiguration für einmaliges Anmelden über den Zugriffsbereich.  
Wenn Sie im Zugriffsbereich auf die Kachel "O.C. Tanner – AppreciateHub" klicken, sollten Sie automatisch bei Ihrer O.C. Tanner – AppreciateHub-Anwendung angemeldet werden.

## Zusätzliche Ressourcen
<a id="additional-resources" class="xliff"></a>
* [Liste der Tutorials zur Integration von SaaS-Apps in Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_01.png
[25]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_25.png


[6]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_02.png
[8]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_03.png
[9]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_04.png
[10]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_05.png
[11]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_06.png
[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png
[20]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_07.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_205.png







