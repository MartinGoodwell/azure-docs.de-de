---
title: Sichern von Workloads im klassischen Azure-Portal mithilfe von Azure Backup Server | Microsoft-Dokumentation
description: "Vergewissern Sie sich, dass Ihre Umgebung ordnungsgemäß für die Sicherung von Workloads mithilfe von Azure Backup Server vorbereitet ist."
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
keywords: 'Azure Backup Server: Sicherungstresor'
ms.assetid: d86450e8-da63-4283-8fd7-2ee629fa14ab
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.translationtype: Human Translation
ms.sourcegitcommit: ef1e603ea7759af76db595d95171cdbe1c995598
ms.openlocfilehash: 348df3f4359e572d3514e1b11ce709f946c2efea
ms.contentlocale: de-de
ms.lasthandoff: 06/16/2017


---
# <a name="preparing-to-back-up-workloads-using-azure-backup-server"></a>Vorbereiten der Sicherung von Workloads per Azure Backup Server
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure Backup Server (klassisch)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (klassisch)](backup-azure-dpm-introduction-classic.md)
>
>

In diesem Artikel geht es um das Vorbereiten Ihrer Umgebung für die Sicherung von Workloads per Azure Backup Server. Mit Azure Backup Server können Sie Anwendungsworkloads wie Hyper-V-VMs, Microsoft SQL Server, SharePoint Server, Microsoft Exchange und Windows-Clients über eine zentrale Konsole schützen.

> [!WARNING]
> Azure Backup Server erbt die Funktionalität des Data Protection Manager (DPM) für die Workloadsicherung. Sie finden bei einigen dieser Funktionen Verweise auf die DPM-Dokumentation. Azure Backup Server stellt jedoch keinen Schutz für Bandspeicher bereit und kann nicht in System Center integriert werden.
>
>

## <a name="1-windows-server-machine"></a>1. Windows Server-Computer
![Schritt 1](./media/backup-azure-microsoft-azure-backup/step1.png)

Der erste Schritt zum Einrichten von Azure Backup Server ist die Bereitstellung eines Windows Server-Computers.

| Standort | Mindestanforderungen | Zusätzliche Anweisungen |
| --- | --- | --- |
| Azure |Virtueller Azure-IaaS-Computer<br><br>A2-Standard: 2 Kerne, 3,5 GB RAM |Sie können mit einem einfachen Katalogimage von Windows Server 2012 R2 Datacenter beginnen. [Das Schützen von IaaS-Workloads mit Azure Backup Server (DPM)](https://technet.microsoft.com/library/jj852163.aspx) ist relativ komplex. Lesen Sie sich den Artikel ganz durch, bevor Sie die Maschine bereitstellen. |
| Lokal |Hyper-V-VM, <br> VMWare-VM<br> oder physischer Host<br><br>2 Kerne und 4 GB RAM |Sie können die DPM-Speicherung deduplizieren, indem Sie die Windows Server-Deduplizierung verwenden. Lesen Sie die weiteren Informationen zur Zusammenarbeit von [DPM und Deduplizierung](https://technet.microsoft.com/library/dn891438.aspx) bei Bereitstellung auf Hyper-V-VMs. |

> [!NOTE]
> Es wird empfohlen, Azure Backup Server auf einem Computer mit Windows Server 2012 R2 Datacenter zu installieren. Viele erforderliche Komponenten werden durch die neueste Version des Windows-Betriebssystems automatisch abgedeckt.
>
>

Wenn Sie Azure Backup Server einer Domäne hinzufügen möchten, empfiehlt es sich, den physischen Server oder virtuellen Computer vor der Installation der Azure Backup Server-Software der Domäne hinzuzufügen. Das Verschieben von Azure Backup Server in eine neue Domäne nach der Bereitstellung wird *nicht unterstützt*.

## <a name="2-backup-vault"></a>2. Sicherungstresor
![Schritt 2](./media/backup-azure-microsoft-azure-backup/step2.png)

Unabhängig davon, ob Sie die Sicherungsdaten an Azure senden oder lokal speichern, muss Azure Backup Server bei einem Tresor registriert sein. Wenn Sie mit der Arbeit mit Azure Backup nicht vertraut sind und Azure Backup Server verwenden möchten, sehen Sie die Azure-Portal-Version dieses Artikels ein: [Vorbereiten der Sicherung von Workloads mit Azure Backup Server](backup-azure-microsoft-azure-backup.md).

> [!IMPORTANT]
> Ab März 2017 können im klassischen Portal keine Sicherungstresore mehr erstellt werden.
> Sie können nun ein Upgrade für Ihre Sicherungstresore auf Recovery Services-Tresore durchführen. Detaillierte Informationen finden Sie im Artikel [Durchführen eines Upgrades für einen Sicherungstresor auf einen Recovery Services-Tresor](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft empfiehlt, ein Upgrade für Ihre Sicherungstresore auf Recovery Services-Tresore durchzuführen.<br/> **Ab dem 1. November 2017**:
>- Für alle verbleibenden Sicherungstresore wird automatisch ein Upgrade auf Recovery Services-Tresore durchgeführt.
>- Der Zugriff auf Ihre Sicherungsdaten im klassischen Portal wird nicht möglich sein. Verwenden Sie stattdessen das Azure-Portal, um auf Ihre Sicherungsdaten in Recovery Services-Tresoren zuzugreifen.
>



## <a name="3-software-package"></a>3. Softwarepaket
![Schritt 3](./media/backup-azure-microsoft-azure-backup/step3.png)

### <a name="downloading-the-software-package"></a>Herunterladen des Softwarepakets
Ähnlich wie die Tresoranmeldedaten können Sie den Microsoft Azure Backup-Server für Anwendungsworkloads von der **Schnellstartseite** des Sicherungstresors herunterladen.

1. Klicken Sie auf **Für Anwendungsworkloads (Datenträger zu Datenträger zu Cloud)**. Sie gelangen auf die Download Center-Seite, von der Sie das Softwarepaket herunterladen können.

    ![Willkommensseite von Microsoft Azure Backup](./media/backup-azure-microsoft-azure-backup/dpm-venus1.png)
2. Klicken Sie auf **Download**.

    ![Download Center 1](./media/backup-azure-microsoft-azure-backup/downloadcenter1.png)
3. Wählen Sie alle Dateien aus, und klicken Sie auf **Weiter**. Laden Sie alle Dateien herunter, die von der Microsoft Azure Backup-Downloadseite eingehen, und speichern Sie alle Dateien in dem gleichen Ordner.
   ![Download Center 1](./media/backup-azure-microsoft-azure-backup/downloadcenter.png)

    Da die Downloadgröße aller Dateien zusammen mehr als 3 G beträgt, dauert es über einen Downloadlink mit 10 MBit/s bis zu 60 Minuten, bis der Download abgeschlossen ist.

### <a name="extracting-the-software-package"></a>Extrahieren des Softwarepakets
Nachdem Sie alle Dateien heruntergeladen haben, klicken Sie auf **MicrosoftAzureBackupInstaller.exe**. Der **Setup-Assistent von Microsoft Azure Backup** wird gestartet, um die Setupdateien an einem Speicherort Ihrer Wahl zu extrahieren. Fahren Sie mit dem Assistenten fort, und klicken Sie auf die Schaltfläche **Extrahieren** , um den Extrahierungsprozess zu starten.

> [!WARNING]
> Zum Extrahieren der Setupdateien sind mindestens 4 GB freier Speicherplatz erforderlich.
>
>

![Setup-Assistent von Microsoft Azure Backup](./media/backup-azure-microsoft-azure-backup/extract/03.png)

Aktivieren Sie nach Abschluss der Extrahierung das Kontrollkästchen, um die gerade extrahierte Datei *setup.exe* zu starten und mit der Installation von Microsoft Azure Backup Server zu beginnen. Klicken Sie dann auf die Schaltfläche **Fertig stellen**.

### <a name="installing-the-software-package"></a>Installieren des Softwarepakets
1. Klicken Sie auf **Microsoft Azure Backup** , um den Setup-Assistenten zu starten.

    ![Setup-Assistent von Microsoft Azure Backup](./media/backup-azure-microsoft-azure-backup/launch-screen2.png)
2. Klicken Sie auf der Willkommensseite auf die Schaltfläche **Weiter** . Sie gelangen zum Abschnitt *Voraussetzungsüberprüfungen* . Klicken Sie auf diesem Bildschirm auf die Schaltfläche **Überprüfen** , um zu ermitteln, ob die Hardware- und Softwarevoraussetzungen für Azure Backup Server erfüllt sind. Wenn alle Voraussetzungen erfolgreich erfüllt wurden, sehen Sie eine Meldung, die darauf hinweist, dass der Computer die Anforderungen erfüllt. Klicken Sie auf die Schaltfläche **Weiter** .

    ![Azure Backup Server – Willkommen und Voraussetzungsüberprüfung](./media/backup-azure-microsoft-azure-backup/prereq/prereq-screen2.png)
3. Für Microsoft Azure Backup Server ist SQL Server Standard erforderlich, und im Azure Backup Server-Installationspaket sind die passenden SQL Server-Binärdaten enthalten. Beim Starten einer neuen Azure Backup Server-Installation sollten Sie die Option **Neue Instanz von SQL Server bei diesem Setup installieren** auswählen und auf die Schaltfläche **Prüfen und installieren** klicken. Nachdem die erforderlichen Komponenten erfolgreich installiert wurden, klicken Sie auf **Weiter**.

    ![Azure Backup Server – SQL-Überprüfung](./media/backup-azure-microsoft-azure-backup/sql/01.png)

    Tritt ein Fehler mit der Empfehlung auf, den Computer neu zu starten, tun Sie dies, und klicken Sie auf **Erneut prüfen**.

   > [!NOTE]
   > Azure Backup Server funktioniert nicht mit einer Remoteinstanz von SQL Server. Die von Azure Backup Server verwendete Instanz muss lokal vorliegen.
   >
   >

4. Geben Sie einen Speicherort für die Installation der Microsoft Azure Backup-Serverdateien an, und klicken Sie auf **Weiter**.

    ![Voraussetzungen 2 für Microsoft Azure Backup](./media/backup-azure-microsoft-azure-backup/space-screen.png)

    Das Scratchverzeichnis ist eine Anforderung für die Sicherung in Azure. Stellen Sie sicher, dass das Scratchverzeichnis eine Größe von mindestens 5 % der Daten aufweist, die in der Cloud gesichert werden. Für den Datenträgerschutz müssen separate Datenträger nach Abschluss der Installation konfiguriert werden. Weitere Informationen zu Speicherpools finden Sie unter [Konfigurieren von Speicherpools und Datenträgerspeicher](https://technet.microsoft.com/library/hh758075.aspx).
5. Geben Sie ein sicheres Kennwort für eingeschränkte lokale Benutzerkonten an, und klicken Sie auf **Weiter**.

    ![Voraussetzungen 2 für Microsoft Azure Backup](./media/backup-azure-microsoft-azure-backup/security-screen.png)
6. Bestimmen Sie, ob Sie mit *Microsoft Update* nach Updates suchen möchten, und klicken Sie auf **Weiter**.

   > [!NOTE]
   > Es wird empfohlen, Windows Update an Microsoft Update umzuleiten, da Microsoft Update Sicherheit und wichtige Updates für Windows und andere Produkte wie Microsoft Azure Backup Server bietet.
   >
   >

    ![Voraussetzungen 2 für Microsoft Azure Backup](./media/backup-azure-microsoft-azure-backup/update-opt-screen2.png)
7. Überprüfen Sie die *Zusammenfassung der Einstellungen* , und klicken Sie auf **Installieren**.

    ![Voraussetzungen 2 für Microsoft Azure Backup](./media/backup-azure-microsoft-azure-backup/summary-screen.png)
8. Die Installation erfolgt in mehreren Phasen. In der ersten Phase wird der Microsoft Azure Recovery Services-Agent auf dem Server installiert. Der Assistent überprüft auch das Vorhandensein der Internetverbindung. Wenn eine Internetverbindung verfügbar ist, können Sie mit der Installation fortfahren, andernfalls müssen Sie Proxydetails angeben, um die Verbindung mit dem Internet herzustellen.

    Der nächste Schritt ist die Konfiguration des Microsoft Azure Recovery Services-Agents. Bei der Konfiguration müssen Sie Ihre Tresoranmeldeinformationen zum Registrieren des Computers für den Sicherungstresor angeben. Sie geben auch eine Passphrase zum Verschlüsseln bzw. Entschlüsseln von Daten an, die zwischen Azure und Ihrem lokalen Standort ausgetauscht werden. Sie können eine automatische Passphrase generieren oder eine eigene Passphrase mit mindestens 16 Zeichen angeben. Fahren Sie mit dem Assistenten fort, bis der Agent konfiguriert wurde.

    ![Voraussetzungen 2 für Azure Backup Server](./media/backup-azure-microsoft-azure-backup/mars/04.png)
9. Nach Abschluss der Registrierung von Microsoft Azure Backup Server fährt der übergreifende Setup-Assistent mit der Installation und Konfiguration von SQL Server und der Azure Backup Server-Komponenten fort. Nachdem die Installation der SQL Server-Komponenten abgeschlossen ist, werden die Azure Backup Server-Komponenten installiert.

    ![Azure Backup Server](./media/backup-azure-microsoft-azure-backup/final-install/venus-installation-screen.png)

Wenn der Installationsschritt abgeschlossen ist, wurden auch die Desktopsymbole des Produkts bereits erstellt. Doppelklicken Sie einfach auf das Symbol, um das Produkt zu starten.

### <a name="add-backup-storage"></a>Hinzufügen von Backup Storage
Die erste Sicherungskopie wird in einem Speicherbereich vorgehalten, der dem Azure Backup Server-Computer zugeordnet ist. Weitere Informationen zum Hinzufügen von Datenträgern finden Sie unter [Konfigurieren von Speicherpools und Datenträgerspeicher](https://technet.microsoft.com/library/hh758075.aspx).

> [!NOTE]
> Sie müssen auch dann Backup Storage hinzufügen, wenn Sie Daten an Azure senden möchten. Bei der aktuellen Architektur von Azure Backup Server enthält der Azure Backup-Tresor die *zweite* Kopie der Daten, und der lokale Speicher enthält die erste (obligatorische) Sicherungskopie.  
>
>

## <a name="4-network-connectivity"></a>4. Netzwerkverbindung
![Schritt 4](./media/backup-azure-microsoft-azure-backup/step4.png)

Azure Backup Server muss mit dem Azure Backup-Dienst verbunden sein, um erfolgreich ausgeführt werden zu können. Verwenden Sie zum Überprüfen, ob der Computer über eine Verbindung mit Azure verfügt, das Cmdlet ```Get-DPMCloudConnection``` in der Azure Backup Server-PowerShell-Konsole. Wenn die Ausgabe des Cmdlets „TRUE“ lautet, besteht eine Verbindung. Andernfalls besteht keine Verbindung.

Gleichzeitig muss das Azure-Abonnement einen fehlerfreien Zustand aufweisen. Um den Status Ihres Abonnements zu ermitteln und es zu verwalten, melden Sie sich beim [Abonnementportal](https://account.windowsazure.com/Subscriptions)an.

Nachdem Sie den Status der Azure-Verbindung und des Azure-Abonnements kennen, können Sie anhand der Tabelle unten ermitteln, welche Auswirkungen mit einer Sicherungs-/Wiederherstellungsfunktion verbunden sind.

| Verbindungszustand | Azure-Abonnement | Sicherung auf Azure | Sicherung auf einen Datenträger | Wiederherstellung von Azure | Wiederherstellung von einem Datenträger |
| --- | --- | --- | --- | --- | --- |
| Verbunden |Aktiv |Zulässig |Zulässig |Zulässig |Zulässig |
| Verbunden |Abgelaufen |Beendet |Beendet |Zulässig |Zulässig |
| Verbunden |Bereitstellung aufgehoben |Beendet |Beendet |Beendet und Azure-Wiederherstellungspunkte gelöscht |Beendet |
| Verbindung vor mehr als 15 Tagen verloren |Aktiv |Beendet |Beendet |Zulässig |Zulässig |
| Verbindung vor mehr als 15 Tagen verloren |Abgelaufen |Beendet |Beendet |Zulässig |Zulässig |
| Verbindung vor mehr als 15 Tagen verloren |Bereitstellung aufgehoben |Beendet |Beendet |Beendet und Azure-Wiederherstellungspunkte gelöscht |Beendet |

### <a name="recovering-from-loss-of-connectivity"></a>Wiederherstellung nach Verbindungsverlust
Wenn Sie über eine Firewall oder einen Proxy verfügen, die bzw. der den Zugriff auf Azure verhindert, müssen Sie im Profil der Firewall bzw. des Proxys die folgenden Domänenadressen auf die Positivliste setzen:

* www.msftncsi.com
* \*.Microsoft.com
* \*.WindowsAzure.com
* \*.microsoftonline.com
* \*.windows.net

Nach dem Wiederherstellen der Verbindung mit Azure für den Azure Backup Server-Computer wird anhand des Azure-Abonnementstatus ermittelt, welche Vorgänge durchgeführt werden können. Die obige Tabelle enthält Details zu den Vorgängen, die nach dem „Verbinden“ des Computers zulässig sind.

### <a name="handling-subscription-states"></a>Behandeln von Abonnementstatus
Es ist möglich, den Status eines Azure-Abonnements von *Abgelaufen* oder *Bereitstellung aufgehoben* in *Aktiv* zu ändern. Dies ist aber mit Auswirkungen auf das Produktverhalten verbunden, solange der Status nicht *Aktiv*lautet:

* Ein Abonnement mit dem Status *Bereitstellung aufgehoben* verliert für den Zeitraum der Aufhebung die Funktionalität. Beim Festlegen auf *Aktiv*wird die Produktfunktionalität für Sicherung/Wiederherstellung wieder aktiviert. Die Sicherungsdaten auf der lokalen Festplatte können auch abgerufen werden, sofern sie mit einer ausreichend langen Beibehaltungsdauer versehen sind. Die Sicherungsdaten in Azure gehen aber unwiederbringlich verloren, wenn das Abonnement in den Status *Bereitstellung aufgehoben* versetzt wird.
* Für ein Abonnement mit dem Status *Abgelaufen* geht die Funktionalität nur so lange verloren, bis es wieder in den Status *Aktiv* versetzt wird. Alle Sicherungen für den Zeitraum, in dem sich das Abonnement im Status *Abgelaufen* befindet, werden nicht ausgeführt.

## <a name="troubleshooting"></a>Problembehandlung
Wenn auf dem Microsoft Azure Backup-Server während der Installationsphase (oder bei der Sicherung oder der Wiederherstellung) Fehler auftreten, verwenden Sie dieses [Dokument mit Fehlercodes](https://support.microsoft.com/kb/3041338), um weitere Informationen zu erhalten.
Sie können auch [Azure Backup – Häufig gestellte Fragen](backup-azure-backup-faq.md)

## <a name="next-steps"></a>Nächste Schritte
Ausführliche Informationen zum [Vorbereiten der Umgebung für DPM](https://technet.microsoft.com/library/hh758176.aspx) finden Sie auf der Microsoft TechNet-Website. Sie finden dort auch Informationen zu den unterstützten Konfigurationen, unter denen Azure Backup Server bereitgestellt und verwendet werden kann.

In den folgenden Artikeln finden Sie zusätzliche Informationen zum Workloadschutz mit einem Microsoft Azure Backup-Server.

* [SQL Server-Sicherung](backup-azure-backup-sql.md)
* [SharePoint Server-Sicherung](backup-azure-backup-sharepoint.md)
* [Sicherung eines anderen Servers](backup-azure-alternate-dpm-server.md)

