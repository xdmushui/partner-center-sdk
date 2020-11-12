---
title: Agreement document resources
description: The AgreementDocument resource is a Microsoft agreement document for preview and download. It is supported by Partner Center in the Microsoft public cloud.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
---

# Agreement document resources supported by Partner Center in the Microsoft public cloud

**Applies to:**

- Partner Center

The **AgreementDocument** resource is currently supported by Partner Center only in the *Microsoft public cloud*. This resource not applicable to:

- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

The **AgreementDocument** resource represents a Microsoft agreement document that is available for preview and download.

## AgreementDocument

An **AgreementDocument** resource includes the following properties:

| Property       | Type   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| country | string | The country or market to which this document applies. |
| language | string | The language in which this document is localized. |
| displayUri | string | A link to preview the agreement document in a browser.  |
| downloadUri |string | A link to download the agreement document (in Microsoft Word format). |
