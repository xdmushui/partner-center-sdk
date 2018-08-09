---
title: Relationships
description: Describes resources related to relationships.
ms.assetid: F6157FE3-7C9D-4A8F-AC11-6F4007594C3D
ms.author: mhopkins
ms.date: 12/15/2017
ms.topic: article
ms.prod: partner-center
ms.technology: partner-center-sdk
ms.localizationpriority: medium
---

# Relationships


**Applies To**

-   Partner Center

Describes resources related to relationships.

## <span id="PartnerRelationship"></span><span id="partnerrelationship"></span><span id="PARTNERRELATIONSHIP"></span>PartnerRelationship


Represents a relationship between two partners.

| Property         | Type                                                           | Description                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | string                                                         | The partner identifier. The partner identifier specifies the tenant id of the partner who is in the recipient (from) side of the relationship. |
| location         | string                                                         | The location of the partner.                                                                                                                   |
| mpnId            | string                                                         | The Microsoft Partner Network (MPN) identifier of the partner.                                                                                 |
| name             | string                                                         | The name of the partner.                                                                                                                       |
| relationshipType | string                                                         | The type of relationship.                                                                                                                      |
| state            | string                                                         | The state of the relationship (e.g. "active").                                                                                                 |
| attributes       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                                                                                       |

 

## <span id="RelationshipRequest"></span><span id="relationshiprequest"></span><span id="RELATIONSHIPREQUEST"></span>RelationshipRequest


Provides the URL by which a customer can establish a relationship with a
partner.

| Property   | Type                                                           | Description                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | string                                                         | The relationship request URL. |
| attributes | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.      |

 

 

 




