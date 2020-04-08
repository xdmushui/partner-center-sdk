---
title: Utility resources
description: The Partner Center REST API contains many resources which describe general-purpose data models used throughout the SDK.
ms.assetid: C77219B9-FFDD-4779-AE15-5B15BA7BA863
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Utility resources


**Applies To**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

The Partner Center REST API contains many resources which describe
general-purpose data models used throughout the SDK.


## <span id="address"/><span id="ADDRESS"/>Address

An address to use for the customer or for partner profiles. For more
information about the supported formats and properties in different
countries/regions, see [Get address formatting rules by
market](get-market-specific-validation-data.md).

| Property     | Type   | Length (min, max) | Description                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | string | (1, 200)          | The first line of the address.                                                                   |
| AddressLine2 | string | (0, 200)          | The second line of the address. This property is optional.                                       |
| City         | string | n/a               | The city.                                                                                        |
| State        | string | (0, 2)            | The state.                                                                                       |
| PostalCode   | string | n/a               | The ZIP code or postal code.                                                                     |
| Country      | string | (2, 2)            | The country/region in ISO country code format.                                                   |
| Region       | string | n/a               | The region.                                                                                      |
| FirstName    | string | (1, 50)           | The first name of a contact at the customer's company/organization.                              |
| LastName     | string | (1, 50)           | The last name of a contact at the customer's company/organization.                               |
| PhoneNumber  | string | n/a               | The phone number of a contact at the customer's company/organization. This property is optional. |
 

## <span id="Contact"/><span id="contact"/><span id="CONTACT"/>Contact

Describes contact information for a specific individual.

| Property    | Type   | Description                  |
|-------------|--------|------------------------------|
| FirstName   | string | The contact's first name.    |
| LastName    | string | The contact's last name.     |
| Email       | string | The contact's email address. |
| PhoneNumber | string | The contact's phone number.  |
 

## <span id="FieldFilter"/><span id="fieldfilter"/><span id="FIELDFILTER"/>FieldFilter

Describes a filter that can be applied to search results.

| Property | Type   | Description                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Operator | string | The filter operator: "equals", "not\_equals", "greater\_than", "greater\_than\_or\_equals", "less\_than", "less\_than\_or\_equals", "substring", "and", "or", "starts\_with", "not\_starts\_with". |
 

## <span id="FileInfo"/><span id="fileinfo"/><span id="FILEINFO"/>FileInfo

Represents an external file uploaded to Partner Center.

| Property                 | Type   | Description                                   |
|--------------------------|--------|-----------------------------------------------|
| Comment                  | string | A comment associated with the file upload.    |
| FileExtension            | string | The file extension.                           |
| FileNameWithoutExtension | string | The name of the file, extension not included. |
| FileSize                 | long   | The size of the file.                         |
| Id                       | string | The unique ID for the file upload.            |
 

## <span id="Link"/><span id="link"/><span id="LINK"/>Link

Contains a URI link and associated information.

| Property | Type                   | Description                        |
|----------|------------------------|------------------------------------|
| URI      | string                 | The URI.                           |
| Method   | string                 | The method represented by the URI. |
| Headers  | Array of KeyValuePairs | The headers for the link.          |
 

## <span id="PasswordProfile"/><span id="passwordprofile"/><span id="PASSWORDPROFILE"/>PasswordProfile

Describes a specific password and if that password needs to be changed.

>[!NOTE]
>Unsupported on Partner Center operated by 21Vianet.

| Property            | Type                          | Description                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Password            | [SecureString](#securestring) | The password.                                                          |
| ForceChangePassword | boolean                       | Determines if the password needs to be forcibly changed on next login. |
 

## <span id="ResourceLinks"/><span id="resourcelinks"/><span id="RESOURCELINKS"/>ResourceLinks

Contains a list of links for a resource.

| Property   | Type                                      | Description                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Self       | [Link](#link)                             | The self URI.                                      |
| Next       | [Link](#link)                             | The next page of items.                            |
| Previous   | [Link](#link)                             | The previous page of items.                        |
| Attributes | [ResourceAttributes](#resourceattributes) | The metadata attributes corresponding to the user. |
 

## <span id="ResourceAttributes"/><span id="resourceattributes"/><span id="RESOURCEATTRIBUTES"/>ResourceAttributes

Contains attribute metadata for a resource.

| Property   | Type   | Description                                 |
|------------|--------|---------------------------------------------|
| Etag       | string | The etag, also known as the object version. |
| ObjectType | string | The type of object of the base resource.    |
 

## <span id="SecureString"/><span id="securestring"/><span id="SECURESTRING"/>SecureString

Stores secured information, such as a password.

| Property | Type | Description                       |
|----------|------|-----------------------------------|
| Length   | int  | The length of the secured string. |


## <span id="ValidationCode"/><span id="validationcode"/><span id="VALIDATIONCODE"/>ValidationCode

Represents a partner's Government Community Cloud validation code.

| Property         | Type         | Description                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| PartnerId        | GUID         | Partner identifier                                                       |
| OrganizationName | string       | The organization name provided during the validation process             |
| ValidationId     | int          | A unique identifier for validation                                       |
| MaxCreates       | nullable int | The maximum customers allowed to be created with this validation code    |
| RemainingCreates | nullable int | Remaining customer creates under this validation ID                      |
| ETag             | string       | The specific version of this resource. Changes when resource is changed. |
