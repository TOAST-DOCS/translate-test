# NHN AppGuard Android Developer's Guide

<a id="document-information"></a>
## 文書情報 { #document-information }

<a id="document-information-2"></a>
### 文書情報 { #document-information-2 }
この文書は、NHN AppGuardを使用するためのSDKマニュアルを含むDeveloper's Guideです。 

<a id="written-on"></a>
### 作成日 { #written-on }
2026-04-14

<a id="contact"></a>
### 連絡先 { #contact }
NHN Cloud Webサイトの[カスタマーサポート > お問い合わせ](https://www.nhncloud.com/kr/support/inquiry)をご利用ください。

<a id="index"></a>
## 目次 { #index }

{%- if variant == 'saas' %}

<a id="preparations-for-application"></a>
### 1. [適用準備](preparation/environment.md) { #preparations-for-application }
1.1 [サポート環境](preparation/environment.md)
1.2 [NHN AppGuardの適用方式](preparation/approach.md)
1.3 [適用前の準備事項](preparation/prerequisites-saas.md)

<a id="protection"></a>
### 2. [保護作業](protection/console.md) { #protection }
2.1 [コンソールでの保護作業](protection/console.md)
2.2 [CLIでの保護作業](protection/cli-saas.md)
2.3 [プラグインでの保護作業](protection/plugin.md)

<a id="index-protection"></a>
### 3. [SDK連携ガイド](sdk/overview-saas.md) { #index-protection }
3.1 [SDK連携](sdk/overview-saas.md)
3.2 [Java SDK連携](sdk/java.md)
3.3 [Unreal SDK連携](sdk/unreal.md)
{%- else %}

<!-- pre-align: ko에 대응 섹션 없음 — 검토 필요 (Second occurrence of 適用準備 with no counterpart in KO; 적용 준비 (k6) appears only once in the KO outline) -->
<a id="sdk-integration-guide"></a>
### 1. [適用準備](preparation/environment.md) { #sdk-integration-guide }
1.1 [対応環境](preparation/environment.md)
1.2 [NHN AppGuard適用方式](preparation/approach.md)
1.3 [適用前の準備事項](preparation/prerequisites-onprem.md)

<a id="index-sdk-integration-guide"></a>
### 2. [保護作業](protection/cli-onprem.md) { #index-sdk-integration-guide }
2.1 [CLIを利用した保護作業](protection/cli-onprem.md)

<a id="encryption-api-application-guide"></a>
### 3. [SDK連携ガイド](sdk/overview-onprem.md) { #encryption-api-application-guide }
3.1 [SDK連携](sdk/overview-onprem.md)
3.2 [Java SDK連携](sdk/java.md)
{%- endif %}

<a id="integrity-verification-guide"></a>
### 4. [暗号化API適用ガイド](encryption/overview.md) { #integrity-verification-guide }
4.1 [暗号化API](encryption/overview.md)
4.2 [秘密鍵の暗号化構造¶](encryption/key-encryption.md)
4.3 [暗号化データの構造](encryption/data-structure.md)
4.4 [暗号化データの復号フロー](encryption/decryption-flow.md)
4.5 [API Reference](encryption/api-reference.md)

<a id="resource-string-obfuscation"></a>
### 5. [アプリ証明ガイド](app-attestation/overview.md) { #resource-string-obfuscation }
5.1 [概要](app-attestation/overview.md)
5.2 [コンソールアプリ証明設定](app-attestation/console.md)
5.3 [アプリ証明の使用方法](app-attestation/sdk.md)

<a id="log-and-callback-information"></a>
### 6. [リソース文字列難読化](resource-string-obfuscation/overview.md) { #log-and-callback-information }
6.1 [概要](resource-string-obfuscation/overview.md)
6.2 [設定ファイルの作成方法](resource-string-obfuscation/config.md)

<a id="checks-and-cautions"></a>
### 7. [ログ及びコールバック情報](logs/overview.md) { #checks-and-cautions }
7.1 [ログ詳細情報](logs/overview.md)
7.2 [コールバックデータ](logs/callback-data.md)
7.3 [制裁ガイド](logs/sanctions-guide.md)

<a id="faq"></a>
### 8. [適用確認及び注意事項](testing/integration.md) { #faq }
8.1 [連携テスト](testing/integration.md)
8.2 [ProGuard適用時の確認事項](testing/proguard.md)
8.3 [アプリ署名キーの完全性検証](testing/signature-verification.md)

### 9. [FAQ](faq/general.md)
9.1 [一般的なエラー](faq/general.md)
9.2 [Cocos2Dゲームのエラー](faq/cocos2d.md)

<a id="copyright"></a>
## 著作権 { #copyright }
---

!!! danger "著作権"
    Copyright © 2022 NHN Cloud Corp. All rights reserved.
    
    この文書は、NHN Cloudの知的資産であるため、NHN Cloudの承認なく文書を変更したり他の用途で使用できません。
    この文書は情報提供の目的でのみ提供されます。 NHN Cloudはこの文書に収録された情報の完全性と正確性を検証するために努力しましたが、発 生する可能性のある内容上の誤りや漏れについては責任を負いません。したがってこの文書の使用や使用結果に伴う責任は全てユーザーにあり、N HN Cloudはこれに対して明示的または黙示的にいかなる保証も行いません。
    関連URL情報を含め、この文書で言及した特定ソフトウェアや製品は、その所有者の著作権法に従います。 これらの著作権法を遵守することはユーザーの責任です。
    NHN Cloudは、この文書の内容を予告なく変更することがあります。
