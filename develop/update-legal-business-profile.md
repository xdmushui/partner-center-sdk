---
title: Update the partner legal business profile
description: How to update the partner legal business profile.
ms.assetid: DEB60680-145D-47C5-BB19-374752D45236
ms.author: mhopkins
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Update the partner legal business profile


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

How to update the partner legal business profile.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.

## <span id="C_"></span><span id="c_"></span>C#


To update the partner legal business profile, first instantiate a **LegalBusinessProfile** object and populate it with the existing profile. For more information, see [Get the partner legal business profile](get-legal-business-profile.md). Then, update the properties that you need to change. The following code example illustrates changing the address and primary contact phone numbers.

Next, get an interface to the partner profile operations collection from the **IAggregatePartner.Profiles** property. Then, retrieve the value of the **LegalBusinessProfile** property to get an interface to legal business profile operations. Finally, call the [**Update**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) or [**UpdateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) method with the changed object to update the profile.

``` csharp
// IAggregatePartner partnerOperations;

var legalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();

// Change the address and primary contact phone number. 
legalBusinessProfile.Address.PhoneNumber = "4255550110";
legalBusinessProfile.PrimaryContact.PhoneNumber = "4255550110";

// Apply changes to the profile.
var updatedLegalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Update(legalBusinessProfile);
```

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request


**Request syntax**

| Method  | Request URI                                                                    |
|---------|--------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1 |

 

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

The legal business profile resource.

**Request example**

```
PUT https://api.partnercenter.microsoft.com/v1/profiles/legalbusiness HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4549ac0c-0f1d-4d8f-b02f-6d36fadcccee
MS-CorrelationId: aa2a0d8c-7a41-470f-97ae-b82e6c338ee4
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 806
Expect: 100-continue

{
    "CompanyName": "Lucerne Publishing",
    "Address": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "123 Main Street",
        "AddressLine2": "",
        "PostalCode": "98052",
        "FirstName": "Gena",
        "LastName": "Soto",
        "PhoneNumber": "4255550110"
    },
    "PrimaryContact": {
        "FirstName": "Gena",
        "LastName": "Soto",
        "Email": "gena@lucernepublishing.com",
        "PhoneNumber": "4255550110"
    },
    "CompanyApproverAddress": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "123 Main Street",
        "AddressLine2": "",
        "PostalCode": "98052",
        "FirstName": null,
        "LastName": null,
        "PhoneNumber": null
    },
    "CompanyApproverEmail": "gena@lucernepublishing.com",
    "VettingStatus": "authorized",
    "VettingSubStatus": "none",
    "Links": {
        "Self": {
            "Uri": "/profiles/legalbusiness",
            "Method": "GET",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "LegalBusinessProfile"
    }
}
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, the response body contains the updated **LegalBusinessProfile**

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center error codes](error-codes.md).

**Response example**

``` json
HTTP/1.1 200 OK
Content-Length: 1157
Content-Type: application/json; charset=utf-8
MS-CorrelationId: aa2a0d8c-7a41-470f-97ae-b82e6c338ee4
MS-RequestId: 4549ac0c-0f1d-4d8f-b02f-6d36fadcccee
MS-CV: KZLU42qJ4EObO75q.0
MS-ServerId: 030020643
Date: Tue, 21 Mar 2017 22:03:15 GMT

﻿ {
    "companyName": "Lucerne Publishing",
    "address": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052",
        "firstName": "Gena",
        "lastName": "Soto",
        "phoneNumber": "4255550110"
    },
    "primaryContact": {
        "firstName": "Gena",
        "lastName": "Soto",
        "email": "gena@lucernepublishing.com",
        "phoneNumber": "4255550110"
    },
    "companyApproverAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052"
    },
    "companyApproverEmail": "gena@lucernepublishing.com",
    "vettingStatus": "authorized",
    "vettingSubStatus": "none",
    "profileType": "LegalBusinessProfile",
    "links": {
        "self": {
            "uri": "/profiles/legalbusiness",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "LegalBusinessProfile"
    }
}
```

 

 




