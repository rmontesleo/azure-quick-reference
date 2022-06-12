# Basic sample to create an Ubuntu Virtual Machine

### Generic Way to create your resource group
```bash
az group create --location <LOCATION_NAME> --resource-group <RESOURCE_GROUP_NAME> 
```

### Create a resource group call LxCliDemo01-rg
```bash
az group create --name LxCliDemo01-rg --location eastus
```

### List your resource groups
```bash
az group list --output table
```


### Create an Ubuntu VM in the group LxCliDemo01-rg
```bash
az vm create \
--resource-group LxCliDemo01-rg \
--image UbuntuLTS \
--name linux-ubuntults-01-vm \
--public-ip-sku Standard \
--admin-username vmadmin \
--generate-ssh-keys \
--verbose
```

### List your virtual machines
```bash
az vm list --output table
```

### Connect to the virtual machine
```bash
ssh  vmadmin@<VIRTUAL_MACHINE_IP>
```
