<!-- machine_translated: true -->

<!-- pre-align:aligned sig=e6088b8c4131 -->

# NHN AppGuard Android Developer's Guide

<a id="document-information"></a>
## Document Information { #document-information }

<a id="document-information-2"></a>
### Document Information { #document-information-2 }

This document is a Developer's Guide, including an SDK manual for using NHN AppGuard. 

<a id="written-on"></a>
### Written on { #written-on }

2026-09-15

<a id="contact"></a>
### Contact { #contact }

For assistance, use [Customer Support > Contact Us](https://www.nhncloud.com/kr/support/inquiry) on the NHN Cloud website.

<a id="index"></a>
## Index { #index }

<a id="preparations-for-application"></a>
### 1. [Preparations for Application](preparation/environment.md) { #preparations-for-application }

1.1 [Supported Environment](preparation/environment.md)
1.2 [How to Apply NHN AppGuard](preparation/approach.md)
{%- if variant == 'saas' %}
1.3 [Checks before Application](preparation/prerequisites-saas.md)
{%- else %}
1.3 [Checks before Application](preparation/prerequisites-onprem.md)
{%- endif %}

{%- if variant == 'saas' %}

<a id="protection"></a>
### 2. [Protection](protection/console.md) { #protection }

2.1 [Protection Using Web Console](protection/console.md)
2.2 [Protection Using CLI](protection/cli-saas.md)
2.3 [Protection Using Plugin](protection/plugin.md)
{%- else %}

<a id="index-protection"></a>
### 2. [Protection](protection/cli-onprem.md) { #index-protection }

2.1 [Protection Using CLI](protection/cli-onprem.md)
{%- endif %}

<a id="unified-configuration-file"></a>
### 3. [Unified Configuration File](configuration/overview.md) { #unified-configuration-file }

3.1 [Overview](configuration/overview.md)
3.2 [Settings by Feature](configuration/sections.md)
{%- if variant == 'saas' %}

<a id="sdk-integration-guide"></a>
### 4. [SDK Integration Guide](sdk/overview-saas.md) { #sdk-integration-guide }

4.1 [SDK Integration](sdk/overview-saas.md)
4.2 [Java SDK Integration](sdk/java.md)
4.3 [Unreal SDK Integration](sdk/unreal.md)
{%- else %}

<a id="index-sdk-integration-guide"></a>
### 4. [SDK Integration Guide](sdk/overview-onprem.md) { #index-sdk-integration-guide }

4.1 [SDK Integration](sdk/overview-onprem.md)
4.2 [Java SDK Integration](sdk/java.md)
{%- endif %}

<a id="encryption-api-application-guide"></a>
### 5. [Encryption API Application Guide](encryption/overview.md) { #encryption-api-application-guide }

5.1 [Encryption API](encryption/overview.md)
5.2 [Private Key Encryption Structure](encryption/key-encryption.md)
5.3 [Encryption Data Structure](encryption/data-structure.md)
5.4 [Encrypted Data Decryption Flow](encryption/decryption-flow.md)
5.5 [API Reference](encryption/api-reference.md)

<a id="integrity-verification-guide"></a>
### 6. [App Attestation Guide](app-attestation/overview.md) { #integrity-verification-guide }

6.1 [Overview](app-attestation/overview.md)
6.2 [Console App Attestation Settings](app-attestation/console.md)
6.3 [How to Use App Attestation](app-attestation/sdk.md)

<a id="resource-string-obfuscation"></a>
### 7. [Resource String Obfuscation](resource-string-obfuscation/overview.md) { #resource-string-obfuscation }

7.1 [Overview](resource-string-obfuscation/overview.md)
7.2 [Configuration File Format](resource-string-obfuscation/config.md)

<a id="log-and-callback-information"></a>
### 8. [Log and Callback Information](logs/overview.md) { #log-and-callback-information }

8.1 [Log Details](logs/overview.md)
8.2 [Callback Data](logs/callback-data.md)
8.3 [Guide to Sanctions](logs/sanctions-guide.md)

<a id="checks-and-cautions"></a>
### 9. [Checks and Cautions](testing/integration.md) { #checks-and-cautions }

9.1 [Integration Test](testing/integration.md)
9.2 [Checks when Applying ProGuard](testing/proguard.md)
9.3 [Integrity Verification for App Signature Key](testing/signature-verification.md)

<a id="faq"></a>
### 10. [FAQ](faq/general.md) { #faq }

10.1 [Common Error](faq/general.md)
10.2 [Cocos2D Game Error](faq/cocos2d.md)

<a id="copyright"></a>
## Copyright { #copyright }

---

!!! danger "Copyright"
    Copyright © 2022 NHN Cloud Corp. All rights reserved.
    
    This document is the intellectual property of NHN Cloud and cannot be modified or used for any other purpose without NHN Cloud's permission. This document is provided for informational purposes only. While NHN Cloud has endeavored to verify the completeness and accuracy of the information contained in this document, NHN Cloud assumes no responsibility for any errors or omissions that may occur. Therefore, the user is solely responsible for the use or results of this document, and NHN Cloud makes no warranties, express or implied, regarding this. 
    Specific software products or products mentioned in this document, including related URL information, are subject to the copyright laws of their respective owners. Compliance with such copyright laws is the user's responsibility.

    NHN Cloud reserves the right to change the contents of this document without prior notice.