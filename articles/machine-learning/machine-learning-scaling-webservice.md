---
title: "Erhöhen der Parallelität eines Azure Machine Learning-Webdiensts | Microsoft-Dokumentation"
description: "Hier erfahren Sie, wie Sie die Parallelität eines Azure Machine Learning-Webdiensts durch Hinzufügen zusätzlicher Endpunkte erhöhen."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "Azure Machine Learning, Webdienste, Operationalisierung, Skalierung, Endpunkt, Parallelität"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
translationtype: Human Translation
ms.sourcegitcommit: 197ebd6e37066cb4463d540284ec3f3b074d95e1
ms.openlocfilehash: 013354515d841003c912ac0338690dd975a79ef7
ms.lasthandoff: 03/31/2017


---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a>Skalieren eines Azure Machine Learning-Webdiensts durch Hinzufügen zusätzlicher Endpunkte
> [!NOTE]
> In diesem Thema werden für einen **klassischen** Machine Learning-Webdienst geltende Verfahren beschrieben. 
> 
> 

Standardmäßig ist jeder veröffentlichte Webdienst konfiguriert, 20 Anforderungen gleichzeitig zu unterstützen, wobei maximal 200 Anforderungen gleichzeitig unterstützt werden können. Während das klassische Azure-Portal eine Möglichkeit zum Festlegen dieses Werts bietet, optimiert Azure Machine Learning diese Einstellung automatisch, um die beste Leistung für Ihren Webdienst zu bieten. Der Portalwert wird ignoriert. 

Wenn Sie die API stärker als mit dem unterstützen Maximalwert von 200 gleichzeitigen Aufrufen auslasten möchten, müssen Sie mehrere Endpunkte im gleichen Webdienst erstellen. Sie können die Last dann wahllos auf alle Endpunkte verteilen.

Die Skalierung eines Webdiensts ist eine gängige Aufgabe. Gründe für die Skalierung sind eine Unterstützung von mehr als 200 gleichzeitigen Anforderungen, das Erhöhen der Verfügbarkeit mittels mehrerer Endpunkte oder das Bereitstellen getrennter Endpunkte für den Webdienst. Sie können die Skalierung erhöhen, indem Sie über das [klassische Azure-Portal](https://manage.windowsazure.com/) oder [Azure Machine Learning Web Services](https://services.azureml.net/)-Portal zusätzliche Endpunkte für den gleichen Webdienst hinzufügen.

Weitere Informationen zum Hinzufügen neuer Endpunkte finden Sie unter [Erstellen von Endpunkten](machine-learning-create-endpoint.md).

Bedenken Sie, dass sich eine hohe Anzahl gleichzeitiger Aufrufe nachteilig auswirken kann, wenn die API nicht mit einer entsprechend hohen Rate aufgerufen wird. Es können sporadische Timeouts und/oder Spitzen in die Latenz auftreten, wenn eine für eine hohe Auslastung konfigurierte API relativ gering ausgelastet wird.

Die synchronen APIs werden in der Regel in Situationen verwendet, in denen eine niedrige Latenz erwünscht ist. Mit Latenz ist hier der Zeitraum gemeint, der von der API benötigt wird, um eine Anforderung abzuschließen, wobei keinerlei Netzwerkverzögerungen berücksichtigt werden. Angenommen, Sie haben eine API mit einer Latenz von 50 ms (Millisekunden). Um die verfügbare Kapazität mit der Drosselungsstufe High (Hoch) und einer Höchstzahl gleichzeitiger Anrufe = 20 voll nutzen zu können, müssen Sie diese API 20 * 1000 / 50 = 400 Mal pro Sekunde aufrufen. Wenn dieses Beispiel fortgesponnen wird, ermöglicht eine Höchstzahl von 200 gleichzeitigen Aufrufen 4.000 Aufrufe der API pro Sekunde, sofern die Latenz 50 ms beträgt.

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png

