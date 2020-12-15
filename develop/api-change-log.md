---
title: Partner Center API change log
description: Tracks changes to APIs
ms.date: 12/15/2020
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# December 2020

## Enhancements to education pricing Eligbility API's

### What changed?

Currently, the Partner Center API has GET and PUT qualifications to vet Education customers’ eligibility. There will be no changes to the GET Qualification API. However, we’ve added a return case to the PUT Qualification API.

- GET— doesn’t change. [Current API article](get-a-customer-s-qualification.md)

- PUT— return case will be added. [Current API article](update-a-customer-s-qualification.md)

These API's will be retired at the end of Feb 2021, to be replaced by new API's as described below.

### Scenarios impacted:

- Customer eligibility for education pricing on select SKU's

### Detail Descriptions: Contract changes

Two new GET and POST Qualifications APIs will be introduced. Note that the new APIs will be using **Qualifications**, not **Qualification**. These will be available for testing in FY21 Q2.

- GET Qualifications

{customer_id}/qualifications

Response example:

   ```

        {

            "Qualification": "Education",

            "VettingStatus": "Denied",

            "VettingReason": “Not an education customer",

            "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC

        }

    ]

  Vetting Status Values: Approved, Denied, InReview, etc.

  Vetting Reason:

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
