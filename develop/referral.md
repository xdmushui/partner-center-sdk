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
| CreatedDateTime       | string in UTC date time format                    | The date the referral was created.                                                                                |
| UpdatedDateTime       | string in UTC date time format                    | The date the referral was last updated.                                                                           |
| Status                | [ReferralStatus](referral.md#ReferralStatus)     | An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the referral status. |
| ReferralSource        | [ReferralSource](referral.md#ReferralSource)     | An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the referral source. |
| CustomerProfile       | [CustomerProfile](referral.md#CustomerProfile)   | Customer contact information                                                                                      |
| Details               | [ReferralDetails](referral.md#ReferralDetails)   | Customer details, notes, deal value, closing date                                                                 |
| Participants          | [Participant](referral.md#Participant)           | Represents the customer interest in Industry, Products, Services, Solutions                                       |


## <span id="ReferralStatus"></span><span id="referralstatus"></span><span id="REFERRALSTATUS"></span>ReferralStatus


An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the referral status.

| Value              | Position     | Description                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Pending            | 0            | Represents a referral that has not been acknowledged                                                                            |
| Active             | 1            | TBD                                    |
| Won                | 2            | TBD                          |
| Lost               | 3            | Represents a referral that has been lost     |
| Archived           | 3            | Represents an archived referral     | 

## <span id="ReferralSource"></span><span id="referralsource"></span><span id="REFERRALSOURCE"></span>ReferralSource


An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the referral source.

| Value              | Position     | Description                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| WebDirect          | 0            | TBD                                                                           |
| PartnerLed         | 1            | TBD                                     |
| AgentLed           | 2            | TBD                          |
| P2P                | 3            | TBD     |
 
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
| IndustryFocus   | [Tag](referral.md#tag)                                       | The industries the customer is in                    |
| Products        | [Tag](referral.md#tag)                                       | The products the customer is interested in           |
| ServiceTypes    | [Tag](referral.md#tag)                                       | The services the customer is interested in           |
| Solutions       | [Tag](referral.md#tag)                                       | The solutions the customer is interested in           |



## <span id="CustomerProfile"></span><span id="customerprofile"></span><span id="CUSTOMERPROFILE"></span>CustomerProfile


Contains the customer contact information

| Property        | Type                                                          | Description                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| Id              | string                                                        | The Id for this CustomerProfile                      |
| Name            | string                                                        | The customer first and last name                     |
| Address         | [Address](referral.md#address)                               | The address of the customer                          |
| Size            | string                                                        | The number of employees at the customers organization|
| Contacts        | [ParticipantUser](referral.md#participantuser)               | The contact information for an individual in the customer organization                    |



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




## <span id="Participant"></span><span id="participant"></span><span id="PARTICIPANT"></span>Participant


Describes the the referrals information for a given participant

| Property                  | Type                                                  | Description                                                           |
|---------------------------|-------------------------------------------------------|-----------------------------------------------------------------------|
| Id                        | string                                                | The ID for this participant                                           |
| CreatedDateTime           | string                                                | The date and time the participant was created                         |
| ExpirationDateTime        | string                                                | The date and time the participant referral will expire                | 
| OrganizationId            | string                                                | The unique identifier of the organization that created the participant|
| LocationId                | string                                                | The unique identifier of the location for the organization that created the participant|
| OrganizationName          | string                                                | The organization name that created the participant                    |
| Users                     | [ParticipantUser](referral.md#ParticipantUser)        | List of individuals at the customer organization                      |
| Status                    | [ParticipantStatus](referral.md#ParticipantStatus)    | Status of the participants referral                                   |
| InvitedByParticipantId    | string                                                | ParticipantId of person                                               |
| ReferralView              | link                                                  |                                                                       |

## <span id="ParticipantUser"></span><span id="participantuser"></span><span id="PARTICIPANTUSER"></span>ParticipantUser

Describes the individual participant user at an organization.

| Property                  | Type                                         | Description                                          |
|---------------------------|----------------------------------------------|------------------------------------------------------|
| TBD


## <span id="ParticipantStatus"></span><span id="participantstatus"></span><span id="PARTICIPANTSTATUS"></span>ParticipantStatus


An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the participant status.

| Value              | Position     | Description                                                                               |
|--------------------|--------------|-------------------------------------------------------------------------------------------|
| Invited            | 0            | Indicates that the participant has been invited                                           |
| Accepted           | 1            | Indicates that the participant has accepted the referral                                  |
| Rejected           | 2            | Indicates that the participant has rejected the referral                                  |
| Expired            | 3            | Indicates that the participant did not take action on the referral                        |
| Missed             | 4            | Indicates that the participant did not see the referral                                   |

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

### ServiceTypes

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

### IndustryFocus

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