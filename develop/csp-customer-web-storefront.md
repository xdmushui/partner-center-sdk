---
title: CSP customer web storefront
description: This sample website code shows a working online store for customers to buy subscriptions to Microsoft products.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
---

# CSP customer web storefront

**Applies to**: Partner Center

**Does not apply to**: Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

This sample app applies only to the global instance of Partner Center.

The [Partner Center storefront](https://github.com/Microsoft/Partner-Center-Storefront) is a **sample website** for an online store that customers can use to buy subscriptions to Microsoft products. You can modify this **sample code** for your own use to [configure the offers](#configure-offers), [add branding](#configure-branding), and [add a payment method](#configure-payment-types).

## Sample code

Download the [Partner Center storefront sample code](https://github.com/Microsoft/Partner-Center-Storefront) from GitHub.

## Configure authentication

Before you build the application, update the following values in the Web.config file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md). You should use your integration sandbox account settings during early development or for testing in production (TiP).

- **partnerCenter.applicationId**
- **partnerCenter.applicationSecret**
- **partnerCenter.domain**
- **webPortal.clientId**
- **webPortal.clientSecret**
- **webPortal.domain**
- **webPortal.azureStorageConnectionString**

## Configure offers

You can configure the set of offers (**MicrosoftOffer**) in the **OfferCatalogViewModel**.

## Configure branding

This sample website tracks the following company and brand information in *BrandingConfiguration.cs* and *PortalBranding.cs*:

- Organization name
- Organization logo
- Header image
- Privacy agreement
- Contact email
- Contact phone number
- Support email
- Support phone number

### Configure payment types

The app currently uses a PayPal gateway, implemented in *PayPalGateway.cs*.