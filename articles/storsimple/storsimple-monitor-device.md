---
title: "Überwachen des StorSimple-Geräts | Microsoft Docs"
description: "Beschreibt, wie Sie den StorSimple Manager-Dienst verwenden, um E/A-Leistung, Kapazitätsauslastung, Netzwerkdurchsatz und Geräteleistung zu überwachen."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: bd4f7704-4f6f-47d0-927a-b1c91eabc453
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/16/2016
ms.author: alkohli
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: d45bb37c8417785db0ea38be4375a998b6d9f109


---
# <a name="use-the-storsimple-manager-service-to-monitor-your-storsimple-device"></a>Verwenden des StorSimple Manager-Diensts zum Überwachen Ihres StorSimple-Geräts
## <a name="overview"></a>Übersicht
Sie können den StorSimple Manager-Dienst verwenden, um bestimmte Geräte innerhalb Ihrer StorSimple-Lösung zu überwachen. Sie können benutzerdefinierte Diagramme basierend auf Metriken zu EA-Leistung, Kapazitätsauslastung, Netzwerkdurchsatz und Geräteleistung erstellen. 

Um die Überwachungsinformationen für ein bestimmtes Gerät anzuzeigen, wählen Sie im klassischen Azure-Portal den StorSimple Manager-Dienst aus. Klicken Sie auf die Registerkarte **Überwachen** , und wählen Sie in der Geräteliste das gewünschte Gerät aus. Die Seite **Überwachen** enthält die folgenden Informationen.

## <a name="io-performance"></a>E/A-Leistung
**E/A-Leistung** verfolgt Metrikdaten nach, die in Zusammenhang mit Lese- und Schreibvorgängen zwischen den iSCSI-Initiatorschnittstellen auf dem Hostserver und dem Gerät oder dem Gerät und der Cloud stehen. Die Leistung kann für ein bestimmtes Volume, einen bestimmten Volumecontainer oder alle Volumecontainer gemessen werden.

Im Diagramm unten sind die E/A-Vorgänge für den Initiator Ihres Geräts für alle Volumes für ein Gerät in der Produktionsumgebung aufgeführt. Bei den dargestellten Metriken handelt es sich um gelesene und geschriebene Bytes pro Sekunde, Lese- und Schreib-E/A-Vorgänge pro Sekunde und um die Wartezeiten bei Lese- und Schreibzugriffen.

![EA-Leistung vom Initiator an das Gerät](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_InitiatorTODevice_For_AllVolumesM.png)

Für das gleiche Gerät sind die E/A-Vorgänge für die Daten vom Gerät zur Cloud für alle Volumecontainer dargestellt. Auf diesem Gerät befinden sich die Daten nur in der linearen Schicht, und nichts wurde in die Cloud ausgelagert. Es treten keine Lese-/Schreibvorgänge vom Gerät in die Cloud auf. Daher treten die Spitzen im Diagramm im Abstand von 5 Minuten auf, was der Häufigkeit entspricht, mit der das Taktsignal zwischen dem Gerät und dem Dienst überprüft wird. 

![EA-Leistung vom Gerät in die Cloud](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainersM.png)

Für das gleiche Gerät wurde beginnend um 14:00 Uhr eine Cloudmomentaufnahme für Volumedaten erstellt. Dies hat bewirkt, dass Daten vom Gerät in die Cloud übertragen wurden. Innerhalb dieses Zeitraums wurden Lese-/Schreibvorgänge für die Cloud bedient. Das EA-Diagramm zeigt in dem Zeitraum, in dem die Momentaufnahme erstellt wurde, eine Spitze in den verschiedenen Metrikdaten. 

![EA-Leistung vom Gerät in die Cloud nach einer Cloudmomentaufnahme](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainers2M.png)

## <a name="capacity-utilization"></a>Kapazitätsauslastung
**Kapazitätsauslastung** verfolgt Metrikdaten im Zusammenhang mit der Menge an Datenspeicherplatz nach, die von den Volumes, den Volumecontainern oder dem Gerät verwendet wird. Sie können Berichte zur Kapazitätsauslastung des primären Speichers, des Cloudspeichers oder des Gerätespeichers erstellen. Die Kapazitätsauslastung kann für ein bestimmtes Volume, einen bestimmten Volumecontainer oder alle Volumecontainer gemessen werden.

Die primäre, Cloud- und Gerätespeicherkapazität kann wie folgt beschrieben werden:

### <a name="primary-storage-capacity-utilization"></a>Kapazitätsauslastung des primären Speichers
In diesen Diagrammen ist die Datenmenge dargestellt, die auf StorSimple-Volumes geschrieben wird, bevor die Daten dedupliziert und komprimiert werden. Sie können die Auslastung des primären Speichers für alle Volumes oder ein einzelnes Volume anzeigen.

Wenn Sie die Diagramme mit der Volume-Kapazitätsauslastung des primären Speichers für alle Volumes und für einzelne Volumes anzeigen und in beiden Fällen die primären Daten addieren, kann es sein, dass die beiden Ergebnisse nicht übereinstimmen. Die Gesamtmenge der primären Daten auf allen Volumes stimmt unter Umständen nicht mit der Summe der primären Daten der einzelnen Volumes überein. Dies kann einen der folgenden Gründe haben:

* **Einbeziehung der Momentaufnahmedaten für alle Volumes**: Dieses Verhalten tritt nur auf, wenn Sie eine Version vor Update 3 ausführen. Die primären Daten, die für alle Volumes angezeigt werden, sind die Summe der primären Daten für jedes Volume und der Momentaufnahmedaten. Die primären Daten, die für ein bestimmtes Volume angezeigt werden, entsprechen nur der Datenmenge, die dem Volume zugeordnet ist (und enthalten nicht die entsprechenden Volume-Momentaufnahmedaten).
  
    Dies lässt sich auch anhand der folgenden Gleichung erläutern:
  
    *Primäre Daten (alle Volumes) = Summe von (Primäre Daten (Volume i) + Größe der Momentaufnahmedaten (Volume i))*
  
    *Hierbei gilt Folgendes: Primäre Daten (Volume i) = Größe der primären Daten, die Volume i zugeordnet sind.*
  
    Wenn die Momentaufnahmen über den Dienst gelöscht werden, wird der Löschvorgang asynchron im Hintergrund durchgeführt. Es kann einige Zeit dauern, bis die Volumedatengröße nach dem Löschen der Momentaufnahmen aktualisiert wird. 
  
    Wenn Update 3 oder höher ausgeführt wird, sind die Momentaufnahmedaten nicht in den Volumedaten enthalten. Und die primäre Auslastung wird wie folgt berechnet:
  
    *Primäre Daten (alle Volumes) = Summe von (Primäre Daten (Volume i))
  
    *Hierbei gilt Folgendes: Primäre Daten (Volume i) = Größe der primären Daten, die Volume i zugeordnet sind.*
* **Volumes mit deaktivierter Überwachung in allen Volumes**: Wenn Sie auf Ihrem Gerät Volumes haben, für die die Überwachung deaktiviert ist, sind die Überwachungsdaten für diese einzelnen Volumes in den Diagrammen nicht verfügbar. In den Daten für alle Volumes im Diagramm sind jedoch die Volumes enthalten, für die die Überwachung deaktiviert ist. 
* **Gelöschte Volumes mit vorhandenen zugeordneten Backups für alle Volumes**: Wenn Volumes mit Momentaufnahmedaten gelöscht werden, die zugeordneten Momentaufnahmen aber noch vorhanden sind, stimmen die Werte unter Umständen nicht überein.
* **Gelöschte Volumes für alle Volumes**: In einigen Fällen sind alte Volumes unter Umständen auch dann noch vorhanden, wenn sie gelöscht wurden. Die Auswirkung des Löschvorgangs wird nicht angezeigt, und für das Gerät wird ggf. eine geringere verfügbare Kapazität angegeben. Sie müssen den Microsoft-Support bitten, diese Volumes zu entfernen.

Die folgenden Diagramme stellen die Kapazitätsauslastung des Primärspeichers eines StorSimple-Geräts vor und nach dem Erstellen einer Cloudmomentaufnahme dar. Da es sich nur um Volumedaten handelt, sollte eine Cloudmomentaufnahme keine Auswirkungen auf den Primärspeicher haben. Wie Sie sehen, zeigt das Diagramm als Ergebnis der Erstellung der Cloudmomentaufnahme keinen Unterschied in der Kapazitätsauslastung des Primärspeichers. Die Erstellung der Cloudmomentaufnahme wurde auf dem betreffenden Gerät um 14:00 Uhr gestartet.

![Kapazitätsauslastung des Primärspeichers vor einer Cloudmomentaufnahme](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes2M.png)

![Kapazitätsauslastung des Primärspeichers nach einer Cloudmomentaufnahme](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes1M.png)

Wenn Sie Update 2 oder höher ausführen, können Sie die Kapazitätsauslastung des Primärspeichers für einzelnes Volumes, für alle Volumes, für alle mehrstufigen Volumes und alle lokalen Volumes aufgeschlüsselt anzeigen (siehe folgende Abbildung). Durch eine Aufschlüsselung nach allen lokalen Volumes können Sie schnell feststellen, wie viel Speicherplatz auf der lokalen Ebene belegt ist.

![Kapazitätsauslastung des Primärspeichers für alle lokalen Volumes](./media/storsimple-monitor-device/localvolumes.png)

### <a name="cloud-storage-capacity-utilization"></a>Kapazitätsauslastung des Cloudspeichers
In diesen Diagrammen ist die Menge des verwendeten Cloudspeichers dargestellt. Diese Daten sind dedupliziert und komprimiert. Diese Datenmenge umfasst Cloudmomentaufnahmen, die möglicherweise Daten enthalten, die in keinem Primärvolume reflektiert und aus Gründen der Legacy oder im Rahmen einer vorgeschriebenen Aufbewahrung gespeichert werden. Sie können die Auslastungszahlen des Primär- und Cloudspeichers vergleichen, um einen Eindruck der Datenreduzierungsrate zu erhalten, wenngleich das Ergebnis des Vergleichs nicht ganz exakt ist. Die folgenden Diagramme stellen die Kapazitätsauslastung des Cloudspeichers eines StorSimple-Geräts vor und nach dem Erstellen einer Cloudmomentaufnahme dar. Die Cloudmomentaufnahme wurde auf dem betreffenden Gerät ungefähr um 14:00 Uhr gestartet, und Sie können sehen, dass die Kapazitätsauslastung des Cloudspeichers um diese Zeit in die Höhe schnellte und von 5,73 MB auf 4,04 GB anstieg.

![Kapazitätsauslastung des Cloudspeichers vor einer Cloudmomentaufnahme](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers2M.png)

![Kapazitätsauslastung des Cloudspeichers nach einer Cloudmomentaufnahme](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers1M.png)

### <a name="device-storage-capacity-utilization"></a>Kapazitätsauslastung des Gerätespeichers
In diesen Diagrammen ist die Gesamtauslastung des Geräts dargestellt. Diese Zahl ist höher als die Auslastung des primären Speichers, da sie auch die lineare SSD-Schicht umfasst. Diese Schicht enthält eine Menge an Daten, die auch auf den anderen Schichten des Geräts vorhanden ist. Die Kapazität der linearen SSD-Schicht ist zyklisch angelegt, d.h. wenn neue Daten eintreffen, werden die alten Daten in die HDD-Schicht (und zu diesem Zeitpunkt dedupliziert und komprimiert) und anschließend in die Cloud verschoben.

Im Lauf der Zeit wird sich die Kapazitätsauslastung des Primärspeichers und des Geräts wahrscheinlich parallel erhöhen, bis die ersten Daten in die Cloud verschoben werden. Zu diesem Zeitpunkt wird die Kapazitätsauslastung des Geräts vermutlich auf dem gleichen Niveau bleiben, die Kapazitätsauslastung des Primärspeichers wird sich jedoch erhöhen, da mehr Daten geschrieben werden.

Die folgenden Diagramme stellen die Kapazitätsauslastung des Primärspeichers eines StorSimple-Geräts vor und nach dem Erstellen einer Cloudmomentaufnahme dar. Die Cloudmomentaufnahme begann um 14:00 Uhr, und die Kapazitätsauslastung des Gerätespeichers begann um diese Zeit, abzunehmen. Die Kapazitätsauslastung des Gerätespeichers fiel von 11,58 GB auf 7,48 GB. Dies weist darauf hin, dass die unkomprimierten Daten in der linearen SSD-Schicht höchst wahrscheinlich dedupliziert, komprimiert und in die HDD-Schicht verschoben wurden. Beachten Sie, dass dieses Abfallen möglicherweise nicht zu beobachten ist, wenn das Gerät sowohl in der SSD- als auch in der HDD-Schicht bereits eine große Menge Daten aufweist. In diesem Beispiel hat das Gerät eine kleine Datenmenge.

![Kapazitätsauslastung des Gerätespeichers vor einer Cloudmomentaufnahme](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil2M.png)

![Kapazitätsauslastung des Gerätespeichers nach einer Cloudmomentaufnahme](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil1M.png)

## <a name="network-throughput"></a>Netzwerkdurchsatz
**Netzwerkdurchsatz** verfolgt Metrikdaten im Zusammenhang mit der Menge an Daten nach, die von den Netzwerkschnittstellen des iSCSI-Initiators auf dem Hostserver und dem Gerät sowie zwischen Gerät und Cloud übertragen werden. Sie können diese Metrikdaten für jede iSCSI-Netzwerkschnittstelle Ihres Geräts überwachen.

Die folgenden Diagramme stellen den Netzwerkdurchsatz für „Data 0“ und „Data 4“ dar. Bei beiden handelt es sich um 1 GbE-Netzwerkschnittstellen auf dem Gerät. In diesem Fall war „Data 0“ cloudfähig, während „Data 4“ iSCSI-fähig war. Sowohl der eingehende als auch der ausgehende Datenverkehr des StorSimple-Geräts ist dargestellt. Die flache Linie im Diagramm, die um 15:24 Uhr beginnt, ist auf die Tatsache zurückzuführen, dass Daten nur alle 5 Minuten erfasst werden, weshalb sie ignoriert werden kann. 

![Netzwerkdurchsatz für Data4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data0M.png)

![Netzwerkdurchsatz für Data4](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data4M.png)

## <a name="device-performance"></a>Geräteleistung
**Geräteleistung** verfolgt Metrikdaten zur Leistung des Geräts nach. Das folgende Diagramm zeigt die Statistik der CPU-Auslastung für ein Gerät in einer Produktionsumgebung.

![CPU-Auslastung des Geräts](./media/storsimple-monitor-device/StorSimple_DeviceMonitor_DevicePerformance1M.png)

## <a name="next-steps"></a>Nächste Schritte
* Informationen zur [Verwendung des StorSimple Manager-Dienstdashboards für Geräte](storsimple-device-dashboard.md).
* Erfahren Sie, wie Sie [Ihr StorSimple-Gerät mithilfe des StorSimple Manager-Diensts verwalten](storsimple-manager-service-administration.md).




<!--HONumber=Nov16_HO3-->


