---
title: "Löschen eines Gateways des virtuellen Netzwerks: PowerShell: Azure klassisch | Microsoft-Dokumentation"
description: "Löschen eines Gateways des virtuellen Netzwerks mithilfe von PowerShell im klassischen Bereitstellungsmodell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: cherylmc
ms.translationtype: Human Translation
ms.sourcegitcommit: 97fa1d1d4dd81b055d5d3a10b6d812eaa9b86214
ms.openlocfilehash: ac797f879ef306a7d423969ecfadca3a423b4cd5
ms.contentlocale: de-de
ms.lasthandoff: 05/11/2017


---
# <a name="delete-a-virtual-network-gateway-using-powershell-classic"></a>Löschen eines Gateways des virtuellen Netzwerks mit PowerShell (klassisch)
> [!div class="op_single_selector"]
> * [Resource Manager – Azure-Portal](vpn-gateway-delete-vnet-gateway-portal.md)
> * [Resource Manager – PowerShell](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [Klassisch – PowerShell](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

In diesem Artikel erfahren Sie, wie Sie ein VPN-Gateway im klassischen Bereitstellungsmodell mithilfe von PowerShell löschen. Ändern Sie nach dem Löschen des Gateways des virtuellen Netzwerks die Netzwerkkonfigurationsdatei, um nicht mehr verwendete Elemente zu entfernen.

##<a name="step-1-connect-to-azure"></a>Schritt 1: Herstellen einer Verbindung mit Azure

### <a name="1-install-the-latest-powershell-cmdlets"></a>1. Installieren Sie die neuesten Azure PowerShell-Cmdlets.

Laden Sie die aktuelle Version der PowerShell-Cmdlets der Azure-Dienstverwaltung herunter, und installieren Sie sie. Weitere Informationen finden Sie unter [Installieren und Konfigurieren von Azure PowerShell](/powershell/azure/overview).

### <a name="2-connect-to-your-azure-account"></a>2. Stellen Sie eine Verbindung mit Ihrem Azure-Konto her. 

Öffnen Sie die PowerShell-Konsole mit erhöhten Rechten, und stellen Sie eine Verbindung mit Ihrem Konto her. Verwenden Sie das folgende Beispiel, um eine Verbindung herzustellen:

```powershell
Add-AzureAccount
```

## <a name="step-2-export-and-view-the-network-configuration-file"></a>Schritt 2: Exportieren und Anzeigen der Netzwerkkonfigurationsdatei

Erstellen Sie auf Ihrem Computer ein Verzeichnis, und exportieren Sie die Netzwerkkonfigurationsdatei in das Verzeichnis. Sie verwenden diese Datei sowohl, um die aktuellen Konfigurationsinformationen anzuzeigen, als auch um die Netzwerkkonfiguration zu ändern.

In diesem Beispiel wird die Netzwerkkonfigurationsdatei in das Verzeichnis „C:\AzureNet“ exportiert.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

Öffnen Sie die Datei in einem Text-Editor, und zeigen Sie den Namen für Ihr klassisches VNet an. Wenn Sie im Azure-Portal ein VNet erstellen, ist der vollständige von Azure verwendete Name im Portal nicht zu sehen. Beispielsweise kann ein VNet, das im Azure-Portal anscheinend den Namen „ClassicVNet1“ trägt, in der Netzwerkkonfigurationsdatei einen viel längeren Namen haben. Der Name kann etwa wie folgt aussehen: „Group ClassicRG1 ClassicVNet1“. Namen virtueller Netzwerke werden unter **VirtualNetworkSite name =** aufgelistet. Verwenden Sie zum Ausführen von PowerShell-Cmdlets die Namen in der Netzwerkkonfigurationsdatei.

## <a name="step-3-delete-the-virtual-network-gateway"></a>Schritt 3: Löschen des Gateways für virtuelle Netzwerke

Wenn Sie ein Gateway eines virtuellen Netzwerks löschen, werden alle Verbindungen mit dem VNet durch das Gateway getrennt. Wenn P2S-Clients mit Ihrem VNet verbunden sind, werden diese ohne Warnung getrennt.

In diesem Beispiel wird das Gateway für virtuelle Netzwerke gelöscht. Vergewissern Sie sich, dass Sie den vollständigen Namen des virtuellen Netzwerks aus der Netzwerkkonfigurationsdatei verwenden.

```powershell
Remove-AzureVNetGateway -VNetName "Group ClassicRG1 ClassicVNet1"
```

Bei Erfolg wird diese Rückgabe angezeigt:

```
Status : Successful
```

## <a name="step-4-modify-the-network-configuration-file"></a>Schritt 4: Ändern der Netzwerkkonfigurationsdatei

Wenn Sie das Gateway eines virtuellen Netzwerks löschen, ändert das Cmdlet die Netzwerkkonfigurationsdatei nicht. Sie müssen die Datei ändern, um die Elemente zu entfernen, die nicht mehr verwendet werden. Die folgenden Abschnitte helfen Ihnen beim Ändern der heruntergeladenen Netzwerkkonfigurationsdatei.

### <a name="local-network-site-references"></a>Verweise auf lokale Netzwerksites

Um Verweisinformationen auf Sites zu entfernen, nehmen Sie Konfigurationsänderungen an **ConnectionsToLocalNetwork/LocalNetworkSiteRef** vor. Das Entfernen eines lokalen Siteverweises veranlasst Azure, einen Tunnel zu löschen. Je nach der von Ihnen erstellten Konfiguration wird möglicherweise keine Datei **LocalNetworkSiteRef** aufgelistet.

```
<Gateway>
   <ConnectionsToLocalNetwork>
     <LocalNetworkSiteRef name="D1BFC9CB_Site2">
       <Connection type="IPsec" />
     </LocalNetworkSiteRef>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

Beispiel:

```
<Gateway>
   <ConnectionsToLocalNetwork>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

###<a name="local-network-sites"></a>Lokale Netzwerksites

Entfernen Sie alle lokalen Sites, die Sie nicht mehr verwenden. Je nach der von Ihnen erstellten Konfiguration ist möglicherweise keine **LocalNetworkSite** aufgelistet.

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
  <LocalNetworkSite name="Site3">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>57.179.18.164</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

In diesem Beispiel haben wir nur Site3 entfernt.

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

### <a name="client-addresspool"></a>Clientadresspool

Wenn Ihr VNet über eine P2S-Verbindung verfügte, haben Sie einen **VPNClientAddressPool**. Entfernen Sie die Clientadresspools, die dem gelöschten Gateway des virtuellen Netzwerks entsprechen.

```
<Gateway>
    <VPNClientAddressPool>
      <AddressPrefix>10.1.0.0/24</AddressPrefix>
    </VPNClientAddressPool>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

Beispiel:

```
<Gateway>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

### <a name="gatewaysubnet"></a>GatewaySubnet

Löschen Sie das **GatewaySubnet**, das dem VNet entspricht.

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
   <Subnet name="GatewaySubnet">
     <AddressPrefix>10.11.1.0/29</AddressPrefix>
   </Subnet>
 </Subnets>
```

Beispiel:

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
 </Subnets>
```

## <a name="step-5-upload-the-network-configuration-file"></a>Schritt 5: Hochladen der Netzwerkkonfigurationsdatei

Speichern Sie die Änderungen, und laden Sie die Netzwerkkonfiguration nach Azure hoch. Stellen Sie sicher, dass Sie den Dateipfad wie für Ihre Umgebung erforderlich ändern.

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

Bei Erfolg sieht die Rückgabe so ähnlich aus wie in diesem Beispiel:

```
OperationDescription        OperationId                      OperationStatus                                                
--------------------        -----------                      ---------------                                           
Set-AzureVNetConfig         e0ee6e66-9167-cfa7-a746-7casb9   Succeeded
