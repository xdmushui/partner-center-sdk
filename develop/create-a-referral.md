---
title: Create a referral
description: How to create a referral
ms.assetid: 
ms.author: mhopkins
ms.date: 10/01/18
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
ms.localizationpriority: medium
---

# Create a referral


**Applies To**

-   Partner Center


How to create a referral

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
-   A customer identifier. If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.


## <span id="C_"></span><span id="c_"></span>C#


To do: Describe in english how to create a referral


``` csharp
<to do>
```

## <span id="REST_Request"></span><span id="rest_request"></span><span id="REST_REQUEST"></span>REST Request


**Request syntax**

| Method   | Request URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v2/referrals/                                                    |

 
**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

This table describes the [Referral](referral.md) properties in the request body.

| Property              | Type                                              | Description                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Status                | [ReferralStatus](referral.md#ReferralStatus)     | An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the referral status. |
| ReferralSource        | [ReferralSource](referral.md#ReferralSource)     | An [Enum](https://docs.microsoft.com/en-us/dotnet/api/system.enum) with values that indicate the referral source. |
| CustomerProfile       | [CustomerProfile](referral.md#CustomerProfile)   | Customer contact information                                                                                      |
| Details               | [ReferralDetails](referral.md#ReferralDetails)   | Customer details, notes, deal value, closing date                                                                 |
| Participants          | [Participant](referral.md#Participant)           | Represents the customer interest in Industry, Products, Services, Solutions                                       |


**Request example**

```json
POST https://api.partner.microsoft.com/v2/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json
{
	"Referral" : {
		"ReferralSource":"",
		"CustomerProfile": {
	        "Name": "Contoso Corporation",
	        "Address": {
	            "AddressLine1": "1 Contoso Way",
	            "AddressLine2": "Suite 200",
	            "City": "Redmond",
	            "State": "WA",
	            "Region": "PNW",
	            "Country": "US",
	            "PostalCode": "98052"
	        }
        },
        "Details": {
		    "Notes": "",
	        "DealValue": "",
	        "ClosingDate": "",
	        "Requirements": {
		        "IndustryFocus": "",
                "Products": "",
		        "ServiceTypes": "",
		        "Solutions": ""		        
	        }
	    },
        "Participants": {
            "OrganizationName": "",
            "Users": {

            }
        }
	}
}
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response

If successful, this API returns a [Referral](referral.md) resource. Save the Referral ID for future use with the Partner Center SDK.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

``` json
<to do>
```

 

 




