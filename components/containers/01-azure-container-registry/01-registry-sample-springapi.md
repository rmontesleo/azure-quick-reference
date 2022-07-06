# Push your image to Azure Registry


### Login into azure account
```bash
az login
```

### Create a Resource group
```bash
az group create --name javaprojects-rg --location eastus2
```

### veriify your resource groups
```bash
az group list --output table
```


### Create the registry
```bash
az acr create \
--resource-group javaprojects-rg \
--name springprojectregistry \
--sku Basic \
--verbose
```

### list your container registries
```bash
az acr list --output table
```


### Choose a working directory to clone the git repository
```bash
git clone https://github.com/rmontesleo/springboot-todo-h2-api-docker.git
```


### Go to springboot-todo-h2-api-docker directory
```bash
cd  springboot-todo-h2-api-docker
```

### Generate the java jar
```bash
mvn clean package
```


### Build your image
```bash
docker build -f Dockerfile  -t springboot-todo-h2-api-aci:v1 .
```

### list your docker images
```bash
docker images
```


### Tag you image
```
docker tag <YOUR_LOCAL_IMAGE_APP_NAME>:<APP_VERSION> <AZURE_REGISTRY_NAME>.azurecr.io/<IMAGE_APP_NAME_IN_AZURE>:<APP_VERSION_IN_AZURE>
```

### Tag version 
```
docker tag springboot-todo-h2-api-aci:v1 springprojectregistry.azurecr.io/springboot-todo-h2-api-aci:v1
```

### verify you have another image (fiffernte tag name but same image id)
```
docker image ls
```

### using the shortcut
```bash
docker images
```

### Logout from other docker repositories
```bash
docker logout
```

## login to the docker azure registry, remember use the credentials provided in the Access key in your Registry settings.
```bash
docker login springprojectregistry.azurecr.io
```

## Push your images to the repository registry

### Push 
```bash
docker push springprojectregistry.azurecr.io/springboot-todo-h2-api-aci:v1
```


### List your images in azure
```bash
az acr repository list --name <YOUR_AZURE_REGISTRY_NAME> --output table
```

###
```bash
az acr repository list --name springprojectregistry --output table
```

### The output will be
``` bash
Result
------------------------
springboot-todo-h2-api-aci
```
