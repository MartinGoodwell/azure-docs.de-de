---
title: "Übergeben von Anmeldeinformationen an Azure mithilfe von DSC | Microsoft Docs"
description: "Überblick über das sichere Übergeben von Anmeldeinformationen an virtuelle Azure-Computer mithilfe von PowerShell DSC"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: ea76b7e8-b576-445a-8107-88ea2f3876b9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
translationtype: Human Translation
ms.sourcegitcommit: 197ebd6e37066cb4463d540284ec3f3b074d95e1
ms.openlocfilehash: acd768c0219ec23c0453a65c575faf5213d9c616
ms.lasthandoff: 03/31/2017


---
# <a name="passing-credentials-to-the-azure-dsc-extension-handler"></a>Übergeben von Anmeldeinformationen an den Azure DSC-Erweiterungs-Handler
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

In diesem Artikel wird die Erweiterung der Konfiguration für den gewünschten Zustand (Desired State Configuration; DSC) für Azure behandelt. Einen Überblick über den DSC-Erweiterungshandler finden Sie unter [Einführung in den Handler der Azure-Erweiterung zum Konfigurieren des gewünschten Zustands](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="passing-in-credentials"></a>Übergeben von Anmeldeinformationen
Möglicherweise müssen Sie als Teil des Konfigurationsvorganges Benutzerkonten einrichten, auf Dienste zugreifen oder ein Programm im Benutzerkontext installieren. Um diese Aktionen durchführen zu können, müssen Sie Anmeldeinformationen bereitstellen. 

DSC lässt parametrisierte Konfigurationen zu, in denen Anmeldeinformationen in die Konfiguration übergeben und sicher in MOF-Dateien gespeichert werden. Der Azure-Erweiterungs-Handler vereinfacht die Verwaltung von Anmeldeinformationen, indem er die automatische Verwaltung von Zertifikaten bietet. 

Ziehen Sie das folgende DSC-Konfigurationsskript, das ein lokales Benutzerkonto mit dem angegebenen Kennwort erstellt, in Betracht:

*user_configuration.ps1*

```
configuration Main
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PSCredential]
        $Credential
    )    
    Node localhost {       
        User LocalUserAccount
        {
            Username = $Credential.UserName
            Password = $Credential
            Disabled = $false
            Ensure = "Present"
            FullName = "Local User Account"
            Description = "Local User Account"
            PasswordNeverExpires = $true
        } 
    }  
} 
```

Es ist wichtig, dass *node localhost* Teil der Konfiguration ist. Ohne diese Anweisung funktionieren die folgenden Schritte nicht, da der Erweiterungshandler insbesondere nach der „node localhost“-Anweisung sucht. Es ist ebenfalls wichtig, dass die Typumwandlung *[PsCredential]*enthalten ist, da dieser spezifische Typ die Verschlüsselung der Anmeldeinformationen durch die Erweiterung auslöst. 

Veröffentlichen dieses Skripts im Blobspeicher:

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

Einrichten der Azure DSC-Erweiterung und Bereitstellen der Anmeldeinformationen:

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a>Schützen der Anmeldeinformationen
Auf das Ausführen dieses Codes folgt die Aufforderung, Anmeldeinformationen anzugeben. Sobald diese angegeben werden, werden sie kurzfristig im Arbeitsspeicher gespeichert. Bei der Veröffentlichung mit dem `Set-AzureVmDscExtension`-Cmdlet werden sie über HTTPS an die VM übertragen, wobei Azure sie verschlüsselt auf den Datenträger speichert. Dafür wird das lokale VM-Zertifikat verwendet. Sie werden dann für kurze Zeit im Arbeitsspeicher entschlüsselt und wieder verschlüsselt, um an DSC übergeben zu werden.

Dieses Verhalten unterscheidet sich von der [Verwendung von sicheren Konfigurationen ohne den Erweiterungs-Handler](https://msdn.microsoft.com/powershell/dsc/securemof). Die Azure-Umgebung bietet eine Möglichkeit zum sicheren Übertragen von Konfigurationsdaten über Zertifikate. Bei der Verwendung des DSC-Erweiterungs-Handlers besteht keine Notwendigkeit, $CertificatePath oder einen $CertificateID/$Thumbprint-Eintrag in ConfigurationData bereitzustellen.

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zum Azure DSC-Erweiterungs-Handler finden Sie unter [Einführung in den Handler der Azure-Erweiterung zum Konfigurieren des gewünschten Zustands](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Sehen Sie sich die [Azure Resource Manager-Vorlage für die DSC-Erweiterung](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)an.

Weitere Informationen zu PowerShell DSC finden Sie im [PowerShell-Dokumentationscenter](https://msdn.microsoft.com/powershell/dsc/overview). 

Weitere Funktionen, die Sie mit PowerShell DSC verwalten können, finden Sie, indem Sie den [PowerShell-Katalog](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) nach weiteren DSC-Ressourcen durchsuchen.


