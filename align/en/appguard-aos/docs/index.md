# NHN AppGuard Android Developer's Guide

<a id="document-information"></a>
## Document Information { #document-information }

<a id="document-information-2"></a>
### Document Information { #document-information-2 }
This document is a Developer's Guide, including an SDK manual for using NHN AppGuard. 

<a id="written-on"></a>
### Written on { #written-on }
04-14-2026

<a id="contact"></a>
### Contact { #contact }
For assistance, use [Customer Support > Contact Us](https://www.nhncloud.com/kr/support/inquiry) on the NHN Cloud website.

<a id="index"></a>
## Index { #index }

{%- if variant == 'saas' %}

<a id="preparations-for-application"></a>
### 1. [Preparations for Application](preparation/environment.md) { #preparations-for-application }
1.1 [Supported Environment](preparation/environment.md)
1.2 [How to Apply NHN AppGuard](preparation/approach.md)
1.3 [Checks before Application](preparation/prerequisites-saas.md)

<a id="protection"></a>
### 2. [Protection](protection/console.md) { #protection }
2.1 [Protection Using Web Console](protection/console.md)
2.2 [Protection Using CLI](protection/cli-saas.md)
2.3 [Protection Using Plugin](protection/plugin.md)

<a id="sdk-integration-guide"></a>
### 3. [SDK Integration Guide](sdk/overview-saas.md) { #sdk-integration-guide }
3.1 [SDK Integration](sdk/overview-saas.md)
3.2 [Java SDK Integration](sdk/java.md)
3.3 [Unreal SDK Integration](sdk/unreal.md)
{%- else %}

<!-- pre-align: ko에 대응 섹션 없음 — 검토 필요 (No KO counterpart; k6 (적용 준비) is already matched to t6 — t9 'Preparation' is a spurious entry with no equivalent in the KO outline, inserted between the two SDK Integration Guide entries) -->
<!-- pre-align: ko에 대응 섹션 없음 — 검토 필요 (t9 'Preparation' appears to duplicate t6 'Preparations for Application'; k6 is already matched to t6, and there is no second ko heading for preparation in this position) -->
<a id="sdk-integration-guide"></a>
### 1. [Preparation](preparation/environment.md) { #sdk-integration-guide }
1.1 [Supported Environments](preparation/environment.md)
1.2 [NHN AppGuard Integration Methods](preparation/approach.md)
1.3 [Prerequisites](preparation/prerequisites-onprem.md)

<a id="index-protection"></a>
### 2. [Protection](protection/cli-onprem.md) { #index-protection }
2.1 [Protection Using CLI](protection/cli-onprem.md)

<a id="index-sdk-integration-guide"></a>
### 3. [SDK Integration Guide](sdk/overview-onprem.md) { #index-sdk-integration-guide }
3.1 [SDK Integration](sdk/overview-onprem.md)
3.2 [Java SDK Integration](sdk/java.md)
{%- endif %}

<a id="encryption-api-application-guide"></a>
### 4. [Encryption API Application Guide](encryption/overview.md) { #encryption-api-application-guide }
4.1 [Encryption API](encryption/overview.md)
4.2 [Private Key Encryption Structure](encryption/key-encryption.md)
4.3 [Encryption Data Structure](encryption/data-structure.md)
4.4 [Decryption Flow for Encryption Data](encryption/decryption-flow.md)
4.5 [API Reference](encryption/api-reference.md)

<a id="integrity-verification-guide"></a>
### 5. [Integrity Verification Guide](app-attestation/overview.md) { #integrity-verification-guide }
5.1 [Overview](app-attestation/overview.md)
5.2 [Console Integrity Verification Settings](app-attestation/console.md)
5.3 [How to Use Integrity Verification](app-attestation/sdk.md)

<a id="resource-string-obfuscation"></a>
### 6. [Resource String Obfuscation](resource-string-obfuscation/overview.md) { #resource-string-obfuscation }
6.1 [Overview](resource-string-obfuscation/overview.md)
6.2 [Configuration File Format](resource-string-obfuscation/config.md)

<a id="log-and-callback-information"></a>
### 7. [Log and Callback Information](logs/overview.md) { #log-and-callback-information }
7.1 [Log Details](logs/overview.md)
7.2 [Callback Data](logs/callback-data.md)
7.3 [Guide to Sanctions](logs/sanctions-guide.md)

<a id="checks-and-cautions"></a>
### 8. [Checks and Cautions](testing/integration.md) { #checks-and-cautions }
8.1 [Integration Test](testing/integration.md)
8.2 [Checks when Applying ProGuard](testing/proguard.md)
8.3 [Integrity Verification for App Signature Key](testing/signature-verification.md)

<a id="faq"></a>
### 9. [FAQ](faq/general.md) { #faq }
9.1 [Common Error](faq/general.md)
9.2 [Cocos2D Game Error](faq/cocos2d.md)

<a id="copyright"></a>
## Copyright { #copyright }
---

!!! danger "Copyright"
    Copyright © 2022 NHN Cloud Corp. All rights reserved.
    
    This document is the intellectual property of NHN Cloud and cannot be modified or used for any other purpose without NHN Cloud's permission. This document is provided for informational purposes only. While NHN Cloud has endeavored to verify the completeness and accuracy of the information contained in this document, NHN Cloud assumes no responsibility for any errors or omissions that may occur. Therefore, the user is solely responsible for the use or results of this document, and NHN Cloud makes no warranties, express or implied, regarding this. 
    Specific software products or products mentioned in this document, including related URL information, are subject to the copyright laws of their respective owners. Compliance with such copyright laws is the user's responsibility.

    NHN Cloud reserves the right to change the contents of this document without prior notice.
