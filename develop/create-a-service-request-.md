---
title: Create a service request
description: How to create a partner center service request.
ms.assetid: 16DA9836-7052-4103-82D4-933E5EEB7E71
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Create a service request


**Applies To**

-   Partner Center
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

How to create a partner center service request.

## <span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>Prerequisites


-   Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials only.
-   A support topic ID. If you do not have a support topic ID, see [Get service request support topics](get-service-request-support-topics--pending-.md).

## <span id="C_"></span><span id="c_"></span>C#


To create a service request, first create and populate a [**ServiceRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object with the title, description, severity and support topic id. Then call the [**IAggregatePartner.ServiceRequests.Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.ipartnerservicerequestcollection.create) method, passing it the newly created ServiceRequest object and a string containing the Agent Locale.

```CSharp
// IAggregatePartner partnerOperations;
// string supportTopicId;

ServiceRequest serviceRequestToCreate = new ServiceRequest()
{
    Title = "TrialSR",
    Description = "Ignore this SR",
    Severity = ServiceRequestSeverity.Critical,
    SupportTopicId = supportTopicId
};

ServiceRequest serviceRequest = partnerOperations.ServiceRequests.Create(serviceRequestToCreate, "en-US");
```

**Sample**: [Console test app](console-test-app.md). **Project**: Partner Center SDK Samples **Class**: CreatePartnerServiceRequest.cs

## <span id="Request"></span><span id="request"></span><span id="REQUEST"></span>Request


**Request syntax**

| Method   | Request URI                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{agent-locale} HTTP/1.1 |

 

**URI parameter**

Use the following URI parameter to identify the agent locale.

| Name             | Type       | Required | Description                                                  |
|------------------|------------|----------|--------------------------------------------------------------|
| **agent-locale** | **string** | Y        | The locale of the organization creating the service request. |

 

**Request headers**

-   See [Partner Center REST headers](headers.md) for more information.

**Request body**

This table describes the required and optional properties in the request body.

| Name             | Type                                                                        | Required | Description                                                                          |
|------------------|-----------------------------------------------------------------------------|----------|--------------------------------------------------------------------------------------|
| Title            | string                                                                      | Y        | The service request title.                                                           |
| Description      | string                                                                      | Y        | The description.                                                                     |
| Severity         | string                                                                      | Y        | The severity: "unknown", "critical", "moderate", or "minimal".                       |
| SupportTopicId   | string                                                                      | Y        | The id of the support topic.                                                         |
| SupportTopicName | string                                                                      | N        | The name of the support topic.                                                       |
| Id               | string                                                                      | N        | The id of the service request.                                                       |
| Status           | string                                                                      | N        | The status of the service request: "none", "open", "closed", or "attention\_needed". |
| Organization     | [ServiceRequestOrganization](servicerequest.md#servicerequestorganization) | N        | Organization for which the service request is created.                               |
| PrimaryContact   | [ServiceRequestContact](servicerequest.md#servicerequestcontact)           | N        | Primary Contact on the service request.                                              |
| LastUpdatedBy    | [ServiceRequestContact](servicerequest.md#servicerequestcontact)           | N        | "Last Updated By" contact for changes to the service request.                        |
| ProductName      | string                                                                      | N        | The name of the product that corresponds to the service request.                     |
| ProductId        | string                                                                      | N        | The id of the product.                                                               |
| CreatedDate      | date                                                                        | N        | The date of the service request's creation.                                          |
| LastModifiedDate | date                                                                        | N        | The date that the service request was last modified.                                 |
| LastClosedDate   | date                                                                        | N        | The date that the service request was last closed.                                   |
| FileLinks        | array of [FileInfo](utility-resources.md#fileinfo) resources               | N        | The collection of File Links that pertain to the service request.                    |
| NewNote          | [ServiceRequestNote](servicerequest.md#servicerequestnote)                 | N        | A note can be added to an existing service request.                                  |
| Notes            | array of [ServiceRequestNotes](servicerequest.md#servicerequestnote)       | N        | A collection of notes added to the service request.                                  |
| CountryCode      | string                                                                      | N        | The country corresponding to the service request.                                    |
| Attributes       | object                                                                      | N        | Contains "ObjectType": "ServiceRequest".                                             |

 

This table describes the required properties in the request body.
**Request example**

```
POST https://api.partnercenter.microsoft.com/v1/servicerequests/en-US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 55f86bfb-d3bb-4fe4-9f01-2fdaef11a81f
MS-CorrelationId: ae43859b-591d-47ea-9fd1-028b4c799118
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 474
Expect: 100-continue

{
    "Id": null,
    "Title": "TrialSR",
    "Description": "Ignore this SR",
    "Severity": "critical",
    "SupportTopicId": "32444671",
    "SupportTopicName": null,
    "Status": "none",
    "Organization": null,
    "PrimaryContact": null,
    "LastUpdatedBy": null,
    "ProductName": null,
    "ProductId": null,
    "CreatedDate": "0001-01-01T00:00:00",
    "LastModifiedDate": "0001-01-01T00:00:00",
    "LastClosedDate": "0001-01-01T00:00:00",
    "NewNote": null,
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <span id="Response"></span><span id="response"></span><span id="RESPONSE"></span>Response


If successful, this method returns the **Service Request** resource properties in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

```
HTTP/1.1 201 Created
Content-Length: 721
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae43859b-591d-47ea-9fd1-028b4c799118
MS-RequestId: 55f86bfb-d3bb-4fe4-9f01-2fdaef11a81f
MS-CV: vB9EuWs/ukaxQmuV.0
MS-ServerId: 101112616
Date: Thu, 22 Dec 2016 20:31:14 GMT

﻿{
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "id": "616122292874576",
    "status": "none",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1",
        "phoneNumber": "2398391056"
    },
    "primaryContact": {
        "organization": {
            "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "name": "TEST_TEST_BugBash1",
            "phoneNumber": "2398391056"
        },
        "contactId": "bb4ebcf5-d84c-4b35-8469-f4cfa4ac909e",
        "lastName": "Account",
        "email": "admin@testtestbugbash1.onmicrosoft.com",
        "phoneNumber": "2066017143"
    },
    "createdDate": "0001-01-01T00:00:00",
    "lastModifiedDate": "0001-01-01T00:00:00",
    "lastClosedDate": "0001-01-01T00:00:00",
    "countryCode": "US",
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```

 

 




