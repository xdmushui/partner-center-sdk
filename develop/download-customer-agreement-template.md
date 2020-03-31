---
title: Get a download link for the Microsoft Customer Agreement template
description: Get a download link for Microsoft Customer Agreement template.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.localizationpriority: medium
---

# Get a download link for the Microsoft Customer Agreement template

Applies to:

- Partner Center

The **AgreementDocument** resource is currently supported by Partner Center only in the *Microsoft public cloud*. This resource doesn't apply to:

- Partner Center operated by 21Vianet
- Partner Center for Microsoft Cloud Germany
- Partner Center for Microsoft Cloud for US Government

This article describes how to get a link to download the Microsoft Customer Agreement template, based on the customer's country and language.

## Prerequisites

- If you are using the Partner Center .NET SDK, version 1.14 or newer is required.
- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario only supports App+User authentication.
- The customer's country to which the Microsoft Customer Agreement template applies.
- The language in which the Microsoft Customer Agreement template should be localized.

> [!IMPORTANT]
> - The Microsoft Customer Agreement is country-specific. When requesting for a link to download the Microsoft Customer Agreement template, Be sure to specify the correct country based on customer's location. or list of supported countries, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).
> - For some countries, the Microsoft Customer Agreement is available in multiple languages. For best customer experience, pick the language that best match the customer's needs. For list of supported languages, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).
> - This method is only supported with the Microsoft Customer Agreement.

## .NET

To retrieve a link to download the Microsoft Customer Agreement template:

1. Retrieve the agreement metadata for the Microsoft Customer Agreement. You must obtain the **templateId** of the Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

2. Use the IAggregatePartner.AgreementTemplates collection.
3. Call the **ById** method and specify the **templateId** of the Microsoft Customer Agreement.
4. Fetch the **Document** property.
5. Call the **ByCountry** method and specify the customer's country to which the agreement template applies. The query defaults to *US* if the method isn't specified. For a list of supported country codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages). This method is **case-sensitive**.
6. Call the **ByLanguage** method and specify the language which the agreement template should be localized in. The query defaults to *en-US* if the method isn't specified or the country code specified isn't supported for the country specified. For list of supported language codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages)
7. Call the **Get** or **GetAsync** method.

```csharp
// IAggregatePartner partnerOperations;

string customerCountry = "US";

string languageForLocalization = "en-US";

var agreementDocument = partnerOperations.AgreementTemplates.ById(microsoftCustomerAgreementDetails.TemplateId).Document.ByCountry(customerCountry).ByLanguage(languageForLocalization).Get();
```

A complete sample can be found in the [GetAgreementDocument](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDocument.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.


## REST request

To retrieve a link to download the Microsoft Customer Agreement template:

1. Retrieve the agreement metadata for the Microsoft Customer Agreement. You must obtain the **templateId** of the Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).
2. Create a REST request to fetch an [**AgreementDocument** resource](./agreement-document-resources.md). For an example, see the [request syntax](#request-syntax) example. You must specify the following information:
    - The **templateId** of the Microsoft Customer Agreement.
    - The country to which the Microsoft Customer Agreement template applies.
    - The language in which the Microsoft Customer Agreement template should be localized.

### Request syntax

Use the following request syntax for this resource:

| Method | Request URI |
|--------|---------------------------------------------------------------------|
| GET | [*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreementtemplates/{agreement-template-id}/document?language={language}&country={country} HTTP/1.1 |

### URI parameters

You can use the following URI parameters with your request:

| Name                   | Type   | Required | Description                                 |
|------------------------|--------|----------|---------------------------------------------|
| agreement-template-id  | string | Yes      | Unique identifier of the agreement type. You can obtain the templateId for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md). This parameter is **case-sensitive**.|
| country                | string | No       | Indicates the country to which the agreement template applies. The query defaults to *US* if the parameter isn't specified. For a list of supported country codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).|
| language               | string | No       | Indicates the language in which the agreement template should be localized. The query defaults to *en-US* if the parameter isn't specified or the country code specified in't supported for the country specified. For list of supported country codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).|

### Request headers

For more information, see [Partner Center REST headers](headers.md).

### Request body

None.

### Request example

```http
GET https://api.partnercenter.microsoft.com/v1/agreementtemplates/117a77b0-9360-443b-8795-c6dedc750cf9/document?language=en-US&country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## REST response

If successful, this method returns an [**AgreementDocument** resource](./agreement-document-resources.md) in the response body.

The resource has a **downloadUri** property, which contains a URL string that can be used to download the agreement template. A different link is returned each time you make a query. This link expires after five minutes.

### Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information.

Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

### Response example

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "displayUri":"https://wopihost.int.l2o.microsoft.com/v1/officehost/agreement/files/Preview...",
    "downloadUri":"https://l2oagreementintbn2.blob.core.windows.net/agreementscontainer/Preview...",
    "language":"en-US",
    "country":"US"
}
```

## List of supported countries and languages

> [!IMPORTANT]
> The country code property is case-sensitive. Please sure to use the correct casing specified in the table below.

| Country                   | Country code   | Supported language code(s) |
|------------------------|--------|----------|
| Åland Islands | AX | en-US |
| Afghanistan | AF | en-US |
| Albania | AL | en-US |
| Algeria | DZ | en-US, fr-FR, en-US |
| American Samoa | AS | en-US |
| Andorra | AD | en-US |
| Angola | AO | en-US, pt-PT |
| Anguilla | AI | en-US |
| Antarctica | AQ | en-US |
| Antigua and Barbuda | AG | en-US |
| Argentina | AR | en-US, es-ES |
| Armenia | AM | en-US |
| Aruba | AW | en-US |
| Australia | AU | en-US |
| Austria | AT | en-US, de-DE |
| Azerbaijan | AZ | en-US |
| Bahamas | BS | en-US |
| Bahrain | BH | en-US, ar-SA |
| Bangladesh | BD | en-US |
| Barbados | BB | en-US |
| Belarus | BY | en-US, ru-RU |
| Belgium | BE | en-US, nl-NL |
| Belize | BZ | en-US, es-ES |
| Benin | BJ | en-US |
| Bermuda | BM | en-US |
| Bhutan | BT | en-US |
| Bolivia | BO | en-US, es-ES |
| Bonaire | BQ | en-US |
| Bosnia and Herzegovina | BA | en-US |
| Botswana | BW | en-US |
| Bouvet Island | BV | en-US |
| Brazil | BR | en-US, pt-BR |
| British Indian Ocean Territory | IO | en-US |
| British Virgin Islands | VG | en-US |
| Brunei | BN | en-US |
| Bulgaria | BG | en-US, bg-BG |
| Burkina Faso | BF | en-US |
| Burundi | BI | en-US |
| Côte d'Ivoire | CI | en-US, fr-FR |
| Cabo Verde | CV | en-US, pt-PT |
| Cambodia | KH | en-US |
| Cameroon | CM | en-US, fr-FR |
| Canada | CA | en-US, fr-FR |
| Cayman Islands | KY | en-US, en-US |
| Central African Republic | CF | en-US |
| Chad | TD | en-US |
| Chile | CL | en-US, es-ES |
| Christmas Island | CX | en-US |
| Cocos (Keeling) Islands | CC | en-US |
| Colombia | CO | en-US, es-ES |
| Comoros | KM | en-US |
| Congo (DRC) | CD | en-US |
| Congo | CG | en-US |
| Cook Islands | CK | en-US |
| Costa Rica | CR | en-US, es-ES |
| Croatia | HR | en-US, hr-HR |
| Curaçao | CW | en-US |
| Cyprus | CY | en-US |
| Czechia | CZ | en-US, cs-CZ |
| Denmark | DK | en-US, da-DK |
| Djibouti | DJ | en-US |
| Dominica | DM | en-US |
| Dominican Republic | DO | en-US, es-ES |
| Ecuador | EC | en-US |
| Egypt | EG | en-US, ar-SA |
| El Salvador | SV | en-US, es-ES |
| Equatorial Guinea | GQ | en-US |
| Eritrea | ER | en-US |
| Estonia | EE | en-US, et-EE |
| eSwatini | SZ | en-US |
| Ethiopia | ET | en-US |
| Falkland Islands | FK | en-US |
| Faroe Islands | FO | en-US |
| Fiji | FJ | en-US |
| Finland | FI | en-US, fi-FI |
| France | FR | en-US, fr-FR |
| French Guiana | GF | en-US, fr-FR  |
| French Polynesia | PF | en-US |
| French Southern Territories | TF | en-US |
| Gabon | GA | en-US |
| Gambia | GM | en-US |
| Georgia | GE | en-US |
| Germany | DE | en-US, de-DE |
| Ghana | GH | en-US |
| Gibraltar | GI | en-US |
| Greece | GR | en-US, el-GR |
| Greenland | GL | en-US |
| Grenada | GD | en-US |
| Guadeloupe | GP | en-US |
| Guam | GU | en-US |
| Guatemala | GT | en-US, es-ES |
| Guernsey | GG | en-US |
| Guinea | GN | en-US |
| Guinea-Bissau | GW | en-US |
| Guyana | GY | en-US |
| Haiti | HT | en-US |
| Heard Island and McDonald Islands | HM | en-US |
| Honduras | HN | en-US, es-ES |
| Hong Kong SAR | HK | en-US, zh-HK |
| Hungary | HU | en-US, hu-HU |
| Iceland | IS | en-US |
| India | IN | en-US, hi-IN |
| Indonesia | ID | en-US, id-ID |
| Iraq | IQ | en-US, ar-SA |
| Ireland | IE | en-US |
| Isle of Man | IM | en-US |
| Israel | IL | en-US, he-IL |
| Italy | IT | en-US, it-IT |
| Jamaica | JM | en-US |
| Jan Mayen | XJ | en-US |
| Japan | JP | en-US, ja-JP |
| Jersey | JE | en-US |
| Jordan | JO | en-US, ar-SA |
| Kazakhstan | KZ | en-US, kk-KZ |
| Kenya | KE | en-US |
| Kiribati | KI | en-US |
| Korea | KR | en-US, ko-KR |
| Kosovo | XK | en-US |
| Kuwait | KW | en-US, ar-SA |
| Kyrgyzstan | KG | en-US, ru-RU |
| Laos | LA | en-US |
| Latvia | LV | en-US, lv-LV |
| Lebanon | LB | en-US, ar-SA |
| Lesotho | LS | en-US |
| Liberia | LR | en-US |
| Libya | LY | en-US, ar-SA |
| Liechtenstein | LI | en-US, de-DE |
| Lithuania | LT | en-US, lt-LT |
| Luxembourg | LU | en-US, fr-FR |
| Macao SAR | MO | en-US, zh-HK |
| Macedonia, FYRO | MK | en-US |
| Madagascar | MG | en-US |
| Malawi | MW | en-US |
| Malaysia | MY | en-US, ms-MY |
| Maldives | MV | en-US |
| Mali | ML | en-US |
| Malta | MT | en-US |
| Marshall Islands | MH | en-US |
| Martinique | MQ | en-US |
| Mauritania | MR | en-US |
| Mauritius | MU | en-US, ar-SA |
| Mayotte | YT | en-US |
| Mexico | MX | en-US, es-ES |
| Micronesia | FM | en-US |
| Moldova | MD | en-US, ro-RO |
| Monaco | MC | en-US, fr-FR |
| Mongolia | MN | en-US |
| Montenegro | ME | en-US |
| Montserrat | MS | en-US |
| Morocco | MA | en-US, fr-FR, en-US |
| Mozambique | MZ | en-US |
| Myanmar | MM | en-US |
| Namibia | NA | en-US |
| Nauru | NR | en-US |
| Nepal | NP | en-US |
| Netherlands | NL | en-US, nl-NL |
| New Caledonia | NC | en-US |
| New Zealand | NZ | en-US |
| Nicaragua | NI | en-US, es-ES |
| Niger | NE | en-US |
| Nigeria | NG | en-US |
| Niue | NU | en-US |
| Norfolk Island | NF | en-US |
| Northern Mariana Islands | MP | en-US |
| Norway | NO | en-US, nb-NO |
| Oman | OM | en-US, ar-SA |
| Pakistan | PK | en-US |
| Palau | PW | en-US |
| Palestinian Authority | PS | en-US |
| Panama | PA | en-US, es-ES |
| Papua New Guinea | PG | en-US |
| Paraguay | PY | en-US, es-ES |
| Peru | PE | en-US, es-ES |
| Philippines | PH | en-US |
| Pitcairn Islands | PN | en-US |
| Poland | PL | en-US, pl-PL |
| Portugal | PT | en-US, pt-PT |
| Puerto Rico | PR | en-US, en-US |
| Qatar | QA | en-US, ar-SA |
| Réunion | RE | en-US |
| Romania | RO | en-US, ro-RO |
| Russia | RU | en-US, ru-RU |
| Rwanda | RW | en-US, fr-FR |
| São Tomé and Príncipe | ST | en-US, fr-FR |
| Saba | XS | en-US |
| Saint-Barthélemy | BL | en-US |
| Saint Kitts and Nevis | KN | en-US |
| Saint Lucia | LC | en-US, en-US |
| Saint Martin | MF | en-US, en-US |
| Saint Pierre and Miquelon | PM | en-US |
| Saint Vincent and the Grenadines | VC | en-US |
| Samoa | WS | en-US |
| San Marino | SM | en-US |
| Saudi Arabia | SA | en-US |
| Senegal | SN | en-US, fr-FR |
| Serbia | RS | en-US, sr-Latn-RS, en-US |
| Seychelles | SC | en-US |
| Sierra Leone | SL | en-US |
| Singapore | SG | en-US, zh-SG |
| Sint Eustatius | XE | en-US |
| Sint Maarten | SX | en-US, en-US |
| Slovakia | SK | en-US, sk-SK |
| Slovenia | SI | en-US, sl-SI |
| Solomon Islands | SB | en-US |
| Somalia | SO | en-US |
| South Africa | ZA | en-US |
| South Georgia and South Sandwich Islands | GS | en-US |
| South Sudan | SS | en-US |
| Spain | ES | en-US, es-ES, en-US, en-US |
| Sri Lanka | LK | en-US |
| St Helena, Ascension, Tristan da Cunha | SH | en-US |
| Suriname | SR | en-US |
| Svalbard | SJ | en-US |
| Sweden | SE | en-US, sv-SE |
| Switzerland | CH | en-US, fr-FR, en-US, en-US |
| Taiwan | TW | en-US, zh-HK |
| Tajikistan | TJ | en-US |
| Tanzania | TZ | en-US |
| Thailand | TH | en-US, th-TH |
| Timor-Leste | TL | en-US |
| Togo | TG | en-US |
| Tokelau | TK | en-US |
| Tonga | TO | en-US |
| Trinidad and Tobago | TT | en-US |
| Tunisia | TN | en-US, fr-FR, en-US |
| Turkey | TR | en-US, tr-TR |
| Turkmenistan | TM | en-US |
| Turks and Caicos Islands | TC | en-US |
| Tuvalu | TV | en-US |
| U.S. Outlying Islands | UM | en-US |
| U.S. Virgin Islands | VI | en-US |
| Uganda | UG | en-US |
| Ukraine | UA | en-US, uk-UA |
| United Arab Emirates | AE | en-US, ar-SA |
| United Kingdom | GB | en-US |
| United States | US | en-US |
| Uruguay | UY | en-US, es-ES |
| Uzbekistan | UZ | en-US, ru-RU |
| Vanuatu | VU | en-US |
| Vatican City | VA | en-US |
| Venezuela | VE | en-US, es-ES |
| Vietnam | VN | en-US, vi-VN |
| Wallis and Futuna | WF | en-US |
| Yemen | YE | en-US, ar-SA |
| Zambia | ZM | en-US |
| Zimbabwe | ZW | en-US |


