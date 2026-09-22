<!-- pre-align:aligned sig=8498e3e7e765 -->

# NHN AppGuard Android Developer's Guide

<a id="document-information"></a>
## 문서 정보 { #document-information }

<a id="document-information-2"></a>
### 문서 정보 { #document-information-2 }
본 문서는 NHN AppGuard를 사용하기 위한 SDK 매뉴얼을 포함한 Developer's Guide입니다.  

<a id="written-on"></a>
### 작성 일자 { #written-on }
2026-09-15

<a id="contact"></a>
### 연락처 { #contact }
NHN Cloud 홈페이지의 [고객지원 > 문의하기](https://www.nhncloud.com/kr/support/inquiry)를 이용해 주시기 바랍니다.

<a id="index"></a>
## 목차 { #index }

<a id="preparations-for-application"></a>
### 1. [적용 준비](preparation/environment.md) { #preparations-for-application }
1.1 [지원 환경](preparation/environment.md)
1.2 [NHN AppGuard 적용 방식](preparation/approach.md)
{%- if variant == 'saas' %}
1.3 [적용 전 준비 사항](preparation/prerequisites-saas.md)
{%- else %}
1.3 [적용 전 준비 사항](preparation/prerequisites-onprem.md)
{%- endif %}

{%- if variant == 'saas' %}

<a id="protection"></a>
### 2. [보호작업](protection/console.md) { #protection }
2.1 [콘솔을 통한 보호작업](protection/console.md)
2.2 [CLI를 통한 보호작업](protection/cli-saas.md)
2.3 [플러그인을 통한 보호작업](protection/plugin.md)
{%- else %}

<a id="index-protection"></a>
### 2. [보호작업](protection/cli-onprem.md) { #index-protection }
2.1 [CLI를 이용한 보호작업](protection/cli-onprem.md)
{%- endif %}

<a id="unified-configuration-file"></a>
### 3. [통합 설정 파일](configuration/overview.md) { #unified-configuration-file }
3.1 [개요](configuration/overview.md)
3.2 [기능별 설정](configuration/sections.md)
{%- if variant == 'saas' %}

<a id="sdk-integration-guide"></a>
### 4. [SDK 연동 가이드](sdk/overview-saas.md) { #sdk-integration-guide }
4.1 [SDK 연동](sdk/overview-saas.md)
4.2 [Java SDK 연동](sdk/java.md)
4.3 [Unreal SDK 연동](sdk/unreal.md)
{%- else %}

<a id="index-sdk-integration-guide"></a>
### 4. [SDK 연동 가이드](sdk/overview-onprem.md) { #index-sdk-integration-guide }
4.1 [SDK 연동](sdk/overview-onprem.md)
4.2 [Java SDK 연동](sdk/java.md)
{%- endif %}

<a id="encryption-api-application-guide"></a>
### 5. [암호화 API 적용 가이드](encryption/overview.md) { #encryption-api-application-guide }
5.1 [암호화 API](encryption/overview.md)
5.2 [개인 키 암호화 구조](encryption/key-encryption.md)
5.3 [암호화 데이터 구조](encryption/data-structure.md)
5.4 [암호화 데이터 복호화 흐름](encryption/decryption-flow.md)
5.5 [API Reference](encryption/api-reference.md)

<a id="integrity-verification-guide"></a>
### 6. [앱 증명 가이드](app-attestation/overview.md) { #integrity-verification-guide }
6.1 [개요](app-attestation/overview.md)
6.2 [콘솔 앱 증명 설정](app-attestation/console.md)
6.3 [앱 증명 사용법](app-attestation/sdk.md)

<a id="resource-string-obfuscation"></a>
### 7. [리소스 문자열 난독화](resource-string-obfuscation/overview.md) { #resource-string-obfuscation }
7.1 [개요](resource-string-obfuscation/overview.md)
7.2 [설정 파일 작성 방법](resource-string-obfuscation/config.md)

<a id="log-and-callback-information"></a>
### 8. [로그 및 콜백 정보](logs/overview.md) { #log-and-callback-information }
8.1 [로그 상세 정보](logs/overview.md)
8.2 [콜백 데이터](logs/callback-data.md)
8.3 [제재 가이드](logs/sanctions-guide.md)

<a id="checks-and-cautions"></a>
### 9. [적용 확인 및 주의 사항](testing/integration.md) { #checks-and-cautions }
9.1 [연동 테스트](testing/integration.md)
9.2 [ProGuard 적용 시 확인 사항](testing/proguard.md)
9.3 [앱 서명 키 무결성 검증](testing/signature-verification.md)

<a id="faq"></a>
### 10. [FAQ](faq/general.md) { #faq }
10.1 [일반 오류](faq/general.md)
10.2 [Cocos2D 게임 오류](faq/cocos2d.md)

<a id="copyright"></a>
## 저작권 { #copyright }
---

!!! danger "저작권"
    Copyright © 2022 NHN Cloud Corp. All rights reserved.
    
    이 문서는 NHN Cloud의 지적 자산이므로 NHN Cloud의 승인 없이 문서를 다른 용도로 임의 변경하여 사용할 수 없습니다.  
    이 문서는 정보 제공의 목적으로만 제공됩니다. NHN Cloud는 이 문서에 수록된 정보의 완전성과 정확성을 검증하기 위해 노력하였으나, 발생할 수 있는 내용상의 오류나 누락에 대해서는 책임지지 않습니다. 따라서 이 문서의 사용이나 사용 결과에 따른 책임은 전적으로 사용자에게 있으며, NHN Cloud는 이에 대해 명시적 혹은 묵시적으로 어떠한 보증도 하지 않습니다.  
    관련 URL 정보를 포함하여 이 문서에서 언급한 특정 소프트웨어 상품이나 제품은 해당 소유자의 저작권법을 따르며, 해당 저작권법을 준수하는 것은 사용자의 책임입니다.

    NHN Cloud는 이 문서의 내용을 예고 없이 변경할 수 있습니다.
