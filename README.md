There are two types of ARM deployments.

Deployments to RG is standard.

Deployments to subscription level covers deployment of Resource Groups, and this is the type this is.

Documentation is here https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/deploy-to-subscription .


A Basic command run is 

```
az deployment create \
  -n demoEmptyRG \
  -l southcentralus \
  --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/emptyRG.json \
  --parameters rgName=demoRG rgLocation=northcentralus

```

A successful deployment process is 

1. SANS name, use az deployment validate as thus

```
az deployment validate \
--location eastus
--template-file /path/to/template.json


```

After which fill in parameters

2. Then use 

```
az deployment create \
--name foo \
--location eastus \
--template-file /path/to/template.json


```

and then fill in parameters.

This is after logging in to cli using 

```
az cloud list
az cloud set --name AzureCloud (or AzureUSGovernment)
az login 

//select account as 

az account list
az account set --subscription Muh-Subscription-ID


```