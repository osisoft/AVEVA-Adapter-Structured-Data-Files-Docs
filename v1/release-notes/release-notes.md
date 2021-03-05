---
uid: ReleaseNotes
---

# Release notes

PI Adapter for Structured Data Files 1.0 <br>
Adapter framework 1.3

## Overview

This represents the initial release for PI Adapter for Structured Data Files. This product collects time series data from source files in a local or remote directory to OMF endpoints in OSIsoft Cloud Services, Edge Data Store, or PI Servers. PI Adapter for Structured Data Files can also collect health and diagnostics information. It supports buffering, static and event data collection, and various Windows and Linux-based operating systems as well as containerization.

**Note:** FTP servers are not supported for this version.

For more information, see the [PI Adapter for Structured Data Files overview](xref:PIAdapterforSDFOverview).

## Known issues

There are no known issues at this time.

## System requirements

Refer to [System requirements](xref:SystemRequirements).

## Installation

Refer to [Install the adapter](xref:InstallTheAdapter).

## Uninstallation

Refer to [Uninstall the adapter](xref:UninstallTheAdapter).

## Security information and guidance

### OSIsoft's commitment

Because the PI System often serves as a barrier protecting control system networks and mission-critical infrastructure assets, OSIsoft is committed to (1) delivering a high-quality product and (2) communicating clearly what security issues have been addressed. This release of PI Adapter for Structured Data Files is the highest quality and most secure version of the PI Adapter for Structured Data Files released to date. OSIsoft's commitment to improving the PI System is ongoing, and each future version should raise the quality and security bar even further.

### Vulnerability communication

The practice of publicly disclosing internally discovered vulnerabilities is consistent with the [Common Industrial Control System Vulnerability Disclosure Framework](https://ics-cert.us-cert.gov/sites/default/files/ICSJWG-Archive/ICSJWG_Vulnerability_Disclosure_Framework_Final_1.pdf) developed by the [Industrial Control Systems Joint Working Group (ICSJWG)](https://ics-cert.us-cert.gov/Industrial-Control-Systems-Joint-Working-Group-ICSJWG). Despite the increased risk posed by greater transparency, OSIsoft is sharing this information to help you make an informed decision about when to upgrade to ensure your PI System has the best available protection.

For more information, refer to [OSIsoft's Ethical Disclosure Policy (https://www.osisoft.com/ethical-disclosure-policy)](https://www.osisoft.com/ethical-disclosure-policy).

To report a security vulnerability, refer to [OSIsoft's Report a Security Vulnerability (https://www.osisoft.com/report-a-security-vulnerability)](https://www.osisoft.com/report-a-security-vulnerability).

### Vulnerability scoring

OSIsoft has selected the [Common Vulnerability Scoring System (CVSS)](https://www.first.org/cvss/v2/guide) to quantify the severity of security vulnerabilities for disclosure. To calculate the CVSS scores, OSIsoft uses the [National Vulnerability Database (NVD) calculator](https://nvd.nist.gov/cvss.cfm?calculator&amp;version=2)  maintained by the National Institute of Standards and Technology (NIST). OSIsoft uses Critical, High, Medium and Low categories to aggregate the CVSS Base scores. This removes some of the opinion related errors of CVSS scoring. As noted in the CVSS specification, Base score range from 0 for the lowest severity to 10 for the highest severity.

### Overview of new vulnerabilities found or fixed

No additional security vulnerabilities are applicable to this release. Sub-components of this release contain known vulnerabilities which are not exploitable in PI Adapter for Structured Data Files.

The following table lists the known vulnerabilities and their mitigation in this product.

 Component | Version | CVE or Reference | CVSS | Mitigation
 --------- | ------- | -----------------| ------ | ----------
 json.Net | 12.0.3 | [Applications that use Newtonsoft.Json might be exposed to DOS vulnerability](https://alephsecurity.com/vulns/aleph-2018004) | 6.8 | Limit MaxDepth when parsing to 100. No code paths result in json parsing and subsequent serialization directly back to a string.

## Technical support and resources

Refer to [Technical support and feedback](xref:TechnicalSupportAndFeedback).
