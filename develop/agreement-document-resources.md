---
title: Agreement document resources
description: Represents an agreement document
ms.date: 08/27/2019
ms.localizationpriority: medium
---

# Agreement document resources

Applies to:

- Partner Center

> [!NOTE]  
> The **AgreementDocument** resource is currently supported by Partner Center in the Microsoft public cloud only. It is not applicable to:
> - Partner Center operated by 21Vianet
> - Partner Center for Microsoft Cloud Germany
> - Partner Center for Microsoft Cloud for US Government

The resource defined here represents an agreement document which is available for preview/download.

## AgreementDocument

An **AgreementDocument** resource includes the following properties:

| Property       | Type   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| country | string | Indicates which country/market this agreement document is for. |
| language | string | Indicates what language the agreement document is localized in. |
| displayUri | string | Link to preview the agreement document in a browser.  |
| downloadUri |string | Link to download the agreement document (in Microsoft word format). |
