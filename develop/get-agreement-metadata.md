---
title: Get agreement metadata for Microsoft Cloud Agreement
description: This topic explains how to get agreement metadata for Microsoft Cloud Agreement. 
ms.date: 9/21/2018
ms.localizationpriority: medium
---

# Get agreement metadata for Microsoft Cloud Agreement


**Applies To**

-   Partner Center

> [!NOTE]  
> The **AgreementMetaData** resource is currently supported by Partner Center in the Microsoft public cloud only. It is not applicable to:
> -   Partner Center operated by 21Vianet
> -   Partner Center for Microsoft Cloud Germany
> -   Partner Center for Microsoft Cloud for US Government


## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites

 - If you are using Partner Center SDK, version 1.9 or newer is required. 
 - Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario supports authentication with App+User credentials only. 

## <span id="Examples"></span><span id="examples"><span id="EXAMPLES"></span>Examples

### C#

To retrieve agreement metadata for Microsoft Cloud Agreement, first retrieve the **IAggregatePartner.AgreementDetails** collection and then call the **Get** or **GetAsync** methods. Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

### Java

To retrieve agreement metadata for Microsoft Cloud Agreement, first call the **IAggregatePartner.getAgreementDetails** function and then call the **get** function. Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:

```java
// IAggregatePartner partnerOperations;

ResourceCollection<AgreementMetaData> agreements = partnerOperations.getAgreements().get();

AgreementMetaData microsoftCloudAgreement;

for (AgreementMetaData metadata : agreements) 
{
    if(metadata.getAgreementType() == AgreementType.MicrosoftCloudAgreement)
    {
        microsoftCloudAgreement = metadata;
    }
}
```

### PowerShell

To retrieve agreement metadata for Microsoft Cloud Agreement, execute the [**Get-PartnerAgreementDetail**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAgreementDetail.md) command. Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <span id="_Request"></span><span id="_request"></span><span id="_REQUEST"></span>REST Request

To retrieve agreement metadata for Microsoft Cloud Agreement, first create a REST Request to retrieve the **AgreementMetaData** collection. Then search for the item in the collection which corresponds to the Microsoft Cloud Agreement.

**Request syntax**

| Method | Request URI                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1 |


**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.


**Request body**

None.


**Request example**

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```


## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>REST Response

If successful, this method returns a collection of **AgreementMetaData** resources in the response body.


**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 1,
    "items": [
        {
            "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
            "agreementType": "MicrosoftCloudAgreement",
            "agreementLink": "https://docs.microsoft.com/partner-center/agreements",
            "versionRank": 0
        }
    ],
    "links": {
        "self": {
            "uri": "/agreements",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

To identify the resource in the response which corresponds to the Microsoft Cloud Agreement, look for the resource whose **agreementType** property has value "MicrosoftCloudAgreement".