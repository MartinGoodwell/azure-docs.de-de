---
title: Deploy templates with the portal in Azure Stack | Microsoft Docs
description: Learn how to use the Azure Stack portal to deploy templates.
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: eafa60f2-16c9-4ef1-b724-47709e9ea29e
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.translationtype: HT
ms.sourcegitcommit: d941879aee6042b38b7f5569cd4e31cb78b4ad33
ms.openlocfilehash: eb6e67dc4707b2b999efcceec1c55dc950c5996e
ms.contentlocale: de-de
ms.lasthandoff: 07/10/2017


---
# <a name="deploy-templates-using-the-azure-stack-portal"></a>Deploy templates using the Azure Stack portal
Use the portal to deploy Azure Resource Manager templates to the Azure Stack development kit.

Resource Manager templates deploy and provision all the resources for your application in a single, coordinated operation.

1. Log in to the portal, click **New**, click **Custom**, and then click **Template deployment**.
2. Click **Edit template**, then paste your JSON template code into the blade, and then click **Save**.
3. Click **Edit parameters**, type values for the parameters listed, and then click **OK**.
4. Click **Subscription**, choose the subscription you want to use, and then click **OK**.
5. Click **Resource group**, choose an existing resource group or create a new one, and then click **OK**.
6. Click **Create**. A new tile on the dashboard tracks the progress of your template deployment.

## <a name="next-steps"></a>Next steps
[Deploy templates with PowerShell](azure-stack-deploy-template-powershell.md)


