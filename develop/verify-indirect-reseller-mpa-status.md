---
title: Verify an indirect reseller's Microsoft Partner Agreement signing status
description: You can use the AgreementStatus API to verify whether an indirect reseller has signed the Microsoft Partner Agreement.
ms.date: 10/30/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-csp
ms.localizationpriority: medium
---

# Verify an indirect reseller's Microsoft Partner Agreement signing status

Applies to:

* Partner Center
* Partner Center for Microsoft Cloud for US Government

You can verify whether an indirect reseller has signed the Microsoft Partner Agreement using their Microsoft Partner Network (MPN) ID or Cloud Solution Provider (CSP) tenant ID (Microsoft ID). You can use one of these identifiers to check the Microsoft Partner Agreement signing status using the **AgreementStatus** API.

## Prerequisites

* Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
* The MPN ID or the CSP tenant ID (Microsoft ID) of the indirect reseller. *You must use one of these two identifiers.*

## <span id="C_"/><span id="c_"/>C#

To get the Microsoft Partner Agreement signature status of an indirect reseller, use your **IAggregatePartner.Compliance** collection and call the **AgreementSignatureStatus** property. Finally, call the [**Get()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) or [**GetAsync()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) methods.

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

**Sample**: [Console test app](console-test-app.md). **Project**:PartnerCenterSDK.FeaturesSamples **Class**: GetAgreementSignatureStatus.cs

## REST

### REST request

#### Request syntax

| Method | Request URI |
| ------ | ----------- |
| **GET** | *[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId} |

##### URI parameters

You must provide one of the following two query parameters to identify the partner. If you don't provide one of these two query parameters, you will receive a **400 (Bad request)** error.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| **MpnId** | int | No | A Microsoft Partner Network ID that identifies the indirect reseller. |
| **TenantId** | GUID | No | A Microsoft ID that identifies the CSP account of the indirect reseller. |

#### Request headers

For more information, see [Partner Center REST headers](https://docs.microsoft.com/en-us/partner-center/develop/headers).

#### Request examples

##### Request using MPN ID

The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's Microsoft Partner Network ID.

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

##### Request using CSP tenant ID

The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's CSP tenant ID (Microsoft ID).

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### REST response

#### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](https://docs.microsoft.com/en-us/partner-center/develop/error-codes).

#### Response example (success)

The following example response successfully returns whether the indirect reseller has signed the Microsoft Partner Agreement.

```http
HTTP/1.1 200 OK
Content-Length: 29
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: jn3r+1wpE06nCt/0.0
MS-ServerId: 0000005B
Date: Tue, 15 Oct 2019 12:44:34 GMT
Connection: close
{
    "isAgreementSigned": true
}
```

#### Response examples (failure)

You may receive responses similar to the following examples when the signing status of the indirect reseller's Microsoft Partner Agreement can't be returned.

##### Non-GUID formatted CSP tenant ID

The following example response is returned when the CSP tenant ID that you passed to the API is not a GUID.

```http
HTTP/1.1 400 Bad Request
Content-Length: 105
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: rbuZl5lbAkyq8WGK.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 08:55:23 GMT
Connection: close
{
    "code": 2000,
    "description": "Tenant Id must be a GUID.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

##### Non-numeric MPN ID

The following example response is returned when the MPN ID that you passed to the API is non-numeric.

```http
HTTP/1.1 400 Bad Request
Content-Length: 103
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: cP5JiS4sv0GJxlJ9.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 08:58:45 GMT
Connection: close
{
    "code": 2000,
    "description": "MPN Id must be numeric.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

##### No MPN ID or CSP tenant ID

The following example response is returned when you haven't passed an MPN ID or CSP tenant ID to the API. You must pass one of the two ID types to the API.

```http
HTTP/1.1 400 Bad Request
Content-Length: 114
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: hEV736v4qk6joDMR.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 09:00:30 GMT
Connection: close
{
    "code": 2001,
    "description": "Both MPN Id and Tenant Id cannot be empty.",
    "data": [],
    "source": "ComplianceController"
}
```

##### Both MPN ID and CSP tenant ID passed

The following example response is returned when you pass both the MPN ID and CSP tenant ID to the API. You must pass *only one* of the two identifier types to the API.

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2000,
    "description": "Both MPN Id and Tenant Id should not be passed.",
    "data": [],
    "source": "ComplianceController"
}
```
