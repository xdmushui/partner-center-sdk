---
title: CountryInformation
description: Descriptive metadata for a country/region.
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/PartnerCenter'
ms.assetid: 19460437-5611-49A1-A7E7-704420C1DE8F
---

# CountryInformation


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Descriptive metadata for a country/region.

## <span id="Properties"></span><span id="properties"></span><span id="PROPERTIES"></span>Properties


| Property                      | Type               | Description                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData                 | string             | The extension data.                                                                                |
| Iso2Code                      | string             | An ISO-2 code.                                                                                     |
| Iso3Code                      | string             | An ISO-3 code.                                                                                     |
| DefaultCulture                | string             | The default culture.                                                                               |
| IsStateRequired               | boolean            | Indicates whether a state/province is required or not.                                             |
| SupportedStatesList           | array of strings   | If a state/province is required, returns the full list for that country/region.                    |
| SupportedLanguagesList        | array of strings   | A list of supported languages.                                                                     |
| SupportedCulturesList         | array of strings   | A list of supported cultures.                                                                      |
| IsPostalCodeRequired          | boolean            | Indicates whether a ZIP code or postal code is required or not.                                    |
| PostalCodeRegex               | string             | The regular expression that defines the ZIP/postal code .                                          |
| IsCityRequired                | boolean            | Indicates whether a city is required or not.                                                       |
| IsVatIdSupported              | boolean            | Indicates whether a VAT ID is required or not.                                                     |
| TaxIdFormat                   | string             | The tax ID format.                                                                                 |
| TaxIdSample                   | string             | The tax ID sample.                                                                                 |
| VatIdRegex                    | string             | The tax ID regular expression.                                                                     |
| PhoneNumberRegex              | string             | The phone number regular expression.                                                               |
| IsRegistrationNumberSupported | boolean            | Indicates whether a registration number is supported or not.                                       |
| IsTaxIdSupported              | boolean            | Indicates whether a tax ID is supported or not. Note that this is different than IsVatIdSupported. |
| ResellerAgreementRegion       | string             | The reseller agreement region.                                                                     |
| GeographicRegion              | string             | The geographic region.                                                                             |
| CountryCallingCodesList       | array of strings   | The calling codes supported in the country/region.                                                 |
| Attributes                    | ResourceAttributes | The metadata attributes corresponding to the CountryInformation resource.                          |

 

## <span id="CountryValidationRules"></span><span id="countryvalidationrules"></span><span id="COUNTRYVALIDATIONRULES"></span>CountryValidationRules


Describes the address formatting rules for a country/region.

| Property                | Type               | Description                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | string             | An ISO-2 code.                                                                                     |
| DefaultCulture          | string             | The default culture.                                                                               |
| IsStateRequired         | boolean            | Indicates whether a state/province is required or not.                                             |
| SupportedStatesList     | array of strings   | If a state/province is required, returns the full list for that country/region.                    |
| SupportedLanguagesList  | array of strings   | A list of supported languages.                                                                     |
| SupportedCulturesList   | array of strings   | A list of supported cultures.                                                                      |
| IsPostalCodeRequired    | boolean            | Indicates whether a ZIP code or postal code is required or not.                                    |
| PostalCodeRegex         | string             | The regular expression that defines the ZIP/postal code .                                          |
| IsCityRequired          | boolean            | Indicates whether a city is required or not.                                                       |
| IsVatIdSupported        | boolean            | Indicates whether a VAT ID is required or not.                                                     |
| TaxIdFormat             | string             | The tax ID format.                                                                                 |
| TaxIdSample             | string             | The tax ID sample.                                                                                 |
| VatIdRegex              | string             | The tax ID regular expression.                                                                     |
| PhoneNumberRegex        | string             | The phone number regular expression.                                                               |
| IsTaxIdSupported        | boolean            | Indicates whether a tax ID is supported or not. Note that this is different than IsVatIdSupported. |
| IsTaxIdOptional         | boolean            | Indicates whether a tax ID is optional or not.                                                     |
| CountryCallingCodesList | array of strings   | The calling codes supported in the country/region.                                                 |
| Attributes              | ResourceAttributes | The metadata attributes corresponding to the CountryInformation resource.                          |

 

 

 




