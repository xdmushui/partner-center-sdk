---
title: Get a download link for the Microsoft Customer Agreement template (preview)
description: Get a download link for Microsoft Customer Agreement template.
ms.date: 09/19/2019
ms.localizationpriority: medium
---

# Get a download link for the Microsoft Customer Agreement template (preview)

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
5. Call the **ByCountry** method and specify the customer's country to which the agreement template applies. The query defaults to *US* if the method isn't specified. For a list of supported country codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).
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
| agreement-template-id  | string | Yes      | Unique identifier of the agreement type. You can obtain the templateId for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md). |
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

| Country                   | Country code   | Supported language code(s) |
|------------------------|--------|----------|
| Anguilla | AI | en-US |
| Antigua and Barbuda | AG | en-US |
| Argentina | AR | en-US, es-ES |
| Aruba | AW | en-US |
| Bahamas | BS | en-US |
| Barbados | BB | en-US |
| Belize | BZ | en-US, es-ES |
| Bermuda | BM | en-US |
| Bolivia | BO | en-US, es-ES |
| Bonaire | BQ | en-US |
| Brazil | BR | en-US, pt-BR |
| Canada | CA | en-US, fr-FR |
| Saint Pierre and Miquelon | PM | en-US |
| Cayman Islands | KY | en-US, en-US |
| Chile | CL | en-US, es-ES |
| Colombia | CO | en-US, es-ES |
| Costa Rica | CR | en-US, es-ES |
| Dominican Republic | DO | en-US, es-ES |
| Ecuador | EC | en-US |
| El Salvador | SV | en-US, es-ES |
| French Guiana | GF | en-US, fr-FR  |
| Guadeloupe | GP | en-US |
| Guatemala | GT | en-US, es-ES |
| Honduras | HN | en-US, es-ES |
| Jamaica | JM | en-US |
| Martinique | MQ | en-US |
| Mexico | MX | en-US, es-ES |
| Nicaragua | NI | en-US, es-ES |
| Panama | PA | en-US, es-ES |
| Paraguay | PY | en-US, es-ES |
| Peru | PE | en-US, es-ES |
| Puerto Rico | PR | en-US, en-US |
| Saint Lucia | LC | en-US, en-US |
| Saint Martin | MF | en-US, en-US |
| Saint Vincent and the Grenadines | VC | en-US |
| Saint Kitts and Nevis | KN | en-US |
| Cura?ao | CW | en-US |
| Antarctica | AQ | en-US |
| British Virgin Islands | VG | en-US |
| Dominica | DM | en-US |
| Falkland Islands | FK | en-US |
| Grenada | GD | en-US |
| Guyana | GY | en-US |
| Haiti | HT | en-US |
| Montserrat | MS | en-US |
| Saba | XS | en-US |
| Saint Barth?lemy | BL | en-US |
| Sint Eustatius | XE | en-US |
| South Georgia and South Sandwich Islands | GS | en-US |
| Sint Maarten | SX | en-US, en-US |
| Suriname | SR | en-US |
| Trinidad and Tobago | TT | en-US |
| Turks and Caicos Islands | TC | en-US |
| United States | US | en-US |
| Uruguay | UY | en-US, es-ES |
| Venezuela | VE | en-US, es-ES |
| U.S. Virgin Islands | VI | en-US |
| Albania | AL | en-US |
| Andorra | AD | en-US |
| Armenia | AM | en-US |
| Austria | AT | en-US, de-DE |
| Azerbaijan | AZ | en-US |
| Belarus | BY | en-US, ru-RU |
| Belgium | BE | en-US, nl-NL |
| Bosnia and Herzegovina | BA | en-US |
| Bulgaria | BG | en-US, bg-BG |
| Croatia | HR | en-US, hr-HR |
| Cyprus | CY | en-US |
| Czechia | CZ | en-US, cs-CZ |
| Denmark | DK | en-US, da-DK |
| Estonia | EE | en-US, et-EE |
| Faroe Islands | FO | en-US |
| Monaco | MC | en-US, fr-FR |
| R?union | RE | en-US |
| Burkina Faso | BF | en-US |
| ?land Islands | AX | en-US |
| Bouvet Island | BV | en-US |
| Gibraltar | GI | en-US |
| Guernsey | GG | en-US |
| Svalbard | SJ | en-US |
| Jan Mayen | XJ | en-US |
| Finland | FI | en-US, fi-FI |
| France | FR | en-US, fr-FR |
| Georgia | GE | en-US |
| Germany | DE | en-US, de-DE |
| Greece | GR | en-US, el-GR |
| Greenland | GL | en-US |
| Hungary | HU | en-US, hu-HU |
| Iceland | IS | en-US |
| Ireland | IE | en-US |
| Isle of Man | IM | en-US |
| Italy | IT | en-US, it-IT |
| Jersey | JE | en-US |
| Latvia | LV | en-US, lv-LV |
| Liechtenstein | LI | en-US, de-DE |
| Lithuania | LT | en-US, lt-LT |
| Luxembourg | LU | en-US, fr-FR |
| Macedonia, FYRO | MK | en-US |
| Madagascar | MG | en-US |
| Malawi | MW | en-US |
| Mali | ML | en-US |
| Malta | MT | en-US |
| Mayotte | YT | en-US |
| Moldova | MD | en-US, ro-RO |
| Montenegro | ME | en-US |
| Netherlands | NL | en-US, nl-NL |
| New Caledonia | NC | en-US |
| Norway | NO | en-US, nb-NO |
| Poland | PL | en-US, pl-PL |
| Portugal | PT | en-US, pt-PT |
| Romania | RO | en-US, ro-RO |
| Russia | RU | en-US, ru-RU |
| San Marino | SM | en-US |
| Serbia | RS | en-US, sr-Latn-RS, en-US |
| Slovakia | SK | en-US, sk-SK |
| Slovenia | SI | en-US, sl-SI |
| Spain | ES | en-US, es-ES, en-US, en-US |
| Sweden | SE | en-US, sv-SE |
| Switzerland | CH | en-US, fr-FR, en-US, en-US |
| Ukraine | UA | en-US, uk-UA |
| United Kingdom | GB | en-US |
| Vatican City | VA | en-US |
| Afghanistan | AF | en-US |
| Botswana | BW | en-US |
| Ethiopia | ET | en-US |
| Namibia | NA | en-US |
| Tajikistan | TJ | en-US |
| Tanzania | TZ | en-US |
| Turkmenistan | TM | en-US |
| Uganda | UG | en-US |
| Zambia | ZM | en-US |
| Central African Republic | CF | en-US |
| Chad | TD | en-US |
| Congo | CG | en-US |
| Congo (DRC) | CD | en-US |
| Djibouti | DJ | en-US |
| Equatorial Guinea | GQ | en-US |
| Eritrea | ER | en-US |
| Gabon | GA | en-US |
| Gambia | GM | en-US |
| Guinea | GN | en-US |
| Guinea-Bissau | GW | en-US |
| Liberia | LR | en-US |
| Sierra Leone | SL | en-US |
| Somalia | SO | en-US |
| South Sudan | SS | en-US |
| St Helena, Ascension, Tristan da Cunha | SH | en-US |
| British Indian Ocean Territory | IO | en-US |
| Kosovo | XK | en-US |
| Lesotho | LS | en-US |
| Mauritania | MR | en-US |
| Palestinian Authority | PS | en-US |
| eSwatini | SZ | en-US |
| Algeria | DZ | en-US, fr-FR, en-US |
| Angola | AO | en-US, pt-PT |
| Bahrain | BH | en-US, ar-SA |
| Benin | BJ | en-US |
| Burundi | BI | en-US |
| Cameroon | CM | en-US, fr-FR |
| Cabo Verde | CV | en-US, pt-PT |
| Comoros | KM | en-US |
| C?te d?Ivoire | CI | en-US, fr-FR |
| Egypt | EG | en-US, ar-SA |
| French Polynesia | PF | en-US |
| Ghana | GH | en-US |
| Iraq | IQ | en-US, ar-SA |
| Israel | IL | en-US, he-IL |
| Jordan | JO | en-US, ar-SA |
| Kenya | KE | en-US |
| Kuwait | KW | en-US, ar-SA |
| Lebanon | LB | en-US, ar-SA |
| Libya | LY | en-US, ar-SA |
| Mauritius | MU | en-US, ar-SA |
| Mongolia | MN | en-US |
| Morocco | MA | en-US, fr-FR, en-US |
| Mozambique | MZ | en-US |
| Niger | NE | en-US |
| Nigeria | NG | en-US |
| Oman | OM | en-US, ar-SA |
| Pakistan | PK | en-US |
| Qatar | QA | en-US, ar-SA |
| Rwanda | RW | en-US, fr-FR |
| S?o Tom? and Pr?ncipe | ST | en-US, fr-FR |
| Saudi Arabia | SA | en-US |
| Senegal | SN | en-US, fr-FR |
| Seychelles | SC | en-US |
| South Africa | ZA | en-US |
| Togo | TG | en-US |
| Tunisia | TN | en-US, fr-FR, en-US |
| Turkey | TR | en-US, tr-TR |
| United Arab Emirates | AE | en-US, ar-SA |
| Yemen | YE | en-US, ar-SA |
| Zimbabwe | ZW | en-US |
| Christmas Island | CX | en-US |
| Cocos (Keeling) Islands | CC | en-US |
| Cook Islands | CK | en-US |
| French Southern Territories | TF | en-US |
| Guam | GU | en-US |
| Heard Island and McDonald Islands | HM | en-US |
| Kiribati | KI | en-US |
| Micronesia | FM | en-US |
| Nauru | NR | en-US |
| Niue | NU | en-US |
| Norfolk Island | NF | en-US |
| Northern Mariana Islands | MP | en-US |
| Palau | PW | en-US |
| Tuvalu | TV | en-US |
| Wallis and Futuna | WF | en-US |
| American Samoa | AS | en-US |
| Samoa | WS | en-US |
| Vanuatu | VU | en-US |
| Australia | AU | en-US |
| Bangladesh | BD | en-US |
| Brunei | BN | en-US |
| Bhutan | BT | en-US |
| Cambodia | KH | en-US |
| Fiji | FJ | en-US |
| Hong Kong SAR | HK | en-US, zh-HK |
| India | IN | en-US, hi-IN |
| Indonesia | ID | en-US, id-ID |
| Japan | JP | en-US, ja-JP |
| Kazakhstan | KZ | en-US, kk-KZ |
| Kyrgyzstan | KG | en-US, ru-RU |
| Laos | LA | en-US |
| Macao SAR | MO | en-US, zh-HK |
| Malaysia | MY | en-US, ms-MY |
| Marshall Islands | MH | en-US |
| Maldives | MV | en-US |
| Myanmar | MM | en-US |
| Nepal | NP | en-US |
| New Zealand | NZ | en-US |
| Papua New Guinea | PG | en-US |
| Pitcairn Islands | PN | en-US |
| Philippines | PH | en-US |
| Singapore | SG | en-US, zh-SG |
| Solomon Islands | SB | en-US |
| Korea | KR | en-US, ko-KR |
| Sri Lanka | LK | en-US |
| Taiwan | TW | en-US, zh-HK |
| Tokelau | TK | en-US |
| Thailand | TH | en-US, th-TH |
| Timor-Leste | TL | en-US |
| Tonga | TO | en-US |
| Uzbekistan | UZ | en-US, ru-RU |
| Vietnam | VN | en-US, vi-VN |
| U.S. Outlying Islands | UM | en-US |

