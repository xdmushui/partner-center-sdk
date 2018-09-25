---
title: Partner Center webhook events
description: Documentation for all Webhook events supported by Partner Center.
ms.date: 02/14/2018
ms.localizationpriority: medium
---

# Partner Center webhook events

**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Partner Center webhook events are resource change events delivered in the form of HTTP POSTs to a registered URL. To receive an event from Partner Center, you host a callback where Partner Center can POST the event. The event is digitally signed so you can validate that it was sent from Partner Center. 

For information on how to receive events, authenticate a callback, and use the Partner Center webhook APIs to create, view, and update an event registration, see [Partner Center Webhooks](partner-center-webhooks.md).


## <span id="supportedEvents"></span><span id="SUPPORTEDEVENTS"></span>Supported Events

The following webhook events are supported by Partner Center.

### <span id="testEvent"></span><span id="TESTEVENT"></span>Test Event

This event allows you to self-onboard and test your registration by requesting a test event and then tracking its progress. You will be able to see the failure messages that are being received from Microsoft while trying to deliver the event. This will only apply to “test-created” events and data older than 7 days will be purged.

>[!NOTE]
>There is a throttle limit of 2 requests per minute when posting a test-created event.

**Properties**

| Property                  | Type                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | The name of the event. In the form {resource}-{action}. For this event, the value is "test-created".                                          |
| ResourceUri               | URI                                | The URI to get the resource. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/registration/validationEvents/{{CorrelationId}}" |
| ResourceName              | string                             | The name of the resource that will trigger the event. For this event, the value is "test".                                  |
| AuditUri                  | URI                                | (Optional) The URI to get the audit record, if it exists. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | string in the UTC date-time format | The date and time when the resource change occurred.                                                         |



**Example**

```
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{{CorrelationId}}",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```


### <span id="subscriptionUpdatedEvent"></span><span id="SUBSCRIPTIONUPDATEDEVENT"></span>Subscription Updated Event

This event is raised when the specified subscription changes. A Subscription Updated event is generated when there is an internal change in addition to when changes are made through the Partner Center API. 

>[!NOTE]
>There is a delay of up to 48 hours between the time a subscription changes and when the Subscription Updated event is triggered.  

**Properties**

| Property                  | Type                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | The name of the event. In the form {resource}-{action}. For this event, the value is "subscription-updated".                                  |
| ResourceUri               | URI                                | The URI to get the resource. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}" |
| ResourceName              | string                             | The name of the resource that will trigger the event. For this event, the value is "subscription".                          |
| AuditUri                  | URI                                | (Optional) The URI to get the audit record, if it exists. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | string in the UTC date-time format | The date and time when the resource change occurred.                                                         |



**Example**

```
{
    "EventName": "subscription-updated",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}",
    "ResourceName": "subscription",
    "AuditUri": "https://api.partnercenter.microsoft.com/v1/auditrecords/{{AuditId}}", 
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```


### <span id="thresholdExceededEvent"></span><span id="THRESHOLDEXCEEDEDEVENT"></span>Threshold Exceeded Event

This event is raised when the amount of Microsoft Azure usage for any customer exceeds their usage spending budget (their threshold). For more information, see  [Set an Azure spending budget for your customers](https://msdn.microsoft.com/partner-center/set-an-azure-spending-budget-for-your-customers).

**Properties**

| Property                  | Type                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | The name of the event. In the form {resource}-{action}. For this event, the value is "usagerecords-thresholdExceeded".                                  |
| ResourceUri               | URI                                | The URI to get the resource. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/usagerecords" |
| ResourceName              | string                             | The name of the resource that will trigger the event. For this event, the value is "usagerecords".                          |
| AuditUri                  | URI                                | (Optional) The URI to get the audit record, if it exists. Uses the syntax: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | string in the UTC date-time format | The date and time when the resource change occurred.                                                         |



**Example**

```
{
    "EventName": "usagerecords-thresholdExceeded",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/customers/usagerecords",
    "ResourceName": "usagerecords",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```



