---
title: "Azure AD Connect: Nahtloses einmaliges Anmelden – Schnellstart | Microsoft-Dokumentation"
description: In diesem Artikel wird beschrieben, wie Sie Ihre ersten Schritte mit dem nahtlosen einmaligen Anmelden von Azure Active Directory gehen.
services: active-directory
keywords: "Was ist Azure AD Connect, Active Directory installieren, erforderliche Komponenten für Azure AD, SSO, Single Sign-On, einmaliges Anmelden"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.translationtype: Human Translation
ms.sourcegitcommit: ef1e603ea7759af76db595d95171cdbe1c995598
ms.openlocfilehash: 451d4fd24dc506fb4a659edb710ab67a66cbbde7
ms.contentlocale: de-de
ms.lasthandoff: 06/16/2017

---

# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a>Azure AD Connect: Nahtloses einmaliges Anmelden – Schnellstart

Mit dem nahtlosen einmaligen Anmelden von Azure Active Directory (Azure AD Seamless Single Sign-On) werden Benutzer automatisch im Unternehmensnetzwerk angemeldet, wenn Sie an ihren Unternehmens-Desktops arbeiten. Dieses Feature ermöglicht Ihren Benutzern einen einfachen Zugriff auf Ihre cloudbasierten Dienste, ohne dass zusätzliche lokale Komponenten erforderlich sind.

## <a name="how-to-deploy-azure-ad-seamless-sso"></a>Bereitstellen der nahtlosen einmaligen Anmeldung von Azure AD

Um die nahtlose einmalige Anmeldung bereitzustellen, führen Sie die folgenden Schritte aus:
1. *Überprüfen der Voraussetzungen:* Richten Sie Ihren Mandanten und Ihre lokale Umgebung ordnungsgemäß ein, bevor Sie das Feature aktivieren.
2. *Aktivieren des Features:* Aktivieren Sie das nahtlose einmalige Anmelden für Ihren Mandanten mit Azure AD Connect.
3. *Ausrollen des Features:* Verwenden Sie die Gruppenrichtlinie, um das Feature für einige oder alle Ihre Benutzer auszurollen.
4. *Testen des Features:* Testen Sie die Benutzeranmeldung mit dem nahtlosen einmaligen Anmelden.

## <a name="step-1-check-prerequisites"></a>Schritt 1: Überprüfen der Voraussetzungen

Stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt werden:

1. Richten Sie Ihren Azure AD Connect-Server ein: Wenn Sie die [Passthrough-Authentifizierung](active-directory-aadconnect-pass-through-authentication.md) als Anmeldemethode verwenden, ist keine weitere Aktion erforderlich. Wenn die [Kennworthashsynchronisierung](active-directory-aadconnectsync-implement-password-synchronization.md) Ihre Anmeldemethode ist und eine Firewall zwischen Azure AD Connect und Azure AD vorhanden ist, sollten Sie Folgendes sicherstellen:
- Sie verwenden die Version 1.1.484.0 oder höher von Azure AD Connect.
- Azure AD Connect kann mit `*.msappproxy.net`-URLs und über Port 443 kommunizieren. Diese Voraussetzung gilt nur, wenn Sie das Feature aktivieren, nicht für tatsächliche Benutzeranmeldungen.
- Azure AD Connect kann direkte IP-Verbindungen zu den [IP-Bereichen des Azure-Rechenzentrums](https://www.microsoft.com/download/details.aspx?id=41653) herstellen. Auch diese Voraussetzung gilt nur, wenn Sie das Feature aktivieren.
2. Für jede AD-Gesamtstruktur, die Sie mit Azure AD (über Azure AD Connect) synchronisieren und für deren Benutzer Sie die nahtlose einmalige Anmeldung aktivieren möchten, benötigen Sie die Anmeldeinformationen des Domänenadministrators.

## <a name="step-2-enable-the-feature"></a>Schritt 2: Aktivieren des Features

Das nahtlose einmalige Anmelden kann mithilfe von [Azure AD Connect](active-directory-aadconnect.md) aktiviert werden.

Wenn Sie Azure AD Connect neu installieren, wählen Sie den [benutzerdefinierten Installationspfad](active-directory-aadconnect-get-started-custom.md) aus. Aktivieren Sie auf der Seite „Benutzeranmeldung“ die Option „Einmaliges Anmelden aktivieren“.

![Azure AD Connect – Benutzeranmeldung](./media/active-directory-aadconnect-sso/sso8.png)

Wenn Sie bereits eine Installation von Azure AD Connect haben, wählen Sie in Azure AD Connect „Change user sign-in page“ (Anmeldeseite „Benutzer wechseln“), und klicken Sie auf „Weiter“. Aktivieren Sie dann die Option „Einmaliges Anmelden aktivieren“.

![Azure AD Connect – Benutzeranmeldung ändern](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Fahren Sie mit dem Assistenten fort, bis Sie zur Seite „Enable single sign on“ (Einmaliges Anmelden aktivieren) gelangen. Stellen Sie für jede AD-Gesamtstruktur, die Sie mit Azure AD (über Azure AD Connect) synchronisieren und für deren Benutzer Sie die nahtlose einmalige Anmeldung aktivieren möchten, die Anmeldeinformationen des Domänenadministrators bereit. 

Nach Abschluss des Assistenten ist das nahtlose einmalige Anmelden für Ihren Mandanten aktiviert.

>[!NOTE]
> Die Anmeldeinformationen des Domänenadministrators werden weder in Azure AD Connect noch in Azure AD gespeichert, werden aber für die Aktivierung des Features verwendet.

## <a name="step-3-roll-out-the-feature"></a>Schritt 3: Ausrollen des Features

Um das Feature für Ihre Benutzer auszurollen, müssen Sie den Einstellungen für Intranetzonen der Benutzer über Gruppenrichtlinien in Active Directory zwei Azure AD-URLs hinzufügen: https://autologon.microsoftazuread-sso.com und https://aadg.windows.net.nsatc.net.

>[!NOTE]
> Die folgenden Anweisungen funktionieren nur für Internet Explorer und Google Chrome unter Windows (wenn ein Satz von URLs vertrauenswürdiger Websites wie für Internet Explorer freigegeben wird). Lesen Sie im nächsten Abschnitt die Anweisungen zum Einrichten von Mozilla Firefox und Google Chrome auf Mac.

### <a name="why-do-you-need-to-modify-users-intranet-zone-settings"></a>Warum müssen Sie Einstellungen von Benutzern für Intranetzonen ändern?

Der Browser berechnet standardmäßig anhand der URL automatisch die richtige Zone (Internet oder Intranet). Beispielsweise ist http://contoso/ der Intranetzone und http://intranet.contoso.com/ der Internetzone zugeordnet (da die URL einen Punkt enthält). Browser senden keine Kerberos-Tickets an Cloudendpunkte wie die beiden Azure AD-URLs, sofern die jeweilige URL nicht als Teil der Intranetzone des Browsers definiert ist.

### <a name="detailed-steps"></a>Ausführliche Schritte

1. Öffnen Sie das Gruppenrichtlinienverwaltungstool.
2. Bearbeiten Sie die Gruppenrichtlinie, die auf einige oder alle Benutzer angewendet wird. In diesem Beispiel verwenden wir die **Default Domain Policy** (Standarddomänenrichtlinie).
3. Navigieren Sie zu **Benutzerkonfiguration\Administrative Vorlagen\Windows-Komponenten\Internet Explorer\Internetsystemsteuerung\Sicherheitsseite**, und wählen Sie die Option **Liste der Site zu Zonenzuweisungen**.
![Einmaliges Anmelden](./media/active-directory-aadconnect-sso/sso6.png)  
4. Aktivieren Sie die Richtlinie, und geben Sie in das Dialogfeld die folgenden Werte (Azure AD-URLs, in denen Kerberos-Tickets weitergeleitet werden) und Daten ein (*1* gibt die Intranetzone an).

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> Wenn Sie das nahtlose einmalige Anmelden z.B. für einige Benutzer verbieten möchten, weil sich diese Benutzer beispielsweise auf freigegebenen Kiosken anmelden, legen Sie die vorherigen Werte auf *4* fest. Diese Aktion fügt der Zone eingeschränkter Sites die Azure AD-URLs hinzu, und löst für das nahtlose einmalige Anmelden ständig einen Fehler aus.

5. Klicken Sie zweimal nacheinander auf **OK******.

![Einmaliges Anmelden](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a>Überlegungen zum Browser

#### <a name="mozilla-firefox"></a>Mozilla Firefox

Mozilla Firefox führt nicht automatisch die Kerberos-Authentifizierung aus. Jeder Benutzer muss den Firefox-Einstellungen manuell die Azure AD-URLs mithilfe der folgenden Schritte hinzufügen:
1. Führen Sie Firefox aus, und geben Sie in die Adressleiste `about:config` ein. Schließen Sie alle Benachrichtigungen, die Sie sehen.
2. Suchen Sie nach der Einstellung **network.negotiate-auth.trusted-uris**. In dieser Einstellung werden in Firefox die vertrauenswürdigen Sites für die Kerberos-Authentifizierung aufgeführt.
3. Klicken Sie mit der rechten Maustaste, und wählen Sie dann „Ändern“ aus.
4. Geben Sie „https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net“ in das Feld ein.
5. Klicken Sie auf „OK“, und öffnen Sie den Browser erneut.

>[!NOTE]
>Das nahtlose einmalige Anmelden funktioniert in Firefox nicht im privaten Modus.

#### <a name="google-chrome-on-mac"></a>Google Chrome unter macOS

Informationen dazu, wie Sie in Google Chrome unter macOS und anderen nicht Windows-basierten Plattformen die Azure AD-URLs für die integrierte Authentifizierung auf eine Whitelist setzen, finden Sie [in diesem Artikel](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist).

Das Ausrollen der Azure AD-URLs für Firefox und Google Chrome unter macOS mithilfe von Active Directory-Gruppenrichtlinienerweiterungen von Drittanbietern kann in diesem Artikel nicht behandelt werden.

## <a name="step-4-test-the-feature"></a>Schritt 4: Testen des Features

Um das Feature für einen bestimmten Benutzer zu testen, stellen Sie sicher, dass _alle_ folgenden Bedingungen erfüllt werden:
  - Ihr Benutzer meldet sich auf einem Gerät des Unternehmens an.
  - Das Gerät ist zuvor Ihrer Active Directory(AD)-Domäne beigetreten.
  - Es muss eine direkte Verbindung zwischen dem Gerät und Ihrem Domänencontroller (DC) bestehen, entweder über das Unternehmensnetzwerk (Kabel- oder Funknetzwerk) oder per Remotezugriff, z.B. über eine VPN-Verbindung.
  - Sie haben [das Feature für diesen Benutzer mithilfe von Gruppenrichtlinien ausgerollt](##step-3-roll-out-the-feature).

So testen Sie das Szenario, wenn der Benutzer nur den Benutzernamen eingibt, jedoch kein Kennwort:
- Melden Sie sich unter *https://myapps.microsoft.com/* in einer neuen, privaten Browsersitzung an.

So testen Sie das Szenario, wenn der Benutzer weder den Benutzernamen noch das Kennwort eingeben muss: 
- Melden Sie sich unter *https://myapps.microsoft.com/contoso.onmicrosoft.com* in einer neuen, privaten Browsersitzung an. Ersetzen Sie „*contoso*“ durch den Namen Ihres Mandanten.
- Melden Sie sich alternativ unter *https://myapps.microsoft.com/contoso.com* in einer neuen, privaten Browsersitzung an. Ersetzen Sie „*contoso.com*“ durch eine überprüfte Domäne (keine Verbunddomäne) in Ihrem Mandanten.

## <a name="next-steps"></a>Nächste Schritte

- [**Technische Einzelheiten**](active-directory-aadconnect-sso-how-it-works.md) – Funktionsweise dieses Features verstehen
- [**Häufig gestellte Fragen**](active-directory-aadconnect-sso-faq.md) – Antworten auf häufig gestellte Fragen
- [**Problembehandlung**](active-directory-aadconnect-troubleshoot-sso.md) – Beheben von häufig auftretenden Problemen mit diesem Feature
- [**UserVoice:**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) Verfassen neuer Feature-Anforderungen

