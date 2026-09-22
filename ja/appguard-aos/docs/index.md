<!-- machine_translated: true -->

<!-- pre-align:aligned sig=e6088b8c4131 -->

# NHN AppGuard Android Developer's Guide

<a id="document-information"></a>
## 文書情報 { #document-information }

<a id="document-information-2"></a>
### 文書情報 { #document-information-2 }

この文書は、NHN AppGuardを使用するためのSDKマニュアルを含むDeveloper's Guideです。 

<a id="written-on"></a>
### 作成日 { #written-on }

2026-09-15

<a id="contact"></a>
### 連絡先 { #contact }

NHN Cloud Webサイトの[カスタマーサポート > お問い合わせ](https://www.nhncloud.com/kr/support/inquiry)をご利用ください。

<a id="index"></a>
## 目次 { #index }

<a id="preparations-for-application"></a>
### 1. [適用準備](preparation/environment.md) { #preparations-for-application }

1.1 [サポート環境](preparation/environment.md)
1.2 [NHN AppGuardの適用方式](preparation/approach.md)
{%- if variant == 'saas' %}
1.3 [適用前の準備事項](preparation/prerequisites-saas.md)
{%- else %}
1.3 [適用前の準備事項](preparation/prerequisites-onprem.md)
{%- endif %}

{%- if variant == 'saas' %}

<a id="protection"></a>
### 2. [保護作業](protection/console.md) { #protection }

2.1 [コンソールでの保護作業](protection/console.md)
2.2 [CLIでの保護作業](protection/cli-saas.md)
2.3 [プラグインでの保護作業](protection/plugin.md)
{%- else %}

<a id="index-protection"></a>
### 2. [保護作業](protection/cli-onprem.md) { #index-protection }

2.1 [CLIを利用した保護作業](protection/cli-onprem.md)
{%- endif %}

<a id="unified-configuration-file"></a>
### 3. [統合設定ファイル](configuration/overview.md) { #unified-configuration-file }

3.1 [概要](configuration/overview.md)
3.2 [機能別設定](configuration/sections.md)
{%- if variant == 'saas' %}

<a id="sdk-integration-guide"></a>
### 4. [SDK連携ガイド](sdk/overview-saas.md) { #sdk-integration-guide }

4.1 [SDK連携](sdk/overview-saas.md)
4.2 [Java SDK連携](sdk/java.md)
4.3 [Unreal SDK連携](sdk/unreal.md)
{%- else %}

<a id="index-sdk-integration-guide"></a>
### 4. [SDK連携ガイド](sdk/overview-onprem.md) { #index-sdk-integration-guide }

4.1 [SDK連携](sdk/overview-onprem.md)
4.2 [Java SDK連携](sdk/java.md)
{%- endif %}

<a id="encryption-api-application-guide"></a>
### 5. [暗号化API適用ガイド](encryption/overview.md) { #encryption-api-application-guide }

5.1 [暗号化API](encryption/overview.md)
5.2 [秘密鍵の暗号化構造](encryption/key-encryption.md)
5.3 [暗号化データの構造](encryption/data-structure.md)
5.4 [暗号化データの復号フロー](encryption/decryption-flow.md)
5.5 [API Reference](encryption/api-reference.md)

<a id="integrity-verification-guide"></a>
### 6. [アプリ証明ガイド](app-attestation/overview.md) { #integrity-verification-guide }

6.1 [概要](app-attestation/overview.md)
6.2 [コンソールアプリ証明設定](app-attestation/console.md)
6.3 [アプリ証明の使用方法](app-attestation/sdk.md)

<a id="resource-string-obfuscation"></a>
### 7. [リソース文字列難読化](resource-string-obfuscation/overview.md) { #resource-string-obfuscation }

7.1 [概要](resource-string-obfuscation/overview.md)
7.2 [設定ファイルの作成方法](resource-string-obfuscation/config.md)

<a id="log-and-callback-information"></a>
### 8. [ログ及びコールバック情報](logs/overview.md) { #log-and-callback-information }

8.1 [ログ詳細情報](logs/overview.md)
8.2 [コールバックデータ](logs/callback-data.md)
8.3 [制裁ガイド](logs/sanctions-guide.md)

<a id="checks-and-cautions"></a>
### 9. [適用確認及び注意事項](testing/integration.md) { #checks-and-cautions }

9.1 [連携テスト](testing/integration.md)
9.2 [ProGuard適用時の確認事項](testing/proguard.md)
9.3 [アプリ署名キーの完全性検証](testing/signature-verification.md)

<a id="faq"></a>
### 10. [FAQ](faq/general.md) { #faq }

10.1 [一般的なエラー](faq/general.md)
10.2 [Cocos2Dゲームのエラー](faq/cocos2d.md)

<a id="copyright"></a>
## 著作権 { #copyright }

---

!!! danger "著作権"
    Copyright © 2022 NHN Cloud Corp. All rights reserved.
    
    この文書は、NHN Cloudの知的資産であるため、NHN Cloudの承認なく文書を他の用途に変更して使用することはできません。
    この文書は情報提供の目的でのみ提供されます。 NHN Cloudはこの文書に収録された情報の完全性と正確性を検証するために努力しましたが、発生する可能性のある内容上の誤りや漏れについては責任を負いません。したがってこの文書の使用や使用結果に伴う責任は全てユーザーにあり、NHN Cloudはこれに対して明示的または黙示的にいかなる保証も行いません。
    関連URL情報を含め、この文書で言及した特定ソフトウェアや製品は、その所有者の著作権法に従います。これらの著作権法を遵守することはユーザーの責任です。

    NHN Cloudは、この文書の内容を予告なく変更することがあります。