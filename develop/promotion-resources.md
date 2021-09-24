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
| startDate | string | The start date for when the promotion is applicable. |
| endDate | string  | The end date for when the promotion is applicable. |
| requiredProducts | list of requiredProducts | Product, SKU details, and pricing policies the promotion is applicable for. | 
| properties | list of properties | Properties for the promotion including whether the promotion is auto-applicable. | 

## RequiredProducts

Product, SKU details, and pricing policies the promotion is applicable for.

| Property          | Type                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| productId| string | An identifier of the product the promotion is available for. |
| skuId | string | An identifier of the SKU the promotion is available for. |
| term | Term | A term including term duration and billing cycle the promotion is available for. |
| pricingPolicies| List of pricingPolicies | A list of policies that define the promotion discount types and values. |

## Term

Represents a term for which the promotion can be purchased.

| Property          | Type                    | Description                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| duration          | string                  | An ISO 8601 representation of the term's duration. The current supported values are P1M (one month), P1Y (one year) and P3Y (three years). 
| billingCycle      | string | Describes how often the promotion will be applied to the billing. Values can include Monthly, Annual, OneTime, or Unknown. | 

## PricingPolicies

Describe the promotion discount types and values.

| Property          | Type               | Description                                                                  |          
|-------------------|--------------------|------------------------------------------------------------------------------|
| type | string | Describe whether the discount is based on percentages or flat rate discounts. |
| value | string  | Defines the amount of the discount applied. |

## Properties

Properties for the promotion.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| isAutoApplicable  | bool  | Indicates whether the promotion is applied automatically or whether it needs to be passed by the partner. |


## PromotionEligibilitiesRequestItem

Properties representing a transaction and a promotion's eligibility.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| id | int| The promotions eligibilities item identifier. |
| catalogItemId | string | The catalog item identifier the promotion will be applied to. Includes product ID, SKU ID, and availability ID. |
| quantity | int | The number of licenses or instances. |
| termDuration | string | An ISO 8601 representation of the term's duration. The current supported values are P1M (one month), P1Y (one year) and P3Y (three years). |
| billingCycle | string | Describes how often the promotion will be applied to the billing. Values can include  Monthly, Annual, OneTime, or Unknown. | 
| promotionID | string | The promotion identifier. |

## PromotionEligibilities

A list of products, SKUs, and their promotion eligibilities.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| id | int| The promotions eligibilities item identifier. |
| catalogItemId | string | The catalog item identifier the promotion will be applied to. Includes product ID, SKU ID and availability ID. |
| quantity | int | The number of licenses or instances. |
| termDuration | string | An ISO 8601 representation of the term's duration. The current supported values are P1M (one month), P1Y (one year) and P3Y (three years). |
| billingCycle | string | Describes how often the promotion will be applied to the billing. Values can include  Monthly, Annual, OneTime or Unknown. | 
| eligibilities | List of PromotionEligibilities | Represents a list of promotion eligibility results. |

## PromotionEligibility

A list of products, SKUs, and their promotion eligibilities.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| promotionId | string | The promotion identifier. |
| isEligible | bool | Describes if the promotion is eligible for the given eligibility request item. |
| errors | List of PromotionEligibilityErrors | Errors describing why a promotion eligibilities request item wasn't eligible. | 

## PromotionEligibilityError

Explains why a promotion eligibility request item wasn't eligible. 

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| type | string | The promotion eligibility error types can include InvalidCatalogItemId, InvalidPromotion, PrerequisiteProductOwnership, RedemptionLimit, SeatCount, OfferPurchasedPreviously or Term. |
| description | string | Describes if the promotion is eligible for the given eligibility request item. |

## RedemptionLimitPromotionEligibilityError

Includes details about why the redemption limit was exceeded.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| maxPromotionRedemptionCount | int | The maximum number of times a promotion can be acquired. |
| remainingPromotionRedemptionCount| int | The remaining number of times a promotion can be acquired. |

## SeatCountPromotionEligibilityError

Includes details about why the seat count limit was exceeded. Both values are nullable.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| minimumRequiredSeats | int? | The minimum licenses a promotion will support. |
| maximumRequiredSeats | int? | The maximum licenses a promotion will support. |

## TermPromotionEligibilityError

Includes details about why the promotion term wasn't accepted.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| eligibleTerms | PromotionTerm | The eligible terms a promotion will support. |

## PromotionTerm

Includes details about why the seat count limit was exceeded.

| Property          | Type               | Description                                        |
|-------------------|--------------------|----------------------------------------------------|
| billingCycle | string | Describes how often the promotion will be applied to the billing. Values can include  Monthly, Annual, OneTime or Unknown. |
| duration | string | Duration of the term being purcahsed. |



