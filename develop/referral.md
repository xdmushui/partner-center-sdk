---
title: Referral
description: Resources that represents a sales lead direct from customer or Microsoft.  
ms.author: mhopkins
ms.date: 10/01/2018
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
ms.localizationpriority: medium
---

# Referral


**Applies To**

-   Partner Center

Resources that represents a sales lead direct from customer or Microsoft.  


## <span id="Referral"></span><span id="referral"></span><span id="REFERRAL"></span>Referral


Represents the referral.

| Property              | Type                                              | Description                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Id                    | string                                            | The ID for this Referral.                                                                                         |
| EngagementId          | string                                            | The EngagementID for this Referral.                                                                               |
| OrganizationId        | string                                            | The Dunn & Bradstreet ID for this customer                                                                         |
| LocationId            | string                                            | TBD                                                                                |
| OrganizationName      | string                                            | The EngagementID for this Referral.                                                                               |
| CreatedDateTime       | string in UTC date time format                    | The date the referral was created.                                                                                |
| UpdatedDateTime       | string in UTC date time format                    | The date the referral was last updated.                                                                           |
| ExpirationDateTime    | string in UTC date time format                    | The date the referral will expire.                                                                           |
| Status                | [ReferralStatus](referral.md#ReferralStatus)      | An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the referral status. |
| ReferralSource        | string                                            | TBD     |
| ReferralType          | [ReferralType](referral.md#ReferralType)          | TBD     |
| CustomerProfile       | [CustomerProfile](referral.md#CustomerProfile)    | Customer contact information                                                                                      |
| Details               | [ReferralDetails](referral.md#ReferralDetails)    | Customer details, notes, deal value, closing date                                                                 |
| Users                 | [User](referral.md#User)                          | Represents the customer interest in Industry, Products, Services, Solutions                                       |
| InviteContext         | [InviteContext](referral.md#InviteContext)        | TBD                                       |
| InvitedByOrganizationID         | string       | TBD                                       |

## <span id="ReferralStatus"></span><span id="referralstatus"></span><span id="REFERRALSTATUS"></span>ReferralStatus


An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the referral status.

| Value              | Position     | Description                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Pending            | 0            | Represents a new referral  |
| Validated          | 1            | Represents a referral that has been acknowledged  |
| Active             | 2            | Represents a referral that has been accepted  |
| Rejected           | 3            | Represents a referral that has been rejected  |
| Expired            | 4            | Represents a referral that has expired  |
| Won                | 5            | Represents a referral that has been won  |
| Lost               | 6            | Represents a referral that has been lost  |

## <span id="ReferralType"></span><span id="referraltype"></span><span id="REFERRALTYPE"></span>ReferralType


Represents the referral type

| Property              | Type                                                       | Description                                                                  |
|-----------------------|------------------------------------------------------------|------------------------------------------------------------------------------|
| to do                 | string                                                     |                 |


## <span id="InviteContext"></span><span id="invitecontext"></span><span id="INVITECONTEXT"></span>InviteContext


Represents the referral invitation

| Property              | Type                                                       | Description                                                                  |
|-----------------------|------------------------------------------------------------|------------------------------------------------------------------------------|
| Notes                 | string                                                     | Additional details from the customer or Microsoft sales agent.               |


## <span id="ReferralDetails"></span><span id="referraldetails"></span><span id="REFERRALDETAILS"></span>ReferralDetails


Represents the referral details

| Property              | Type                                                       | Description                                                                  |
|-----------------------|------------------------------------------------------------|------------------------------------------------------------------------------|
| Notes                 | string                                                     | Additional details from the customer or Microsoft sales agent.               |
| DealValue             | decimal                                                    | Estimated value the referral may be worth.                                   |
| ClosingDate           | string in UTC date time format                             | Estimated date in which the customer wants to close.                         |
| Requirements          | [ReferralRequirements](referral.md#ReferralRequirements)  | Industry, products, service type, and solutions the customer is intered in   |

## <span id="ReferralRequirements"></span><span id="referralrequirements"></span><span id="REFERRALREQUIREMENTS"></span>ReferralRequirements


Contains the customer requirements

| Property        | Type                                                          | Description                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| Industries      | [Tag](referral.md#tag)                                       | The industries the customer is in                    |
| Products        | [Tag](referral.md#tag)                                       | The products the customer is interested in           |
| Services        | [Tag](referral.md#tag)                                       | The services the customer is interested in           |
| Solutions       | [Tag](referral.md#tag)                                       | The solutions the customer is interested in           |



## <span id="CustomerProfile"></span><span id="customerprofile"></span><span id="CUSTOMERPROFILE"></span>CustomerProfile


Contains the customer contact information

| Property        | Type                                                          | Description                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| Id              | string                                                        | The Id for this CustomerProfile                      |
| Name            | string                                                        | The customer first and last name                     |
| Address         | [Address](referral.md#address)                               | The address of the customer                          |
| Size            | string                                                        | The number of employees at the customers organization|
| Contacts        | [User](referral.md#User)               | The contact information for an individual in the customer organization                    |



## <span id="Address"></span><span id="address"></span><span id="ADDRESS"></span>Address


An address to use for the customer. For more information about the supported formats and properties in different countries/regions, see [Get address formatting rules by market](get-market-specific-validation-data.md).

| Property        | Type        | Description                                                   |
|-----------------|-------------|---------------------------------------------------------------|
| AddressLine1    | string      | The first line of the address.                                |
| AddressLine2    | string      | The second line of the address. This property is optional.    |
| City            | string      | The City.                                                     |
| State           | string      | The State.                                                    |
| PostalCode      | string      | The Zip code or postal code                                   |
| Country         | string      | The country/region in ISO country code format.                |


## <span id="Contact"></span><span id="contact"></span><span id="CONTACT"></span>Contact


Describes contact information for a specific individual.

| Property    | Type   | Description                  |
|-------------|--------|------------------------------|
| FirstName   | string | The contact's first name.    |
| LastName    | string | The contact's last name.     |
| PhoneNumber | string | The contact's phone number.  |
| Email       | string | The contact's email address. |




## <span id="User"></span><span id="user"></span><span id="USER"></span>User


Describes the the referrals information for a given user

| Property                  | Type                                                  | Description                                                           |
|---------------------------|-------------------------------------------------------|-----------------------------------------------------------------------|

[to do]

## <span id="Tag"></span><span id="tag"></span><span id="TAG"></span>Tag


Describes the tag.

| Property                  | Type                                                  | Description                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | string                                                | The ID for this tag                                           |

### Products

``` json
[
  {
    "id": "Azure"
  },
  {
    "id": "EnterpriseMobilityAndSecurity"
  },
  {
    "id": "Exchange"
  },
  {
    "id": "DeveloperTools"
  },
  {
    "id": "Dynamics365Business"
  },
  {
    "id": "Dynamics365Enterprise"
  },
  {
    "id": "DynamicsAX,GP,NAV,SL"
  },
  {
    "id": "Microsoft365"
  },
  {
    "id": "Office"
  },
  {
    "id": "PowerBI"
  },
  {
    "id": "Project"
  },
  {
    "id": "SharePoint"
  },
  {
    "id": "SkypeForBusiness"
  },
  {
    "id": "Surface"
  },
  {
    "id": "SurfaceHub"
  },
  {
    "id": "SQL"
  },
  {
    "id": "Teams"
  },
  {
    "id": "Visio"
  },
  {
    "id": "Windows"
  },
  {
    "id": "Yammer"
  }
]
```

### Services

``` json
[
  {
    "id": "ConsultingAndProfessional"
  },
  {
    "id": "CustomSolution(ISV)"
  },
  {
    "id": "DeploymentOrMigration"
  },
  {
    "id": "Hardware"
  },
  {
    "id": "Integration"
  },
  {
    "id": "IPServices(ISV)"
  },
  {
    "id": "LearningAndCertification"
  },
  {
    "id": "Licensing"
  },
  {
    "id": "ManagedServices"
  },
  {
    "id": "ProjectServices"
  }
]
```

### Industries

``` json
[
  {
    "id": "Agriculture, Forestry, & Fishing"
  },
  {
    "id": "Communications & Media"
  },
  {
    "id": "Education"
  },
  {
    "id": "Financial Services"
  },
  {
    "id": "Government"
  },
  {
    "id": "Healthcare"
  },
  {
    "id": "Hospitality"
  },
  {
    "id": "Manufacturing"
  },
  {
    "id": "Power & Utilities"
  },
  {
    "id": "Public Safety and National Security"
  },
  {
    "id": "Retail & Consumer Goods"
  },
  {
    "id": "Services"
  },
  {
    "id": "Travel & Transportation"
  },
  {
    "id": "Wholesale & Distribution"
  }
]
```

### Solutions

``` json
[
  {
    "id": "AdvancedAnalytics"
  },
  {
    "id": "ApplicationIntegration"
  },
  {
    "id": "ArtificialIntelligence"
  },
  {
    "id": "AzureSecurityOperationManagement"
  },
  {
    "id": "AzureStack"
  },
  {
    "id": "BackupDisasterRecovery"
  },
  {
    "id": "BigData"
  },
  {
    "id": "Blockchain"
  },
  {
    "id": "Chatbot"
  },
  {
    "id": "CloudDatabaseMigration"
  },
  {
    "id": "CloudMigration"
  },
  {
    "id": "CloudVoice"
  },
  {
    "id": "CognitiveServices"
  },
  {
    "id": "CompetitiveDatabaseMigration"
  },
  {
    "id": "Containers"
  },
  {
    "id": "DataWarehouse"
  },
  {
    "id": "DatabaseonLinux"
  },
  {
    "id": "DevelopmentandTest"
  },
  {
    "id": "DevOps"
  },
  {
    "id": "DigitalMedia"
  },
  {
    "id": "Dynamics365forCustomerService"
  },
  {
    "id": "Dynamics365forFieldService"
  },
  {
    "id": "Dynamics365forFinanceOperations"
  },
  {
    "id": "Dynamics365forRetail"
  },
  {
    "id": "Dynamics365forSales"
  },
  {
    "id": "Dynamics365forTalent"
  },
  {
    "id": "DynamicsonAzure"
  },
  {
    "id": "EnterpriseBusinessIntelligence"
  },
  {
    "id": "Gaming"
  },
  {
    "id": "HighPerformanceComputing"
  },
  {
    "id": "HybridStorage"
  },
  {
    "id": "IdentityandAccessManagement"
  },
  {
    "id": "InformationManagement"
  },
  {
    "id": "InternetofThings"
  },
  {
    "id": "MachineLearning"
  },
  {
    "id": "Microserviceapplications"
  },
  {
    "id": "MobileApplications"
  },
  {
    "id": "MySQLPostgresMigrationtoAzure"
  },
  {
    "id": "Networking"
  },
  {
    "id": "NoSQLMigration"
  },
  {
    "id": "RedhatonAzure"
  },
  {
    "id": "RegulatoryComplianceGDPR"
  },
  {
    "id": "SAPonAzure"
  },
  {
    "id": "ServerlessComputing"
  },
  {
    "id": "SharepointonAzure"
  },
  {
    "id": "SQLServerUpgrade"
  },
  {
    "id": "ThreatProtection"
  },
  {
    "id": "WebDevelopment"
  }
]
```

### Customer Size

``` json
[
  {
    "id": "1to50employees"
  },
  {
    "id": "51to500employees"
  },
  {
    "id": "Morethan500employees"
  },
  {
    "id": "1to9employees"
  },
  {
    "id": "10to50employees"
  },
  {
    "id": "51to250employees"
  },
  {
    "id": "251to1000employees"
  },
  {
    "id": "1001to5000employees"
  },
  {
    "id": "5001to10000employees"
  },
  {
    "id": "10001to20000employees"
  },
  {
    "id": "Morethan20000employees"
  }
]
```