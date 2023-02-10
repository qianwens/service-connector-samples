## Connect AKS and Azure Storage
### create linker resource 
az rest --method put --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwentest/providers/Microsoft.ServiceLinker/linkers/storagelinker?api-version=2022-11-01-preview --body @azurestorage_secret.json --debug

### get configuration 
az rest --method post --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwentest/providers/Microsoft.ServiceLinker/linkers/storagelinker/listConfigurations?api-version=2022-11-01-preview

listConfigurations API returns the secret keys that stores the storage connection string.
Check [Sample listConfigurations reponse](secret_response.json)

### Use secret in pod yaml
Secret Name: sc-storagelinker-secret.
Key Name: AZURE_STORAGEACCOUNT_CONNECTIONSTRING
Check [Sample Pod Using Secret](pod_secret.yaml). 

## Connect AKS and Azure Storage using Azure Key Vault as secret store
### create linker resource for Azure Key Vault to enable key vault CSI
az rest --method put --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwentest/providers/Microsoft.ServiceLinker/linkers/keyvaultlinker?api-version=2022-11-01-preview --body @azurekeyvault_csi.json --debug


### create linker resource for Azure storage using Key Vault store the secrets
az rest --method put --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwentest/providers/Microsoft.ServiceLinker/linkers/storagewithsecretstorelinker?api-version=2022-11-01-preview --body @azurestorage_secret_kv.json --debug

### sample pod yaml
Service connector store the connection string in azure key vault and sync the secret from AKV to k8s secrets.
Secret Name: sc-storagelinker-secret.
Key Name: AZURE_STORAGEACCOUNT_CONNECTIONSTRING
Check [Sample Pod Using Secret](pod_secret.yaml). 

## Connect AKS and Azure Storage with Dapr component
### create linker resource 
az rest --method put --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwentest/providers/Microsoft.ServiceLinker/linkers/storagelinker?api-version=2022-11-01-preview --body @azurestorage_dapr.json --debug

Service connector create dapr component in AKS by default, user can also choose to create dapr component in AKS by themselves by opt-out the configuration in linker payload as below:

az rest --method put --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwentest/providers/Microsoft.ServiceLinker/linkers/storagelinker?api-version=2022-11-01-preview --body @azurestorage_dapr_optout_config.json --debug


## Connect AKS and Azure Storage with Dapr component using Azure Key Vault as secret store
### create linker resource for Azure Key Vault to enable key vault CSI
az rest --method put --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwentest/providers/Microsoft.ServiceLinker/linkers/keyvaultlinker?api-version=2022-11-01-preview --body @azurekeyvault_csi.json --debug

### create linker resource for Azure storage
az rest --method put --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwentest/providers/Microsoft.ServiceLinker/linkers/storagewithsecretstorelinker?api-version=2022-11-01-preview --body @azurestorage_dapr_kv.json --debug

### generate dapr manifest 
If user choose to create dapr component in AKS by themselves, they can get the dapr manifest from generateConfiguration API.

az rest --method post --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwentest/providers/Microsoft.ServiceLinker/linkers/storagelinker/generateConfigurations?api-version=2022-11-01-preview

generateConfiguration API returns the manifest of dapr component
Check [Sample dapr manifest reponse](dapr_response.json)