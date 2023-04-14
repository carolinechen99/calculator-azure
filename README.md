# calculator-azure
This project deploys a full stack web app to AKS service with docker

## Prerequisites
These are run in [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)



These are Azure resource providers required to support Container insights. To check the registration status, run the following commands:
    
``` bash
    az provider show -n Microsoft.OperationsManagement -o table
    az provider show -n Microsoft.OperationalInsights -o table
```

If they are not registered, register Microsoft.OperationsManagement and Microsoft.OperationalInsights using the following commands:

``` bash
    az provider register --namespace Microsoft.OperationsManagement
    az provider register --namespace Microsoft.OperationalInsights
```
Create a resource group
``` bash
    az group create --name calculator --location eastus2
```

Create AKS Cluster
``` bash
az aks create -g calculator -n calculator_aksgroup --enable-managed-identity --node-count 1 --enable-addons monitoring --enable-msi-auth-for-monitoring  --generate-ssh-keys
```
Connect to AKS Cluster
``` bash
az aks get-credentials --resource-group calculator --name calculator_akscluster
```
Verify the connection to your cluster using the kubectl get command to return a list of the cluster nodes.
``` bash
kubectl get nodes
```