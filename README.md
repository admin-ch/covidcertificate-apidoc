# Swiss Covid Certificate - API documentation - WIP

- [Swiss Covid Certificate - API documentation - WIP](#swiss-covid-certificate---api-documentation---wip)
  * [Introduction](#introduction)
    + [Links to EU digital green certificate](#links-to-eu-digital-green-certificate)
  * [Third party system integration](#third-party-system-integration)
    + [Prerequisites](#prerequisites)
    + [Integration achitecture](#integration-achitecture)
      - [Integration with OneTime password](#integration-with-onetime-password)
    + [Security architecture](#security-architecture)
      - [Authorized user](#authorized-user)
      - [TLS tunnel](#tls-tunnel)
    + [Integration cookbook](#integration-cookbook)
    + [Integration examples](#integration-examples)
  * [API doc](#api-doc)
    + [Generation API](#generation-api)
      - [Error list](#error-list)
    + [Revokation API](#revokation-api)
    + [Verification API](#verification-api)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

## Introduction

The swiss covid certificate system can be used by third party systems in order to generate, revoke and verify covid certificates compatible with the EU digital green certificate. This repository contains technical information about how to integrate third party systems.

The swiss covid certificate system is hosted and maintained by FOITT.

### Links to EU digital green certificate
- Specification of EU digital greeen certificate: https://ec.europa.eu/health/ehealth/covid-19_en
- Code repository of EU digital greeen certificate: https://github.com/eu-digital-green-certificates

## Third party system integration

### Prerequisites

1. Only authorized users (natural persons) can access the generation and revokation API. Authorized users are determined by the cantons or FOPH.
2. Verification API is freely accessible.
3. Third party systems have to sign an agreement with FOITT in order to access the generation and verification API.

### Integration achitecture

#### Integration with OneTime password

![image](https://user-images.githubusercontent.com/319676/118224719-035c5e80-b484-11eb-8809-a90a7ea1548b.png)

The use of the API is done by using an OTP that has been loaded beforehand in the primary system and introduced in the REST request. The OTP has a limited validity.

1. The authorized user previously registered and recognised by eIAM can obtain an OTP by logging on to the Web management UI page.
2. When the authorized user accesses the Web management UI, its rights are verified by eIAM System
3. The authorized user must insert this OTP in the primary system so that it is transmitted when calling the API.
4. One-way authentication is used to create the TLS tunnel to protect the data transfer.
5. The OTP is transferred so that the authorized user can be identified, as header of the request.
6. The content is hashed and signed with primary key of the "SwissGov Regular CA 01" certificate.
7. The dataset structured as JSON Schema is created and transported within the secured TLS tunnel.
8. The Management Service REST Api checks the integrity of the data and signature received and the OTP. 

#### API sequence diagram

![image](https://user-images.githubusercontent.com/319676/118361751-0db64f80-b58d-11eb-8f5a-fc7e193a1a00.png)

### Security architecture

#### Authorized user

The authorized users are onboarded in EIAM and can use a CHLogin or a HIN identity. They access the API by sending an OneTime password (a JSON Web Token - JWT) generated from the Web UI.

#### TLS tunnel

A TLS tunnel (single way authentication) is made between the primary system and the API gateway. One "SwissGov Regular CA 01" certificate is delivered to each primary system for this purpose.

#### Content signature

The content transferred to the API is signed with the "SwissGov Regular CA 01" certificate. The public key of the "SwissGov Regular CA 01" certificate has not to be added to the API request.

### Integration cookbook

TBD 

### Integration examples

TBD

## API doc

### Generation API

The generation API allows to create 3 types of covid certificate: vaccination, test and recovery.

Please import the `api-doc.json` file in the https://editor.swagger.io to see the visualization.

#### Error list
There is a custom error body for the request if the server side parameter validation fails.
- `{451, "No vaccination data was specified"}`
- `{452, "No person data was specified"}`
- `{453, "Invalid dateOfBirth! Must be younger than 1900-01-01"}`
- `{454, "Invalid vaccine prophylaxis"}`
- `{455, "Invalid medicinal product"}`
- `{456, "Invalid marketing authorization holder"}`
- `{457, "Invalid number of doses"}`
- `{458, "Invalid vaccination date! Date cannot be in the future"}`
- `{459, "Invalid country of vaccination"}`
- `{460, "Invalid given name! Must not exceed 50 chars"}`
- `{461, "Invalid family name! Must not exceed 50 chars"}`
- `{462, "No test data was specified"}`
- `{463, "Invalid member state of test"}`
- `{464, "Invalid type of test"}`
- `{465, "Invalid test name"}`
- `{466, "Invalid test manufacturer"}`
- `{467, "Invalid testing center or facility"}`
- `{468, "Invalid sample or result date time! Sample date must be before current date and before result date"}`
- `{469, "No recovery data specified"}`
- `{470, "Invalid date of first positive test result"}`
- `{471, "Invalid country of test"}`

### Revokation API

### Verification API


