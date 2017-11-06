---
title: Partner Center REST error codes
description: Partner Center REST APIs return a JSON object that contains a status code that indicates whether your request was successful or why it failed.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/PartnerCenter'
ms.assetid: 08AC1F2E-5847-4AD8-AE5B-0173C5DB589A
---

# Partner Center REST error codes


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Partner Center REST APIs return a JSON object that contains a status code that indicates whether your request was successful or why it failed.

-   Success responses: A 2xx status code indicates that the client's request was successfully received, understood, and accepted.
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


Any response with a status code indicating an error (4xx or 5xx) includes an error message with additional details about the error condition(s) encountered.

The table and the code samples describe the schema of an error response.

| Name          | Type   | Description                                                                                                                                                                                                |
|---------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| code          | string | Always returned. Indicates the kind of error that occurred. Non-null, non-empty. Maximum length: 64 characters.                                                                                            |
| description   | string | Always returned. Describes the error in detail, and provides additional debugging information. Non-null, non-empty. Maximum length is 1024 characters.                                                     |
| data          | object | Only returned for some error types. A key-value object containing parameters associated with an error code. See specific error codes for the format of what is included.                                   |
| source        | string | Set to "Error" for error messages.                                                                                                                                                                         |
| other\_errors | array  | Only returned when their are multiple causes for a failure. A list of additional error objects, in which each error object includes an error\_code, message, and parameters as defined for the main error. |

 

```
{

  "code": <string>,
  "description": <string>,
  "data": <Dictionary<string,string>>,
  "Source": "Error",
  "other_errors": [
    {
      "error_code": <string>,
      "message": <string>,
      "parameters": < Dictionary<string,string>>,
    }, 
  ]
}
```

## <span id="pc_error_code_list"></span><span id="PC_ERROR_CODE_LIST"></span>Error codes


### <span id="pc_error_400"></span><span id="PC_ERROR_400"></span>

**400: Bad Request** (generic error codes)

**Description**

The 400 (Bad Request) status code means that the request could not be understood by the server due to malformed syntax, missing required properties, properties that couldn't be parsed according to their type (and length). It is a non-retryable error condition. The client should not repeat the request without modifications.

Note that extraneous properties in requests are generally completely ignored and thus not expected to be met with a 400 (Bad request) status code.

### <span id="pc_error_401"></span><span id="PC_ERROR_401"></span>

**401: Unauthorized** (user authorization error codes)

**Description**

The request requires user authentication. If the request already included Authorization credentials, then the 401 (Unauthorized) status code means that authorization has been refused for those credentials. It is a non-retryable error condition.

It's possible the call could succeed with other authorization material, making it a different request. Due to the sensitive nature of such errors, the server tends to not provide a lot of details.

When appropriate (missing or incorrect header), the server could return the following WWW-Authenticate response header to the client, giving it a hint about what the server needs:

```
WWW-Authenticate: OAuth realm=urn:cpsvc:cpid:{some cid}
```

### <span id="pc_error_403"></span><span id="PC_ERROR_403"></span>

**403: Forbidden**

**Description**

The client was not authorized to make the request. This is a non-retryable error condition.

### <span id="pc_error_404"></span><span id="PC_ERROR_404"></span>

**404: Not found**

**Description**

The server has not found anything matching the request URI. No indication is given of whether the condition is temporary or permanent. This status code is commonly used when the server does not wish to reveal exactly why the request has been refused, or when no other response is applicable.

This status code also applies to cases where request properties are Ids or URIs that do not map to known objects/resources, for example a syntactically correct offer id/URI.

This is a non-retryable error condition.

### <span id="pc_error_405"></span><span id="PC_ERROR_405"></span>

**405: Method not allowed**

**Description**

The method specified in the request is not allowed for the resource identified by the URI. For example, PUT on a resource that only support GET and POST. This is a non-retryable error condition.

See the Allow header in the response for a list of valid methods for the requested resource.

### <span id="pc_error_406"></span><span id="PC_ERROR_406"></span>

**406: Not acceptable**

**Description**

The client specified a media type (in the accept header of the request) that the server does not currently handle. This is a non-retryable error condition.

### <span id="pc_error_409"></span><span id="PC_ERROR_409"></span>

**409: Conflict**

**Description**

The request could not be completed due to a conflict with the current state of the resource. It is used in situations where it is expected that the user might be able to resolve the conflict and resubmit the new request. This is a non-retryable error condition (i.e. the request should not be submitted again as is).

### <span id="pc_error_410"></span><span id="PC_ERROR_410"></span>

**410: Gone**

**Description**

The requested resource existed but is no longer available at the server and no forwarding address is known. This condition is expected to be permanent. This is a non-retryable error condition.

### <span id="pc_error_412"></span><span id="PC_ERROR_412"></span>

**412: Precondition failed**

**Description**

A precondition in one or more of the request headers evaluated to false when it was tested on the server. This status code allows the client to place preconditions on the current resource meta-information (header field data) and thus prevent the requested method from being applied to a resource other than the one intended. For example, it is used when optimistic concurrency detection is implemented using an If-Match header. This is a non-retryable error condition.

### <span id="pc_error_429"></span><span id="PC_ERROR_429"></span>

**429: Too many requests**

**Description**

The client has sent too many requests in a given amount of time (due to rate limiting). The response representations should include details explaining the condition, and may include a Retry-After header indicating how long to wait before making a new request. This is a retryable error condition.

### <span id="pc_error_500"></span><span id="PC_ERROR_500"></span>

**500: Internal server error**

**Description**

The server encountered an unexpected condition which prevented it from fulfilling the request. This is a non-retryable error condition.

### <span id="pc_error_501"></span><span id="PC_ERROR_501"></span>

**501: Not implemented**

**Description**

The request was meaningful but the server does not support the functionality required to fulfill it. This is a non-retryable error condition.

### <span id="pc_error_502"></span><span id="PC_ERROR_502"></span>

**502: Bad gateway**

**Description**

The server acting as a gateway or proxy received an incorrect response from the upstream server it accessed in attempting to fulfill the request. This is a non-retryable error condition.

### <span id="pc_error_503"></span><span id="PC_ERROR_503"></span>

**503: Service unavailable**

**Description**

The server is currently unable to handle the request due to temporary overloading or maintenance of an underlying server. The implication is that this is a temporary condition which will be alleviated after some delay. If known, the length of the delay may be indicated in a Retry-After header, in which case it is a retryable error condition. If no Retry-After is given, the client should handle the response as it would for a 500 (Internal Server Error) response.

### <span id="pc_error_504"></span><span id="PC_ERROR_504"></span>

**504: Gateway timeout**

**Description**

The server acting as a gateway or proxy is currently unable to handle the request due to a temporary overloading or maintenance of an underlying server. The implication is that this is a temporary condition which will be alleviated after some delay. If known, the length of the delay may be indicated in a Retry-After header, in which case it is a retryable error condition. If no Retry-After is given, the client should handle the response as it would for a 500 (Internal Server Error) response.

 

 




