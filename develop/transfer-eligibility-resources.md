---
title: TransferEligibility resources
description: A partner creates a transfer when a customer wants their subscription with the partner to be transferred to another partner.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# TransferEligibility resources

**Applies to:**

- Partner Center
- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

A partner creates a transfer when a customer wants their subscription with the partner to be transferred to another partner.

## TransferEligibility

Describes a transferEligibility.

| Property              | Type             | Description                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | string           | The customer's subscription identifier.                                                  |
| isEligible            | bool             | Indicates whether the subscription is eligible for the transfer.                         |
| Reason                | string           | The reason property explains why the subscription isn't eligible for transfer. |