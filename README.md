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