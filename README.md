# Network Security Group (NSG) Flow Logs
author: Nathan Swift

The following deployment will setup an Azure Policy and Assignment to ensure that your NSGs are sending Flow Logs to use Network Watcher: Traffic Analytics, Azure Sentinel, or Log Analytics.

Deployment Instructions: Launch Cloud Shell, Update variables with your information below, run script in Cloud Shell

```#Fill out parameters below in variables

#This Policy will review NSGs only in the selected region. You can create other assignments to include other regions.
$nsgRegion = "REGION"

#A string with the storage id for the flowlogs to be sent to. It will be used for deployment purposes only. Make sure this storage account is located in the same region as the NSG. The format must be: '/subscriptions/{subscription id}/resourceGroups/{resourceGroup name}/providers/Microsoft.Storage/storageAccounts/{storage account name}
$storageId = "/subscriptions/{subscription id}/resourceGroups/{resourceGroup name}/providers/Microsoft.Storage/storageAccounts/{storage account name}"

#A string with the Log Analytics Resource id for the flowlogs to be sent to. It will be used for deployment purposes only. The format must be: '/subscriptions/{subscription id}/resourceGroups/{resourceGroup name}/providers/microsoft.operationalinsights/workspaces/{Log Analytics Workspace name}
$logAnalyticsWorkspaceId = "/subscriptions/{subscription id}/resourceGroups/{resourceGroup name}/providers/microsoft.operationalinsights/workspaces/{Log Analytics Workspace name}"

#A string with the Log Analytics WorkspaceId id for the flowlogs to be sent to. It will be used for deployment purposes only.
$workspaceId = "GUID"

#A Location string with the Log Analytics WorkspaceId Region
$workspaceRegion = "REGION"

#The name of the resource group where the flowLog resources will be created. This will be used only if a deployment is required. This is the resource group where the Network Watchers are located.
$networkWatcherRG = "NetworkWatcherRG"

#The name of the network watcher under which the flowLog resources will be created. Make sure it belongs to the same region as the NSG.
$networkWatcherName = "NetworkWatcher_<REGION>"

#/subscriptions/SUBID' or '/providers/Microsoft.Management/managementGroups/id
$policyScope = "/subscriptions/SUBID"

$date = get-date -Format "MMyyddhhmm"

New-AzSubscriptionDeployment -Name $date -Location $nsgRegion -TemplateUri "https://raw.githubusercontent.com/swiftsolves-msft/NSGFlowLogs/main/azuredeploy.json" -nsgRegion $nsgRegion -storageId $storageId -logAnalyticsWorkspaceId $logAnalyticsWorkspaceId -workspaceId $workspaceId -workspaceRegion $workspaceRegion -networkWatcherRG $networkWatcherRG -networkWatcherName $networkWatcherName -policyScope $policyScope```
