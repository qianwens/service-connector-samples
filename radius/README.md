
## Create connector to azure storage using user managed identity authentication type
Add property "action" to opt-out configuration:
```json
"configurationInfo": {
    "action": "optOut"
}
```
Add property "roles" to customize RBAC role.
Add property "deleteOrUpdateBehavior" to force clean up the role assignment after delete connector:
```json
"authInfo": {
    "authType": "userAssignedIdentity",
    "clientId": "f0dd5dc3-9844-4727-bf0a-07e4d02a9457",
    "subscriptionId": "d82d7763-8e12-4f39-a7b6-496a983ec2f4",
    "roles": ["2a2b9908-6ea1-4ae2-8e65-a410df84e7d1"],
    "deleteOrUpdateBehavior": "ForcedCleanup"
 }
```

az rest --method put --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwen-euap/providers/Microsoft.ServiceLinker/linkers/storagelinkerRadius?api-version=2022-11-01-preview --body @storage_customized_role.json --debug

az rest --method get --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwen-euap/providers/Microsoft.ServiceLinker/linkers/storagelinkerRadius?api-version=2022-11-01-preview

Add property "customizedKeys" to customize environment variable names. Add this property in "configurationInfo" in the connection resource payload.
```json
"customizedKeys": {
    "AZURE_STORAGEBLOB_RESOURCEENDPOINT": "endpoint"
}
```
az rest --method post --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwen-euap/providers/Microsoft.ServiceLinker/linkers/storagelinkerRadius/generateConfigurations?api-version=2022-11-01-preview --body @storage_customized_env.json

az rest --method delete --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwen-euap/providers/Microsoft.ServiceLinker/linkers/storagelinkerRadius?api-version=2022-11-01-preview


## Create connector to azure storage using access key authentication type
Add property "permission" to limit access key permission:
```json
"authInfo": {
    "authType": "accessKey",
    "permissions": ["Read"]
}
```
az rest --method put --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourcegroups/qianwens/providers/Microsoft.ContainerService/managedClusters/qianwen-euap/providers/Microsoft.ServiceLinker/linkers/storagelinkerRadius2?api-version=2022-11-01-preview --body @storage_access_key.json --debug