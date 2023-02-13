

## Create connector with customized role
az rest --method put --url https://management.azure.com/subscriptions/937bc588-a144-4083-8612-5f9ffbbddb14/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwen-eu/providers/Microsoft.ServiceLinker/linkers/storage?api-version=2022-11-01-preview --body @storage_customized_role.json

az rest --method put --url https://management.azure.com/subscriptions/937bc588-a144-4083-8612-5f9ffbbddb14/resourceGroups/qianwen-canary/providers/Microsoft.Web/sites/qianwen-euap/providers/Microsoft.ServiceLinker/linkers/storage?api-version=2022-11-01-preview --body @storage_customized_role.json


az rest --method put --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwen-ne/providers/Microsoft.ServiceLinker/linkers/storage?api-version=2022-11-01-preview --body @storage_customized_role.json