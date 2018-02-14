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

Partner Center Webhook events are resource change events delivered in the form of HTTP POSTs to a registered URL. To receive an event from Partner Center, you host a callback where Partner Center can POST the event. The event is digitally signed so you can validate that it was sent from Partner Center. 

For information on how to receive events, authenticate a callback, and use the Partner Center APIs to create, view, and update an event registration, see [Partner Center Webhooks](partner-center-webhooks.md).


## <span id="supportedEvents"></span><span id="SUPPORTEDEVENTS"></span>Supported Events

The following webhook events are supported by Partner Center.

### <span id="testEvent"></span><span id="TESTEVENT"></span>Test Event

This event allows you to self-onboard and test your registration by requesting a test event and then tracking its progress. You will be able to see the failure messages that are being received from Microsoft while trying to deliver the event. This will only apply to “test-created” events and data older than 7 days will be purged.

**Properties**

| Name                      | Description                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| **EventName**             | test-created|
| **ResourceUri**           | "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f"                                                 |
| **ResourceName**          | test                                                |   


**Sample**

```
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <span id="subscriptionUpdatedEvent"></span><span id="SUBSCRIPTIONUPDATEDEVENT"></span>Subscription Updated Event

This event is raised when the subscription changes. These events will be generated when there is an internal change in addition to when changes are made through the Partner Center API. 

**Properties**

| Name                      | Description                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| **EventName**             | subscription-updated                                                                  |
| **ResourceUri**           | "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f"                                                 |
| **ResourceName**          | subscription                                                |   


**Sample**

```
{
    "EventName": "subscription-updated",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/",
    "ResourceName": "subscription",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```



