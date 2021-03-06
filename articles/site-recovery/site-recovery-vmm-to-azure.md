---
title: Replizieren virtueller Hyper-V-Computer in VMM-Clouds in Azure | Microsoft-Dokumentation
description: Orchestrieren von Replikation, Failover und Wiederherstellung von Hyper-V-VMs, die in System Center VMM-Clouds verwaltet werden, in Azure
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: raynew
ms.translationtype: HT
ms.sourcegitcommit: 0425da20f3f0abcfa3ed5c04cec32184210546bb
ms.openlocfilehash: 475b0cea9be58c9b6fa13645e3c19cc3b689aab2
ms.contentlocale: de-de
ms.lasthandoff: 07/20/2017

---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-site-recovery-in-the-azure-portal"></a>Replizieren von virtuellen Hyper-V-Computern in VMM-Clouds in Azure per Site Recovery im Azure-Portal
> [!div class="op_single_selector"]
> * [Azure-Portal](site-recovery-vmm-to-azure.md)
> * [Klassisches Azure](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell – Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell (klassisch)](site-recovery-deploy-with-powershell.md)


In diesem Artikel erfahren Sie, wie Sie lokale virtuelle Hyper-V-Computer, die in System Center-VMM-Clouds verwaltet werden, mithilfe des [Azure Site Recovery](site-recovery-overview.md)-Diensts über das Azure-Portal in Azure replizieren.

Kommentare können Sie am Ende dieses Artikels oder im [Forum zu Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) hinterlassen.

Wenn Sie Computer zu Azure migrieren möchten (ohne Failback), erfahren Sie [in diesem Artikel](site-recovery-migrate-to-azure.md) mehr darüber.


## <a name="deployment-steps"></a>Bereitstellungsschritte

Führen Sie anhand des Artikels diese Bereitstellungsschritte aus:


1. [Erfahren Sie mehr](site-recovery-components.md) über die Architektur für diese Bereitstellung. [Informieren Sie sich](site-recovery-hyper-v-azure-architecture.md) darüber hinaus über die Funktionsweise der Hyper-V-Replikation in Site Recovery.
2. Überprüfen Sie die Voraussetzungen und Einschränkungen.
3. Richten Sie Azure-Netzwerk- und -Speicherkonten ein.
4. Bereiten Sie den lokalen VMM-Server und die Hyper-V-Hosts vor.
5. Erstellen Sie einen Recovery Services-Tresor. Der Tresor enthält Konfigurationseinstellungen und dient zum Orchestrieren der Replikation.
6. Geben Sie die Einstellungen für die Datenquelle an. Registrieren Sie den VMM-Server im Tresor. Installieren Sie den Azure Site Recovery-Anbieter auf dem VMM-Server und den Microsoft Recovery Services-Agent auf den Hyper-V-Hosts.
7. Geben Sie die Ziel- und Replikationseinstellungen an.
8. Aktivieren Sie die Replikation für die VMs.
9. Führen Sie ein Testfailover aus, um sicherzustellen, dass alles wie erwartet funktioniert.



## <a name="prerequisites"></a>Voraussetzungen


**Supportbedarf** | **Details**
--- | ---
**Azure** | Informieren Sie sich über die [Azure-Anforderungen](site-recovery-prereq.md#azure-requirements).
**Lokale Server** | [Erfahren Sie mehr](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-in-vmm-clouds-to-azure) zu den Anforderungen für den lokalen VMM-Server und die Hyper-V-Hosts.
**Lokale Hyper-V-VMs** | Auf VMs, die Sie replizieren möchten, sollte ein [unterstütztes Betriebssystem](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) ausgeführt werden, das die [Azure-Voraussetzungen](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) erfüllt.
**Azure-URLs** | Der VMM-Server benötigt Zugriff auf diese URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Stellen Sie bei Verwendung von auf IP-Adressen basierenden Firewallregeln sicher, dass hierfür die Kommunikation mit Azure möglich ist.<br/></br> Lassen Sie die [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) (IP-Bereiche für Azure-Rechenzentren) und den HTTPS-Port (443) zu.<br/></br> Lassen Sie IP-Adressbereiche für die Azure-Region Ihres Abonnements und für die Region „USA, Westen“ (wird für Zugriffsteuerung und Identitätsverwaltung verwendet) zu.


## <a name="prepare-for-deployment"></a>Vorbereiten der Bereitstellung
Für die Vorbereitung der Bereitstellung benötigen Sie Folgendes:

1. [Richten Sie ein Azure-Netzwerk ein](#set-up-an-azure-network) , in dem sich Azure-VMs nach dem Failover befinden.
2. [Richten Sie ein Azure-Speicherkonto ein](#set-up-an-azure-storage-account) , das für replizierte Daten verwendet werden kann.
3. [Bereiten Sie den VMM-Server vor](#prepare-the-vmm-server) , um die Site Recovery-Bereitstellung durchführen zu können.
4. Bereiten Sie die Netzwerkzuordnung vor. Richten Sie Netzwerke ein, damit Sie die Netzwerkzuordnung während der Site Recovery-Bereitstellung konfigurieren können.

### <a name="set-up-an-azure-network"></a>Richten Sie ein Azure-Netzwerk ein
Sie benötigen ein Azure-Netzwerk, mit dem nach dem Failover erstellte virtuelle Azure-Computer eine Verbindung herstellen.

* Das Netzwerk muss sich in der gleichen Region befinden wie der Recovery Services-Tresor.
* Richten Sie das Azure-Netzwerk im [Resource Manager-Modus](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) oder im [klassischen Modus](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) ein (je nachdem, welches Ressourcenmodell Sie für virtuelle Azure-Computer nach dem Failover verwenden möchten).
* Wir empfehlen Ihnen, ein Netzwerk einzurichten, bevor Sie beginnen. Falls Sie es nicht tun, müssen Sie diesen Schritt während der Site Recovery-Bereitstellung ausführen.
Von Site Recovery verwendete Azure-Netzwerke können nicht innerhalb eines Abonnements oder über mehrere Abonnements hinweg [verschoben](../azure-resource-manager/resource-group-move-resources.md) werden.

### <a name="set-up-an-azure-storage-account"></a>Richten Sie ein Azure-Speicherkonto ein
* Sie benötigen ein Standard-/Premium-Azure Storage-Konto zum Speichern nach Azure replizierter Daten. [Storage Premium](../storage/storage-premium-storage.md) wird für virtuelle Computer verwendet, die eine konsistent hohe E/A-Leistung und geringe Latenz zum Hosten von E/A-intensiven Workloads erfordern. Wenn Sie ein Premiumkonto zum Speichern replizierter Daten verwenden möchten, benötigen Sie außerdem ein Standard-Speicherkonto zum Speichern von Replikationsprotokollen, in denen laufende Änderungen lokaler Daten erfasst werden. Das Konto muss sich in derselben Region wie der Recovery Services-Tresor befinden.
* Richten Sie ein Konto im [Resource Manager-Modus](../storage/storage-create-storage-account.md) oder im [klassischen Modus](../storage/storage-create-storage-account-classic-portal.md) ein (je nachdem, welches Ressourcenmodell Sie für virtuelle Azure-Computer nach dem Failover verwenden möchten).
* Es wird empfohlen, ein Konto einzurichten, bevor Sie beginnen. Falls Sie es nicht tun, müssen Sie diesen Schritt während der Site Recovery-Bereitstellung ausführen.
- Beachten Sie, dass von Site Recovery verwendete Azure-Speicherkonten nicht innerhalb eines Abonnements oder über mehrere Abonnements hinweg [verschoben](../azure-resource-manager/resource-group-move-resources.md) werden können.

### <a name="prepare-the-vmm-server"></a>Bereiten Sie den VMM-Server vor
* Stellen Sie sicher, dass der VMM-Server die [Voraussetzungen](#prerequisites)erfüllt.
* Während der Bereitstellung von Site Recovery können Sie angeben, dass alle Clouds auf einem VMM-Server im Azure-Portal verfügbar sein sollen. Falls nur bestimmte Clouds im Portal angezeigt werden sollen, können Sie diese Einstellung in der Cloud in der VMM-Administratorkonsole aktivieren.

### <a name="prepare-for-network-mapping"></a>Bereiten Sie die Netzwerkzuordnung vor
Sie müssen die Netzwerkzuordnung während der Site Recovery-Bereitstellung einrichten. Die Netzwerkzuordnung wird zwischen VMM-VM-Quellnetzwerken und Azure-Zielnetzwerken erstellt und ermöglicht Folgendes:

* Computer, für die das Failover in demselben Netzwerk durchgeführt wird, können eine Verbindung miteinander herstellen. Dies gilt auch, wenn das Failover nicht auf die gleiche Weise oder innerhalb desselben Wiederherstellungsplans durchgeführt wird.
* Wenn ein Netzwerkgateway im Azure-Zielnetzwerk eingerichtet ist, können virtuelle Azure-Computer eine Verbindung mit lokalen virtuellen Computern herstellen.
* Zur Einrichtung der Netzwerkzuordnung benötigen Sie Folgendes:

  * Stellen Sie sicher, dass VMs auf dem Hyper-V-Quellhostserver mit einem VMM-VM-Netzwerk verbunden sind. Dieses Netzwerk sollte mit einem logischen Netzwerk verbunden sein, das der Cloud zugeordnet ist.
  * Ein Azure-Netzwerk wie [oben](#set-up-an-azure-network)

## <a name="create-a-recovery-services-vault"></a>Erstellen eines Recovery Services-Tresors
1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com)an.
2. Klicken Sie auf **Neu** > **Überwachung und Verwaltung** > **Backup und Site Recovery (OMS)**.

    ![Neuer Tresor](./media/site-recovery-vmm-to-azure/new-vault3.png)
3. Geben Sie unter **Name**einen Anzeigenamen an, mit dem der Tresor identifiziert wird. Wenn Sie mehrere Abonnements haben, müssen Sie ein Abonnement auswählen.
4. [Erstellen Sie eine Ressourcengruppe](../azure-resource-manager/resource-group-template-deploy-portal.md), oder wählen Sie eine vorhandene Ressourcengruppe aus. Geben Sie eine Azure-Region an. Computer werden in dieser Region repliziert. Sie finden eine Liste der unterstützten Regionen unter Geografische Verfügbarkeit auf der Seite [Azure Site Recovery – Preisübersicht](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Wenn Sie schnell über das Dashboard auf den Tresor zugreifen möchten, klicken Sie auf **An Dashboard anheften** > **Tresor erstellen**.

    ![Neuer Tresor](./media/site-recovery-vmm-to-azure/new-vault.png)

Der neue Tresor wird unter **Dashboard** > **Alle Ressourcen** und auf dem Hauptblatt **Recovery Services-Tresore** angezeigt.


## <a name="select-the-protection-goal"></a>Auswählen des Schutzziels

Wählen Sie aus, was Sie replizieren möchten und wohin die Daten repliziert werden sollen.

1. Wählen Sie unter **Recovery Services-Tresore** den Tresor aus.
2. Klicken Sie unter **Erste Schritte** auf **Site Recovery** > **Bereiten Sie die Infrastruktur vor** > **Schutzziel**.

    ![Ziele wählen](./media/site-recovery-vmm-to-azure/choose-goals.png)
3. Wählen Sie unter **Schutzziel** die Option **To Azure** (Zu Azure) und dann **Yes, with Hyper-V** (Ja, mit Hyper-V) aus. Wählen Sie **Ja** , um zu bestätigen, dass Sie VMM zum Verwalten von Hyper-V-Hosts und des Wiederherstellungsstandorts verwenden. Klicken Sie dann auf **OK**.

## <a name="set-up-the-source-environment"></a>Einrichten der Quellumgebung

Installieren Sie den Azure Site Recovery-Anbieter auf dem VMM-Server, und registrieren Sie den Server im Tresor. Installieren Sie den Azure Recovery Services-Agent auf den Hyper-V-Hosts.

1. Klicken Sie auf **Infrastruktur vorbereiten** > **Quelle**.

    ![Quelle einrichten](./media/site-recovery-vmm-to-azure/set-source1.png)

2. Klicken Sie unter **Quelle vorbereiten** auf **+ VMM**, um einen VMM-Server hinzuzufügen.

    ![Quelle einrichten](./media/site-recovery-vmm-to-azure/set-source2.png)

3. Vergewissern Sie sich unter **Server hinzufügen**, dass unter **Servertyp** der Eintrag **System Center-VMM-Server** angezeigt wird und dass der VMM-Server die [Voraussetzungen und URL-Anforderungen](#prerequisites) erfüllt.
4. Laden Sie die Installationsdatei für den Azure Site Recovery-Anbieter herunter.
5. Laden Sie den Registrierungsschlüssel herunter. Sie benötigen diese Angaben beim Ausführen des Setups. Der Schlüssel ist nach der Erstellung fünf Tage lang gültig.

    ![Quelle einrichten](./media/site-recovery-vmm-to-azure/set-source3.png)


## <a name="install-the-provider-on-the-vmm-server"></a>Installieren des Anbieters auf dem VMM-Server

1. Führen Sie die Anbietersetupdatei auf dem VMM-Server aus.
2. Unter **Microsoft Update** können Sie Updates aktivieren, damit Updates für den Anbieter gemäß Ihrer Microsoft Update-Richtlinie installiert werden.
3. Ändern Sie unter **Installation** den Speicherort für die Anbieterinstallation, oder akzeptieren Sie den Standardspeicherort, und klicken Sie auf **Installieren**.

    ![Installationsspeicherort](./media/site-recovery-vmm-to-azure/provider2.png)
4. Klicken Sie nach Abschluss der Installation auf **Registrieren**, um den VMM-Server im Tresor zu registrieren.
5. Klicken Sie auf der Seite **Tresoreinstellungen** auf **Durchsuchen**, um die Tresorschlüsseldatei auszuwählen. Geben Sie das Azure Site Recovery-Abonnement und den Tresornamen an.

    ![Serverregistrierung](./media/site-recovery-vmm-to-azure/provider10.PNG)
6. Geben Sie unter **Internetverbindung**an, wie für den Anbieter, der auf dem VMM-Server ausgeführt wird, über das Internet eine Verbindung mit Site Recovery hergestellt wird.

   * Wenn der Anbieter eine direkte Verbindung herstellen soll, wählen Sie **Direkt mit Azure Site Recovery verbinden (ohne Proxyserver)** aus.
   * Wenn für den vorhandenen Proxy eine Authentifizierung erforderlich ist oder wenn Sie einen benutzerdefinierten Proxy verwenden möchten, wählen Sie **Unter Verwendung eines Proxyservers mit Azure Site Recovery verbinden** aus.
   * Geben Sie bei einem benutzerdefinierten Proxy die Adresse, den Port und Anmeldeinformationen ein.
   * Bei Verwendung eines Proxys sollten Sie die unter [Voraussetzungen](#on-premises-prerequisites) beschriebenen URLs bereits zugelassen haben.
   * Wenn Sie einen benutzerdefinierten Proxy verwenden, wird ein ausführendes VMM-Konto (DRAProxyAccount) automatisch mit den angegebenen Proxyanmeldeinformationen erstellt. Konfigurieren Sie den Proxyserver so, dass dieses Konto erfolgreich authentifiziert werden kann. In der VMM-Konsole können die Einstellungen des ausführenden VMM-Kontos geändert werden. Erweitern Sie unter **Einstellungen** die Option **Sicherheit** > **Ausführende Konten**, und ändern Sie das Kennwort für DRAProxyAccount. Sie müssen den VMM-Dienst neu starten, damit diese Einstellung wirksam wird.

     ![Internet](./media/site-recovery-vmm-to-azure/provider13.PNG)
7. Akzeptieren oder ändern Sie den Speicherort eines SSL-Zertifikats, das für die Datenverschlüsselung automatisch generiert wird. Dieses Zertifikat wird verwendet, wenn Sie Datenverschlüsselung für eine Cloud im Azure Site Recovery-Portal aktivieren. Bewahren Sie dieses Zertifikat sicher auf. Wenn Sie ein Failover zu Azure ausführen, benötigen Sie es für die Entschlüsselung, falls die Datenverschlüsselung aktiviert ist.
8. Geben Sie unter **Servername**einen Anzeigenamen ein, um den VMM-Server im Tresor zu identifizieren. Geben Sie in einer Clusterkonfiguration den Rollennamen des VMM-Clusters an.
9. Aktivieren Sie die Option **Cloudmetadaten synchronisieren**, wenn Metadaten für alle Clouds auf dem VMM-Server mit dem Tresor synchronisiert werden sollen. Diese Aktion muss für jeden VMM-Server nur einmal ausgeführt werden. Wenn Sie nicht alle Clouds synchronisieren möchten, können Sie diese Einstellung deaktiviert lassen und in den Cloudeigenschaften in der VMM-Konsole jede Cloud einzeln synchronisieren. Klicken Sie auf **Registrieren** , um den Prozess abzuschließen.

    ![Serverregistrierung](./media/site-recovery-vmm-to-azure/provider16.PNG)
10. Die Registrierung beginnt. Nach Abschluss der Registrierung wird der Server unter **Site Recovery-Infrastruktur** > **VMM-Server** angezeigt.


## <a name="install-the-azure-recovery-services-agent-on-hyper-v-hosts"></a>Installieren des Azure Recovery Services-Agent auf den Hyper-V-Hosts

1. Nachdem Sie den Anbieter eingerichtet haben, müssen Sie die Installationsdatei für den Azure Recovery Services-Agent herunterladen. Führen Sie das Setup auf jedem Hyper-V-Server in der VMM-Cloud aus.

    ![Hyper-V-Standorte](./media/site-recovery-vmm-to-azure/hyperv-agent1.png)
2. Klicken Sie in der **Voraussetzungsüberprüfung** auf **Weiter**. Alle fehlenden Komponenten, die Voraussetzung sind, werden automatisch installiert.

    ![Voraussetzungen Recovery Services-Agent](./media/site-recovery-vmm-to-azure/hyperv-agent2.png)
3. Übernehmen oder ändern Sie in den **Installationseinstellungen** den Installationsspeicherort und den Cachespeicherort. Sie können den Cache auf einem Laufwerk konfigurieren, auf dem mindestens 5 GB Speicherplatz verfügbar sind, aber wir raten Ihnen zu einem Cachelaufwerk mit mindestens 600 GB freiem Speicherplatz. Klicken Sie dann auf **Weiter**.
4. Klicken Sie nach Abschluss der Installation auf **Schließen** , um den Vorgang zu beenden.

    ![MARS-Agent registrieren](./media/site-recovery-vmm-to-azure/hyperv-agent3.png)

### <a name="command-line-installation"></a>Installation über die Befehlszeile
Sie können den Microsoft Azure Recovery Services-Agent mit dem folgenden Befehl über die Befehlszeile installieren:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-to-site-recovery-from-hyper-v-hosts"></a>Einrichten des Internetzugriffs auf Site Recovery per Proxy auf Hyper-V-Hosts

Für den Recovery Services-Agent, der auf Hyper-V-Hosts ausgeführt wird, ist für die VM-Replikation Internetzugriff auf Azure erforderlich. Gehen Sie bei der Einrichtung wie folgt vor, wenn Sie über einen Proxy auf das Internet zugreifen:

1. Öffnen Sie das Microsoft Azure Backup-MMC-Snap-In auf dem Hyper-V-Host. Standardmäßig ist auf dem Desktop oder unter „C:\Programme\Microsoft Azure Recovery Services Agent\bin\wabadmin“ eine Verknüpfung für Microsoft Azure Backup verfügbar.
2. Klicken Sie im Snap-In auf **Eigenschaften ändern**.
3. Geben Sie auf der Registerkarte **Proxykonfiguration** Informationen zum Proxyserver an.

    ![MARS-Agent registrieren](./media/site-recovery-vmm-to-azure/mars-proxy.png)
4. Vergewissern Sie sich, dass der Agent die unter [Voraussetzungen](#on-premises-prerequisites) beschriebenen URLs erreichen kann.

## <a name="set-up-the-target-environment"></a>Einrichten der Zielumgebung
Geben Sie das Azure-Speicherkonto, das für die Replikation verwendet werden soll, und das Azure-Netzwerk an, mit dem Azure-VMs nach dem Failover eine Verbindung herstellen.

1. Klicken Sie auf **Infrastruktur vorbereiten** > **Ziel**, und wählen Sie das Abonnement und die Ressourcengruppe aus, in dem bzw. der Sie die virtuellen Computer erstellen möchten, für die ein Failover durchgeführt wurde. Wählen Sie das Bereitstellungsmodell aus, das in Azure für die virtuellen Computer verwendet werden soll, für die ein Failover durchgeführt wurde (klassisch oder Resource Manager).

    ![Speicher](./media/site-recovery-vmm-to-azure/enablerep3.png)

2. Site Recovery prüft, ob Sie über ein oder mehrere kompatible Azure-Speicherkonten und -Netzwerke verfügen.

    ![Speicher](./media/site-recovery-vmm-to-azure/compatible-storage.png)

3. Falls Sie noch kein Speicherkonto erstellt haben und dies unter Verwendung von Resource Manager nachholen möchten, können Sie auf **+Speicherkonto** klicken und diesen Schritt direkt ausführen.  Geben Sie auf dem Blatt **Speicherkonto erstellen** einen Kontonamen, einen Typ, ein Abonnement und einen Standort an. Das Konto sollte sich an demselben Standort wie der Recovery Services-Tresor befinden.

   ![Speicher](./media/site-recovery-vmm-to-azure/gs-createstorage.png)


   * Wenn Sie ein Speicherkonto mit dem klassischen Modell erstellen möchten, verwenden Sie das Azure-Portal. [Weitere Informationen](../storage/storage-create-storage-account-classic-portal.md)
   * Wenn Sie ein Storage Premium-Konto für replizierte Daten verwenden, müssen Sie ein weiteres Standardspeicherkonto zum Speichern von Replikationsprotokollen einrichten, mit denen laufende Änderungen lokaler Daten erfasst werden.
5. Falls Sie noch kein Azure-Netzwerk erstellt haben und dies unter Verwendung von Resource Manager nachholen möchten, können Sie auf **+Netzwerk** klicken und diesen Schritt direkt ausführen. Geben Sie auf dem Blatt **Virtuelles Netzwerk erstellen** einen Netzwerknamen, einen Adressbereich, Subnetzdetails, ein Abonnement und einen Standort an. Das Netzwerk sollte sich an demselben Standort wie der Recovery Services-Tresor befinden.

   ![Netzwerk](./media/site-recovery-vmm-to-azure/gs-createnetwork.png)

   Falls Sie ein Netzwerk mit dem klassischen Modell erstellen möchten, verwenden Sie hierfür das Azure-Portal. [detaillierte Kapazitätsplanung](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)

### <a name="configure-network-mapping"></a>Konfigurieren der Netzwerkzuordnung

* [kurze Übersicht](#prepare-for-network-mapping) über die Abläufe bei der Netzwerkzuordnung durch.
* Vergewissern Sie sich, dass virtuelle Computer auf dem VMM-Server über eine Verbindung mit einem VM-Netzwerk verfügen und dass Sie mindestens ein virtuelles Azure-Netzwerk erstellt haben. Einem einzelnen Azure-Netzwerk können mehrere VM-Netzwerke zugeordnet werden.

Konfigurieren Sie die Zuordnung wie folgt:

1. Klicken Sie unter **Site Recovery-Infrastruktur** > **Netzwerkzuordnungen** > **Netzwerkzuordnung** auf das Symbol **+Netzwerkzuordnung**.

    ![Netzwerkzuordnung](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. Wählen Sie unter **Netzwerkzuordnung hinzufügen** den VMM-Quellserver und **Azure** als Ziel aus.
3. Überprüfen Sie das Abonnement und das Bereitstellungsmodell nach einem Failover.
4. Wählen Sie unter **Quellnetzwerk**das lokale VM-Quellnetzwerk aus, das Sie über die Liste des VMM-Servers zuordnen möchten.
5. Wählen Sie unter **Zielnetzwerk**das Azure-Netzwerk aus, in dem Replikate von Azure-VMs nach der Erstellung angeordnet werden. Klicken Sie dann auf **OK**.

    ![Netzwerkzuordnung](./media/site-recovery-vmm-to-azure/network-mapping2.png)

Wenn die Netzwerkzuordnung beginnt, passiert Folgendes:

* Vorhandene VMs im VM-Quellnetzwerk werden mit dem Zielnetzwerk verbunden, wenn die Zuordnung beginnt. Neue VMs, die mit dem VM-Quellnetzwerk verbunden sind, werden mit dem zugeordneten Azure-Netzwerk verbunden, wenn die Replikation durchgeführt wird.
* Wenn Sie eine vorhandene Netzwerkzuordnung ändern, verwenden virtuelle Replikatcomputer bei der Verbindungsherstellung die neuen Einstellungen.
* Fall das Zielnetzwerk mehrere Subnetze enthält und eines dieser Subnetze den gleichen Namen besitzt wie das Subnetz des virtuellen Quellcomputers, stellt der virtuelle Replikatcomputer nach dem Failover eine Verbindung mit diesem Zielsubnetz her.
* Ist kein Zielsubnetz mit einem übereinstimmenden Namen vorhanden, stellt der virtuelle Computer eine Verbindung mit dem ersten Subnetz im Netzwerk her.

## <a name="configure-replication-settings"></a>Konfigurieren der Replikationseinstellungen
1. Klicken Sie zum Erstellen einer neuen Replikationsrichtlinie auf **Infrastruktur vorbereiten** > **Replikationseinstellungen** > **+Erstellen und zuordnen**.

    ![Netzwerk](./media/site-recovery-vmm-to-azure/gs-replication.png)
2. Geben Sie unter **Richtlinie erstellen und zuordnen**einen Richtliniennamen an.
3. Geben Sie unter **Kopierhäufigkeit**an, wie oft Sie Deltadaten nach der ersten Replikation replizieren möchten (alle 30 Sekunden, nach 5 Minuten oder nach 15 Minuten).

    > [!NOTE]
    >  Eine Häufigkeit von 30 Sekunden wird bei der Replikation nach Storage Premium nicht unterstützt. Die Einschränkung richtet sich nach der Anzahl von Momentaufnahmen pro Blob (100), die von Storage Premium unterstützt wird. [Weitere Informationen](../storage/storage-premium-storage.md#snapshots-and-copy-blob)

4. Geben Sie unter **Aufbewahrungszeitraum des Wiederherstellungspunkts**das Aufbewahrungszeitfenster für die einzelnen Wiederherstellungspunkte in Stunden an. Geschützte Computer können innerhalb eines Zeitfensters an einem beliebigen Punkt wiederhergestellt werden.
5. Geben Sie unter **App-konsistente Momentaufnahmehäufigkeit**an, wie häufig (1 bis 12 Stunden) Wiederherstellungspunkte erstellt werden sollen, die anwendungskonsistente Momentaufnahmen enthalten. Hyper-V verwendet zwei Momentaufnahmen: eine Standard-Momentaufnahme, die eine inkrementelle Momentaufnahme des gesamten virtuellen Computers bereitstellt, und eine anwendungskonsistente Momentaufnahme, die eine Zeitpunkt-Momentaufnahme der Anwendungsdaten innerhalb des virtuellen Computers erfasst. Anwendungskonsistente Momentaufnahmen verwenden den Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS), um sicherzustellen, dass Anwendungen sich bei der Erstellung der Momentaufnahme in einem konsistenten Zustand befinden. Beachten Sie, dass die Leistung von Anwendungen auf virtuellen Quellcomputern durch die Aktivierung anwendungskonsistenter Momentaufnahmen beeinträchtigt wird. Stellen Sie sicher, dass der festgelegte Wert kleiner als die konfigurierte Anzahl der zusätzlichen Wiederherstellungspunkte ist.
6. Geben Sie unter **Startzeit der ersten Replikation**an, wann die erste Replikation starten soll. Da die Replikation über Ihre Internetbandbreite durchgeführt wird, ist es ratsam, sie außerhalb der Zeiten mit der höchsten Arbeitsbelastung einzuplanen.
7. Geben Sie unter **In Azure gespeicherte Daten verschlüsseln**an, ob ruhende Daten im Azure-Speicher verschlüsselt werden sollen. Klicken Sie dann auf **OK**.

    ![Replikationsrichtlinie](./media/site-recovery-vmm-to-azure/gs-replication2.png)
8. Wenn Sie eine neue Richtlinie erstellen, wird sie der VMM-Cloud automatisch zugeordnet. Klicken Sie auf **OK**. Sie können dieser Replikationsrichtlinie unter **Replikation** > <Richtlinienname> > **VMM-Cloud zuordnen** zusätzliche VMM-Clouds (und die darin enthaltenen virtuellen Computer) zuordnen.

    ![Replikationsrichtlinie](./media/site-recovery-vmm-to-azure/policy-associate.png)

## <a name="capacity-planning"></a>Kapazitätsplanung

Nachdem Sie nun Ihre grundlegende Infrastruktur eingerichtet haben, können Sie sich mit der Kapazitätsplanung beschäftigen und ermitteln, ob Sie zusätzliche Ressourcen benötigen.

Site Recovery verfügt über einen Kapazitätsplaner, der Sie dabei unterstützt, die richtigen Ressourcen für die Quellumgebung, die Site Recovery-Komponenten, das Netzwerk und den Speicher zuzuordnen. Sie können den Planer im Schnellmodus für Schätzungen, die auf einer durchschnittlichen Anzahl von VMs, Datenträgern und Speicher basieren, oder im ausführlichen Modus, in dem Sie Zahlen auf Workloadebene eingeben, ausführen. Vorbereitung:

* Sammeln Sie Informationen zu Ihrer Replikationsumgebung, z.B. VMs, Datenträger pro VM und Speicher pro Datenträger.
* Schätzen Sie die tägliche Änderungsrate für replizierte Daten. Zur Unterstützung können Sie den [Capacity Planner für Hyper-V-Replikat](https://www.microsoft.com/download/details.aspx?id=39057) verwenden.

1. Klicken Sie auf **Herunterladen**, um das Tool herunterzuladen, und führen Sie es anschließend aus. [entsprechenden Artikel](site-recovery-capacity-planner.md) durch.
2. Wählen Sie anschließend unter **Haben Sie den Capacity Planner ausgeführt?** die Option **Ja** aus.

   ![Kapazitätsplanung](./media/site-recovery-vmm-to-azure/gs-capacity-planning.png)

   Erfahren Sie mehr über das [Steuern der Netzwerkbandbreite](#network-bandwidth-considerations).




## <a name="enable-replication"></a>Replikation aktivieren

Bevor Sie starten, stellen Sie sicher, dass Ihr Azure-Benutzerkonto die erforderlichen [Berechtigungen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) zum Aktivieren der Replikation eines neuen virtuellen Computers in Azure besitzt.

Aktivieren Sie die Replikation jetzt wie folgt:

1. Klicken Sie auf **Schritt 2: Replizieren Sie die Anwendung** > **Quelle**. Klicken Sie nach der erstmaligen Aktivierung der Replikation im Tresor auf **+Replizieren**, um die Replikation für weitere Computer zu aktivieren.

    ![Replikation aktivieren](./media/site-recovery-vmm-to-azure/enable-replication1.png)
2. Wählen Sie auf dem Blatt **Quelle** den VMM-Server und die Cloud aus, in der sich die Hyper-V-Hosts befinden. Klicken Sie dann auf **OK**.

    ![Replikation aktivieren](./media/site-recovery-vmm-to-azure/enable-replication-source.png)
3. Wählen Sie unter **Ziel** das Abonnement, das Bereitstellungsmodell für die Zeit nach dem Failover und das Speicherkonto für die replizierten Daten aus.

    ![Replikation aktivieren](./media/site-recovery-vmm-to-azure/enable-replication-target.png)
4. Wählen Sie das Speicherkonto aus, das Sie verwenden möchten. Falls Sie keines der bereits vorhandenen Speicherkonten verwenden möchten, können Sie ein [Speicherkonto erstellen](#set-up-an-azure-storage-account). Wenn Sie ein Storage Premium-Konto für replizierte Daten verwenden, müssen Sie ein weiteres Standardspeicherkonto zum Speichern von Replikationsprotokollen einrichten, mit denen laufende Änderungen lokaler Daten erfasst werden. Um mit dem Resource Manager-Modell ein Speicherkonto zu erstellen, klicken Sie auf **Neu erstellen**. Wenn Sie ein Speicherkonto mit dem klassischen Modell erstellen möchten, verwenden Sie das [Azure-Portal](../storage/storage-create-storage-account-classic-portal.md). Klicken Sie dann auf **OK**.
5. Wählen Sie das Azure-Netzwerk und das Subnetz aus, mit dem virtuelle Azure-Computer, die nach einem Failover erstellt werden, eine Verbindung herstellen. Wählen Sie die Option **Jetzt für die ausgewählten Computer konfigurieren** aus, um die Netzwerkeinstellung auf alle Computer anzuwenden, die geschützt werden sollen. Wählen Sie **Später konfigurieren** aus, um das Azure-Netzwerk pro Computer auszuwählen. Falls Sie keines der bereits vorhandenen Netzwerke verwenden möchten, können Sie [ein Netzwerk erstellen](#set-up-an-azure-network). Klicken Sie zum Erstellen eines Netzwerks mit dem Resource Manager-Modell auf **Neu erstellen**. Falls Sie ein Netzwerk mit dem klassischen Modell erstellen möchten, verwenden Sie hierfür das [Azure-Portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Wählen Sie, falls zutreffend, ein Subnetz aus. Klicken Sie dann auf **OK**.
6. Klicken Sie auf **Virtuelle Computer** > **Virtuelle Computer auswählen**, und wählen Sie die Computer aus, die Sie replizieren möchten. Sie können nur Computer auswählen, für die die Replikation aktiviert werden kann. Klicken Sie dann auf **OK**.

    ![Replikation aktivieren](./media/site-recovery-vmm-to-azure/enable-replication5.png)

7. Geben Sie unter **Eigenschaften** > **Eigenschaften konfigurieren**das Betriebssystem für die ausgewählten VMs und den Betriebssystem-Datenträger aus.

    - Stellen Sie sicher, dass der Name des virtuellen Azure-Computers (Zielname) den [Anforderungen für virtuelle Azure-Computer](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) entspricht.   
    - Standardmäßig werden alle Datenträger des virtuellen Computers für die Replikation ausgewählt, doch Sie können Datenträger löschen, um sie auszuschließen.

        - Möglicherweise möchten Sie Datenträger ausschließen, um die Replikationsbandbreite zu verringern. Beispielsweise möchten Sie vielleicht nicht, dass Datenträger mit temporären Daten oder Daten, die bei jedem Neustart eines Computers oder einer App aktualisiert werden (etwa „pagefile.sys“ oder Microsoft SQL Server tempdb), repliziert werden. Durch Aufheben der Auswahl eines Datenträgers können Sie ihn von der Replikation ausschließen.
        - Nur Basisdatenträger können ausgeschlossen werden. Betriebssystemdatenträger können Sie nicht ausschließen.
        - Es wird empfohlen, keine dynamischen Datenträger auszuschließen. Site Recovery kann nicht ermitteln, ob eine virtuelle Festplatte in einer Gast-VM einfach oder dynamisch ist. Wenn keiner der abhängigen dynamischen Volumendatenträger ausgeschlossen wird, werden geschützte dynamische Datenträger bei einem VM-Failover als fehlerhaft angesehen, und auf die Daten des Datenträgers kann nicht zugegriffen werden.
        - Nach Aktivierung der Replikation können Sie keine Datenträger für die Replikation hinzufügen oder entfernen. Wenn Sie einen Datenträger hinzufügen oder entfernen möchten, müssen Sie den Schutz für den virtuellen Computer deaktivieren und anschließend wieder aktivieren.
        - Für Datenträger, die Sie manuell in Azure erstellen, wird kein Failback durchgeführt. Wenn Sie also beispielsweise ein Failover für drei Datenträger durchführen und zwei Datenträger direkt auf dem virtuellen Azure-Computer erstellen, wird nur für die drei Datenträger, für die das Failover ausgeführt wurde, ein Failback von Azure zu Hyper-V durchgeführt. Manuell erstellte Datenträger können nicht in das Failback oder in die umgekehrte Replikation von Hyper-V zu Azure einbezogen werden.
        - Wenn Sie einen Datenträger ausschließen, der für den Betrieb einer Anwendung erforderlich ist, müssen Sie ihn nach dem Failover zu Azure manuell in Azure erstellen, damit die replizierte Anwendung ausgeführt werden kann. Alternativ können Sie Azure Automation in einen Wiederherstellungsplan integrieren, um den Datenträger während des Failovers des Computers zu erstellen.

    Klicken Sie zum Speichern der Änderungen auf **OK**. Sie können später weitere Eigenschaften festlegen.

    ![Replikation aktivieren](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

8. Wählen Sie unter **Replikationseinstellungen** > **Replikationseinstellungen konfigurieren** die Replikationsrichtlinie aus, die Sie für die geschützten VMs anwenden möchten. Klicken Sie dann auf **OK**. Sie können die Replikationsrichtlinie unter **Replikationsrichtlinien** > <Richtlinienname> > **Einstellungen bearbeiten** ändern. Von Ihnen vorgenommene Änderungen werden für Computer, die bereits repliziert werden, und für neue Computer verwendet.

   ![Replikation aktivieren](./media/site-recovery-vmm-to-azure/enable-replication7.png)

Sie können den Fortschritt des Auftrags **Schutz aktivieren** unter **Aufträge** > **Site Recovery-Aufträge** verfolgen. Nachdem der Auftrag **Schutz abschließen** ausgeführt wurde, ist der Computer bereit für das Failover.

### <a name="view-and-manage-vm-properties"></a>Anzeigen und Verwalten von VM-Eigenschaften

Es wird empfohlen, dass Sie die Eigenschaften des Quellcomputers überprüfen. Beachten Sie, dass der Name des virtuellen Azure-Computers die [Anforderungen für virtuelle Azure-Computer](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)erfüllen muss.

1. Klicken Sie unter **Geschützte Elemente** auf **Replizierte Elemente**, und wählen Sie den Computer aus, um die Details dazu anzuzeigen.

    ![Replikation aktivieren](./media/site-recovery-vmm-to-azure/vm-essentials.png)
2. Unter **Eigenschaften** können Sie die Informationen zur Replikation und zum Failover für den virtuellen Computer anzeigen.

    ![Replikation aktivieren](./media/site-recovery-vmm-to-azure/test-failover2.png)
3. Unter **Compute und Netzwerk** > **Compute-Eigenschaften** können Sie den Namen und die Zielgröße des virtuellen Azure-Computers angeben. Ändern Sie ggf. den Namen, damit er die [Azure-Anforderungen](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) erfüllt. Sie können auch Informationen zum Zielnetzwerk, zum Subnetz sowie zur IP-Adresse anzeigen und ändern, die dem virtuellen Azure-Computer zugewiesen wird.
Beachten Sie Folgendes:

   * Sie können die Ziel-IP-Adresse festlegen. Wenn Sie keine Adresse angeben, wird für den Computer, für den das Failover durchgeführt wurde, DHCP verwendet. Wenn Sie eine Adresse festlegen, die beim Failover nicht verfügbar ist, tritt beim Failover ein Fehler auf. Dieselbe Ziel-IP-Adresse kann für das Testfailover verwendet werden, wenn die Adresse im Testfailover-Netzwerk verfügbar ist.
   * Die Anzahl der Netzwerkkarten hängt von der Größe ab, die Sie für den virtuellen Zielcomputer angeben. Hierbei gilt Folgendes:

     * Wenn die Anzahl der Netzwerkkarten des Quellcomputers maximal der Anzahl der Netzwerkkarten entspricht, die für die Größe des Zielcomputers zulässig ist, hat der Zielcomputer die gleiche Anzahl von Netzwerkkarten wie der Quellcomputer.
     * Wenn die Anzahl von Netzwerkadaptern für den virtuellen Quellcomputer die maximal zulässige Anzahl für die Größe des Zielcomputers übersteigt, wird die Anzahl verwendet, die maximal für die Größe des Zielcomputers zulässig ist.
     * Ein Beispiel: Wenn ein Quellcomputer zwei Netzwerkkarten besitzt und der Zielcomputer aufgrund seiner Größe vier Netzwerkkarten unterstützt, erhält der Zielcomputer zwei Netzwerkkarten. Wenn der Quellcomputer dagegen zwei Netzwerkadapter besitzt und der Zielcomputer aufgrund seiner Größe nur einen Adapter unterstützt, erhält der Zielcomputer nur einen Adapter.     
     * Wenn der virtuelle Computer über mehrere Netzwerkkarten verfügt, werden alle mit dem gleichen Netzwerk verbunden.

     ![Replikation aktivieren](./media/site-recovery-vmm-to-azure/test-failover4.png)

4. Unter **Datenträger** werden das Betriebssystem und die Datenträger auf der VM angezeigt, die repliziert wird.

#### <a name="managed-disks"></a>Verwaltete Datenträger

Unter **Compute und Netzwerk** > **Compute-Eigenschaften** können Sie die Einstellung „Verwaltete Datenträger verwenden“ für den virtuellen Computer auf „Ja“ festlegen, wenn Sie Ihrem Computer bei der Migration zu Azure verwaltete Datenträger anfügen möchten. Managed Disks vereinfacht die Datenträgerverwaltung für Azure-IaaS-VMs durch die Verwaltung der Speicherkonten, die den VM-Datenträgern zugeordnet sind. [Weitere Informationen zu Managed Disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - Verwaltete Datenträger werden erstellt und nur beim Failover zu Azure an den virtuellen Computer angefügt. Beim Aktivieren des Schutzes werden Daten von lokalen Computern weiterhin auf Speicherkonten repliziert.
   Verwaltete Datenträger können nur für virtuelle Computer erstellt werden, die über das Resource Manager-Bereitstellungsmodell bereitgestellt werden.  

  > [!NOTE]
  > Ein Failback von Azure zur lokalen Hyper-V-Umgebung wird für Computer mit verwalteten Datenträgern derzeit nicht unterstützt. Legen Sie „Verwaltete Datenträger verwenden“ nur dann auf „Ja“ fest, wenn Sie beabsichtigen, diesen Computer zu Azure zu migrieren.

   - Wenn Sie „Verwaltete Datenträger verwenden“ auf „Ja“ festlegen, stehen nur Verfügbarkeitsgruppen in der Ressourcengruppe zur Auswahl, bei denen „Verwaltete Datenträger verwenden“ auf „Ja“ festgelegt ist. Der Grund hierfür ist, dass virtuelle Computer mit verwalteten Datenträgern nur in Verfügbarkeitsgruppen enthalten sein können, deren Eigenschaft „Verwaltete Datenträger verwenden“ auf „Ja“ festgelegt ist. Stellen Sie sicher, dass die Eigenschaft „Verwaltete Datenträgern verwenden“ der erstellten Verfügbarkeitsgruppen Ihrer Absicht entspricht, verwaltete Datenträger beim Failover zu verwenden.  In gleicher Weise gilt: Wenn Sie „Verwaltete Datenträger verwenden“ auf „Nein“ festlegen, stehen nur Verfügbarkeitsgruppen in der Ressourcengruppe zur Auswahl, deren Eigenschaft „Verwaltete Datenträger verwenden“ auf „Nein“ festgelegt ist. [Weitere Informationen zu verwalteten Datenträgern und Verfügbarkeitsgruppen](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Wenn das für die Replikation verwendete Speicherkonto zu einem beliebigen Zeitpunkt mit der Speicherdienstverschlüsselung verschlüsselt wurde, tritt bei der Erstellung verwalteter Datenträger während des Failovers ein Fehler auf. Sie können entweder „Verwaltete Datenträger verwenden“ auf „Nein“ festlegen und den Failoverversuch wiederholen oder den Schutz für den virtuellen Computer deaktivieren und diesen in einem Speicherkonto schützen, für das die Speicherdienstverschlüsselung zu keinem Zeitpunkt aktiviert war.
  > [Weitere Informationen zu Speicherdienstverschlüsselung und verwalteten Datenträgern](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-the-deployment"></a>Testen der Bereitstellung

Zum Testen der Bereitstellung können Sie ein Testfailover für einen einzelnen virtuellen Computer durchführen. Alternativ können Sie einen Wiederherstellungsplan erstellen, der mehrere virtuelle Computer enthält.

### <a name="before-you-start"></a>Vorbereitung

 - Wenn Sie die Verbindung mit Azure-VMs nach dem Failover per RDP herstellen möchten, informieren Sie sich über die [Vorbereitung auf das Herstellen der Verbindung](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - Für den vollständigen Test müssen Sie Active Directory und DNS in Ihre Testumgebung kopieren. [Weitere Informationen](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>Durchführen eines Test-Failovers

1. Klicken Sie zum Ausführen eines Failovers für einen einzelnen virtuellen Computer unter **Replizierte Elemente** auf den virtuellen Computer und anschließend auf **+Testfailover**.
2. Klicken Sie zum Ausführen eines Failovers für einen Wiederherstellungsplan unter **Wiederherstellungspläne** mit der rechten Maustaste auf den Plan, und klicken Sie anschließend auf **Testfailover**. Eine Anleitung zum Erstellen eines Wiederherstellungsplans finden Sie [hier](site-recovery-create-recovery-plans.md).
3. Wählen Sie unter **Testfailover** das Azure-Netzwerk aus, mit dem virtuelle Azure-Computer nach dem Failover eine Verbindung herstellen.
4. Klicken Sie auf **OK**, um den Failovervorgang zu starten. Sie können den Status verfolgen, indem Sie auf den virtuellen Computer klicken, um die Eigenschaften zu öffnen. Alternativ können Sie unter **Site Recovery-Aufträge** auf den Auftrag **Testfailover** klicken.
5. Nach Abschluss des Failovers sollte der Azure-Replikatcomputer im Azure-Portal unter **Virtuelle Computer** angezeigt werden. Vergewissern Sie sich, dass der virtuelle Computer die richtige Größe hat, mit dem richtigen Netzwerk verbunden ist und ausgeführt wird.
6. Wenn Sie die Vorbereitung für Verbindungen nach dem Failover durchgeführt haben, sollten Sie eine Verbindung mit dem virtuellen Azure-Computer herstellen können.
7. Klicken Sie anschließend auf dem Wiederherstellungsplan auf **Cleanup-Test-Failover** (Testfailover bereinigen). Erfassen und speichern Sie unter **Notizen** alle Beobachtungen im Zusammenhang mit dem Test-Failover. Dadurch werden die während des Testfailovers erstellten virtuellen Computer gelöscht.

Weitere Informationen finden Sie im Artikel [Testfailover in Azure](site-recovery-test-failover-to-azure.md).

## <a name="monitor-the-deployment"></a>Überwachen der Bereitstellung

Hier wird beschrieben, wie Sie die Konfigurationseinstellungen, den Status und die Integrität für die Site Recovery-Bereitstellung überwachen können:

1. Klicken Sie auf den Tresornamen, um auf das Dashboard **Zusammenfassung** zuzugreifen. In diesem Dashboard werden Site Recovery-Aufträge, Replikationsstatus, Wiederherstellungspläne, Serverzustand und Ereignisse angezeigt.  Sie können die **Zusammenfassung** so anpassen, dass die nützlichsten Kacheln und Layouts angezeigt werden (einschließlich des Status anderer Site Recovery- und Backup-Tresore).

    ![Zusammenfassung](./media/site-recovery-vmm-to-azure/essentials.png)
2. Unter **Integrität** können Sie Probleme mit lokalen Servern (VMM- oder Konfigurationsserver) sowie die Ereignisse überwachen, die von Site Recovery in den letzten 24 Stunden ausgelöst wurden.
3. Über die Kacheln **Replizierte Elemente**, **Wiederherstellungspläne** und **Site Recovery-Aufträge** können Sie die Replikation verwalten und überwachen. Ausführlichere Informationen zu Aufträgen finden Sie unter **Aufträge** > **Site Recovery-Aufträge**.

## <a name="command-line-installation-for-the-azure-site-recovery-provider"></a>Befehlszeileninstallation für den Azure Site Recovery-Anbieter

Der Azure Site Recovery-Anbieter kann über die Befehlszeile installiert werden. Mit dieser Methode kann der Anbieter in Server Core für Windows Server 2012 R2 installiert werden.

1. Laden Sie die Installationsdatei und den Registrierungsschlüssel des Anbieters in einen Ordner herunter. Beispiel: C:\ASR.
2. Extrahieren Sie über eine Eingabeaufforderung mit erhöhten Rechten das Installationsprogramm des Anbieters, indem Sie diese Befehle ausführen:

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Führen Sie diesen Befehl aus, um die Komponenten zu installieren:

            C:\ASR> setupdr.exe /i
4. Führen Sie anschließend die folgenden Befehle aus, um den Server im Tresor zu registrieren:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of the server> /Credentials <path of the credentials file> /EncryptionEnabled <full file name to save the encryption certificate>       

Hierbei gilt:

* **/Credentials**: erforderlicher Parameter zum Angeben des Speicherorts der Registrierungsschlüsseldatei.  
* **/FriendlyName**: erforderlicher Parameter für den Namen des Hyper-V-Hostservers, der im Azure Site Recovery-Portal angezeigt wird.
* * **/EncryptionEnabled**: optionaler Parameter beim Replizieren von Hyper-V-VMs in VMM-Clouds in Azure. Geben Sie an, ob Sie virtuelle Computer in Azure verschlüsseln möchten (Verschlüsselung im ruhenden Zustand). Stellen Sie sicher, dass der Dateiname über die Erweiterung **.pfx** verfügt. Die Verschlüsselung ist standardmäßig deaktiviert.
* **/proxyAddress**: optionaler Parameter, der die Adresse des Proxyservers angibt.
* **/proxyport**: optionaler Parameter, der den Port des Proxyservers angibt.
* **/proxyUsername**: optionaler Parameter, der den Proxybenutzernamen angibt (sofern für den Proxy eine Authentifizierung erforderlich ist).
* **/proxyPassword**: optionaler Parameter, der das Kennwort für die Authentifizierung mit dem Proxyserver angibt (sofern für den Proxy eine Authentifizierung erforderlich ist).


### <a name="network-bandwidth-considerations"></a>Aspekte der Netzwerkbandbreite
Sie können den Capacity Planner verwenden, um die Bandbreite zu berechnen, die Sie für die Replikation benötigen (erste Replikation und dann Deltareplikation). Zur Steuerung der verwendeten Bandbreite für die Replikation stehen verschiedene Optionen zur Verfügung:

* **Bandbreite einschränken**: Hyper-V-Datenverkehr, der an einem sekundären Standort repliziert wird, verläuft über einen speziellen Hyper-V-Host. Sie können die Bandbreite auf dem Hostserver drosseln.
* **Bandbreite optimieren**: Sie können beeinflussen, wie viel Bandbreite für die Replikation verwendet wird, indem Sie einige Registrierungsschlüssel nutzen.

#### <a name="throttle-bandwidth"></a>Bandbreite einschränken
1. Öffnen Sie das Microsoft Azure Backup-MMC-Snap-In auf dem Hyper-V-Hostserver. Standardmäßig ist auf dem Desktop oder unter „C:\Programme\Microsoft Azure Recovery Services Agent\bin\wabadmin“ eine Verknüpfung für Microsoft Azure Backup verfügbar.
2. Klicken Sie im Snap-In auf **Eigenschaften ändern**.
3. Wählen Sie auf der Registerkarte **Drosselung** die Option **Internet-Bandbreiteneinschränkung für Sicherungsvorgänge aktivieren** aus, und legen Sie die Grenzwerte für Geschäftszeiten und arbeitsfreie Zeiten fest. Der gültige Bereich reicht von 512 KBit/s bis 102 MBit/s.

    ![Bandbreite drosseln](./media/site-recovery-vmm-to-azure/throttle2.png)

Sie können auch das Cmdlet [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) verwenden, um die Drosselung festzulegen. Hier ein Beispiel:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** gibt an, dass keine Drosselung erforderlich ist.

#### <a name="influence-network-bandwidth"></a>Netzwerkbandbreite beeinflussen
Mit dem Registrierungswert **UploadThreadsPerVM** wird die Anzahl von Threads gesteuert, die für die Datenübertragung (erste Replikation oder Deltareplikation) eines Datenträgers verwendet werden. Bei einem höheren Wert wird die Netzwerkbandbreite für die Replikation erhöht. Mit dem Registrierungswert **DownloadThreadsPerVM** wird die Anzahl von Threads angegeben, die während des Failbacks für die Datenübertragung verwendet werden.

1. Navigieren Sie in der Registrierung zu **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.

   * Ändern Sie den Wert **UploadThreadsPerVM** (oder erstellen Sie den Schlüssel, falls er nicht vorhanden ist), um die für die Datenträgerreplikation verwendeten Threads zu steuern.
   * Ändern Sie den Wert **DownloadThreadsPerVM** (oder erstellen Sie den Schlüssel, falls er nicht vorhanden ist), um die Threads zu steuern, die für den Failback-Datenverkehr von Azure verwendet werden.
2. Der Standardwert ist 4. In einem absichtlich mit großen Reserven ausgestatteten Netzwerk müssen die Standardwerte dieser Registrierungsschlüssel geändert werden. Der maximale Wert beträgt 32. Überwachen Sie den Datenverkehr, um den Wert zu optimieren.

## <a name="next-steps"></a>Nächste Schritte

Nach Abschluss der ersten Replikation, und wenn Sie die Bereitstellung getestet haben, können Sie bei Bedarf Failover auslösen. [Informieren Sie sich](site-recovery-failover.md) über die unterschiedlichen Failoverarten und deren Durchführung.

