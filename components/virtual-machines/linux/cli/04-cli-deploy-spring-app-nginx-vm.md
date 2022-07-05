# Deploy Spring Application and NGINX on Azure Virtual Machine

### Clone GitHub repository
```bash
git clone https://github.com/rmontesleo/springboot-todo-h2-api-iaas.git
```

### go to the project folder
```bash
cd springboot-todo-h2-api-iaas
```

### Build Java Jar
```bash
mvn clean package
```

### Create the resource Group
```bash
az group create --name springtodoapp-rg --location eastus2
```

### See the available images related with java
```bash
az vm image list --all --offer Java --output table
```

### See the sizes of the virtual machines
```bash

## see all sizes of the virtual machines
az vm list-sizes --location east-us2 --output table

## use the less command
az vm list-sizes --location east-us2 --output table | less
```

### Create the virtual machine
```bash
az vm create \
--resource-group springtodoapp-rg \
--name vm-linux-springapp-nginx \
--image tidalmediainc:minecraft-java-ubuntu-20-minimal:minecraft-java-ubuntu-20-minimal:1.0.1 \
--size "Standard_B1ms" \
--public-ip-sku Standard \
--admin-username vmadmin \
--generate-ssh-keys \
--ssh-key-values ~/.ssh/azure/spring/springapp-nginx \
--verbose
```

### upload jar file
```bash
scp -i  ~/.ssh/azure/spring/springapp-nginx.private  target/springboot-todo-h2-api.jar vmadmin@<VM_IP>:/home/vmadmin
```

### Open port 80
```bash
az vm open-port --port 80  \
--resource-group springtodoapp-rg \
--name vm-linux-springapp-nginx \
--priority 100 \
--nsg-name webPort
```


### Login to the virtual machine
```bash
ssh -i  ~/.ssh/azure/spring/springapp.private vmadmin@<VM_IP>
```

---

### Start java application (server)
```bash
java -jar springboot-todo-h2-api-iaas.jar &
```

### Test the api (server)
```bash
curl localhost:8080

curl localhost:8080/api/todoapp/swagger-ui.html
```

---

## Install nginx server

### Update system
```bash
sudo apt-get -y update 
```

### install nginx 
```bash
sudo apt-get -y install nginx
```

### test nginx on the server
```bash
curl localhost
```

### edit configuration file
```bash
sudo vim /etc/nginx/sites-available/default
```

###
```bash
server {

    ...
    server_name <APPLICATION_NAME>.<DOMAIN>  www.<APPLICATION_NAME>.<DOMAIN>
    location / {
        proxy_pass http://localhost:<APPLICATION_PORT>;
        proxy_http_version 1.1;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;

    }
}

```


### verify the nginx configuration is right
```bash
sudo nginx -t
```

### restart service
```bash
sudo service nginx restart
```
---


### Test the api on port 80 (client)
```bash
curl http://<VM_IP>/api/todoapp/swagger-ui.html
``` 


## See some information about your VM

### see the ip of all virtual machines
```bash
az vm list-ip-addresses
```

### See the ip of your vm
```bash
az vm list-ip-addresses --resource-group springtodoapp-rg --name vm-linux-springapp-nginx --output table
```

### get information of vm-linux-springapp-nginx in the resource group springtodoapp-rg
```bash
az vm show --resource-group springtodoapp-rg --name vm-linux-springapp-nginx
```

