---
title: Partner Center REST error codes
description: 
    Partner Center REST APIs return a JSON object that contains a status
    code that indicates whether your request was successful or why it
    failed.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/PartnerCenter'
ms.assetid: 08AC1F2E-5847-4AD8-AE5B-0173C5DB589A
---

# Partner Center REST error codes


<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Partner Center REST APIs return a JSON object that contains a status
code that indicates whether your request was successful or why it
failed.

-   Success responses: A 2xx status code indicates that the client's
    request was successfully received, understood, and accepted.
-   [Error responses](#pc-error-payload)
-   Error codes
    -   [400: Bad request](#pc-error-400)
    -   [401: Unauthorized](#pc-error-401)
    -   [403: Forbidden](#pc-error-403)
    -   [404: Not found](#pc-error-404)
    -   [405: Method not allowed](#pc-error-405)
    -   [406: Not acceptable](#pc-error-406)
    -   [409: Conflict, error code](#pc-error-409)
    -   [412: Precondition failed](#pc-error-412)
    -   [429: Too many requests](#pc-error-429)
    -   [500: Internal server error](#pc-error-500)
    -   [501: Not implemented](#pc-error-501)
    -   [502: Bad gateway](#pc-error-502)
    -   [503: Service unavailable](#pc-error-503)
    -   [504: Gateway timeout](#pc-error-504)

## <span id="pc_error_payload"></span><span id="PC_ERROR_PAYLOAD"></span>Error responses


Any response with a status code indicating an error (4xx or 5xx)
includes an error message with additional details about the error
condition(s) encountered.

The following table and code sample describes the schema of an error
response.

| Name        | Type   | Description                                                                                                                                            |
|-------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| code        | string | Always returned. Indicates the kind of error that occurred. Non-null.                                                                                  |
| description | string | Always returned. Describes the error in detail, and provides additional debugging information. Non-null, non-empty. Maximum length is 1024 characters. |
| data        | array  | Only returned for some error types. A list of error objects.                                                                                           |
| source      | string | Always returned. The source of the error.                                                                                                              |

 

```
{
  "code": <string>,
  "description": <string>,
  "data": [

  ],
  "source": <string>
## }
WWW-Authenticate: OAuth realm=urn:cpsvc:cpid:{some cid}


