---
title: Festlegen von Sicherheitsrichtlinien in Azure Security Center | Microsoft Docs
description: "Dieses Dokument enthält Informationen dazu, wie Sie Sicherheitsrichtlinien in Azure Security Center konfigurieren können."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3b9e1c15-3cdb-4820-b678-157e455ceeba
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.translationtype: HT
ms.sourcegitcommit: 26c07d30f9166e0e52cb396cdd0576530939e442
ms.openlocfilehash: aefec15c72c6cf8389a29b03be70abb4c7f020b9
ms.contentlocale: de-de
ms.lasthandoff: 07/19/2017

---
# <a name="set-security-policies-in-azure-security-center"></a>Festlegen von Sicherheitsrichtlinien in Azure Security Center
Dieses Dokument hilft Ihnen dabei, Sicherheitsrichtlinien in Security Center zu konfigurieren. Es werden die erforderlichen Schritte zum Ausführen dieser Aufgabe beschrieben.

>[!NOTE] 
>Ab Anfang Juni 2017 verwendet Security Center den Microsoft Monitoring Agent zum Erfassen und Speichern von Daten. Weitere Informationen finden Sie unter [Azure Security Center – Plattformmigration](security-center-platform-migration.md). Die Informationen in diesem Artikel stellen Security Center-Funktionen nach dem Umstieg auf den Microsoft Monitoring Agent vor.
>

## <a name="what-are-security-policies"></a>Was sind Sicherheitsrichtlinien?
In einer Sicherheitsrichtlinie wird der Satz von Sicherheitsmechanismen definiert, die für Ressourcen in dem angegebenen Abonnement zu empfehlen sind. In Security Center definieren Sie Richtlinien für Ihre Azure-Abonnements gemäß den Sicherheitsanforderungen Ihres Unternehmens sowie gemäß der Art von Anwendungen oder der Vertraulichkeit der Daten in den einzelnen Abonnements.

So gelten beispielsweise für Ressourcen, die zu Entwicklungs- oder Testzwecken verwendet werden, unter Umständen andere Sicherheitsanforderungen als für Ressourcen, die für Produktionsanwendungen verwendet werden. Ebenso kann für Anwendungen mit reglementierten Daten, etwa personenbezogene Informationen (Personally Identifiable Information), eine höhere Sicherheitsstufe erforderlich sein. Die in Azure Security Center aktivierten Sicherheitsrichtlinien werden dazu verwendet, Sicherheitsempfehlungen und die Überwachung zu steuern, damit Sie potenzielle Sicherheitsrisiken identifizieren und Bedrohungen entschärfen können. Weitere Informationen dazu, wie Sie die für Sie am besten geeignete Option ermitteln können, finden Sie unter [Planungs- und Betriebshandbuch für Azure Security Center](security-center-planning-and-operations-guide.md) .

## <a name="set-security-policies"></a>Festlegen von Sicherheitsrichtlinien
Sie können Sicherheitsrichtlinien für jedes Abonnement konfigurieren. Damit Sie eine Sicherheitsrichtlinie ändern können, müssen Sie ein Besitzer oder Mitwirkender dieses Abonnements sein. Melden Sie sich am Azure-Portal an, und führen Sie die folgenden Schritte aus, um Sicherheitsrichtlinien in Security Center zu konfigurieren:

1. Klicken Sie auf dem Security Center-Dashboard auf die Kachel **Richtlinie** .
2. Wählen Sie auf dem Blatt „Sicherheitsrichtlinie“ das Abonnement aus, für das die Sicherheitsrichtlinie aktiviert werden soll.

    ![Definieren von Richtlinien](./media/security-center-policies/security-center-policies-fig1-ga.png)
3. Das Blatt **Sicherheitsrichtlinie** für das ausgewählte Abonnement wird mit einer Reihe von Optionen geöffnet. Auf diesem Blatt stehen folgende Optionen zur Verfügung:

   * **Präventionsrichtlinie**: Verwenden Sie diese Option, um Richtlinien auf Abonnementebene zu konfigurieren.  
   * **E-Mail-Benachrichtigung**: Verwenden Sie diese Option zum Konfigurieren einer E-Mail-Benachrichtigung, die beim ersten täglichen Auftreten einer Warnung und für Warnungen mit hohem Schweregrad gesendet wird. E-Mail-Optionen können nur für Abonnementrichtlinien konfiguriert werden. Weitere Informationen zum Konfigurieren einer E-Mail-Benachrichtigung finden Sie unter [Bereitstellen von Sicherheitskontaktinformationen in Azure Security Center](security-center-provide-security-contact-details.md) .
   * **Tarif**: Verwenden Sie diese Option, um für die Tarifauswahl ein Upgrade durchzuführen. Weitere Informationen zu den Preisoptionen finden Sie auf der [Security Center-Seite](security-center-pricing.md).
4. Stellen Sie sicher, dass die Option **Datensammlung für virtuelle Computer** auf **Ein** festgelegt ist. Diese Option aktiviert die automatische Protokollsammlung für vorhandene und neue Ressourcen mit dem Microsoft Monitoring Agent. Dies ist derselbe Agent, den auch die Operations Management Suite und der Log Analytics-Dienst verwenden. Die von diesem Agent gesammelten Daten werden entweder in vorhandenen Log Analytics-Arbeitsbereichen gespeichert, die mit Ihrem Azure-Abonnement verknüpft sind, oder unter Berücksichtigung des geografischen Standorts des virtuellen Computers in neuen Arbeitsbereichen.

5. Klicken Sie auf dem Blatt **Sicherheitsrichtlinie** auf **Präventionsrichtlinie**, um die verfügbaren Optionen anzuzeigen. Klicken Sie auf **Ein**, um die Sicherheitsempfehlungen zu aktivieren, die für dieses Abonnement relevant sind.

    ![Auswählen der Sicherheitsrichtlinien](./media/security-center-policies/security-center-policies-fig4-newUI.png)

Die folgende Tabelle gibt Aufschluss über die einzelnen Optionen:

| Richtlinie | Zustand „Ein“ |
| --- | --- |
| Systemupdates |Ruft eine tägliche Liste mit verfügbaren Sicherheitsupdates und kritischen Updates von Windows Update oder Windows Server Update Services ab. Die abgerufene Liste richtet sich nach dem Dienst, der für den virtuellen Computer konfiguriert wurde. Darin wird empfohlen, die fehlenden Updates anzuwenden. Bei Linux-Systemen wird für die Richtlinie das von der Distribution bereitgestellte Paketverwaltungssystem genutzt, um Pakete mit verfügbaren Updates zu ermitteln. Außerdem werden Sicherheitsupdates und kritische Updates für [Azure Cloud Services](../cloud-services/cloud-services-how-to-configure.md)-VMs ermittelt. |
| Sicherheitsrisiken des Betriebssystems |Führt eine tägliche Analyse von Betriebssystemkonfigurationen durch, um Probleme zu ermitteln, die mit einer Anfälligkeit des virtuellen Computers für Angriffe verbunden sind. Außerdem werden in der Richtlinie Konfigurationsänderungen empfohlen, um diesen Sicherheitsrisiken zu begegnen. Weitere Informationen zu den speziellen Konfigurationen, die überwacht werden, finden Sie in der [Liste mit den empfohlenen Basisregeln](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335) . (Zu diesem Zeitpunkt wird Windows Server 2016 nicht vollständig unterstützt.) |
| Endpoint Protection |Empfiehlt die Bereitstellung von Endpoint Protection für alle virtuellen Windows-Computer, um Viren, Spyware und andere Schadsoftware zu erkennen und zu entfernen. |
| Datenträgerverschlüsselung |Empfiehlt die Aktivierung der Datenträgerverschlüsselung auf allen virtuellen Computern, um den Datenschutz im Ruhezustand zu optimieren. |
| Netzwerksicherheitsgruppen |Empfiehlt die Konfiguration von [Netzwerksicherheitsgruppen](../virtual-network/virtual-networks-nsg.md) , um den eingehenden und ausgehenden Datenverkehr für VMs mit öffentlichen Endpunkten zu steuern. Netzwerksicherheitsgruppen, die für ein Subnetz konfiguriert sind, werden für alle Netzwerkschnittstellen der virtuellen Computer übernommen, sofern nichts anderes angegeben ist. Zusätzlich zur Überprüfung, ob eine Netzwerksicherheitsgruppe konfiguriert wurde, bewertet diese Richtlinie Sicherheitsregeln für eingehende Daten, um Regeln zu identifizieren, die eingehenden Datenverkehr zulassen. |
| Web Application Firewall |Empfiehlt die Bereitstellung einer Web Application Firewall auf virtuellen Computern, wenn eine der folgenden Bedingungen erfüllt ist: </br></br>[Öffentliche IP-Adresse auf Instanzebene](../virtual-network/virtual-networks-instance-level-public-ip.md) (Instance-level Public IP, ILPIP) wird verwendet, und die Eingangssicherheitsregeln für die zugeordnete Netzwerksicherheitsgruppe sind so konfiguriert, dass sie den Zugriff auf Port 80/443 ermöglichen.</br></br>Es wird eine IP-Adresse mit Lastenausgleich verwendet, und die zugehörigen Regeln für Lastenausgleich und eingehenden NAT-Datenverkehr (Netzwerkadressübersetzung) sind so konfiguriert, dass Zugriff auf den Port 80/443 zugelassen wird. Weitere Informationen finden Sie unter [Unterstützung des Azure-Ressourcen-Managers für Load Balancer](../load-balancer/load-balancer-arm.md). |
| Firewall der nächsten Generation |Erweitert den Schutz von Netzwerken über die in Azure integrierten Netzwerksicherheitsgruppen hinaus. Security Center erkennt Bereitstellungen, für die eine Firewall der nächsten Generation empfohlen wird, und ermöglicht Ihnen die Bereitstellung eines virtuellen Geräts. |
| SQL-Überwachung und -Bedrohungserkennung |Empfiehlt die Aktivierung der Zugriffsüberwachung für Azure-Datenbanken zur Erfüllung von Complianceanforderungen sowie die Aktivierung der erweiterten Bedrohungserkennung zu Untersuchungszwecken. |
| SQL-Verschlüsselung |Empfiehlt, dass die Verschlüsselung im Ruhezustand für Ihre Azure SQL-Datenbank, die zugehörigen Sicherungen und die Transaktionsprotokolldateien aktiviert wird. So können Ihre Daten auch dann nicht gelesen werden, wenn unberechtigt darauf zugegriffen wird. |
| Sicherheitsrisikobewertung |Empfiehlt die Installation einer Lösung zur Sicherheitsrisikobewertung auf dem virtuellen Computer. |
| Speicherverschlüsselung |Dieses Feature ist derzeit für Azure-Blobs und -Dateien verfügbar. Beachten Sie, dass nach dem Aktivieren der Speicherdienstverschlüsselung nur neue Daten verschlüsselt werden. Alle vorhandenen Dateien in diesem Speicherkonto bleiben unverschlüsselt. |

Klicken Sie nach dem Konfigurieren aller Optionen auf dem Blatt **Sicherheitsrichtlinie**, das die Empfehlungen enthält, auf **OK**, und klicken Sie anschließend auf dem Blatt **Sicherheitsrichtlinie**, das die ursprünglichen Einstellungen enthält, auf **Speichern**.

> [!NOTE]
> Der Tarif gilt auf Ressourcengruppenebene weiterhin. Weitere Informationen finden Sie auf der [Seite mit der Preisübersicht](https://azure.microsoft.com/pricing/details/security-center/).
>
>

## <a name="see-also"></a>Weitere Informationen
In diesem Dokument haben Sie erfahren, wie Sie Sicherheitsrichtlinien in Azure Security Center konfigurieren können. Weitere Informationen zu Azure Security Center finden Sie in den folgenden Quellen:

* [Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md)festgelegt ist. Hier erfahren Sie, wie Sie die Entwurfsaspekte in Bezug auf die Einführung von Azure Security Center planen und verstehen.
* [Überwachen der Sicherheitsintegrität in Azure Security Center](security-center-monitoring.md). Hier erfahren Sie, wie Sie die Integrität Ihrer Azure-Ressourcen überwachen.
* [Verwalten von und Reagieren auf Sicherheitswarnungen in Azure Security Center](security-center-managing-and-responding-alerts.md). Hier erfahren Sie, wie Sie Sicherheitswarnungen verwalten und darauf reagieren.
* [Überwachen von Partnerlösungen mit Azure Security Center](security-center-partner-solutions.md). Hier erfahren Sie, wie Sie den Integritätsstatus Ihrer Partnerlösungen überwachen.
* [Azure Security Center – häufig gestellte Fragen](security-center-faq.md)festgelegt ist. Enthält häufig gestellte Fragen zur Verwendung des Diensts.
* [Azure Security-Blog](http://blogs.msdn.com/b/azuresecurity/). Hier finden Sie Blogbeiträge zur Sicherheit und Compliance von Azure.

