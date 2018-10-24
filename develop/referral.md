---
title: Referral
description: Resources that represents a sales lead direct from a customer, Microsoft or another partner.  
ms.date: 10/01/2018
ms.localizationpriority: medium
---

# Referral

**Applies To**

-   Partner Center

Resources that represent a sales lead direct from a customer, Microsoft, or another partner.   


## <span id="Referral"></span><span id="referral"></span><span id="REFERRAL"></span>Referral

Represents the referral.

| Property              | Type                                              | Description                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Id                    | string                                            | The ID for this Referral.                                                                                         |
| EngagementId          | string                                            | The EngagementID for this Referral. Multiple referrals can be associated to a single EngagementID                 |
| Name                  | string                                            | The name of the Referral.                 |
| OrganizationId        | string                                            | The organization ID of the party that owns the referral (Microsoft Partner Account ID / MSFT).           |
| BusinessProfileId     | string                                            | The business profile ID of the organization that owns the referral.                                       |
| OrganizationName      | string                                            | The organization name that owns the referral. Example: Store your own Dynamics 365 lead/opportunity ID   |
| ExternalReferenceId   | string                                            | An external identifier for the referral.                                                                          |
| CreatedDateTime       | string in UTC date time format                    | The date the referral was created.                                                                                |
| UpdatedDateTime       | string in UTC date time format                    | The date the referral was last updated.                                                                           |
| ExpirationDateTime    | string in UTC date time format                    | The date the referral will expire.                                                                                |
| Status                | [ReferralStatus](referral.md#ReferralStatus)      | An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status. |
| Substatus          | [ReferralSubstatus](referral.md#ReferralSubstatus)      | An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status detail. |
| StatusReason          | string                                            | A descriptive message about the status. Example: Why was the referral marked as lost? |
| ReferralType          | [ReferralType](referral.md#ReferralType)          | Represents the referral type.                                                                                     |
| Qualification         | [ReferralQualification](referral.md#ReferralQualification)| Represents the quality of the referral.                                                                           |
| CustomerProfile       | [CustomerProfile](referral.md#CustomerProfile)    | Customer contact information.                                                                                     |
| Consent               | [CustomerConsent](referral.md#CustomerConsent)    | Consent flags around sharing information with other organizations and allowing them to contact the customer.         |
| Details               | [ReferralDetails](referral.md#ReferralDetails)    | Customer details, notes, deal value, closing date.                                                                |
| Team                  | [Member](referral.md#Member)                      | Represents users in the organizations that are involved in the partner engagement.                                |
| InviteContext         | [InviteContext](referral.md#InviteContext)        | Represents additional information a user can provide when inviting another organization into the partner engagement.  |


## <span id="ReferralStatus"></span><span id="referralstatus"></span><span id="REFERRALSTATUS"></span>ReferralStatus

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.

| Value           | Position     | Description                                                                                |
|-----------------|--------------|--------------------------------------------------------------------------------------------|
| None            | 0            |                                                                                            |
| New             | 1            | Represents a new referral.                                                                 |
| Active          | 2            | Represents an active referral.                                                             |
| Closed          | 3            | Represents a closed referral.                                                              |


## <span id="ReferralSubstatus"></span><span id="referralSubstatus"></span><span id="REFERRALSubstatus"></span>ReferralSubstatus

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.

| Value           | Position     | Description                                                                                |
|-----------------|--------------|--------------------------------------------------------------------------------------------|
| None            | 0            |                                                                                            |
| Pending         | 1            | Represents a new referral that is pending.                                                 |
| Received        | 2            | Represents a new referral that has been received by the receiving party.                   |
| Accepted        | 3            | Represents an active accepted referral.                                                    |
| Won             | 4            | Represents a closed referral that has been won.                                            |
| Lost            | 5            | Represents a closed referral that has been lost.                                           |
| Declined        | 6            | Represents a closed referral that has been declined.                                       |
| Expired         | 7            | Represents a closed referral that has expired.                                             |

**Status & Substatus transition states**

| Status                | Allowed Status Transition     | Allowed Status Details                |
|-----------------------|-------------------------------|---------------------------------------|
| New                   | New, Active, Closed           | Pending, Received                     |
| Active                | Active, Closed                | Accepted                              |
| Closed                | Closed                        | Won, Lost, Declined, Expired          |


## <span id="ReferralType"></span><span id="referraltype"></span><span id="REFERRALTYPE"></span>ReferralType

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral type.

| Property              | Type                                                  | Description                                                                     |
|-----------------------|-------------------------------------------------------|---------------------------------------------------------------------------------|
| Shared                | 0                                                     | Represents a referral in which all parties involved will collaborate to close.  |
| Independent           | 1                                                     | Represents a referral in which two parties will collaborate to close.           |


## <span id="ReferralQualification"></span><span id="referralqualification"></span><span id="REFERRALQUALIFICATION"></span>ReferralQualification

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.

| Value                | Position     | Description                                                                                 |
|----------------------|--------------|---------------------------------------------------------------------------------------------|
| None                 | 0            | Represents a referral that has no quality measure associated.                               |
| Direct               | 1            | Represents a referral that has been created directly by a customer.                         |
| MarketingQualified   | 2            | Represents a referral that has been generated via Microsoft marketing automation systems.   |
| SalesQualified       | 3            | Represents a referral from a Microsoft sales agent.                                         |


## <span id="CustomerProfile"></span><span id="customerprofile"></span><span id="CUSTOMERPROFILE"></span>CustomerProfile

Contains the customer contact information.

| Property        | Type                                                          | Description                                             |
|-----------------|---------------------------------------------------------------|---------------------------------------------------------|
| Id              | string                                                        | The Id for this CustomerProfile.                        |
| Name            | string                                                        | The customer organization name.                         |
| Address         | [Address](referral.md#address)                                | The address of the customer.                            |
| Size            | string                                                        | The number of employees at the customers organization.  |
| Team            | [Member](referral.md#Member)                                  | The contacts for the customer organization.             |
| Ids            | [CustomerProfileType](referral.md#CustomerProfileType)                      | External ID's for the customer.             |

## <span id="CustomerProfileType"></span><span id="customerprofiletype"></span><span id="CUSTOMERPROFILETYPE"></span>CustomerProfileType

Contains the External ID's for the customer. 

| Property        | Type                                                          | Description                                             |
|-----------------|---------------------------------------------------------------|---------------------------------------------------------|
| Duns            | string                                                        | The Dun & Bradstreet number for the customer. https://www.dnb.com/duns-number                        |
| External        | string                                                        | A customer ID unique to your organization.                      |



## <span id="Address"></span><span id="address"></span><span id="ADDRESS"></span>Address

An address to use for the customer. For more information about the supported formats and properties in different countries/regions, see [Get address formatting rules by market](get-market-specific-validation-data.md).

| Property        | Type        | Description                                                   |
|-----------------|-------------|---------------------------------------------------------------|
| AddressLine1    | string      | The first line of the address.                                |
| AddressLine2    | string      | The second line of the address. This property is optional.    |
| City            | string      | The city.                                                     |
| State           | string      | The state.                                                    |
| PostalCode      | string      | The zip code or postal code                                   |
| Country         | string      | The country/region in ISO country code format.                |
| Region          | string      | The region.                                                   |


## <span id="Member"></span><span id="member"></span><span id="MEMBER"></span>Member

Describes contact information for a specific individual.

| Property    | Type   | Description                  |
|-------------|--------|------------------------------|
| FirstName   | string | The contact's first name.    |
| LastName    | string | The contact's last name.     |
| PhoneNumber | string | The contact's phone number.  |
| Email       | string | The contact's email address. |


## <span id="CustomerConsent"></span><span id="customerconsent"></span><span id="CUSTOMERCONSENT"></span>CustomerConsent

Consent flags around sharing information with other organizations and allowing them to contact the customer.

| Property                                         | Type      | Description                                                                                |
|--------------------------------------------------|-----------|--------------------------------------------------------------------------------------------|
| ConsentToMicrosoftToShareInfoWithPartners        | boolean   | Consent provided by the customer to share their info with other organizations.             |
| ConsentToMicrosoftToContact                      | boolean   | Consent provided by the customer that allows other organizations to contact the customer.  |
| ConsentToMicrosoftToContactSpecificPartners      | boolean   | Consent provided by the customer to contact fewer than 3 partners.                         |


## <span id="InviteContext"></span><span id="invitecontext"></span><span id="INVITECONTEXT"></span>InviteContext

Additional information that can be shared when inviting another organizations. 

| Property              | Type                                                       | Description                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Notes                 | string                                                     | Additional notes that the receiving organization will receive.                |
| InvitedByOrganizationId | string                                                   | The organization ID that sent the referral. (Microsoft Partner Account ID / MSFT).                                    |


## <span id="ReferralDetails"></span><span id="referraldetails"></span><span id="REFERRALDETAILS"></span>ReferralDetails

Represents the referral details.

| Property              | Type                                                       | Description                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Notes                 | string                                                     | Additional notes that the receiving organization will receive.                |
| DealValue             | decimal                                                    | Value of the referral.                                    |
| Currency              | string                                                    | Currency of the referral.                                    |
| ClosingDateTime       | string in UTC date time format                         | Date the customer is looking to close by.                           |
| Requirements          | [ReferralRequirements](referral.md#ReferralRequirements)   | Industry, products, service type, and solutions the customer is interested in.|


## <span id="ReferralRequirements"></span><span id="referralrequirements"></span><span id="REFERRALREQUIREMENTS"></span>ReferralRequirements

Contains the customer requirements.

| Property        | Type                                                         | Description                                          |
|-----------------|--------------------------------------------------------------|------------------------------------------------------|
| Industries      | [Tag](referral.md#tag)                                       | The industries the customer is interested in.        |
| Products        | [Tag](referral.md#tag)                                       | The products the customer is interested in.          |
| Services        | [Tag](referral.md#tag)                                       | The services the customer is interested in.          |
| Solutions       | [SolutionTag](referral.md#SolutionTag)                       | Describes the solutions                              |

## <span id="SolutionTag"></span><span id="solutiontag"></span><span id="SOLUTIONTAG"></span>SolutionTag

Contains the solution details.

| Property        | Type                                         | Description                                          |
|-----------------|----------------------------------------------|------------------------------------------------------|
| Id              | string                                       | The ID of the solution.        |
| Name            | string                                       | The name of the solution.          |
| SolutionType    | [SolutionType](referral.md#SolutionType)     | The type of solution.          |

## <span id="SolutionType"></span><span id="solutiontype"></span><span id="SOLUTIONTYPE"></span>SolutionType

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the solution type.

| Property        | Type                                    | Description                                                     |
|-----------------|-----------------------------------------|-----------------------------------------------------------------|
| None            | 0                                       |                                                                 |
| Category        | 1                                       | Leverages pre-defined solution names.                            |
| Name            | 2                                       | Allows for custom solution names to be provided in the referral. |


## <span id="Tag"></span><span id="tag"></span><span id="TAG"></span>Tag

Describes the tag.

| Property                  | Type                                                  | Description                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | string                                                | The ID for this tag.                                          |


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