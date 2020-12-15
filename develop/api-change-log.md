---
title: Partner Center API change log
description: Tracks changes to APIs
ms.date: 12/15/2020
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# December 2020

## Enhancements to education pricing Eligibility APIs

Check here monthly for changes to Partner Center APIs.

### What has changed?

Currently, the Partner Center API has GET and PUT qualifications to veify Education customers’ eligibility. There will be no changes to the GET Qualification API. However, we’ve added a return case to the PUT Qualification API.

- GET—doesn’t change. [Current API article](get-a-customer-s-qualification.md)

- PUT—return case will be added. [Current API article](update-a-customer-s-qualification.md)

These APIs will be retired at the end of Feb 2021, to be replaced by new APIs as described below.

### Scenarios impacted:

- Customer eligibility for education pricing on select SKUs

### Detail descriptions: Contract changes

Two new GET and POST Qualifications APIs will be introduced. Note that the new APIs will be using **Qualifications**, not **Qualification**. The APIs will be available for testing in FY21 Q2.

 ```
- GET Qualifications
GET

{customer_id}/qualifications

Response example:

  

        {

            "Qualification": "Education",

            "VettingStatus": "Denied",

            "VettingReason": “Not an education customer",

            "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC

        }

    ]

  Vetting Status Values: Approved, Denied, InReview, etc.

  Vetting reason:

•Not an Education Customer
•No longer an Education Customer
•Not an Education Customer - After Review
•Restricted being an Education Customer
•Not an Academic Domain
•Not an eligible Library
•Not an eligible Museum
Etc.
 
- POST Qualifications
POST

    {customer_id}/qualifications

    [

       ```

            "Qualification": "Education"

        }

    ]

Response example:

    ```

        {

            "Qualification": "Education",

            "VettingStatus": "InReview",

            "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC

        }

    ]

----------------
