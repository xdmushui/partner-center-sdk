---
title: Agreement metadata resources
description: Provides metadata about all the agreement types that partners can provide confirmation of customer acceptance.
ms.date: 05/21/2019
ms.localizationpriority: medium
---

# Agreement metadata resources

Applies to:

- Partner Center

> [!NOTE]  
> The **AgreementMetaData** resource is currently supported by Partner Center in the Microsoft public cloud only. It is not applicable to:
> - Partner Center operated by 21Vianet
> - Partner Center for Microsoft Cloud Germany
> - Partner Center for Microsoft Cloud for US Government

The **AgreementMetaData** collection provides metadata about all the agreement types that partners can provide confirmation of customer acceptance. Currently, the **AgreementMetaData** collection only returns metadata for one agreement type, which is the Microsoft Cloud Agreement.

## AgreementMetaData

Agreement metadata returned includes the following:

| Property      | Type               | Description                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | string             | Unique identifier of an agreement template.                                       |
| type          | string             | Agreement type. Currently, supported values include "MicrosoftCloudAgreement" and "MicrosoftCustomerAgreement" (preview). |
| agreementLink | string             | URL to the agreement template.                                                    |
