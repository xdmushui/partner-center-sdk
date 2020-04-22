---
title: Analytics resources
description: Partner Center resources for data used to report on usage, deployment, and consumption.
ms.assetid: 1FEB08D6-AD0C-4B01-B7A8-AE05C914912B
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Analytics resources

**Applies to:**

- Partner Center

The resources defined here contain data used to report on usage, deployment, and consumption.

## PartnerLicensesDeploymentInsights

The **PartnerLicensesDeploymentInsights** resource contains partner-level insights about license deployment.

| Property                  | Type                                                           | Description                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | number                                                         | The percentage of licenses deployed.                                                |
| licensesSold              | number                                                         | The number of licenses sold.                                                        |
| processedDateTime         | string in UTC date-time format                                 | The date and time when the data was aggregated.                                     |
| serviceName               | string                                                         | The service name (for example:  o365, crm).                                                  |
| channel                   | string                                                         | The channel name of the service (for example:  reseller).                                    |
| attributes                | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "PartnerLicensesDeploymentInsights" |

## PartnerLicensesUsageInsights

The **PartnerLicensesUsageInsights** resource contains partner-level insights about license usage.

| Property                     | Type                                                           | Description                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | number                                                         | The percentage of licenses deployed.                                           |
| workloadName                 | string                                                         | The workload name (for example:  exchange).                                             |
| processedDateTime            | string in UTC date-time format                                 | The date and time when the data was aggregated.                                |
| serviceName                  | string                                                         | The service name (for example:  o365, crm).                                             |
| channel                      | string                                                         | The channel name of the service (for example:  reseller).                               |
| attributes                   | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "PartnerLicensesUsageInsights" |

## CustomerLicensesDeploymentInsights

The **CustomerLicensesDeploymentInsights** resource contains customer-level insights about license deployment.

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
| serviceName       | string                                                         | The service name (for example:  o365, crm).                                                   |
| channel           | string                                                         | The channel name of the service (for example:  reseller).                                     |
| attributes        | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "CustomerLicensesDeploymentInsights" |

## CustomerLicensesUsageInsights

The **CustomerLicensesUsageInsights** resource contains customer-level insights about license usage.

| Property          | Type                                                           | Description                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | string                                                         | The workload code.                                                              |
| workloadName      | number                                                         | The workload name (for example:  Exchange).                                              |
| usagePercent      | number                                                         | The adjusted percentage of licenses used.                                       |
| licensesActive    | number                                                         | The number of active licenses.                                                  |
| licensesQualified | number                                                         | The number of qualified licenses.                                               |
| customerId        | string                                                         | The customer identifier.                                                        |
| customerName      | string                                                         | The customer name.                                                              |
| productName       | string                                                         | The product name.                                                               |
| serviceCode       | string                                                         | The service code of the license.                                                |
| processedDateTime | string in UTC date-time format                                 | The date and time when the data was aggregated.                                 |
| serviceName       | string                                                         | The service name (for example:  o365, crm).                                              |
| channel           | string                                                         | The channel name of the service (for example:  reseller).                                |
| attributes        | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "CustomerLicensesUsageInsights" |