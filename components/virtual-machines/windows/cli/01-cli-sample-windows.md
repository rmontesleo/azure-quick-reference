# Basic sample create a Virtual Machine Windows Server 2016

### Create your resource group
```bash
az group create --name <RESOURCE_GROUP_NAME>  --location <YOUR_SELECTED_LOCATION>
```

### Create a resource group call wind-demo-vm-rg

```bash
az group create --name wind-demo-vm-rg  --location eastus
```

### Generic way to create your VM 
```
az vm create \
--resource-group <RESOURCE_GROUP_NAME> \
--name <VIRTUAL_MACHINE_NAME> \
--image <VIRTUAL_MACHINE_IMAGE> \
--public-ip-sku Standard \
--admin-username <ADMIN_USERNAME>
```

### Create a virtual machine
```bash
az vm create \
--resource-group WinCliDemo01-rg \
--image win2016datacenter \
--name win2016dc-cli \
--public-ip-sku Standard \
--admin-username vmadmin
```

### For more samples to create your VM check
```bash
az vm create --help | less
```

