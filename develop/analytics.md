---
title: Analytics
description: 
    The resources defined here contain data used to report on usage,
    deployment, and consumption.
ms.assetid: 1FEB08D6-AD0C-4B01-B7A8-AE05C914912B
ms.author: mhopkins
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Analytics


**Applies To**

-   Partner Center

The resources defined here contain data used to report on usage,
deployment, and consumption.

## <span id="PartnerLicensesDeploymentInsights"></span><span id="partnerlicensesdeploymentinsights"></span><span id="PARTNERLICENSESDEPLOYMENTINSIGHTS"></span>PartnerLicensesDeploymentInsights


Contains partner level insights about license deployment.

| Property                  | Type                                                           | Description                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | number                                                         | The percentage of licenses deployed.                                                |
| licensesSold              | number                                                         | The number of licenses sold.                                                        |
| processedDateTime         | string in UTC date-time format                                 | The date and time when the data was aggregated.                                     |
| serviceName               | string                                                         | The service name (e.g. o365, crm).                                                  |
| channel                   | string                                                         | The channel name of the service (e.g. reseller).                                    |
| attributes                | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "PartnerLicensesDeploymentInsights" |

 

## <span id="PartnerLicensesUsageInsights"></span><span id="partnerlicensesusageinsights"></span><span id="PARTNERLICENSESUSAGEINSIGHTS"></span>PartnerLicensesUsageInsights


Contains partner level insights about license usage.

| Property                     | Type                                                           | Description                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | number                                                         | The percentage of licenses deployed.                                           |
| workloadName                 | string                                                         | The workload name (e.g. exchange).                                             |
| processedDateTime            | string in UTC date-time format                                 | The date and time when the data was aggregated.                                |
| serviceName                  | string                                                         | The service name (e.g. o365, crm).                                             |
| channel                      | string                                                         | The channel name of the service (e.g. reseller).                               |
| attributes                   | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "PartnerLicensesUsageInsights" |

 

## <span id="CustomerLicensesDeploymentInsights"></span><span id="customerlicensesdeploymentinsights"></span><span id="CUSTOMERLICENSESDEPLOYMENTINSIGHTS"></span>CustomerLicensesDeploymentInsights


Contains customer level insights about license deployment.

| Property          | Type                                                           | Description                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | number                                                         | The number of licenses deployed.                                                     |
| licensesSold      | number                                                         | The number of licenses sold.                                                         |
| deploymentPercent | number                                                         | The adjusted percentage of licenses deployed.                                        |
| customerId        | string                                                         | The customer identifier.                                                             |
| customerName      | string                                                         | The customer name.                                                                   |
| productName       | string                                                         | The product name.                                                                    |
| serviceCode       | string                                                         | The service code of the license.                                                     |
| processedDateTime | string in UTC date-time format                                 | The date and time when the data was aggregated.                                      |
| serviceName       | string                                                         | The service name (e.g. o365, crm).                                                   |
| channel           | string                                                         | The channel name of the service (e.g. reseller).                                     |
| attributes        | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "CustomerLicensesDeploymentInsights" |

 

## <span id="CustomerLicensesUsageInsights"></span><span id="customerlicensesusageinsights"></span><span id="CUSTOMERLICENSESUSAGEINSIGHTS"></span>CustomerLicensesUsageInsights


Contains customer level insights about license usage.

| Property          | Type                                                           | Description                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | string                                                         | The workload code.                                                              |
| workloadName      | number                                                         | The workload name (e.g. Exchange).                                              |
| usagePercent      | number                                                         | The adjusted percentage of licenses used.                                       |
| licensesActive    | number                                                         | The number of active licenses.                                                  |
| licensesQualified | number                                                         | The number of qualified licenses.                                               |
| customerId        | string                                                         | The customer identifier.                                                        |
| customerName      | string                                                         | The customer name.                                                              |
| productName       | string                                                         | The product name.                                                               |
| serviceCode       | string                                                         | The service code of the license.                                                |
| processedDateTime | string in UTC date-time format                                 | The date and time when the data was aggregated.                                 |
| serviceName       | string                                                         | The service name (e.g. o365, crm).                                              |
| channel           | string                                                         | The channel name of the service (e.g. reseller).                                |
| attributes        | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "CustomerLicensesUsageInsights" |

 

 

 




