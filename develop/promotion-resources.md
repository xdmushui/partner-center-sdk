---
title: Promotion resources
description: Describes the resources for promotions applied to transactions for new commerce subscriptions.
ms.date: 09/23/2021
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
---

# Promotions resources

**Applies To**

- Partner Center

**Appropriate roles**

- Global admin
- Admin agent

> [!Note] 
> New Commerce changes are currently available only to partners who are part of the Microsoft 365 and Dynamics 365 new commerce experience technical preview.

Describes the resources for promotions applied to transactions for new commerce subscriptions.

## Promotion

Discount applied when purchasing a product SKU if eligibility criteria is met.

| Property          | Type                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| id | string                  | The promotion identifier. |
| name | string                  | The friendly name of the promotion. |
| description | string                  | A description of the promotion. |
| segment | string | The segment the promotion can be applied in. |
| requiredProducts | list of rerquiredProducts | Product, SKU details, and pricing policies the promotion is applicable for. | 
| properties | list of properties | Properties for the promotion including the start date, end dates, and tag information. | 

## requiredProducts

Product, SKU details, and pricing policies the promotion is applicable for.

| Property          | Type                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| productId| string | An identifier of the product the promotion is available for. |
| skuId | string | An identifier of the SKU the promotion is available for. |
| term | List of Terms | A list that includes durations and billing cycles the promotion is available for. |
| pricingPolicies| List of pricingPolicies | A list of policies that define the promotion discount types and values. |

## term

Represents a term for which the promotion can be purchased.

| Property          | Type                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| duration          | string                  | An ISO 8601 representation of the term's duration. The current supported values are P1M (one month), P1Y (one year) and P3Y (three years). |
| billingCycle      | BillingCycleType | Describes how often the promotion will be applied to the billing. Values can include Monthly, Annual, or OneTime | 

## pricingPolcies

Describe the promotion discount types and values.

| Property          | Type               | Description                                                                  |          
|-------------------|--------------------|------------------------------------------------------------------------------|
| type | string | Describe whether the discount is based on percentages or flat rate discounts. |
| value | string  | Defines the amount of the discount applied. |

## properties

Properties for the promotion including the start date, end dates, and tag information.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| startDate | string | The start date for when the promotion is applicable. |
| endDate | string  | The end date for when the promotion is applicable. |
| tag | string  | Includes extra information about the promotion, often used for internal execution paths. |


## PromotionEligibilitiesRequestItem

Properties representing a transaction and a promotion's eligibility.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| ID | int| The promotions eligibilities item identifier. |
| CatalogItemId | string | The catalog item identifier the promotion will be applied to. Includes product ID, SKU ID, and availability ID. |
| Quantity | int | The number of licenses or instances. |
| TermDuration | string | An ISO 8601 representation of the term's duration. The current supported values are P1M (one month), P1Y (one year) and P3Y (three years). |
| BillingCycle | billingCycleType | Describes how often the promotion will be applied to the billing. Values can include  Monthly, Annual, or OneTime | 
| PromotionID | string | The promotion identifier. |

## BillingCycleType

A value that indicates a type of billing cycle.

| Value              | Position     | Description                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Unknown            | 0            | Enum initializer.                                                                          |
| Monthly            | 1            | Indicates that the partner will be charged monthly.                                        |
| Annual             | 2            | Indicates that the partner will be charged annually.                                       |
| None               | 3            | Indicates that the partner will not be charged. This value may be used for trial items.    |
| OneTime            | 4            | Indicates that the partner will be charged one time.                                       |

## PromotionEligibilities

A list of products, SKUs, and their promotion eligibilities.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| ID | int| The promotions eligibilities item identifier. |
| CatalogItemId | string | The catalog item identifier the promotion will be applied to. Includes product ID, SKU ID and availability ID. |
| Quantity | int | The number of licenses or instances. |
| TermDuration | string | An ISO 8601 representation of the term's duration. The current supported values are P1M (one month), P1Y (one year) and P3Y (three years). |
| BillingCycle | billingCycleType | Describes how often the promotion will be applied to the billing. Values can include  Monthly, Annual or OneTime | 
| Eligibilities | List of PromotionEligibilities | Represents a list of promotion eligibility results. |

## PromotionEligibility

A list of products, SKUs, and their promotion eligibilities.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| PromotionId | string | The promotion identifier. |
| IsEligible | bool | Describes if the promotion is eligible for the given eligibility request item. |
| Errors | List of PromotionEligibilityErrors | Errors describing why a promotion eligibilities request item wasn't eligible. | 

## PromotionEligibilityError

Explains why a promotion eligibility request item wasn't eligible.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| Type | string | The promotion identifier. |
| Description | bool | Describes if the promotion is eligible for the given eligibility request item. |

## RedemptionLimitPromotionEligibilityError

Includes details about why the redemption limit was exceeded.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| MaxPromotionRedemptionCount | int | The maximum number of times a promotion can be acquired. |
| RemainingPromotionRedemptionCount| int | The remaining number of times a promotion can be acquired. |

## SeatCountPromotionEligibilityError

Includes details about why the seat count limit was exceeded.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| MinimumRequiredSeats | int | The minimum licenses a promotion will support. |
| MaximumRequiredSeats | int | The maximum licenses a promotion will support. |

TermPromotionEligibilityError

Includes details about why the promotion term wasn't accepted.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| EligibleTerms | PromotionTerm | The minimum licenses a promotion will support. |

## PromotionTerm

Includes details about why the seat count limit was exceeded.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| BillingCycle | BillingCycleType | Defined how often billing will occur. |
| Duration | string | How long the promotion will be available for. |



