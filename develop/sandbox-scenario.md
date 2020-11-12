---
title: Partner sandbox capabilities that support reseller relationship
description: Partner sandbox has ability to support relationships between the partner and the customer
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# Partner sandbox capabilities that support reseller relationship

**Applies to:**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer. 

## Prerequisites

- Partner Center account credentials. The sandbox scenario supports authentication with both the standalone App and App+User credentials.
- A customer ID (customer-tenant-id). If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home). Select **CSP** from the Partner Center menu, followed by **Customers**. Select the customer from the customer list, then select **Account**. On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section. The Microsoft ID is the same as the customer ID (customer-tenant-id).
- All Azure Reserved Virtual Machine Instances and software purchase orders must be cancelled before deleting a customer from the Tip integration sandbox.

## Scenarios Supporting Reseller Relationship

1.	Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer. 
2.	Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.



### In the Sandbox

**Direct bill partners**:

•	Can add existing customers

•	Cannot request relationships with new customers

**Indirect providers** :

•	Can add existing customers

•	Cannot request relationships with new customers

•	Cannot have a relationship with an Indirect reseller

**Indirect reseller**:

•	Can have a relationships with existing customers

•	Cannot request new relationships or add new customers

### In Partner Center

**Direct bill partners**:

•	Can add new customers

•	Can request relationships with new customers

**Indirect providers**:

•	Can add new customers

•	Can request relationships with new customers

•	Can have relationships with indirect resellers

**Indirect resellers**:

•	Can’t add new customers

•	Can request relationships with new customers

3. Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.

4. Sandbox Remove Reseller Relationship will call Delete customer AP. This will remove the relationship as well as delete the customer tenant. {baseURL}/v1/Customers/{customer-Tenant-id}

Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details. However, there are some differences between the Product and Sandbox capabilities.

### REQUEST SYNTAX

|**Method**|**Delete**|
|-------------|------------|
|Delete|{baseURL}/v1/Customers/{customer-Tenant-id} |

Request body
None

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](https://docs.microsoft.com/partner-center/develop/error-codes).

## Next steps

- [Activate Sandbox subscriptions for Azure Marketplace products](activate-sandbox-subscription-azure-marketplace-products.md)

- [Cancel an order from Sandbox](cancel-an-order-from-the-integration-sandbox.md)

- [Test and debug](test-and-debug.md) 
