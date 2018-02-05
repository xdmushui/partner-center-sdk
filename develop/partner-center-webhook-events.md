---
title: Partner Center webhook events
description: 
    Documentation for all Webhook events supported by Partner Center.
ms.assetid: 
ms.author: v-thpr
ms.date: 02/05/2018
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# Partner Center webhook events


<span class="sidebar_heading" style="font-weight: bold;">Applies
To</span>

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Partner Center Webhook events... 

## <span id="receivingEvents"></span><span id="RECEIVINGEVENTS"></span>Receiving events from Partner Center

To receive events from Partner Center, you must expose a publicly accessible endpoint; and because this endpoint is exposed, you must validate that the communication is from Partner Center. All Webhook events that you receive are digitally signed with a certificate that chains to the Microsoft Root. A link to the certificate used to sign the event will also be provided. This will allow the certificate to be renewed without you having to re-deploy or re-configure your service. Partner Center will make 10 attempts to deliver the event. If the event is still not delivered after 10 attempts, it will me moved into an offline queue and no further attempts will be made at delivery. 

The following sample shows an event posted from Partner Center.

```
POST /webhooks/callback
Content-Type: application/json
Authorization: Signature VOhcjRqA4f7u/4R29ohEzwRZibZdzfgG5/w4fHUnu8FHauBEVch8m2+5OgjLZRL33CIQpmqr2t0FsGF0UdmCR2OdY7rrAh/6QUW+u+jRUCV1s62M76jbVpTTGShmrANxnl8gz4LsbY260LAsDHufd6ab4oejerx1Ey9sFC+xwVTa+J4qGgeyIepeu4YCM0oB2RFS9rRB2F1s1OeAAPEhG7olp8B00Jss3PQrpLGOoAr5+fnQp8GOK8IdKF1/abUIyyvHxEjL76l7DVQN58pIJg4YC+pLs8pi6sTKvOdSVyCnjf+uYQWwmmWujSHfyU37j2Fzz16PJyWH41K8ZXJJkw==
X-MS-Certificate-Url: https://3psostorageacct.blob.core.windows.net/cert/pcnotifications.microsoft.com.cer
X-MS-Signature-Algorithm: rsa-sha256
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 195

{
    "EventName": "test-created",
    "ResourceUri": "http://localhost:16722/v1/webhooks/registration/test",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
} 
```

**Note** the Authorization header has a scheme of “Signature”. This is a base64 encoded signature of the content.

## <span id="AuthenticateCallback"></span><span id="authenticatecallback"></span><span id="AUTHENTICATECALLBACK"></span>How to authenticate the callback


To authenticate the callback event received from Partner Center, do the following:

1.	Verify the required headers are present (Authorization, x-ms-certificate-url, x-ms-signature-algorithm).
2.	Download the certificate used to sign the content (x-ms-certificate-url).
3.	Verify the Certificate Chain.
4.	Verify the “Organization” of the certificate.
5.	Read the content with UTF8 encoding into a buffer.
6.	Create an RSA Crypto Provider.
7.	Verify the data matches what was signed with the specified hash algorithm (e.g. SHA256).
8.	If the verification succeeds, process the message.

## <span id="EventModel"></span><span id="eventmodel"></span><span id="EVENTMODEL"></span>Event model


The following table describes the properties of a Partner Center event.

**Properties**

| Name                      | Description                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| **EventName**             | The name of the event. In the form {resource}-{action}. For example, "test-created".  |
| **ResourceUri**           | The URI of the resource that changed.                                                 |
| **ResourceName**          | The name of the resource that changed.                                                |
| **AuditUrl**              | Optional. The URI of the Audit record.                                                |
| **ResourceChangeUtcDate** | The date and time, in UTC format, when the resource change occurred.                  |


**Sample**

The following sample shows the structure of a Partner Center event.

```
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```
