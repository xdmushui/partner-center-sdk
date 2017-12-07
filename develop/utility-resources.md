---
title: Utility Resources
description: 
    The Partner Center REST API contains many resources which describe
    general-purpose data models used throughout the SDK.
ms.assetid: C77219B9-FFDD-4779-AE15-5B15BA7BA863
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Utility Resources


<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

The Partner Center REST API contains many resources which describe
general-purpose data models used throughout the SDK.

## <span id="address"></span><span id="ADDRESS"></span>Address


An address to use for the customer or for partner profiles. For more
information about the supported formats and properties in different
countries/regions, see [Get address formatting rules by
market](get_market_specific_validation_data.htm).

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

 

## <span id="Contact"></span><span id="contact"></span><span id="CONTACT"></span>Contact


Describes contact information for a specific individual.

| Property    | Type   | Description                  |
|-------------|--------|------------------------------|
| FirstName   | string | The contact's first name.    |
| LastName    | string | The contact's last name.     |
| Email       | string | The contact's email address. |
| PhoneNumber | string | The contact's phone number.  |

 

## <span id="FieldFilter"></span><span id="fieldfilter"></span><span id="FIELDFILTER"></span>FieldFilter


Describes a filter that can be applied to search results.

| Property | Type   | Description                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Operator | string | The filter operator: "equals", "not\_equals", "greater\_than", "greater\_than\_or\_equals", "less\_than", "less\_than\_or\_equals", "substring", "and", "or", "starts\_with", "not\_starts\_with". |

 

## <span id="FileInfo"></span><span id="fileinfo"></span><span id="FILEINFO"></span>FileInfo


Represents an external file uploaded to Partner Center.

| Property                 | Type   | Description                                   |
|--------------------------|--------|-----------------------------------------------|
| Comment                  | string | A comment associated with the file upload.    |
| FileExtension            | string | The file extension.                           |
| FileNameWithoutExtension | string | The name of the file, extension not included. |
| FileSize                 | long   | The size of the file.                         |
| Id                       | string | The unique ID for the file upload.            |

 

## <span id="Link"></span><span id="link"></span><span id="LINK"></span>Link


Contains a URI link and associated information.

| Property | Type                   | Description                        |
|----------|------------------------|------------------------------------|
| URI      | string                 | The URI.                           |
| Method   | string                 | The method represented by the URI. |
| Headers  | Array of KeyValuePairs | The headers for the link.          |

 

## <span id="PasswordProfile"></span><span id="passwordprofile"></span><span id="PASSWORDPROFILE"></span>PasswordProfile


Describes a specific password and if that password needs to be changed.

**Note**  Unsupported on Partner Center operated by 21Vianet.

 

| Property            | Type                          | Description                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Password            | [SecureString](#securestring) | The password.                                                          |
| ForceChangePassword | boolean                       | Determines if the password needs to be forcibly changed on next login. |

 

## <span id="ResourceLinks"></span><span id="resourcelinks"></span><span id="RESOURCELINKS"></span>ResourceLinks


Contains a list of links for a resource.

| Property   | Type                                      | Description                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Self       | [Link](#link)                             | The self URI.                                      |
| Next       | [Link](#link)                             | The next page of items.                            |
| Previous   | [Link](#link)                             | The previous page of items.                        |
| Attributes | [ResourceAttributes](#resourceattributes) | The metadata attributes corresponding to the user. |

 

## <span id="ResourceAttributes"></span><span id="resourceattributes"></span><span id="RESOURCEATTRIBUTES"></span>ResourceAttributes


Contains attribute metadata for a resource.

| Property   | Type   | Description                                 |
|------------|--------|---------------------------------------------|
| Etag       | string | The etag, also known as the object version. |
| ObjectType | string | The type of object of the base resource.    |

 

## <span id="SecureString"></span><span id="securestring"></span><span id="SECURESTRING"></span>SecureString


Stores secured information, such as a password.

| Property | Type | Description                       |
|----------|------|-----------------------------------|
| Length   | int  | The length of the secured string. |

 

 

 




