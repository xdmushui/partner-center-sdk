---
title: Partner Center API change log
description: This page lists changes in the Partner Center APIs for December 2020
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
---

# December 2020 changes to Partner Center APIs

## Enhancements to education pricing Eligibility APIs

Check here monthly for changes to Partner Center APIs.

### What has changed?

Currently, the Partner Center API has GET and PUT qualifications to verify Education customers’ eligibility. There will be no changes to the GET Qualification API. However, we’ve added a return case to the PUT Qualification API.

- GET - doesn't change. [Current API article](get-a-customer-s-qualification.md)
- PUT - return case will be added. [Current API article](update-a-customer-s-qualification.md)

These APIs will be retired at the end of February 2021, to be replaced by new APIs as described below.

### Scenarios impacted:

Customer eligibility for education pricing on select SKUs

### Detail descriptions: Contract changes

Two new GET and POST Qualifications APIs will be introduced. The new APIs will be using **Qualifications**, not **Qualification**. The APIs will be available for testing in FY21 Q2.

#### GET Qualifications

```http
GET {customer_id}/qualifications
```

#### Response example:

```json
        {
            "Qualification": "Education",
            "VettingStatus": "Denied",
            "VettingReason": "Not an education customer",
            "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
        }
```

#### Response fields: 

- VettingStatus values: Approved, Denied, InReview, etc.

- VettingReason values:
   - Not an Education Customer
   - No longer an Education Customer
   - Not an Education Customer - After Review
   - Restricted being an Education Customer
   - Not an Academic Domain
   - Not an eligible Library
   - Not an eligible Museum
 
#### POST Qualifications

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### Response example:

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## Next steps

[Partner Center REST API reference](partner-center-rest-api-reference.md)
