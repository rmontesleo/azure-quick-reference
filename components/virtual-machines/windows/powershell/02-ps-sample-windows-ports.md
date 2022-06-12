# Basic Sample creating a VM and open port

## Login in to Azure account
```powershell
Connect-AzAccount
```

### Verify if you have any virtual machine created
```powershell
Get-AzVm
```

### Create the resource group call RGWinPSDemo01 in the east of the USA
```powershell
New-AzResourceGroup -Name "powershellgrp" -Location "EastUS"
```

### Create your Virtual Machine
```powershell
New-AzVm -ResourceGroupName "powershellgrp" ` 
-Name "aznewvm" `
-Location "EastUS" `
-VirtualNetworkName "mynewVNet" `
-SubnetName "default" `
-SecurityGroupName  "mynewNSG"  ` 
-PublicIpAddressName "mypublicip" `
-OpenPorts 80,3389
```
### You can stop your VM if its required
```
Stop-AzVm -Name "aznewvm" -ResourceGroupName "powershellgrp"
```
