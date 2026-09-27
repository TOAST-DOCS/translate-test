<!-- pre-align:aligned sig=763014a10170 -->

<a id="nhn-cloud-sdk-user-guide-release-notes-ios"></a>
## NHN Cloud > User Guide for SDK > Release Notes > iOS { #nhn-cloud-sdk-user-guide-release-notes-ios }

<a id="90-2025-04-29"></a>
## 1.9.0 (2025. 04. 29.) { #90-2025-04-29 }

<a id="nhn-cloud-push"></a>
### NHN Cloud Push { #nhn-cloud-push }

<a id="nhn-cloud-push-added-features"></a>
#### 機能追加 
* Notification Hubサポート 
    * NHNCloudPush SDKでNotification Hubを利用できます。
    * NHNCloudPushConfigurationのserviceTypeプロパティにNHNCloudPushServiceTypeNotificationHub値を設定して使用可能です。

<a id="86-2024-11-15"></a>
## 1.8.6 (2024. 11. 15.) { #86-2024-11-15 }

<a id="86-2024-11-15-nhn-cloud-push"></a>
### NHN Cloud Push { #86-2024-11-15-nhn-cloud-push }

<a id="86-2024-11-15-nhn-cloud-push-improved"></a>
#### 改善事項
* DeviceIDを設定できるAPIを追加 

<a id="85-2024-10-08"></a>
## 1.8.5 (2024. 10. 08.) { #85-2024-10-08 }

<a id="nhn-cloud-iap"></a>
### NHN Cloud IAP { #nhn-cloud-iap }

<a id="nhn-cloud-iap-improved"></a>
#### 改善事項
* 決済詳細情報送信機能の改善

<a id="84-2024-09-11"></a>
## 1.8.4 (2024. 09. 11.) { #84-2024-09-11 }

<a id="84-2024-09-11-nhn-cloud-push"></a>
### NHN Cloud Push { #84-2024-09-11-nhn-cloud-push }

<a id="84-2024-09-11-nhn-cloud-push-improved"></a>
#### 改善事項
* Notification重複受信問題の改善(iOS 18 Beta)
    * iOS 18でアプリケーションがForeground状態の時にNotificationが重複して受信されないようにします(OSバグ)。

<a id="83-2024-07-23"></a>
## 1.8.3 (2024. 07. 23.) { #83-2024-07-23 }

<a id="common"></a>
### 共通 { #common }

<a id="common-improved"></a>
#### 改善事項
* 安定性改善

<a id="82-2024-06-25"></a>
## 1.8.2 (2024. 06. 25.) { #82-2024-06-25 }

<a id="82-2024-06-25-common"></a>
### 共通 { #82-2024-06-25-common }

<a id="82-2024-06-25-common-improved"></a>
#### 改善事項
* 安定性改善

<a id="81-2024-02-27"></a>
## 1.8.1 (2024. 02. 27.) { #81-2024-02-27 }

<a id="81-2024-02-27-common"></a>
### 共通 { #81-2024-02-27-common }

<a id="81-2024-02-27-common-improved"></a>
#### 改善事項
* Privacy manifest適用 

<a id="81-2024-02-27-nhn-cloud-push"></a>
### NHN Cloud Push { #81-2024-02-27-nhn-cloud-push }

<a id="81-2024-02-27-nhn-cloud-push-improved"></a>
#### 改善事項
* 特定環境でメッセージクリックアクションがすぐに動作しない問題を修正   

<a id="80-2024-01-23"></a>
## 1.8.0 (2024. 01. 23.) { #80-2024-01-23 }

<a id="80-2024-01-23-nhn-cloud-iap"></a>
### NHN Cloud IAP { #80-2024-01-23-nhn-cloud-iap }

<a id="80-2024-01-23-nhn-cloud-iap-improved"></a>
#### 改善事項
* 決済検証方式の改善
    * 新規SDKでも(旧)領収書検証を使用できるように改善
        * [(新)領収書検証 + Notification V2](/Mobile%20Service/IAP/ja/console-apple-guide/#notification-v2)
        * [(旧)領収書検証 + Notification V1 (Deprecated)](/Mobile%20Service/IAP/ja/console-apple-guide/#notification-v1-deprecated)

<a id="71-2023-12-19"></a>
## 1.7.1 (2023. 12. 19.) { #71-2023-12-19 }

<a id="71-2023-12-19-common"></a>
### 共通 { #71-2023-12-19-common }

<a id="71-2023-12-19-common-improved"></a>
#### 改善事項
* 署名適用
    * 配布されるバイナリに`NHN Cloud Corp.`署名が適用されました。

<a id="logger"></a>
### Logger { #logger }

<a id="logger-improved"></a>
#### 改善事項
* Instance LoggerのNetworkInsight安定性の改善 

<a id="symboluploaderv004"></a>
### SymbolUploader(v0.0.4) { #symboluploaderv004 }

<a id="symboluploaderv004-improved"></a>
#### 改善事項
* 安定性改善

<a id="70-2023-11-14"></a>
## 1.7.0 (2023. 11. 14.) { #70-2023-11-14 }

<a id="70-2023-11-14-common"></a>
### 共通 { #70-2023-11-14-common }

<a id="70-2023-11-14-common-improved"></a>
#### 改善事項
* 最小サポートバージョンの引き上げ
    * 9.0 > 11.0
* 未サポートアーキテクチャのサポート終了
    *  i386, armv7s, armv7

<a id="70-2023-11-14-nhn-cloud-iap"></a>
### NHN Cloud IAP { #70-2023-11-14-nhn-cloud-iap }

<a id="70-2023-11-14-nhn-cloud-iap-improved"></a>
#### 改善事項
* 決済検証方法の変更 - [(新)領収書検証 + Notification V2](/Mobile%20Service/IAP/ja/console-apple-guide/#notification-v2)

<a id="62-2023-08-29"></a>
## 1.6.2 (2023. 08. 29.) { #62-2023-08-29 }

<a id="62-2023-08-29-common"></a>
### 共通 { #62-2023-08-29-common }

<a id="62-2023-08-29-common-improved"></a>
#### 改善事項
* CountryCode取得に失敗する問題を修正

<a id="nhn-cloud-ocr"></a>
### NHN Cloud OCR { #nhn-cloud-ocr }

<a id="nhn-cloud-ocr-added-features"></a>
#### 機能追加
* クレジットカード/身分証認識結果データに認識領域を追加

<a id="61-2023-07-25"></a>
## 1.6.1 (2023. 07. 25.) { #61-2023-07-25 }

<a id="61-2023-07-25-nhn-cloud-iap"></a>
### NHN Cloud IAP { #61-2023-07-25-nhn-cloud-iap }

<a id="61-2023-07-25-nhn-cloud-iap-improved"></a>
#### 改善事項
* 決済詳細情報送信機能の改善

<a id="60-2023-07-11"></a>
## 1.6.0 (2023. 07. 11.) { #60-2023-07-11 }

<a id="60-2023-07-11-nhn-cloud-ocr"></a>
### NHN Cloud OCR { #60-2023-07-11-nhn-cloud-ocr }

<a id="60-2023-07-11-nhn-cloud-ocr-added-features"></a>
#### 機能追加
* OCR(ID Card Recognizer)追加

<a id="50-2023-06-27"></a>
## 1.5.0 (2023. 06. 27.) { #50-2023-06-27 }

<a id="50-2023-06-27-nhn-cloud-push"></a>
### NHN Cloud Push { #50-2023-06-27-nhn-cloud-push }

<a id="50-2023-06-27-nhn-cloud-push-improved"></a>
#### 改善事項
* トークン登録機能の改善
    * アプリの通知権限とは関係なくトークンを登録できるオプションを提供します。

<a id="50-2023-06-27-nhn-cloud-push-symboluploaderv003"></a>
#### SymbolUploader(v0.0.3)
* 安定性の改善

<a id="40-2023-05-30"></a>
## 1.4.0 (2023. 05. 30.) { #40-2023-05-30 }

<a id="40-2023-05-30-common"></a>
### 共通 { #40-2023-05-30-common }

<a id="40-2023-05-30-common-improved"></a>
#### 改善事項
* SPM(swift package manager)配布方式を追加

<a id="40-2023-05-30-nhn-cloud-iap"></a>
### NHN Cloud IAP { #40-2023-05-30-nhn-cloud-iap }

<a id="40-2023-05-30-nhn-cloud-iap-added-featrues"></a>
#### 機能追加
* 決済詳細情報送信機能を追加 
    * IAPコンソールのTransactionタブで決済詳細情報を照会できます。

<a id="40-2023-05-30-nhn-cloud-iap-symboluploaderv002"></a>
#### SymbolUploader(v0.0.2)
* run script改善 
    * Cocoapods, SPM対応追加
    
<a id="31-2023-05-19---hotfix"></a>
## 1.3.1 (2023. 05. 19.) - Hotfix { #31-2023-05-19---hotfix }

<a id="31-2023-05-19---hotfix-nhn-cloud-push"></a>
### NHN Cloud Push { #31-2023-05-19---hotfix-nhn-cloud-push }

<a id="31-2023-05-19---hotfix-nhn-cloud-push-improved"></a>
#### 改善事項
* トークン登録機能改善
    * トークン登録時にアプリの通知設定が無効になっている場合、再度`NHNCloudPushErrorPermissionDenied`を返します。

<a id="30-2023-02-28"></a>
## 1.3.0 (2023. 02. 28.) { #30-2023-02-28 }

<a id="30-2023-02-28-common"></a>
### 共通 { #30-2023-02-28-common }

<a id="30-2023-02-28-common-improved"></a>
#### 改善事項
* 安定性改善

<a id="21-2023-01-31"></a>
## 1.2.1 (2023. 01. 31.) { #21-2023-01-31 }

<a id="21-2023-01-31-nhn-cloud-push"></a>
### NHN Cloud Push { #21-2023-01-31-nhn-cloud-push }

<a id="21-2023-01-31-nhn-cloud-push-improved"></a>
#### 改善事項
* トークン登録機能の改善

<a id="21-2023-01-31-nhn-cloud-ocr"></a>
### NHN Cloud OCR { #21-2023-01-31-nhn-cloud-ocr }

<a id="21-2023-01-31-nhn-cloud-ocr-improved"></a>
#### 改善事項
* クレジットカード認識性能の改善
* 安定性の改善

<a id="20-2022-11-29"></a>
## 1.2.0 (2022. 11. 29.) { #20-2022-11-29 }

<a id="nhn-cloud-logger"></a>
### NHN Cloud Logger { #nhn-cloud-logger }

<a id="nhn-cloud-logger-added-features"></a>
#### 機能追加
* 公共機関用Loggerをサポート

<a id="20-2022-11-29-nhn-cloud-push"></a>
### NHN Cloud Push { #20-2022-11-29-nhn-cloud-push }

<a id="20-2022-11-29-nhn-cloud-push-improved"></a>
#### 改善事項
* プッシュイベント転送の改善

<a id="20-2022-11-29-nhn-cloud-ocr"></a>
### NHN Cloud OCR { #20-2022-11-29-nhn-cloud-ocr }

<a id="20-2022-11-29-nhn-cloud-ocr-improved"></a>
#### 改善事項
* UI改善

<a id="10-2022-10-25"></a>
## 1.1.0 (2022. 10. 25.) { #10-2022-10-25 }

<a id="10-2022-10-25-common"></a>
### 共通 { #10-2022-10-25-common }

<a id="10-2022-10-25-common-improvements"></a>
#### 改善事項
* 安定性改善

<a id="10-2022-10-25-nhn-cloud-iap"></a>
### NHN Cloud IAP { #10-2022-10-25-nhn-cloud-iap }

<a id="10-2022-10-25-nhn-cloud-iap-added-features"></a>
#### 機能追加
* [すべてのストア]有効購読照会および未消費決済履歴照会APIの追加

<a id="10-2022-10-25-nhn-cloud-ocr"></a>
### NHN Cloud OCR { #10-2022-10-25-nhn-cloud-ocr }

<a id="10-2022-10-25-nhn-cloud-ocr-added-features"></a>
#### 機能追加
* OCR(Credit Card Recognizer)追加

<a id="00-2022-07-12"></a>
## 1.0.0 (2022. 07. 12.) { #00-2022-07-12 }

<a id="00-2022-07-12-common"></a>
### 共通 { #00-2022-07-12-common }

<a id="00-2022-07-12-common-improvements"></a>
#### 改善事項
* 安定性改善
* モジュール名NHN Cloud SDKに変更
    * TOAST SDKはDeprecatedになりました。

<a id="300-2022-03-29"></a>
## 0.30.0 (2022. 03. 29.) { #300-2022-03-29 }

<a id="toast-iap"></a>
### TOAST IAP { #toast-iap }

<a id="toast-iap-added-features"></a>
#### 機能追加
* ToastPurchaseResultにサンドボックス決済かどうかを追加(sandboxPayment)

<a id="292-2021-11-23"></a>
## 0.29.2 (2021. 11. 23.) { #292-2021-11-23 }

<a id="toast-push"></a>
### TOAST Push { #toast-push }

<a id="toast-push-improvements"></a>
#### 改善事項
* 安全性の改善

<a id="291-2021-10-26"></a>
## 0.29.1 (2021. 10. 26.) { #291-2021-10-26 }

<a id="291-2021-10-26-toast-iap"></a>
### TOAST IAP { #291-2021-10-26-toast-iap }

<a id="291-2021-10-26-toast-iap-improvements"></a>
#### 改善事項
* 安全性の改善

<a id="290-2021-07-06"></a>
## 0.29.0 (2021. 07. 06.) { #290-2021-07-06 }

<a id="290-2021-07-06-common"></a>
### 共通 { #290-2021-07-06-common }

<a id="290-2021-07-06-common-improvements"></a>
#### 改善事項
* 安全性の改善

<a id="290-2021-07-06-toast-iap"></a>
### TOAST IAP { #290-2021-07-06-toast-iap }

<a id="290-2021-07-06-toast-iap-added-features"></a>
#### 機能追加
* 月決済限度機能の追加

<a id="280-2021-05-25"></a>
## 0.28.0 (2021. 05. 25.) { #280-2021-05-25 }

<a id="280-2021-05-25-common"></a>
### 共通 { #280-2021-05-25-common }

<a id="280-2021-05-25-common-improvements"></a>
#### 改善事項
* xcframework追加
    * arm Simulatorサポートの追加

<a id="toast-logger"></a>
### TOAST Logger { #toast-logger }

<a id="toast-logger-crashreporter-buildinfo-20210525"></a>
#### CrashReporter (BuildInfo 20210525)
* アーキテクチャ分類方式の改善
    * iOS14 Core Libraryがシンボリケーションされない問題を改善

<a id="272-2021-03-23"></a>
## 0.27.2 (2021. 03. 23.) { #272-2021-03-23 }

<a id="272-2021-03-23-common"></a>
### 共通 { #272-2021-03-23-common }

<a id="272-2021-03-23-common-improvements"></a>
#### 改善事項
* 安全性の改善

<a id="272-2021-03-23-toast-logger"></a>
### TOAST Logger { #272-2021-03-23-toast-logger }

<a id="272-2021-03-23-toast-logger-symboluploader-v001"></a>
#### SymbolUploader (v0.0.1)
* SymbolUploader追加

<a id="271-2020-11-24"></a>
## 0.27.1 (2020. 11. 24.) { #271-2020-11-24 }

<a id="271-2020-11-24-toast-iap"></a>
### TOAST IAP { #271-2020-11-24-toast-iap }

<a id="271-2020-11-24-toast-iap-improvements"></a>
#### 改善事項 
* サブスクリプションプロダクトの再購入エラー修正 (iOS 14 ) 
- Appstoreからプロダクト情報を得られなかった場合、ToastProductsResponseがnilを返すように変更 
 
<a id="271-2020-11-24-toast-push"></a>
### TOAST Push { #271-2020-11-24-toast-push }

<a id="271-2020-11-24-toast-push-improvements"></a>
#### 改善事項 
* トークン解除リクエスト時に、登録されたトークンがない場合、Callbackが発生しない問題の改善 
 
<a id="270-2020-09-11"></a>
## 0.27.0 (2020. 09. 11.) { #270-2020-09-11 }

<a id="270-2020-09-11-toast-iap"></a>
### TOAST IAP { #270-2020-09-11-toast-iap }

<a id="270-2020-09-11-toast-iap-added-features"></a>
#### 機能追加 
* ToastProductにローカライズされたプロダクト情報の追加 (localizedTitle、 localizedDescription) 
 
<a id="270-2020-09-11-toast-iap-improvements"></a>
#### 機能改善 
* iOS 14 beta変更事項に対応  
    * 決済失敗のDelegateが受信できない問題の改善 
     
<a id="270-2020-09-11-toast-push"></a>
### TOAST Push { #270-2020-09-11-toast-push }

<a id="270-2020-09-11-toast-push-improvements"></a>
#### 改善事項 
* 安全性の改善 
     
<a id="260-2020-07-28"></a>
## 0.26.0 (2020. 07. 28.) { #260-2020-07-28 }

<a id="260-2020-07-28-toast-push"></a>
### TOAST Push { #260-2020-07-28-toast-push }

<a id="260-2020-07-28-toast-push-added-features"></a>
#### 機能追加 
* ユーザータグ機能のサポート 
 
<a id="251-2020-07-03"></a>
## 0.25.1 (2020. 07. 03.) { #251-2020-07-03 }

<a id="251-2020-07-03-toast-logger"></a>
### TOAST Logger { #251-2020-07-03-toast-logger }

<a id="251-2020-07-03-toast-logger-improvements"></a>
#### 改善事項 
* 安全性の改善 
 
<a id="251-2020-07-03-toast-push"></a>
### TOAST Push { #251-2020-07-03-toast-push }

<a id="251-2020-07-03-toast-push-improvements"></a>
#### 改善事項 
* 安全性の改善 
 
<a id="250-2020-06-23"></a>
## 0.25.0 (2020. 06. 23.) { #250-2020-06-23 }

<a id="250-2020-06-23-common"></a>
### 共通 { #250-2020-06-23-common }

<a id="250-2020-06-23-common-improvements"></a>
#### 改善事項 
* 安全性の改善 
 
<a id="250-2020-06-23-toast-push"></a>
### TOAST Push { #250-2020-06-23-toast-push }

<a id="250-2020-06-23-toast-push-improvements"></a>
#### 改善事項 
* 通知オプション設定のインターフェイスを分離 
 
<a id="241-2020-05-26"></a>
## 0.24.1 (2020. 05. 26.) { #241-2020-05-26 }

<a id="241-2020-05-26-toast-push"></a>
### TOAST Push { #241-2020-05-26-toast-push }

<a id="241-2020-05-26-toast-push-improvements"></a>
#### 機能改善 
* トークン登録の機能改善 
 
<a id="240-2020-04-28"></a>
## 0.24.0 (2020. 04. 28.) { #240-2020-04-28 }

<a id="240-2020-04-28-common"></a>
### 共通 { #240-2020-04-28-common }
* TOAST SDKサポートバージョンの最小バージョンを変更(iOS 8.0 -> iOS 9.0) 
* 安全性の改善 
 
<a id="240-2020-04-28-toast-iap"></a>
### TOAST IAP { #240-2020-04-28-toast-iap }

<a id="240-2020-04-28-toast-iap-added-features"></a>
#### 追加事項 
* プロモーション決済の実行するか選択できるOptional Delegateを追加 
 
<a id="240-2020-04-28-toast-push"></a>
### TOAST Push { #240-2020-04-28-toast-push }

<a id="240-2020-04-28-toast-push-improvements"></a>
#### 改善事項  
* 安全性の改善 
 
<a id="230-2020-03-24"></a>
## 0.23.0 (2020. 03. 24.) { #230-2020-03-24 }

<a id="230-2020-03-24-toast-logger"></a>
### TOAST Logger { #230-2020-03-24-toast-logger }

<a id="230-2020-03-24-toast-logger-improvements"></a>
#### 改善事項 
* CrashReport CallStackに誤った文字列が含まれて可能性がある問題を修正 
 
<a id="230-2020-03-24-toast-push"></a>
### TOAST Push { #230-2020-03-24-toast-push }

<a id="230-2020-03-24-toast-push-added-features"></a>
#### 追加事項 
* 通知オプション設定の機能追加 
    * 初期化時にフォアグラウンドで通知を表示するか、バッジアイコンの表示するか、通知音を使用するかの設定が可能 
     
<a id="221-2020-02-25"></a>
## 0.22.1 (2020. 02. 25.) { #221-2020-02-25 }

<a id="221-2020-02-25-toast-push"></a>
### TOAST Push { #221-2020-02-25-toast-push }

<a id="221-2020-02-25-toast-push-improvements"></a>
#### 改善事項 
* トークン登録の機能改善 
    * 初回トークン登録時にユーザーIDが設定されていない場合は、デバイス識別子を使用して登録します。 
    * トークンに登録した後、ユーザーIDを設定、または変更すると、トークン情報を更新します。 
     
<a id="220-2020-02-11"></a>
## 0.22.0 (2020. 02. 11.) { #220-2020-02-11 }

<a id="220-2020-02-11-toast-iap"></a>
### TOAST IAP { #220-2020-02-11-toast-iap }

<a id="220-2020-02-11-toast-iap-improvements"></a>
#### 改善事項 
* 安全性の改善 
 
 
<a id="210-2019-12-24"></a>
## 0.21.0 (2019. 12. 24.) { #210-2019-12-24 }

<a id="210-2019-12-24-toast-logger"></a>
### TOAST Logger { #210-2019-12-24-toast-logger }

<a id="210-2019-12-24-toast-logger-improvements"></a>
#### 改善事項 
* Crash発生の位置情報の分類方式を改善するため、データを追加 
 
<a id="210-2019-12-24-toast-iap"></a>
### TOAST IAP { #210-2019-12-24-toast-iap }

<a id="210-2019-12-24-toast-iap-improvements"></a>
#### 改善事項 
* APIセキュリティ機能の追加
* 安全性の改善 
* Swiftインターフェイス追加定義 
 
<a id="201-2019-12-04"></a>
## 0.20.1 (2019. 12. 04.) { #201-2019-12-04 }
 
<a id="201-2019-12-04-common"></a>
### 共通 { #201-2019-12-04-common }
 
<a id="201-2019-12-04-common-improvements"></a>
#### 改善事項 
 
* 初期化ロジックの改善 
 
<a id="200-2019-11-26"></a>
## 0.20.0 (2019. 11. 26.) { #200-2019-11-26 }
 
<a id="200-2019-11-26-toast-push"></a>
### TOAST Push { #200-2019-11-26-toast-push }
 
<a id="200-2019-11-26-toast-push-improvements"></a>
#### 改善事項 
 
* トークン登録/削除結果通知を、コールバック構造に変更、Delegate削除 
* 以前登録した同意情報でトークンを再登録する機能追加 
* VoIP機能をサブモジュールに分離 
* Swiftインターフェイスを追加定義 
 
<a id="193-2019-10-29"></a>
## 0.19.3 (2019. 10. 29.) { #193-2019-10-29 }
 
<a id="193-2019-10-29-common"></a>
### 共通 { #193-2019-10-29-common }
 
<a id="193-2019-10-29-common-bug-fixes"></a>
#### バグ修正 
 
* Xcode 11未満でリンカーエラー発生の問題を修正 
 
<a id="192-2019-10-25"></a>
## 0.19.2 (2019. 10. 25.) { #192-2019-10-25 }
 
<a id="192-2019-10-25-toast-push"></a>
### TOAST Push { #192-2019-10-25-toast-push }
 
<a id="192-2019-10-25-toast-push-improvements"></a>
#### 改善事項 
 
* (旧) TCPushSDKマイグレーションのサポート 
 
<a id="191-2019-10-18"></a>
## 0.19.1 (2019. 10. 18.) { #191-2019-10-18 }
 
<a id="191-2019-10-18-toast-push"></a>
### TOAST Push { #191-2019-10-18-toast-push }
 
<a id="191-2019-10-18-toast-push-improvements"></a>
#### 改善事項 
 
* トークン登録の機能改善 
 
<a id="190-2019-10-15"></a>
## 0.19.0 (2019. 10. 15.) { #190-2019-10-15 }
 
<a id="190-2019-10-15-toast-push"></a>
### TOAST Push { #190-2019-10-15-toast-push }
 
<a id="190-2019-10-15-toast-push-added-features"></a>
#### 追加事項 
 
* 通知実行に対する通知の機能を追加 
 
<a id="180-2019-10-01"></a>
## 0.18.0 (2019. 10. 01.) { #180-2019-10-01 }
 
<a id="180-2019-10-01-common"></a>
### 共通 { #180-2019-10-01-common }
 
<a id="180-2019-10-01-common-improvements"></a>
#### 改善事項 
 
* iOS 13 / Xcode 11対応
 
<a id="180-2019-10-01-toast-iap"></a>
### TOAST IAP { #180-2019-10-01-toast-iap }
 
<a id="180-2019-10-01-toast-iap-added-features"></a>
#### 追加事項 
 
* 購入リクエスト時にユーザーデータ設定をの機能を追加 
 
<a id="180-2019-10-01-toast-iap-improvements"></a>
#### 改善事項 
 
* 復元機能を実行した後、復元された決済の項目のみ返すよう変更 
 
<a id="180-2019-10-01-toast-push"></a>
### TOAST Push { #180-2019-10-01-toast-push }
 
<a id="180-2019-10-01-toast-push-improvements"></a>
#### 改善事項 
 
* ToastPushConfigurationオブジェクトのNullabilityプロパティの変更 
* リッチメッセージ作成ロジックの改善により、ToastPushMediaオブジェクトのsourceType、extensionのプロパティを削除 
* リッチメッセージのソース情報にハングルURLも対応 
 
<a id="180-2019-10-01-toast-push-bug-fixes"></a>
#### バグ修正 
 
* コンソール設定で、メッセージ受信/確認の機能が未使用と設定されている場合、リッチメッセージが正常に表示されなかったバグを修正 
* iOS 13以上の環境でデバイストークンを獲得できないバグを修正 
 
<a id="170-2019-08-27"></a>
## 0.17.0 (2019. 08. 27.) { #170-2019-08-27 }
 
<a id="170-2019-08-27-common"></a>
### 共通 { #170-2019-08-27-common }
 
<a id="170-2019-08-27-common-improvements"></a>
#### 改善事項  
* 安全性の改善 
 
<a id="170-2019-08-27-toast-iap"></a>
### TOAST IAP { #170-2019-08-27-toast-iap }
 
<a id="170-2019-08-27-toast-iap-added-features"></a>
#### 追加事項 
 
* 自動更新型の消費性サブスクリプションプロダクトの追加 
 
<a id="170-2019-08-27-toast-iap-improvements"></a>
#### 改善事項 
 
* プロダクト一覧を照会時、invalidProductsに有効な商品が返されていた問題を修正 
 
<a id="170-2019-08-27-toast-push"></a>
### TOAST Push { #170-2019-08-27-toast-push }
 
<a id="170-2019-08-27-toast-push-improvements"></a>
#### 改善事項 
 
* プッシュメッセージに通知音を設定せず、送信時のデフォルト通知音が設定されるよう改善 
 
<a id="161-2019-07-29"></a>
## 0.16.1 (2019. 07. 29.) { #161-2019-07-29 }
 
<a id="161-2019-07-29-common"></a>
### 共通 { #161-2019-07-29-common }
 
<a id="161-2019-07-29-common-improvements"></a>
#### 改善事項  
* 国名コードを取得できない問題を修正 
 
<a id="160-2019-07-23"></a>
## 0.16.0 (2019. 07. 23.) { #160-2019-07-23 }
 
<a id="160-2019-07-23-toast-logger"></a>
### TOAST Logger { #160-2019-07-23-toast-logger }
 
<a id="160-2019-07-23-toast-logger-improvements"></a>
#### 改善事項  
* シンボルが存在するバイナリーの場合、CrashReport CallStackにシンボル文字が含まれるよう改善 
* CrashReport Reasonが出力されない問題の修正 
 
<a id="160-2019-07-23-toast-iap"></a>
### TOAST IAP { #160-2019-07-23-toast-iap }
 
<a id="160-2019-07-23-toast-iap-improvements"></a>
#### 改善事項 
 
* 決済成功状態から以前の決済状態に変更される問題を修正 
* アプリ内での購入が許可されていない状態で決済がリクエストされていた問題を修正 
* プロモーション決済の改善 
 
<a id="160-2019-07-23-toast-push"></a>
### TOAST Push { #160-2019-07-23-toast-push }
 
<a id="160-2019-07-23-toast-push-improvements"></a>
#### 改善事項 
 
* メッセージ/アクションの受信delegate変更 
 
<a id="150-2019-06-25"></a>
## 0.15.0 (2019. 06. 25.) { #150-2019-06-25 }
 
<a id="150-2019-06-25-toast-iap"></a>
### TOAST IAP { #150-2019-06-25-toast-iap }
 
<a id="150-2019-06-25-toast-iap-improvements"></a>
#### 改善事項 
 
* 新規決済、プロモーション決済、未消費内訳の詳細をリクエストすると、未完了決済のアイテムを再処理するロジックを追加 
 
<a id="150-2019-06-25-toast-push"></a>
### TOAST Push { #150-2019-06-25-toast-push }
 
<a id="150-2019-06-25-toast-push-added-features"></a>
#### 追加事項 
 
* 初期化すると、国、言語コード設定を行う機能を追加 
* トークン情報のアップデート機能を追加 
* 通知オプション設定機能を追加 
 
<a id="150-2019-06-25-toast-push-improvements"></a>
#### 改善事項 
 
* 通知オプションの基本設定の変更 
    * アプリ実行中は通知を表示しないよう変更 
        * 以前と同じ動作をするためには[こちら](./push-ios/#_6)を確認してください。 
         
<a id="141-2019-05-16"></a>
## 0.14.1 (2019. 05. 16.) { #141-2019-05-16 }
 
<a id="141-2019-05-16-toast-iap"></a>
### TOAST IAP { #141-2019-05-16-toast-iap }
 
<a id="141-2019-05-16-toast-iap-improvements"></a>
#### 改善事項 
 
* 処理中の再処理決済件と同一の商品購買時に保有した商品に処理される現象改善 
 
<a id="141-2019-05-16-toast-push"></a>
### TOAST Push { #141-2019-05-16-toast-push }
 
<a id="141-2019-05-16-toast-push-improvements"></a>
#### 改善事項 
 
* 端末機カレンダーの設定によって、地表イベントの発生時間が誤って収集されていたバグ修正 
 
<a id="140-2019-05-14"></a>
## 0.14.0 (2019. 05. 14.) { #140-2019-05-14 }
 
<a id="140-2019-05-14-common"></a>
### 共通 { #140-2019-05-14-common }
 
<a id="140-2019-05-14-common-improvements"></a>
#### 改善事項 
 
* Networkエラーコードの統合 
* 安全性改善 
 
<a id="140-2019-05-14-toast-iap"></a>
### TOAST IAP { #140-2019-05-14-toast-iap }
 
<a id="140-2019-05-14-toast-iap-improvements"></a>
#### 改善事項 
 
* 購買復元機能の改善 
    * AppStore購買内訳をベースに漏れた決済の復元機能を追加  
    * 復元失敗エラーコード追加 
* 購入結果クラスへのストア要求(プロモーション)フラグの追加 
* 再処理対象の拡大 
* 決済の流れ改善 
 
<a id="140-2019-05-14-toast-push"></a>
### TOAST Push { #140-2019-05-14-toast-push }
 
<a id="140-2019-05-14-toast-push-improvements"></a>
#### 改善事項 
 
* 安全性改善 
* メッセージ受信Delegate で配信されるpayload 情報にメッセージID 情報追加 
* 広告性メッセージ受信同意、夜間広告性メッセージ受信同意が不要なVoIPの場合、受信同意可否に関わらずメッセージ受信 
 
<a id="130-2019-03-26"></a>
## 0.13.0 (2019. 03. 26.) { #130-2019-03-26 }
 
<a id="130-2019-03-26-common"></a>
### 共通 { #130-2019-03-26-common }
 
<a id="130-2019-03-26-common-improvements"></a>
#### 改善事項 
 
* Public Classの使用性改善 
  * Description追加 
  * Nullability、 NSCoding、 NSCopyingの支援 
 
<a id="toast-core"></a>
### TOAST Core { #toast-core }
 
<a id="toast-core-improvements"></a>
#### 改善事項 
 
* 内部例外処理追加 
 
<a id="130-2019-03-26-toast-logger"></a>
### TOAST Logger { #130-2019-03-26-toast-logger }
 
<a id="130-2019-03-26-toast-logger-added-features"></a>
#### 追加事項 
 
* arm64eアーキテクチャを使用する機器のCrash分析支援 
* PLCrashReporter Dependency 変更 
 
<a id="130-2019-03-26-toast-logger-improvements"></a>
#### 改善事項 
 
* Configuration Interface 変更 
  * Deprecate 
    * configurationWithProjectKey 
  * Add 
    * configurationWithAppKey 
 
* UserIDの設定時点によって転送するLogのUserIDが更新されないかもしれない問題修正 
 
<a id="130-2019-03-26-toast-iap"></a>
### TOAST IAP { #130-2019-03-26-toast-iap }
 
<a id="130-2019-03-26-toast-iap-improvements"></a>
#### 改善事項 
 
* 内部例外処理追加 
 
<a id="130-2019-03-26-toast-push"></a>
### TOAST Push { #130-2019-03-26-toast-push }
 
<a id="130-2019-03-26-toast-push-added-features"></a>
#### 追加事項 
 
* unregisterToken API の追加 
 
<a id="124-2019-03-19"></a>
## 0.12.4 (2019. 03. 19.) { #124-2019-03-19 }
 
<a id="124-2019-03-19-toast-core"></a>
### TOAST Core { #124-2019-03-19-toast-core }
 
<a id="124-2019-03-19-toast-core-improvements"></a>
#### 改善事項 
 
* 例外を追加する 
 
<a id="123-2019-02-26"></a>
## 0.12.3 (2019. 02. 26.) { #123-2019-02-26 }
 
<a id="toast-core-common"></a>
### TOAST Core、 Common { #toast-core-common }
 
<a id="toast-core-common-improvements"></a>
#### 改善事項 
 
* util関数に例外を追加 
 
<a id="123-2019-02-26-toast-iap"></a>
### TOAST IAP { #123-2019-02-26-toast-iap }
 
<a id="123-2019-02-26-toast-iap-improvements"></a>
#### 改善事項 
 
* 商品情報のキャッシングを追加する 
* 例外を追加する 
 
<a id="122-2019-02-08---hotfix"></a>
## 0.12.2 (2019. 02. 08.) - Hotfix { #122-2019-02-08---hotfix }
 
<a id="122-2019-02-08---hotfix-toast-core"></a>
### TOAST Core { #122-2019-02-08---hotfix-toast-core }
 
<a id="122-2019-02-08---hotfix-toast-core-improvements"></a>
#### 改善事項 
 
* ToastTransferで断続的に発生していたCrashを防止するためのコードを追加 
 
<a id="121-2019-01-08"></a>
## 0.12.1 (2019. 01. 08.) { #121-2019-01-08 }
 
<a id="121-2019-01-08-toast-iap"></a>
### TOAST IAP { #121-2019-01-08-toast-iap }
 
<a id="121-2019-01-08-toast-iap-improvements"></a>
#### 改善事項 
 
* 特定状況で決済状態がVerifyEndの決済の再処理が動作しない問題の修正 
 
<a id="120-2018-12-27"></a>
## 0.12.0 (2018. 12. 27.) { #120-2018-12-27 }
 
<a id="120-2018-12-27-toast-core"></a>
### TOAST CORE { #120-2018-12-27-toast-core }
 
<a id="120-2018-12-27-toast-core-improvements"></a>
#### 改善事項 
 
* ToastTransferで断続的に発生していたCrashを防止するためのコードを追加 
 
<a id="120-2018-12-27-toast-push"></a>
### TOAST Push { #120-2018-12-27-toast-push }
 
<a id="120-2018-12-27-toast-push-added-features"></a>
#### 追加事項 
 
* 新規機能追加 
 
<a id="120-2018-12-27-toast-iap"></a>
### TOAST IAP { #120-2018-12-27-toast-iap }
 
<a id="120-2018-12-27-toast-iap-improvements"></a>
#### 改善事項 
 
* Appleで再処理するTransactionの処理ができるようにUserID Checkロジックの例外処理を追加 
* ToastOperationで断続的に発生していたCrashを防止するためのコードを追加  
 
 
<a id="111-2018-12-04"></a>
## 0.11.1 (2018. 12. 04.) { #111-2018-12-04 }
 
<a id="111-2018-12-04-toast-iap"></a>
### TOAST IAP { #111-2018-12-04-toast-iap }
 
<a id="111-2018-12-04-toast-iap-added-features"></a>
#### 追加事項 
 
* 新規機能追加 
 
 
<a id="110-2018-11-20"></a>
## 0.11.0 (2018. 11. 20.) { #110-2018-11-20 }
 
<a id="toast-log-crash"></a>
### TOAST Log & Crash { #toast-log-crash }
 
<a id="toast-log-crash-added-features"></a>
#### 追加事項 
 
* Network Insights機能追加 
 
 
<a id="90-2018-09-04"></a>
## 0.9.0 (2018. 09. 04.) { #90-2018-09-04 }
 
<a id="90-2018-09-04-toast-log-crash"></a>
### TOAST Log & Crash { #90-2018-09-04-toast-log-crash }
 
<a id="90-2018-09-04-toast-log-crash-added-features"></a>
#### 追加事項 
 
* 新規機能追加 
