# Mobile Application
This Azure Resource Template project was created using the tooling in Visual Studio that is provided through installing the Azure SDK.

The template deploys a set of resources that collectively provide a sample architecture for a mobile application.

# Create a basic mobile app using a template

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FBritBoy70%2Fazure-solutions-basic-mobile%2Fmaster%2FMobileApp%2FTemplates%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2FBritBoy70%2Fazure-solutions-basic-mobile%2Fmaster%2FMobileApp%2FTemplates%2Fazuredeploy.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>

For information about using this template, see below.

## Resources
The template deploys the following resources to Azure:

1. Azure App Services Hosting Plan - multiple instances across multiple regions.
2. Azure App Services Web Site (to host web services for mobile app) - multiple instances across multiple regions.
3. Redis Cache instance- multiple instances across multiple regions.
4. Azure DocumentDB
6. Azure storage
7. Azure Notification Hub and Namespace
8. Traffic Manager with endpoints for each of the deployed web sites.
8. CDN service configured with the FQDN of the Traffic Manager instance as source url
9. Application Insights and alerts for Azure web sites - multiple instances across multiple regions.

> By default resources inherit their deployment location to that of the containing resource group. Exceptions are:
> * Application Insights service is governed by the value of the *AppInsightsLocation* parameter.
> * App Service hosting plan, which deploys to multiple locations specified in the *WebLocations* parameter.
> * App Service web site, which deploys to multiple locations specified in the *WebLocations* parameter.
> * Redis Cache, which deploys to multiple locations specified in the *WebLocations* parameter.
> * AppInsights rules and alerts, which deploy to multiple locations specified in the *WebLocations* parameter.

> All resources are given a unique name through a combination of a prefix, set through the template parameters, followed by a unique string derived from the resource group ID.

## Parameters:
* __NamePrefix__: This string is used as a standard prefix for all resource names in the deployment. Resource names themselves are defined by variables.
* __ApplanSKU__: Sets the SKU fo the App Services hosting plan that will contain the web sites for the solution.
* __AppPlanWorkerSize__: Sets the size (small, medium, large) of the hosting plan.
* __StorageType__: Specifies the tier (for performance, resilience and price) of the Azure storage account.
* __AppInsightsLocation__: Specifies the deployment location for AppInsights. At the time of creation only *CentralUS* is allowed, but the parameter will make it easier to change in future.
* __WebLocations__: An array that contains the locations for instances of the App service hosting plan, web site, Redis instance and AppInsights rules. Default is for a single location - that of the containing resource group.

## Outputs:
To ease integration with Release Management this template provides key values as outputs.
* __TrafficMgrFQDN__: The url of the Traffic Manager endpoint to access the web site.
* __StorageName__: The name of the storage account.
* __StorageBlobEndpoint__: The URL for the storage account blob endpoint.
* __StorageKey__: The primary key for the storage account, as a securestring.
* __DocDbEndPoint__: The URL of the documentDB endpoint.
* __DocDbKey__: The primary master key for the documentDB, as a securestring.


## Notes:
1. AppInsights is available in *EastUS*, *SouthCentralUS*, *NorthEurope* and *WestEurope* the *allowedValues* for the *AppInsightsLocation* parameter are set accordingly. To change, once the service is allowed elsewhere, add the new locations to the list of values.
