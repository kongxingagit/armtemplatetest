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



More tips here 

http://www.frankysnotes.com/2018/05/5-simple-steps-to-get-clean-arm-template.html

https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/template-functions
----------

Step 4 - Use Use Unique String

When you deploy in Azure some names are global, and by definition need to be unique. This is why adding a suffix or a unique identifier to your named is a good practice. An excellent way to get an identifier is to use the function uniqueString(). This function will create a 64Bits hash based on the information passed in parameter.

"suffix": "[uniqueString(resourceGroup().id, resourceGroup().location)]"

In the example just above, we pass the identifier of the resource group and its name. It means that every time you will be deploying in the same resource group and at that location suffix will be the same. However, if your solution is deployed in multiple locations (for a disaster recovery, or another scenario), suffix will have a different value.

To use it, let's say the name of a virtual machine was passed as a parameter. Then we will create a variable and concatenate the parameter and our suffix.

"VMName": "[toLower(concat(parameters('virtualMachineName'), variables('suffix')))]",

Then instead of using the parameter inside your ARM template, you will be using this new variable.

-----