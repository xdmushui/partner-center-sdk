---
title: ServiceRequest
description: 
    Partners can file service requests on behalf of their partners to report
    disruptions services provided by Microsoft or to request other technical
    support that they are incapable of providing.
ms.assetid: E9FBF7D8-A7E8-4DC6-B370-8339B9EE16B7
ms.author: v-thpr
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
---

# ServiceRequest


**Applies To**

-   Partner Center
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Partners can file service requests on behalf of their partners to report
disruptions services provided by Microsoft or to request other technical
support that they are incapable of providing.

## <span id="ServiceRequest"></span><span id="servicerequest"></span><span id="SERVICEREQUEST"></span>ServiceRequest


Describes a service request filed by a partner, including how that
request is progressing.

| Property         | Type                                                          | Description                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Title            | string                                                        | The service request title.                                                           |
| Description      | string                                                        | The description.                                                                     |
| Severity         | string                                                        | The severity: "unknown", "critical", "moderate", or "minimal".                       |
| SupportTopicId   | string                                                        | The id of the support topic.                                                         |
| SupportTopicName | string                                                        | The name of the support topic.                                                       |
| Id               | string                                                        | The id of the service request.                                                       |
| Status           | string                                                        | The status of the service request: "none", "open", "closed", or "attention\_needed". |
| Organization     | [ServiceRequestOrganization](#servicerequestorganization)     | Organization for which the service request is created.                               |
| PrimaryContact   | [ServiceRequestContact](#servicerequestcontact)               | Primary Contact on the service request.                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | "Last Updated By" contact for changes to the service request.                        |
| ProductName      | string                                                        | The name of the product that corresponds to the service request.                     |
| ProductId        | string                                                        | The id of the product.                                                               |
| CreatedDate      | date                                                          | The date of the service request's creation.                                          |
| LastModifiedDate | date                                                          | The date that the service request was last modified.                                 |
| LastClosedDate   | date                                                          | The date that the service request was last closed.                                   |
| FileLinks        | array of [FileInfo](utility-resources.md#fileinfo) resources | The collection of File Links that pertain to the service request.                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | A note can be added to an existing service request.                                  |
| Notes            | array of [ServiceRequestNotes](#servicerequestnote)           | A collection of notes added to the service request.                                  |
| CountryCode      | string                                                        | The country corresponding to the service request.                                    |
| Attributes       | ResourceAttributes                                            | The metadata attributes corresponding to the service request.                        |

 

## <span id="ServiceRequestContact"></span><span id="servicerequestcontact"></span><span id="SERVICEREQUESTCONTACT"></span>ServiceRequestContact


Describes a contact that creates or modifies a service request.

| Property     | Type                                                      | Description                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Organization | [ServiceRequestOrganization](#servicerequestorganization) | Organization for which the service request is created. |
| ContactId    | string                                                    | The contact's unique id.                               |
| LastName     | string                                                    | The last name of the contact.                          |
| FirstName    | string                                                    | The first name of the contact.                         |
| Email        | string                                                    | The email of the contact.                              |
| PhoneNumber  | string                                                    | The phone number of the contact.                       |

 

## <span id="ServiceRequestNote"></span><span id="servicerequestnote"></span><span id="SERVICEREQUESTNOTE"></span>ServiceRequestNote


Describes a note attached to a service request.

| Property      | Type   | Description                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | string | The name of the creator of the note.         |
| CreatedDate   | date   | The date and time when the note was created. |
| Text          | string | The text of the note.                        |

 

## <span id="ServiceRequestOrganization"></span><span id="servicerequestorganization"></span><span id="SERVICEREQUESTORGANIZATION"></span>ServiceRequestOrganization


Describes the organization for which the service request is created.

| Property    | Type   | Description                           |
|-------------|--------|---------------------------------------|
| Id          | string | The unique id of the organization.    |
| Name        | string | The name of the organization.         |
| PhoneNumber | string | The phone number of the organization. |

 

## <span id="SupportTopic"></span><span id="supporttopic"></span><span id="SUPPORTTOPIC"></span>SupportTopic


Describes a support topic. Service requests specify a support topic to
ensure that they are processed quickly and effectively.

| Property    | Type               | Description                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| Name        | string             | The name of the support topic.                                |
| Description | string             | The description of the support topic.                         |
| Id          | string             | The unique id of the support topic.                           |
| Attributes  | ResourceAttributes | The metadata attributes corresponding to the service request. |

 

 

 




