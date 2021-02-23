---
uid: ReleaseNotes
---


# Release notes

PI Adapter for Azure Event Hubs 1.0
Adapter framework 1.3

## Overview

<!--Insert a brief description of your product here and a cross-reference for more information.  If these release notes cover service packs or patches in addition to the major release numbers, briefly identify each version covered.-->

## Fixes and enhancements

<!--*Remove this section if this is the first release of a product. If multiple releases are covered by this note, for example, if service packs and patches are added, these can either be sectioned by release, or, if lengthy, can have sub-pages per release.* -->

### Fixes

The following items were resolved in this release of *{ product name }*:

<!-- Use table style:-->
Work item | Description
---- | -----------
*{ work item # }* | *{ item description }*

### Enhancements

The following features were added in this release of *{ product name }*:

<!--*Use bullet style:*-->
* *{ new feature }*
* *{ new feature }*

## Known issues

The following problems and enhancements have been deferred until a future release.

<!--*Use bullets and tables as necessary (table format below).* -->
Item | Description
---- | -----------
*{ item # }* | *{ problem/enhancement description }*

## Setup

### System requirements

<!--*Provide a cross-reference to the system requirements section. For example,*-->

Refer to [System requirements](xref:SystemRequirements).

### Installation and upgrade

<!--*Provide a cross-reference to the installation procedure. For example,*-->

Refer to [Install the adapter](xref:InstallTheAdapter).

### Uninstallation

<!--*Provide a cross-reference to the uninstallation procedure. For example,*-->

Refer to [Uninstall the adapter](xref:UninstallTheAdapter).

## Security information and guidance

<!-- For information on how to complete this section, please refer to the [Security Wiki](https://dev.azure.com/osieng/engineering/_wiki/wikis/Architecture.wiki/1216/SDL-practice-described-in-release-notes)-->

### OSIsoft’s commitment

Because the PI System often serves as a barrier protecting control system networks and mission-critical infrastructure assets, OSIsoft is committed to (1) delivering a high-quality product and (2) communicating clearly what security issues have been addressed. This release of *{ product name }* is the highest quality and most secure version of the *{ product name }* released to date. OSIsoft's commitment to improving the PI System is ongoing, and each future version should raise the quality and security bar even further.

### Vulnerability communication

The practice of publicly disclosing internally discovered vulnerabilities is consistent with the [Common Industrial Control System Vulnerability Disclosure Framework](https://ics-cert.us-cert.gov/sites/default/files/ICSJWG-Archive/ICSJWG_Vulnerability_Disclosure_Framework_Final_1.pdf) developed by the [Industrial Control Systems Joint Working Group (ICSJWG)](https://ics-cert.us-cert.gov/Industrial-Control-Systems-Joint-Working-Group-ICSJWG). Despite the increased risk posed by greater transparency, OSIsoft is sharing this information to help you make an informed decision about when to upgrade to ensure your PI System has the best available protection.

For more information, refer to OSIsoft’s [Ethical Disclosure Policy](https://www.osisoft.com/ethical-disclosure-policy).

To report a security vulnerability, refer to OSIsoft's [Report a Security Vulnerability](https://www.osisoft.com/report-a-security-vulnerability).

### Vulnerability scoring

OSIsoft has selected the [Common Vulnerability Scoring System (CVSS)](https://www.first.org/cvss/v2/guide) to quantify the severity of security vulnerabilities for disclosure. To calculate the CVSS scores, OSIsoft uses the [National Vulnerability Database (NVD) calculator](https://nvd.nist.gov/cvss.cfm?calculator&amp;version=2) maintained by the National Institute of Standards and Technology (NIST).  OSIsoft uses Critical, High, Medium and Low categories to aggregate the CVSS Base scores. This removes some of the opinion-related errors of CVSS scoring.  As noted in the [CVSS specification](https://www.first.org/cvss/specification-document), Base scores range from 0 for the lowest severity to 10 for the highest severity.

### Overview of new vulnerabilities found or fixed

This section is intended to provide relevant security-related information to guide your installation or upgrade decision. OSIsoft is proactively disclosing aggregate information about the number and severity of *{ product name }* security vulnerabilities that are fixed in this release.

<!--*Provide an overview of the types of security vulnerabilities fixed in this release*-->

<!--*NOTE:  If NO security vulnerabilities are identified in the current release, please use the following italicized statement:*-->

_No security-related information is applicable to this release_

<!--*When vulnerabilities exist, product teams should decide which format works best specific to the release and/or is applicable.  Two different samples are provided below.*-->

**Sample A** - For this release of the *{ product name }*, *{ x number }* of security vulnerability has been identified and fixed.

Based on the CVSS scoring system this issue has been categorized as a High (7.0 – 8.9). This high-level security issue is network accessible and has been resolved in the *{ product release name and version }*. To reduce exposure to this security issue, either limit access to the port used by the PI SQL products, or upgrade to the latest release.

* **Sample A with OSIsoft sub-component** - Based on the CVSS scoring system this issue has been categorized as a High (7.0 – 8.9). This high-level security issue has been resolved in *{ OSIsoft’s PI SDK version 1.1 sub-component }* which has been packaged in this *{ PI ProcessBook 1998 release }*. To reduce exposure to this security issue upgrade to the latest release.

* **Sample A with 3rd Party sub-component** - Based on the CVSS scoring system this issue has been categorized as a High (7.0 – 8.9). This high-level security issue has been resolved in the 3rd Party *{ OpenSSL sub-component }* which has been packaged in this *{ PI Adapter for OPC UA 1.2 }* release . To reduce exposure to this security issue upgrade to the latest release.

**Sample B** - For this release of the *{ product name }*, *{x number}* of security vulnerability has been identified and fixed. The table below provides an overview of the types and severity of the security fixes.

Security vulnerabilities fixed in this release  
Severity category| CVSS base score range  | Number of fixed vulnerabilities
---- | ------ | -----------
Critical | 9.0-10 | *{ quantity }*
High | 7.0-8.9 | *{ quantity }*
Medium | 4.0-6.9 | *{ quantity }*
Low | 0-3.9 | *{ quantity }*

* **Sample B with sub-components** - For this release of the *{product name}*, *{x number}* of security vulnerability has been identified and fixed. The tables below provide an overview of the types and severity of the security fixes. {*Some/All*} of the vulnerabilities were associated with *{OSIsoft/3rd Party}* sub-component {*name*} which is packaged in this release.

    Summary of security vulnerabilities fixed in this release

    Severity category| CVSS base score range  | Number of fixed vulnerabilities
    ---- | ------ | -----------
    Critical | 9.0-10 | *{ quantity }*
    High | 7.0-8.9 | *{ quantity }*
    Medium | 4.0-6.9 | *{ quantity }*
    Low | 0-3.9 | *{ quantity }*

    Security vulnerabilities fixed in the *{OSIsoft/3rd Party}* sub-component {*name*}
    Severity category| CVSS base score range  | Number of fixed vulnerabilities
    ---- | ------ | -----------
    Critical | 9.0-10 | *{ quantity }*
    High | 7.0-8.9 | *{ quantity }*
    Medium | 4.0-6.9 | *{ quantity }*
    Low | 0-3.9 | *{ quantity }*

### Security vulnerabilities addressed in previous releases

<!--*If vulnerabilities were addressed in previous maintenance releases of this product, document the severity category and the number of fixed vulnerabilities below either in tabular or text format for each previous maintenance release that addressed a security vulnerability. Otherwise, remove this text and related heading.*-->

## Documentation overview

<!--*Remove this section if there is no documentation besides the documentation in which these release notes are included. For additional documentation, provide a brief description.

Example:*-->

**PI System Explorer User Guide:** Provides an overview and explains the functions of the PI System Explorer interface.

## Technical support and resources

<!--*Provide a cross-reference to the Technical Support and feedback section. For example,*-->

Refer to [Technical support and feedback](xref:TechnicalSupportAndFeedback).
