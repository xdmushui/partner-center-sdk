---
title: Partner Center REST API change log
description: This page lists changes in the Partner Center REST APIs 
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.topic: reference
ms.date: 10/08/2021
---

# Recent changes to Partner Center REST APIs

This article summarizes changes made to the Partner Center REST APIs.

## October 2021

Changes for October are to support [New commerce licnese-based](purchase-new-commerce-license-based).

| Feature area | Change type | API/objects |
|------------------------|------------------|-----------------------------------------------------------------|
| New commerce subscription management | New field in public contract | [PATCH {baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}](get-a-subscription-by-id) |
| New commerce upgrades and trial conversions | New field in public contract | [POST {baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/transition](transition-a-subscription) |
| New commerce transitions | New field in public contract | [GET {baseUrl}/v1/customers/{customer_id}/subscriptions/{subscription_id}/transitions](transition-a-subscription) |
| Migrating to new commerce | New API | [POST {baseUrl}/v1/customers/{customer_tenant_id}/migrations/newcommerce/validate](validate-subscription-for-migration) |
| Migrating to new commerce | New API | [POST {baseUrl}/v1/customers/{customer_tenant_id}/migrations/newcommerce](create-migration) |
| Migrating to new commerce | New API | [GET {baseUrl}/v1/customers/{customer_tenant_id}/migrations/newcommerce/{migration-id}](get-new-commerce-migration) |
| Purchasing new commerce | New field in public contract | [POST {baseURL}/v1/customers/{customer-id}/orders"](create-an-order-for-a-customer-of-an-indirect-reseller) |
| Purchasing new commerce | New field in public contract | [POST{baseURL}/v1/customers/{customer-id}/carts ](create-a-cart) |
| Purchasing new commerce | New field in public contract | [PUT{baseURL}/v1/customers/{customer-id}/carts/{cart-id}](update-a-cart) |
| New commerce promotions | New API | [POST {baseURL}/v1/customers/{customerId}/promotionEligibilities](verify-promotion-eligibility) |
| New commerce promotions | New API | [GET {baseURL}/v1/productpromotions/{promotion-id}?country={country-code}](get-promotion-by-id) |
| New commerce promotions | New API | [GET {baseURL}/v1/productpromotions?country={country-code}&segment={segment}](get-promotions) |
| New commerce promotions | New resource | [Promotions resource](promotion-resources) |
| Catalog updates for new commerce | New field in public contract | [GET {baseURL}/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment}  ](get-a-list-of-products) |
| Catalog updates for new commerce | New field in public contract | [POST {baseURL}/v1/customers/{customer-tenant-id}/products?targetView={targetView}](get-a-list-of-products-by-customer) |
| Catalog updates for new commerce | New field in public contract | [GET {baseURL}/v1/products/{product-id}?country={country}](get-a-list-of-products) |
| Catalog updates for new commerce | New field in public contract | [POST {baseURL}/v1/customers/{customer-tenant-id}/products/{product-id}/skus](get-a-list-of-skus-for-a-product-by-customer) |
| Catalog updates for new commerce | New field in public contract | [GET {baseURL}/v1/products/{product-id}/skus?country={country-code}&targetSegment={target-segment}](get-a-list-of-skus-for-a-product) |
| Catalog updates for new commerce | New field in public contract | [GET {baseURL}/v1/products/{product-id}/skus/{sku-id}?country={country-code}](get-a-sku-by-id) |
| Catalog updates for new commerce | New field in public contract | [GET {baseURL}/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment}](get-a-list-of-availabilities-for-a-sku) |
| Catalog updates for new commerce | New field in public contract | [POST {baseURL}/v1/customers/{customer-tenant-id}/products/{product-id}/skus/{sku-id}](get-a-list-of-skus-for-a-product-by-customer) |
| Catalog updates for new commerce | New field in public contract | [GET {baseURL}/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}?country={country-code}](get-a-list-of-availabilities-for-a-sku) |
| Catalog updates for new commerce | New field in public contract | [Product resources](product-resources) |
| ISV margin discounts for CSPs | New resource | [Margin resource](margin-resources) |
| ISV margin discounts for CSPs | New API | [GET {baseURL}/v1/margins](get-margins) |
| ISV margin discounts for CSPs | New API | [GET {baseURL}/v1/margins/download](download-margins) |
| Telco pay-as-you-go in new commerce | New API | [PUT  {baseURL}/customers/{customerId}/subscriptions/overage](update-subscription-overage) |
| Telco pay-as-you-go in new commerce | New API | [GET  {baseURL}/customers/{customerId}/subscriptions/overage ](get-subscription-overage) |
| Telco pay-as-you-go in new commerce | New field in public contract | [Add ConsumptionType to Sku model](product-resources#sku) |

## July 2021

Changes for July were to support [Windows 365 attestation](/partner-center/pricing-and-offers#offer-attestation) required for some Windows 365 SKUs only.

| Feature area | Change type | API/objects |
|------------------------|------------------|-----------------------------------------------------------------|
| Windows 365 Attestation | New field in public contract | [Sku resoruce](product-resources#sku) |
| Windows 365 Attestation | New field in public contract | [Offer resource](offer-resources) |
| Windows 365 Attestation | New field in public contract | [Cart line item resource](cart-resources#cartlineitem) |
| Windows 365 Attestation | New field in public contract | [GET {baseURL}/v1/products/{product-id}/skus?country={country-code}&targetSegment={target-segment}](get-a-list-of-skus-for-a-product) |
| Windows 365 Attestation | New field in public contract | [GET {baseURL}/v1/products/{product-id}/skus/{sku-id}?country={country-code}](get-a-list-of-skus-for-a-product) |
| Windows 365 Attestation | New field in public contract | [PUT {baseURL}/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1](create-a-cart) |

## December 2020

Two new GET and POST Qualifications APIs introduced. The new APIs will be using Qualifications, not Qualification. The APIs will be available for testing in FY21 Q2.

| Feature area | Change type | API/objects |
|------------------------|------------------|-----------------------------------------------------------------|
| Customer qualification | New API | [GET {baseURL}/v1/customers/{customer-tenant-id}/qualifications](get-customer-qualification-asynchronous) |
| Customer qualification | New API | [POST {baseURL}/v1/customers/{customer_id}/qualifications?code={validationCode}](update-customer-qualification-asynchronous) |


### What has changed?

Currently, the Partner Center API has GET and PUT qualifications to verify Education customers’ eligibility. There will be no changes to the GET Qualification API. However, we’ve added a return case to the PUT Qualification API.

- GET - doesn't change.
- PUT - return case will be added.

These APIs will be retired at the end of February 2021, to be replaced by new APIs as described below.

### Scenarios impacted:

Customer eligibility for education pricing on select SKUs

### Detail descriptions

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
