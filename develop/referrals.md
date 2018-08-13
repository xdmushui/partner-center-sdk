---
title: Referrals
description: Resources that represents a sales lead direct from customer or Microsoft.  
ms.author: mhopkins
ms.date: 09/03/2018
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
ms.localizationpriority: medium
---

# Referrals


**Applies To**

-   Partner Center

Resources that represents a sales lead direct from customer or Microsoft.  


## <span id="Referral"></span><span id="referral"></span><span id="REFERRAL"></span>Referral


Represents the referral.

| Property              | Type                            | Description                                                                          |
|-----------------------|---------------------------------|--------------------------------------------------------------------------------------|
| id                    | string                          | The ID for this Referral.                                                            |
| CreatedDate           | string in UTC date time format  | The date the referral was created.                                                   |
| UpdatedDate           | string in UTC date time format                            | The date the referral was last updated.                     |
| Status                | [ReferralStatus](referrals.md#ReferralStatus)             |                                                             |
| ReferralSource        | [ReferralSource](referrals.md#ReferralSource)             |                                                             |
| CustomerProfile       | [CustomerProfile](referrals.md#CustomerProfile)           |                                                             |
| CustomerRequirements  | [CustomerRequirements](referrals.md#CustomerRequirements) |                                                             |
| AdditionalInformation |                                                           |                                                             |
| Activities            |                                                           |                                                             |
| Participants          | [Participants](referrals.md#Participants)                 |                                                             |


## <span id="ReferralStatus"></span><span id="referralstatus"></span><span id="REFERRALSTATUS"></span>ReferralStatus


An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the referral status.

| Value              | Position     | Description                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Pending            | 0            |                                                                            |
| Active             | 1            |                                      |
| Won                | 2            |                           |
| Lost               | 3            |      |
 

## <span id="ReferralSource"></span><span id="referralsource"></span><span id="REFERRALSOURCE"></span>ReferralSource


An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the referral source.

| Value              | Position     | Description                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| WebDirect          | 0            |                                                                            |
| PartnerLed         | 1            |                                      |
| AgentLed           | 2            |                           |
| P2P                | 3            |      |
 


## <span id="CustomerProfile"></span><span id="customerprofile"></span><span id="CUSTOMERPROFILE"></span>CustomerProfile


Contains the customer contact information

| Property        | Type                                                          | Description                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| Id              | string                                                        | The Id for this CustomerProfile                      |
| Name            | string                                                        | The customer first and last name                     |
| Address         | [Address](referrals.md#address)                               | The address of the customer                          |
| Contact         | [Contact](referrals.md#contact)                               | The customer contact information                     |


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
| Email       | string | The contact's email address. |
| PhoneNumber | string | The contact's phone number.  |


## <span id="CustomerRequirements"></span><span id="customerrequirements"></span><span id="CUSTOMERREQUIREMENTS"></span>CustomerRequirements


Contains the customer requirements

| Property        | Type                                                          | Description                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| Industries      | list?                                                         | The industries the customer is in                    |
| Products        | list?                                                         | The products the customer is interested in           |
| Services        | list?                                                         | The services the customer is interested in           |
| Solutions       | string                                                        |                                                      |
| CustomerNeed    | string                                                        |                                                      |


## <span id="Participant"></span><span id="participant"></span><span id="PARTICIPANT"></span>Participant


Describes the referral participant information.

| Property                  | Type                                                          | Description                                          |
|---------------------------|----------------------------------------------|------------------------------------------------------|
| Id                        | string                                                        |                                                      |
| OrganizationId            | string                                                        |                                                      |
| Users                     |                                                          |                                                      |
| InvitedByParticipantId    |                                         |                                                      |
| ReferralActivities        | link?                                       |                                                      |
| ReferralView              | link?                                       |                                                      |
| Status                    | [ParticipantStatus](referrals.md#ParticipantStatus) |                                                    |

## <span id="ParticipantStatus"></span><span id="participantstatus"></span><span id="PARTICIPANTSTATUS"></span>ParticipantStatus


An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the participant status.

| Value              | Position     | Description                                                                               |
|--------------------|--------------|-------------------------------------------------------------------------------------------|
| Invited            | 0            |                                                                                           |
| Accepted           | 1            |                                                                                           |
| Rejected           | 2            |                           |
| Expired            | 3            |      |
| Missed             | 3            |      |