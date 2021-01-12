# Release Notes 1.1.3

## Table Of Contents

* [Scope](./#scope)
* [Documentation](./#documentation)
* [Code](./#code)
* [Tests](./#tests)
  * [a. In scope](./#a-in-scope)
  * [b. Not in scope or in progress](./#b-not-in-scope-or-in-progress)
  * [c. Test Execution Metrics](./#c-test-execution-metrics)
* [Known Issues](./#known-issues)
* [Acronyms](./#acronyms)

## Scope

MOSIP **1.1.3** succeeds **1.1.2** with enhancements and important defect fixes which were identified in [Release 1.1.2](../release-notes-1.1.2/#list-of-known-issues).

**Release Date:** December 14, 2020

**Key Highlights**

* [Enhancements](release-notes-1.1.3-features.md)
* [Defect fixes](release-notes-1.1.3-bug-fixes.md)

## Documentation

### 1. Platform

Includes functional requirements, process flows, architecture and high level design.

[Link to documentation](https://docs.mosip.io/platform/modules).

### 2. APIs

All APIs are documented [here](https://docs.mosip.io/platform/apis).

### 3. Design

Low level design documents for each module are available in the respective github repos.

## Code

* [Commons](https://github.com/mosip/commons/tree/v1.1.3)
* [Pre-registration](https://github.com/mosip/pre-registration/tree/v1.1.3)
* [Registration](https://github.com/mosip/registration/tree/v1.1.3)
* [ID Repository](https://github.com/mosip/id-repository/tree/v1.1.3)
* [ID Authentication](https://github.com/mosip/id-authentication/tree/v1.1.3)
* [Partner Management Services](https://github.com/mosip/partner-management-services/tree/v1.1.3)
* [Resident Services](https://github.com/mosip/resident-services/tree/v1.1.3)
* [Admin Services](https://github.com/mosip/admin-services/tree/v1.1.3)
* [Print Services](https://github.com/mosip/print/tree/v1.1.3)
* [Config Respository](https://github.com/mosip/mosip-config/tree/v1.1.3)
* [Reference Implementation](https://github.com/mosip/mosip-ref-impl/tree/v1.1.3)

{% hint style="info" %}
Code needs to be deployed as per the procedure depicted in [Sandbox Installer](https://github.com/mosip/mosip-infra/tree/1.1.3/deployment/sandbox-v2).
{% endhint %}

## Tests

### a. In scope

Basic integration testing was done covering the below modules.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Title</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Functional Testing</td>
      <td style="text-align:left">
        <p>Pre-registration (Dynamic UI &amp; APIs)</p>
        <p>Registration Client (Dynamic UI, functionality and upgrade)</p>
        <p>Kernel (APIs)</p>
        <p>Registration Processor (All flows have been covered)</p>
        <p>ID Authentication (APIs)</p>
        <p>Partner Management (APIs)</p>
        <p>ID Repository (APIs)</p>
        <p>Resident Services (APIs)</p>
        <p>Admin (UI &amp; APIs)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Configuration Testing</td>
      <td style="text-align:left">Testing was done for default configuration (two languages) and single
        language with changed ui specification for pre-registration and registration
        client (Further more we have changed the seed data to single language).</td>
    </tr>
    <tr>
      <td style="text-align:left">Version Tested</td>
      <td style="text-align:left">v1.1.3</td>
    </tr>
    <tr>
      <td style="text-align:left">Types of testing</td>
      <td style="text-align:left">
        <p>Smoke</p>
        <p>Functional</p>
        <p>Integration</p>
        <p>Regression</p>
        <p>Security</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Browser</td>
      <td style="text-align:left">Pre-Registration and Admin UI (Tested with the latest version of Chrome
        browser)</td>
    </tr>
    <tr>
      <td style="text-align:left">OS Support</td>
      <td style="text-align:left">Registration Client on Windows 10, MOSIP server components run as micro-services
        encapsulated as docker images</td>
    </tr>
  </tbody>
</table>

| Areas | Technology Used |
| :--- | :--- |
| Deployment Script Environment | CentOS on AWS |
| Registration Client with TPM 2.0 | Windows 10 |
| Biometrics Standard | CBEFF format \(Version - 2.0\) |
| MDS | MDS v0.9.5 |
| ABIS | ABIS Spec Version v0.9 |
| SDK | SDK Spec Version v0.9 |
| Key-store | HSM |
| Anti-virus | ClamAV |
| Maps | OpenstreetMap |
| Transliteration | ICU4J \(Library with French, Arabic languages\) |

### b. Not in scope or in progress

<table>
  <thead>
    <tr>
      <th style="text-align:left">Title</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Non-Functional Testing</td>
      <td style="text-align:left">
        <p>Performance Testing</p>
        <p>Reliability and Disaster recovery Testing</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">HSM</td>
      <td style="text-align:left">Testing was done using SoftHSM</td>
    </tr>
    <tr>
      <td style="text-align:left">Browser Support</td>
      <td style="text-align:left">Testing for Pre-registration and Admin UI was done using Chrome (latest
        version)</td>
    </tr>
  </tbody>
</table>

### c. Test Execution Metrics

| Test Execution | Test Cases | Executed Tests | Pass | Fail | Pending Execution | Pass% | Fail% |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Pre-registration | 111 | 107 | 103 | 4 | 4 | 96% | 4% |
| Resident Services | 47 | 37 | 34 | 3 | 10 | 92% | 8% |
| Admin Services | 165 | 160 | 153 | 7 | 5 | 96% | 4% |
| Authentication | 47 | 44 | 39 | 5 | 3 | 89% | 11% |
| Partner Management | 71 | 61 | 61 | 0 | 10 | 100% | 0% |
| Registration | 100 | 96 | 94 | 2 | 4 | 98% | 2% |
| Integration Scenarios | 27 | 20 | 17 | 3 | 7 | 85% | 15% |
| **Total** | 568 | 522 | 501 | 21 | 46 | 96% | 4% |

## Known Issues

The top issues identified in MOSIP 1.1.3 are listed below.

| Bug ID | Summary | Module |
| :--- | :--- | :--- |
| [MOSIP-10604](https://mosip.atlassian.net/browse/MOSIP-10604) | Wrong location data getting populated for demographic details in Reg-Client | Registration Client |
| [MOSIP-10729](https://mosip.atlassian.net/browse/MOSIP-10729) | Document upload page showing the Documents Categories even though they are inactive | Registration Client |
| [MOSIP-10719](https://mosip.atlassian.net/browse/MOSIP-10719) | In Update-UIN flow, if the Name fields are not filled and continued then "Mandatory Fields should be highlighted" | Registration Client |
| [MOSIP-10718](https://mosip.atlassian.net/browse/MOSIP-10718) | Incorrect error message while onboarding for "expired token" | Registration Client |
| [MOSIP-10716](https://mosip.atlassian.net/browse/MOSIP-10716) | UIN Update process should not make the DOB as mandatory field | Registration Client |
| [MOSIP-10715](https://mosip.atlassian.net/browse/MOSIP-10715) | Incorrect error message thrown for "Onboarding process" when RID is not assigned to user | Registration Client |
| [MOSIP-10605](https://mosip.atlassian.net/browse/MOSIP-10605) | DoB is not handled like the age for displaying Parent/Guardian details in an adult packet | Registration Client |
| [MOSIP-10568](https://mosip.atlassian.net/browse/MOSIP-10568) | Registration client Preview and acknowledgement pages have issues due to templates | Registration Client |
| [MOSIP-10503](https://mosip.atlassian.net/browse/MOSIP-10503) | In registration client packet upload page, packets uploaded from admin portal are not getting cleared leading to confusion | Registration Client |
| [MOSIP-9783](https://mosip.atlassian.net/browse/MOSIP-9783) | Sometimes images are displayed in inappropriate areas leading to restart of the registration client | Registration Client |
| [MOSIP-10849](https://mosip.atlassian.net/browse/MOSIP-10849) | Notification not working when a packet is reprocessed | Registration Processor |
| [MOSIP-10590](https://mosip.atlassian.net/browse/MOSIP-10590) | Double entries in Audit log for registration | Registration Client |
| [MOSIP-10587](https://mosip.atlassian.net/browse/MOSIP-10587) | Unable to upload more than 200 packets | Admin Services |
| [MOSIP-10469](https://mosip.atlassian.net/browse/MOSIP-10469) | Unable to create machine from admin console | Admin Services |
| [MOSIP-10241](https://mosip.atlassian.net/browse/MOSIP-10241) | While performing Bulk Upload for a table using Admin master Bulk Upload history table associated with it should also be updated | Admin Services |
| [MOSIP-10515](https://mosip.atlassian.net/browse/MOSIP-10515) | Unable to upload data in History tables via bulk Upload | Admin Services |
| [MOSIP-10854](https://mosip.atlassian.net/browse/MOSIP-10854) | Unable to upload the data using bulk upload from zoneUserHistory table | Admin Services |
| [MOSIP-10484](https://mosip.atlassian.net/browse/MOSIP-10484) | Incorrect role displayed in Admin UI when logged in as admin | Admin Services |
| [MOSIP-10397](https://mosip.atlassian.net/browse/MOSIP-10397) | API for Machine Master Create/Update doesn't handle the TPM Key updates | Admin Services |
| [MOSIP-10386](https://mosip.atlassian.net/browse/MOSIP-10386) | The centerType should not be removed from the already created center if it is deactivated | Admin Services |
| [MOSIP-10294](https://mosip.atlassian.net/browse/MOSIP-10294) | Unable to Activate or Deactivate the Holiday Master Data | Admin Services |
| [MOSIP-9255](https://mosip.atlassian.net/browse/MOSIP-9255) | The transaction is logged when only the table is selected with no csv and operation mentioned | Admin Services |
| [MOSIP-600](https://mosip.atlassian.net/browse/MOSIP-600) | Lunch Start time and Lunch End time is not visible in UI | Admin Services |
| [MOSIP-10621](https://mosip.atlassian.net/browse/MOSIP-10621) | Websub Subscription fails with error for one or more topics when 4 topics are subscribed in a row. | Commons |
| [MOSIP-534](https://mosip.atlassian.net/browse/MOSIP-534) | Updated keys are not present \(updated keys\) in the Key\_Store table in derby DB | Commons |
| [MOSIP-10408](https://mosip.atlassian.net/browse/MOSIP-10408) | Able to do OTP authentication with a different partner | Authentication |
| [MOSIP-10732](https://mosip.atlassian.net/browse/MOSIP-10732) | Able to insert values as string in id repo when they are defined as simpleType in the ID schema | Authentication |
| [MOSIP-10658](https://mosip.atlassian.net/browse/MOSIP-10658) | Changes in IDA templates are not reflected until service restart | Authentication |
| [MOSIP-10252](https://mosip.atlassian.net/browse/MOSIP-10252) | Change in policy/partner is not notified to IDA | Partner Management |
| [MOSIP-10843](https://mosip.atlassian.net/browse/MOSIP-10843) | Booking are getting created for Non-working days but not Working days | Pre-registration |
| [MOSIP-10586](https://mosip.atlassian.net/browse/MOSIP-10586) | SEND OTP remains disabled even after entering Captcha if Captcha is enabled | Pre-registration |
| [MOSIP-9852](https://mosip.atlassian.net/browse/MOSIP-9852) | No email is received after booking appointment | Pre-registration |
| [MOSIP-10834](https://mosip.atlassian.net/browse/MOSIP-10834) | The preregistartion.identity.name property should be present under UI | Pre-registration |
| [MOSIP-10492](https://mosip.atlassian.net/browse/MOSIP-10492) | The Age field is populated as NaN when navigated using keyboard | Pre-registration |

To see all open defects, see [https://mosip.atlassian.net/issues/?filter=10709](https://mosip.atlassian.net/issues/?filter=10709)

## Acronyms

| Acronyms | Full Form |
| :--- | :--- |
| MOSIP | Modular Open Source Identity Platform |
| ABIS | Automated Biometric Identification System |
| API | Application Programming Interface |
| ID | Identity |
| IDA | Identity Authentication |
| NFR | Non-Functional Requirements |
| OTP | One Time Password |
| SDK | Software Development Kit |
| JWT | Java Web Token |
| K8 | Kubernetes |
| UIN | Unique Identification Number |
| VID | Virtual ID |
| CBEFF | Common Biometric Exchange Formats Framework |
| CORS | Cross Origin Resource Sharing |
| HSM | Hardware Security Module |
| TPM | Trusted Platform Module |
| SDK | Software Development Kit |
| MDS | MOSIP Device Service |
| ICU4J | International Components for Unicode for Java |
| WIP | Work In Progress |
| TBD | To Be Determined/Done |
| MDS | MOSIP Device Specification |

