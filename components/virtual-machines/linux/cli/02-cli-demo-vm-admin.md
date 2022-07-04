# Basic administration of Azure Virtual Machines with CLI in 12 steps

## 1) Create the resource group and the virtual machine

### 1.1) Create the resource group lnx-demo-vm-rg
```bash
az group create --name lnx-demo-vm-rg --location eastus-2
```

### 1.2) Create the vm01
```bash
az vm create --resource-group lnx-demo-vm-rg \
--location eastus2 \
--name vm01 \
--image UbuntuLTS \
--public-ip-sku Standard \
--admin-username azuredeveloper \
--generate-ssh-keys \
--ssh-key-values ~/.ssh/vm01 \
--verbose
```

---

### 2) Get help
```bash
az vm --help
az vm create --help
az vm create --help | less
```

---

## 3) Connect to the virtual machine

### 3.1) Connect to vm01 if you are using the default id_rsa
```bash
ssh azuredeveloper@<AZURE_VM01_PUBLIC_IP>
```

### 3.2) Connect to vm01 if you are using the another key
```bash
ssh -i /home/${USER}/.ssh/vm01.private azuredeveloper@<AZURE_VM01_PUBLIC_IP>
```

---

### 4) See the images of the virtual machines
```bash

### Return information of most common virtual machine images
az vm image list
az vm image list --help

### get the information on a table format
az vm image list --output table

### get the offer of images related with java
az vm image list --output table --all --offer Java   --output table

### get the offer of images related with ubuntu
az vm image list --output table --all --offer Ubuntu --output table
```

---

### 5) See the sizes list of the vm
```bash
az vm list-sizes --location eastus-2
az vm list-sizes --location east-us2 --output tsv
az vm list-sizes --location east-us2 --output table
```

---

## 6) Creat vm02

### 6.1) Create a virtual machine vm02 with a different size of the default
```bash
az vm create --resource-group  lnx-demo-vm-rg \
--location eastus-2 \
--name vm02 \
--image UbuntuLTS \
--admin-username azuredeveloper \
--generate-ssh-keys \
--ssh-key-values /home/leo/.ssh/vm02 \
--size "Standard_DS2_v2" \
--verbose
```

### 6.2) Connect to vm02
```bash
ssh -i ~/.ssh/vm02.private azuredeveloper@<AZURE_VM02_PUBLIC_IP>
```

---

## 7.0) see the list of your virtual machines
```bash
az vm list 
```

## 7.1) see in table format
```bash
az vm list --output table
```

---

## 8) See the ip of your virtual machines
```bash
az vm list-ip-addresses 

### list the ip addreses of yout virtual machine in table format
az vm list-ip-addresses --output table

### Get the ip of the vm01
az vm list-ip-addresses --resource-group  lnx-demo-vm-rg --name vm01 --output table
```

### 9 Get information of any virtual machine
```bash
### get information of vm01 in the resource group lnx-demo-vm-rg
az vm show --resource-group  lnx-demo-vm-rg --name vm01

### get information of vm01 in the resource group  lnx-demo-vm-rg, but only the admin username
az vm show --resource-group  lnx-demo-vm-rg --name vm01 --query "osProfile.adminUsername"

### get information of vm01 in the resource group  lnx-demo-vm-rg, but only the admin username in tsv format
az vm show --resource-group  lnx-demo-vm-rg --name vm01 --query "osProfile.adminUsername" -o tsv

### get the admin username of the vm01 and assign the value to the local variable vmname
vmname=$(az vm show --resource-group  lnx-demo-vm-rg --name vm01 --query "osProfile.adminUsername" -o tsv)

### display the value of this variable
echo $vmname
```


---

## 10) stop your virtual machine
```bash
az vm stop  --name vm2 --resource-group  lnx-demo-vm-rg
```

---

## 11 delete your virtual machines
```bash
az vm delete --name vm02 --resource-group  lnx-demo-vm-rg
```

---

## 12 install software on vm01
```bash
### Connect to the virtual machine (client)
ssh -i ~/.ssh/vm01.private azuredeveloper@<AZURE_VM01_PUBLIC_IP>

### update the software in ubuntu (server)
sudo apt-get -y update && sudo apt-get -y upgrade

### install nginx (server)
sudo apt-get -y install nginx

### test in the virtual machine (server)
curl localhost


### Get help of open-port option (client)
az vm open-port --help | less

### open the port 80 on vm01 (client)
az vm open-port --port 80 --resource-group lnx-demo-vm-rg --name vm01 --verbose

### test on your own machine (client)
curl http://<AZURE_VM01_PUBLIC_IP>
```