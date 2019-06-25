---
title: Enable secure application model
description: Secure your Partner Center and control panel apps.
ms.date: 06/25/2019
ms.localizationpriority: medium
---

# Enable secure application model

Applies to:

- Partner Center

Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.

You can use the new model to elevate security for Partner Center API integration calls. This will help all parties (including Microsoft, CSP partners, and CPVs) to protect their infrastructure and customer data from security risks.

## Scope

This topic concerns the following actors:

- CPVs
  - A CPV is an independent software vendor that develops apps for use by CSP partners to integrate with Partner Center APIs.
  - A CPV is not a CSP partner with direct access to the Partner Center dashboard or APIs.
- CSP indirect providers and CSP direct partners who are using app ID + user authentication and directly integrate with Partner Center APIs.

## Security requirements

For answers to frequently asked questions (FAQ) about this change to multi-factor authentication, download the [security requirements FAQ](http://assetsprod.microsoft.com/security-requirements-faq.pdf) document.

## Secure application model

Marketplace applications need to impersonate CSP partner privileges to call Microsoft APIs. Security attacks on these sensitive applications can lead to the compromise of customer data.

For an overview and details of the new authentication framework, download the [secure application model](http://assetsprod.microsoft.com/secure-application-model-guide.pdf) document. This document covers principles and best practices to make marketplace applications sustainable and robust from security compromises.

### Details for CPVs

For examples of how to implement multi-factor authentication in your control panel app, download the [CPV overview document](http://assetsprod.microsoft.com/cpv-partner-application-overview.pdf) and [sample application for CPVs](https://www.yammer.com/cloudpartnercommunity/#/files/154857341).

### Details for CSP partners

For examples of how to implement multi-factor authentication in your Partner Center app, download the [CSP overview document](http://assetsprod.microsoft.com/csp-partner-application-overview.pdf) and [sample application for CSP partners](https://www.yammer.com/cloudpartnercommunity/#/files/154857342).

## Implementing multi-factor authentication

For more information about implementing multi-factor authentication, see [How it works: Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks).
