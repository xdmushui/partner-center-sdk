---
title: Enable multi-factor authentication
description: Configure your Partner Center and control panel apps for multi-factor authentication.
ms.date: 10/18/2018
ms.localizationpriority: medium
---

# Enable multi-factor authentication


**Applies To**

-   Partner Center


## <span id="overview"/><span id="Overview"/><span id="OVERVIEW"/>Overview

Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture. You can rely on the new model to elevate security for Partner Center API integration calls. This will help all parties including Microsoft, CSP partners, and control panel vendors to protect their infrastructure and customer data from security risks.


## <span id="scope"/><span id="SCOPE"/>Scope

This topic concerns the following actors:

- Control panel vendors (CPV) - A control panel vendor is an independent software vendor that develops apps for use by CSP partners to integrate with Partner Center APIs. A control panel vendor is not a CSP partner with direct access to the Partner dashboard or APIs.
- CSP indirect providers and CSP direct partners who are using app ID + user authentication and directly integrate with Partner Center APIs.

## <span id="faq"/><span id="FAQ"/>Security requirements FAQ

For answers to frequently asked questions about this change to multi-factor authentication, download the [Security requirements FAQ](https://assetsprod.microsoft.com/new-security-requirements-faq.pdf) document.

## <span id=""/><span id=""/>Secure application model
Marketplace applications need to impersonate CSP partner privileges to call Microsoft APIs. Security attacks on these sensitive applications can lead to the compromise of customer data. 

Download the [Secure application model](http://assetsprod.microsoft.com/secure-application-model-guide.pdf) document for an overview and details of the new authentication framework. This document covers principles and best practices to make marketplace applications sustainable and robust from security compromises.
 
### <span id="how-to-for-cpv"/><span id="How-To-for-CPV"/><span id="HOW-TO-FOR-CPV"/>How to for control panel vendors (CPV)

Download the [CPV overview document](http://assetsprod.microsoft.com/cpv-partner-application-overview.pdf) and [sample application for control panel vendors](https://www.yammer.com/cloudpartnercommunity/#/files/154857341) for an example of how to implement multi-factor authentication in your control panel app. 


### <span id="how-to-for-csp"/><span id="How-To-for-CSP"/><span id="HOW-TO-FOR-CSP"/>How to for cloud solution provider partners (CSP)

Download the [CSP overview document](http://assetsprod.microsoft.com/csp-partner-application-overview.pdf) and [sample application for cloud solution provider partners](https://www.yammer.com/cloudpartnercommunity/#/files/154857342) for an example of how to implement multi-factor authentication in your Partner Center app. 

## <span id="implement-mfa"/><span id="IMPLEMENT-MFA"/>Implement multi-factor authentication

Getting past multiple authentication factors presents a significant challenge for attackers. Even if an attacker manages to learn the user's password, it is useless without also having possession of the additional authentication method. For more information, see [How it works: Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks).