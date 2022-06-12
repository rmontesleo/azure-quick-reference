# Basic sample creating Virtual Machines with PowerShell


## Login in to Azure account
```powershell
Connect-AzAccount
```

### Verify if you have any virtual machine created
```
Get-AzVm
```

### Generic way to create the resource group
```powershell
New-AzResourceGroup -Name <RESOURCE_GROUP_NAME> -Location <YOUR_SELECTED_LOCATION>
```

### Create the resource group call RGWinPSDemo01 in the east of the USA
```powershell
New-AzResourceGroup -Name RGWinPSDemo01 -Location EastUS
```

### Generic way toCreate your VM.
```powershell
New-AzVM -ResourceGroupName <RESOURCE_GROUP_NAME> `
-Name <VIRTUAL_MACHINE_NAME> `
-Location <YOUR_SELECTED_LOCATION> `
-VirtualNetworkName <VIRTUAL_NETWORK_NAME> `
-SubnetName <SUBNET_NAME> `
-SecurityGroupName <SECURITY_GROUP_NAME> `
--PublicIPAddressName <PUBLIC_IP_NAME> `
-OpenPorts [LIST_YOUR_PORTS]
```


### For this sample the powershell ask for the username and password. Remember password is ask once.
### By the fault creates a Windows Server 2016 Virtual Machine.
### The size is D2s_v3 size.  **Check the cost of this size or change it if you need it.**
```powershell
New-AzVM  `
-ResourceGroupName "RGWinPSDemo01" `
-Name "win2016dcrps" `
-Location "EastUS" `
-VirtualNetworkName "VMDemoVNet" `
-SubnetName "VMDemoSubNet" `
-SecurityGroupName "VMDemoSG" `
```

### You can stop your VM if its required
```powershell
Stop-AzVm -Name "win2016dcrps" -ResourceGroupName "RGWinPSDemo01"
```