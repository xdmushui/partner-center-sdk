---
title: Agreement resources
description: Represents a Microsoft cloud customer agreement
ms.date: 8/02/2018
ms.localizationpriority: medium
---

# Agreement resources


**Applies To**

- Partner Center

> [!NOTE]  
> The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only. It is not applicable to:
> - Partner Center operated by 21Vianet
> - Partner Center for Microsoft Cloud Germany
> - Partner Center for Microsoft Cloud for US Government

The resource defined here represents a Microsoft cloud customer agreement.


## <span id="Agreement"/><span id="agreement"/><span id="AGREEMENT"/>Agreement

Represents the details of certification provided by the partner.

| Property       | Type   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | string                         |Object identifier of the logged in user in the partner tenant who is providing confirmation on behalf of the partner organization.                                                                             |
| primaryContact | [Contact](./utility-resources.md#contact) | Information about the user from the customer organization who accepted the Microsoft Cloud Agreement, including:  </br> - firstName </br> - lastName</br> - email</br> - phoneNumber (optional) |
| dateAgreed     | string in UTC date time format |The date when the customer accepted the agreement.                                 |
| templateId     |string                          |Unique identifier of the agreement that the customer accepted. Currently, the only supported value is "998b88de-aa99-4388-a42c-1b3517d49490", which is the unique identifier for the Microsoft Cloud Agreement.                             |
| type           |AgreementType enum              | Agreement type. Currently, the only supported value is "MicrosoftCloudAgreement". |
| agreementLink  | string                         | URL to the agreement template.                                                    |
  


