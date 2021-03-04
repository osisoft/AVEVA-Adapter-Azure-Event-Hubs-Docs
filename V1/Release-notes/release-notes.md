---
uid: ReleaseNotes
---


# Release notes

PI Adapter for Azure Event Hubs 1.0<br>
Adapter framework 1.3 

## Overview

PI Adapter for Azure Event Hubs is a data-collection component that transfers time-series data from Event Hubs to OMF endpoints in OSIsoft Cloud Services or PI Servers.  For more information, refer to [PI Adapter for Azure Event Hubs overview](xref:index). 


## Known issues

The following problems and enhancements have been deferred until a future release.

<!--*Use bullets and tables as necessary (table format below).* -->
Item | Description
---- | -----------
197937 | Timeout may occur when submitting a POST for data selection configurations to the adapter that contain more than 10,000 streams.

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

<!-- For information on how to complete this section, please refer to the [Security Wiki](https://dev.azure.com/osieng/engineering/_wiki/wikis/Architecture.wiki/15575/SDL-practice-described-in-release-notes)-->

### OSIsoft’s commitment

Because the PI System often serves as a barrier protecting control system networks and mission-critical infrastructure assets, OSIsoft is committed to (1) delivering a high-quality product and (2) communicating clearly what security issues have been addressed. This release of PI Adapter for Azure Event Hubs is the highest quality and most secure version of the PI Adapter for Azure Event Hubs released to date. OSIsoft's commitment to improving the PI System is ongoing, and each future version should raise the quality and security bar even further.

### Vulnerability communication

The practice of publicly disclosing internally discovered vulnerabilities is consistent with the [Common Industrial Control System Vulnerability Disclosure Framework](https://ics-cert.us-cert.gov/sites/default/files/ICSJWG-Archive/ICSJWG_Vulnerability_Disclosure_Framework_Final_1.pdf) developed by the [Industrial Control Systems Joint Working Group (ICSJWG)](https://ics-cert.us-cert.gov/Industrial-Control-Systems-Joint-Working-Group-ICSJWG). Despite the increased risk posed by greater transparency, OSIsoft is sharing this information to help you make an informed decision about when to upgrade to ensure your PI System has the best available protection.

For more information, refer to OSIsoft’s [Ethical Disclosure Policy](https://www.osisoft.com/ethical-disclosure-policy).

To report a security vulnerability, refer to OSIsoft's [Report a Security Vulnerability](https://www.osisoft.com/report-a-security-vulnerability).

### Vulnerability scoring

OSIsoft has selected the [Common Vulnerability Scoring System (CVSS)](https://www.first.org/cvss/v2/guide) to quantify the severity of security vulnerabilities for disclosure. To calculate the CVSS scores, OSIsoft uses the [National Vulnerability Database (NVD) calculator](https://nvd.nist.gov/cvss.cfm?calculator&amp;version=2) maintained by the National Institute of Standards and Technology (NIST).  OSIsoft uses Critical, High, Medium and Low categories to aggregate the CVSS Base scores. This removes some of the opinion-related errors of CVSS scoring.  As noted in the [CVSS specification](https://www.first.org/cvss/specification-document), Base scores range from 0 for the lowest severity to 10 for the highest severity.

### Overview of new vulnerabilities found or fixed

This section is intended to provide relevant security-related information to guide your installation or upgrade decision. OSIsoft is proactively disclosing aggregate information about the number and severity of PI Adapter for Azure Event Hubs security vulnerabilities that are fixed in this release.

<!--*Provide an overview of the types of security vulnerabilities fixed in this release*-->

<!--*NOTE:  If NO security vulnerabilities are identified in the current release, please use the following italicized statement:*-->

_No security-related information is applicable to this release_

<!--*When vulnerabilities exist, product teams should decide which format works best specific to the release and/or is applicable.  Two different samples are provided below.*-->

## Technical support and resources

<!--*Provide a cross-reference to the Technical Support and feedback section. For example,*-->

Refer to [Technical support and feedback](xref:TechnicalSupportAndFeedback).
