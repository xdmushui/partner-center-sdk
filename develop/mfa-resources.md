---
title: Partner Security requirements resources
description: Understand multi-factor authentication (MFA) adoption details to meet Partner Security Requirements.
ms.service: partner-dashboard
ms.subservice:  partnercenter-sdk
ms.date: 05/29/2020
---

# Partner security requirements resources

This article helps you understand multi-factor authentication (MFA) adoption details, to help your organization meet partner security requirement status. 

## Portal request without MFA

Indicate a user who accesses Partner Center portal without MFA authentication.

| Property                            | Type            | Description                           |
|-------------------------------------|-----------------|---------------------------------------|
| ObjectId                            | string          | User Object ID                        |
| TenantId                            | string          | CSP tenant ID                         |
| Upn                                 | string          | User principal name                   |
| LastNonMfaCompliantLoginDateTime    | datetime        | Latest time user login-in without MFA |


## API request summarized by Application

A summary of API request made by APP + User credential, aggregated by request date and Application ID.

| Property                            | Type            | Description               |
|-------------------------------------|-----------------|---------------------------|
| LoginDate                           | datetime        | API request date          |
| MfaCompliantRequestCount            | long            | Request count with MFA    |
| TotalRequestCount                   | long            | Total request count       |
| ApplicationId                       | string          | The application ID        |
| ApplicationName                     | string          | The application name      |


## API request details

API request made by APP + User credential. 

| Property                            | Type            | Description                              |
|-------------------------------------|-----------------|------------------------------------------|
| RequestId                           | string          | MS-RequestId                             |
| CorrelationId                       | string          | MS-CorrelationId                         |
| OperationName                       | string          | The API path with request method         |
| RequestDateTime                     | DateTime        | The API request time                     |
| IpAddress                           | string          | Source IP address                        |
| ObjectId                            | string          | User object ID                           |
| TenantId                            | string          | CSP tenant ID                            |
| Upn                                 | string          | User principal name                      |
| ApplicationId                       | string          | Your application                         |
| MfaCompliant                        | bool            | Indicate the request with or without MFA |
