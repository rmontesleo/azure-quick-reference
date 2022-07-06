# Create the container instances

### Basic way to create an azure container instance
```bash
az container create \
--resource-group <YOUR_RESOURCE_GROUP> \
--name  <CONTAINER_NAME> \
--image <REGISTRY_NAME>/<IMAGE_NAME>:<VERSION> \
--dns-name-label <DNS_NAME_LABEL> \
--ip-address Public --ports <REQUIRED_PORTS> \
--environment-variables <YOUR_ENV_VARIABLES>
```


### Get more information typing
```bash
az container create --help | less
```

### Create the default instance, this "fail", because we explicitly need open port 8080
```bash
az container create \
--resource-group javaprojects-rg \
--name myapi-01  \
--image springprojectregistry.azurecr.io/springboot-todo-h2-api-aci:v1 \
--dns-name-label myapi-01 \
--verbose
```

### see your instance
```bash
az container list --output table
```


### open port 8080 in container instance
```bash
az container create \
--resource-group javaprojects-rg \
--name myapi-02  \
--image springprojectregistry.azurecr.io/springboot-todo-h2-api-aci:v1 \
--dns-name-label myapi-02 \
--ip-address Public --ports 8080
```


### see your instance
```bash
az container list --output table
```


### Delete your containers

```bash
az container delete --resource-group <AZURE_RESOURCE_GROUP_NAME> --name <CONTAINER_NAME>
```

### Delete your containers
```bash
az container delete --resource-group javaprojects-rg --name myapi-01

az container delete --resource-group javaprojects-rg --name myapi-02
```
