---
title: Partner Center REST headers
description: 
    The following HTTP request and response headers are supported by the
    Partner Center REST API.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/PartnerCenter'
ms.assetid: 38A43A4C-EC31-4554-A747-0DC04B77CB99
---

# Partner Center REST headers


<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

The following HTTP request and response headers are supported by the
Partner Center REST API. Not all API calls accept all headers.

## <span id="Request_headers"></span><span id="request_headers"></span><span id="REQUEST_HEADERS"></span>Request headers


The following HTTP request headers are supported by the Partner Center
REST API.

| Header                       | Description                                                                                                                                                                                                                                                                            | Value Type |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Authorization:               | Required. The authorization token in the form Bearer &lt;token&gt;.                                                                                                                                                                                                                    | string     |
| Accept:                      | Specifies the request and response type, "application/json".                                                                                                                                                                                                                           | string     |
| MS-RequestId:                | A unique identifier for the call, used to ensure idempotency. In the case of a timeout, the retry call should include the same value. Upon receiving a response (success or business failure), the value should be reset for the next call.                                            | guid       |
| MS-CorrelationId:            | A unique identifier for the call, useful in logs and network traces for troubleshooting errors. The value should be reset for every call. All operations should include this header. For more information, see the Correlation ID information in [Test and debug](test-and-debug.md). | guid       |
| MS-Contract-Version:         | Required. Specifies the version of the API requested; generally api-version: v1 unless otherwise specified in the [Scenarios](scenarios.md) section.                                                                                                                                  | string     |
| If-Match:                    | Used for concurrency control. Some API calls require passing the ETag via the If-Match header. The ETag is usually on the resource and therefore, requires GET-ting the latest. For more information, see the ETag information in [Test and debug](test-and-debug.md).                | string     |
| MS-PartnerCenter-Application | Optional. Specifies the name of the application that is using the Partner Center REST API.                                                                                                                                                                                             | string     |
| X-Locale:                    | Optional. Specifies the language in which the rates are returned. Default is "en-US".                                                                                                                                                                                                  | string     |

 

## <span id="Response_headers"></span><span id="response_headers"></span><span id="RESPONSE_HEADERS"></span>Response headers


The following HTTP response headers may be returned by the Partner
Center REST API.

| Header            | Description                                                                                                                                                                                                                                 | Value Type |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Accept:           | Specifies the request and response type, "application/json".                                                                                                                                                                                | string     |
| MS-RequestId:     | A unique identifier for the call, used to ensure idempotency. In the case of a timeout, the retry call should include the same value. Upon receiving a response (success or business failure), the value should be reset for the next call. | guid       |
| MS-CorrelationId: | A unique identifier for the call, useful the logs and network traces for troubleshooting errors. The value should be reset for every call. All operations should include this header.                                                       | guid       |

 

 

 




