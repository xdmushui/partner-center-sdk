---
title: Partner Center supported languages and locales
description: List of ISO2 and ISO3 supported locales for Partner Center. 
ms.date: 01/23/2018
ms.localizationpriority: medium
---

# Partner Center supported languages and locales


**Applies To**

-   Partner Center
-   Partner Center operated by 21Vianet
-   Partner Center for Microsoft Cloud Germany
-   Partner Center for Microsoft Cloud for US Government

Some Partner Center APIs require a value indicating a locale, country or region. For example, the [Partner Center REST header](headers.md) X-Locale requires a value in the format “language – country” (“en-us” indicates “English – United States”).

In the Partner Center managed APIs, the [CountryValidationRules](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.countryvalidationrules.countryvalidationrules) class and the [OfferCategory.Locale](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.offers.offercategory.locale), [ServiceRequest.CountryCode](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.countrycode), or [CustomerBillingProfile.Culture](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile.culture) properties require string values that indicate a language or country/region (in the form of an ISO2 language code or ISO3 country/region code), a locale, or a culture (a language ID combined with a country/region code).

The following table lists the locales (language – country/region), languages, and country/region codes that are supported in the Partner Center APIs. 

| Locale     | Language                | ISO 2 Language Code | ISO 3 Country/Region Code | Country/Region (short form) |
|------------|-------------------------|---------------------|---------------------------|-----------------------------|
| bg-bg	     | Bulgarian	           | BG                  | BGR                       | Bulgaria                    |
| ca-es	     | Catalan                 | ES                  | ESP                       | Spain                       |
| cs-cz	     | Czech                   | CZ                  | CZE                       | Czechia                     |
| da-dk	     | Danish                  | DK                  | DNK                       | Denmark                     |
| de-de	     | German                  | DE                  | DEU                       | Germany                     |
| el-gr	     | Greek                   | GR                  | GRC                       | Greece                      |
| en-us	     | English                 | US                  | USA                       | United States               |
| es-es	     | Spanish                 | ES                  | ESP                       | Spain                       |
| et-ee	     | Estonian                | EE                  | EST                       | Estonia                     |
| eu-es	     | Basque                  | ES                  | ESP                       | Spain                       |
| fi-fi	     | Finish                  | FI                  | FIN                       | Finland                     |
| fr-fr      | French                  | FR                  | FRA                       | France                      |
| gl-es	     | Galician                | ES                  | EPS                       | Spain                       |
| he-il	     | Hebrew                  | IL                  | ISR                       | Israel                      |
| hi-in	     | Hindi                   | IN                  | IND                       | India                       |
| hr-hr	     | Croatian                | HR                  | HRV                       | Croatia                     |
| hu-hu	     | Hungarian               | HU                  | HUN                       | Hungary                     |
| id-id	     | Indonesian              | ID                  | IDN                       | Indonesia                   |
| it-it	     | Italian                 | IT                  | ITA                       | Italy                       |
| ja-jp	     | Japanese                | JP                  | JPN                       | Japan                       |
| kk-kz	     | Kazakh                  | KZ                  | KAZ                       | Kazakhstan                  |
| ko-kr	     | Korean                  | KR                  | KOR                       | Korea                       |
| lt-lt	     | Lithuanian              | LT                  | LTU                       | Lithuania                   |
| lv-lv	     | Latvian                 | LV                  | LVA                       | Latvia                      |
| ms-my	     | Malay                   | MY                  | MYS                       | Malaysia                    |
| nb-no	     | Norwegian (Bokmal)      | NO                  | NOR                       | Norway                      |
| nl-nl	     | Dutch                   | NL                  | NLD                       | Netherlands                 |
| pl-pl	     | Polish                  | PL                  | POL                       | Poland                      |
| pt-br	     | Portuguese              | BR                  | BRA                       | Brazil                      |
| pt-pt	     | Portuguese              | PT                  | PRT                       | Portugal                    |
| ro-ro	     | Romanian                | RO                  | ROU                       | Romania                     |
| ru-ru	     | Russian                 | RU                  | RUS                       | Russia                      |
| sk-sk	     | Slovak                  | SK                  | SVK                       | Slovakia                    |
| sl-si	     | Slovenian               | SI                  | SVN                       | Slovenia                    |
| sr-cyrl-rs | Serbian (Cyrillic)      | RS                  | SRB                       | Serbia                      |
| sr-latn-rs | Serbian (Latin)         | RS                  | SRB                       | Serbia                      |
| sv-se	     | Swedish                 | SE                  | SWE                       | Sweden                      |
| th-th	     | Thai                    | TH                  | THA                       | Thailand                    |
| tr-tr	     | Turkish                 | TR                  | TUR                       | Turkey                      |
| uk-ua	     | Ukranian                | UA                  | UKR                       | Ukraine                     |
| vi-vn	     | Vietnamese              | VN                  | VNM                       | Vietnam                     |
| zh-cn	     | Chinese (Simplified)    | CN                  | CHN                       | China                       |
| zh-sg	     | Chinese (Simplified)    | SG                  | SGP                       | Singapore                   |
| zh-tw	     | Chinese (Traditional)   | TW                  | TWN                       | Taiwan                      |
 

