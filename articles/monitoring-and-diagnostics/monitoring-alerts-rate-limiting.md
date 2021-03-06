---
title: "Ratenlimits für SMS, E-Mail-Nachrichten und Webhooks | Microsoft-Dokumentation"
description: "Lassen Sie sich per SMS, Webhook und E-Mail benachrichtigen, wenn bestimmte Ereignisse im Aktivitätsprotokoll eintreten."
author: anirudhcavale
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.translationtype: Human Translation
ms.sourcegitcommit: 64bd7f356673b385581c8060b17cba721d0cf8e3
ms.openlocfilehash: 1b4196d3b1d41458c7dd20b6986cc09100ae318c
ms.contentlocale: de-de
ms.lasthandoff: 05/02/2017


---

# <a name="rate-limiting-for-sms-emails-and-webhooks"></a>Ratenlimits für SMS, E-Mail-Nachrichten und Webhooks
Das Ratenlimit führt zu einer Unterbrechung der Benachrichtigungen, wenn zu viele Benachrichtigungen an eine bestimmte Telefonnummer oder E-Mail-Adresse gesendet werden. Das Limit stellt sicher, dass die Kommunikation zu Aktivitätsprotokollwarnungen und Dienstintegritätswarnungen überschaubar und sinnvoll bleibt.

Die Regeln sind für SMS und E-Mail identisch. Folgende Ratenlimits gelten:
 - SMS: 10 Nachrichten pro Stunde
 - E-Mail: 100 Nachrichten pro Stunde

## <a name="rate-limit-rules"></a>Regeln für Ratenlimits
- Für eine bestimmte Telefonnummer oder E-Mail-Adresse wird die Rate begrenzt, wenn sie mehr als den Schwellenwert an Nachrichten erhält.
- Eine Telefonnummer oder E-Mail-Adresse kann Mitglied von Aktionsgruppen mehrerer Abonnements sein. Die Ratenlimits gelten für alle Abonnements, d.h., sie gelten, sobald der Schwellenwert erreicht wird, auch wenn von mehreren Abonnements gesendet wurde.  
- Wenn für eine Telefonnummer oder E-Mail-Adresse ein Ratenlimit gilt, wird eine weitere Nachricht vom selben Typ gesendet, um über das Ratenlimit zu informieren. In der SMS oder E-Mail wird angegeben, wann das Ratenlimit abläuft.

## <a name="rate-limit-of-webhooks"></a>Ratenlimit von Webhooks ##
Es gibt derzeit kein Ratenlimit für Webhooks.

## <a name="next-steps"></a>Nächste Schritte ##
Weitere Informationen zum [Verhalten von SMS-Warnungen](monitoring-sms-alert-behavior.md)  
Verschaffen Sie sich einen [Übersicht über Aktivitätsprotokollwarnungen](monitoring-overview-alerts.md), und erfahren Sie, wie Sie gewarnt werden können.  
[Konfigurieren von Warnungen, wenn eine Dienstintegritätsbenachrichtigung gesendet wird](monitoring-activity-log-alerts-on-service-notifications.md)

