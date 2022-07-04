# Basic sample to create an Ubuntu Virtual Machine

### Generic Way to create your resource group
```bash
az group create --location <LOCATION_NAME> --resource-group <RESOURCE_GROUP_NAME> 
```

### Create a resource group call lnx-demo-vm-rg
```bash
az group create --name lnx-demo-vm-rg --location eastus
```

### List your resource groups in json format (default)
```bash
az group list
```



### List your resource groups in table format
```bash
az group list --output table
```


### Create an Ubuntu VM in the lnx-demo-vm-rg
### This command generate the id_rsa id_rsa.pub keys
```bash
az vm create \
--resource-group lnx-demo-vm-rg \
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
ssh vmadmin@<VIRTUAL_MACHINE_IP>
```
