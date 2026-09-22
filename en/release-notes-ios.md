<!-- pre-align:aligned sig=763014a10170 -->

<a id="nhn-cloud-sdk-user-guide-release-notes-ios"></a>
## NHN Cloud > SDK User Guide > Release Notes > iOS { #nhn-cloud-sdk-user-guide-release-notes-ios }

<a id="90-2025-04-29"></a>
## 1.9.0 (2025. 04. 29.) { #90-2025-04-29 }

<a id="90-2025-04-29-nhn-cloud-push"></a>
### NHN Cloud Push { #90-2025-04-29-nhn-cloud-push }

<a id="90-2025-04-29-nhn-cloud-push-added-features"></a>
#### Added Features
* Added Notification Hub 
    * NHN Cloud Push SDK supports Notification Hub
    * You can use it by setting the value NHNCloudPushServiceTypeNotificationHub in the serviceType property of NHNCloudPushConfiguration.

<a id="86-2024-11-15"></a>
## 1.8.6 (2024. 11. 15.) { #86-2024-11-15 }

<a id="86-2024-11-15-nhn-cloud-push"></a>
### NHN Cloud Push { #86-2024-11-15-nhn-cloud-push }

<a id="86-2024-11-15-nhn-cloud-push-improved"></a>
#### Improved
* Added API to set device ID 

<a id="85-2024-10-08"></a>
## 1.8.5 (2024. 10. 08.) { #85-2024-10-08 }

<a id="85-2024-10-08-nhn-cloud-iap"></a>
### NHN Cloud IAP { #85-2024-10-08-nhn-cloud-iap }

<a id="85-2024-10-08-nhn-cloud-iap-improved"></a>
#### Improved
* Improved the feature to send payment details

<a id="84-2024-09-11"></a>
## 1.8.4 (2024. 09. 11.) { #84-2024-09-11 }

<a id="84-2024-09-11-nhn-cloud-push"></a>
### NHN Cloud Push { #84-2024-09-11-nhn-cloud-push }

<a id="84-2024-09-11-nhn-cloud-push-improved"></a>
#### Improved
* Fixed duplicate notification issue (iOS 18 Beta)
    * Improved so that duplicate notifications are not received when an application is in the foreground in iOS 18 (OS bugs).

<a id="83-2024-07-23"></a>
## 1.8.3 (2024. 07. 23.) { #83-2024-07-23 }

<a id="83-2024-07-23-common"></a>
### Common { #83-2024-07-23-common }

<a id="83-2024-07-23-common-improved"></a>
#### Improved
* Improved stability

<a id="82-2024-06-25"></a>
## 1.8.2 (2024. 06. 25.) { #82-2024-06-25 }

<a id="82-2024-06-25-common"></a>
### Common { #82-2024-06-25-common }

<a id="82-2024-06-25-common-improved"></a>
#### Improved
* Improved stability

<a id="81-2024-02-27"></a>
## 1.8.1 (2024. 02. 27.) { #81-2024-02-27 }

<a id="81-2024-02-27-common"></a>
### Common { #81-2024-02-27-common }

<a id="81-2024-02-27-common-improved"></a>
#### Improved
* Applied Privacy manifest

<a id="81-2024-02-27-nhn-cloud-push"></a>
### NHN Cloud Push { #81-2024-02-27-nhn-cloud-push }

<a id="81-2024-02-27-nhn-cloud-push-improved"></a>
#### Improved
* Fixed an issue where message click actions do not work immediately in certain environments

<a id="80-2024-01-23"></a>
## 1.8.0 (2024. 01. 23.) { #80-2024-01-23 }

<a id="80-2024-01-23-nhn-cloud-iap"></a>
### NHN Cloud IAP { #80-2024-01-23-nhn-cloud-iap }

<a id="80-2024-01-23-nhn-cloud-iap-improved"></a>
#### Improved
* Improved payment verification methods
    * Improved to enable (old) receipt verification in new SDKs
        * [(New) Receipt verification + Notification V2](/Mobile%20Service/IAP/en/console-apple-guide/#new-receipt-verification-notification-v2)
        * [(Old) Receipt verification + Notification V1 (Deprecated)](/Mobile%20Service/IAP/en/console-apple-guide/#old-receipt-verification-notification-v1-soon-to-be-deprecated)

<a id="71-2023-12-19"></a>
## 1.7.1 (2023. 12. 19.) { #71-2023-12-19 }

<a id="71-2023-12-19-common"></a>
### Common { #71-2023-12-19-common }

<a id="71-2023-12-19-common-improved"></a>
#### Improved
* Signature applied
    * Applied the `NHN Cloud Corp.` signature to the binaries being distributed.

<a id="71-2023-12-19-logger"></a>
### Logger { #71-2023-12-19-logger }

<a id="71-2023-12-19-logger-improved"></a>
#### Improved
* Improved NetworkInsight stability of Instance Logger

<a id="71-2023-12-19-symboluploaderv004"></a>
### SymbolUploader(v0.0.4) { #71-2023-12-19-symboluploaderv004 }

<a id="71-2023-12-19-symboluploaderv004-improved"></a>
#### Improved
* Improved stability

<a id="70-2023-11-14"></a>
## 1.7.0 (2023. 11. 14.) { #70-2023-11-14 }

<a id="70-2023-11-14-common"></a>
### Common { #70-2023-11-14-common }

<a id="70-2023-11-14-common-improved"></a>
#### Improved
* Raised the minimum supported version
    * 9.0 > 11.0
* Ended support for architectures
    *  i386, armv7s, armv7

<a id="70-2023-11-14-nhn-cloud-iap"></a>
### NHN Cloud IAP { #70-2023-11-14-nhn-cloud-iap }

<a id="70-2023-11-14-nhn-cloud-iap-improved"></a>
#### Improved
* Changed payment verification methods - [(New) Receipt verification + Notification V2](/Mobile%20Service/IAP/en/console-apple-guide/#new-receipt-verification-notification-v2)

<a id="62-2023-08-29"></a>
## 1.6.2 (2023. 08. 29.) { #62-2023-08-29 }

<a id="62-2023-08-29-common"></a>
### Common { #62-2023-08-29-common }

<a id="62-2023-08-29-common-improved"></a>
#### Improved
* Fixed an issue where CountryCode is not obtained

<a id="62-2023-08-29-nhn-cloud-ocr"></a>
### NHN Cloud OCR { #62-2023-08-29-nhn-cloud-ocr }

<a id="62-2023-08-29-nhn-cloud-ocr-added-features"></a>
#### Added Features
* Added recognition area in the result of credit card/ID card recognition

<a id="61-2023-07-25"></a>
## 1.6.1 (2023. 07. 25.) { #61-2023-07-25 }

<a id="61-2023-07-25-nhn-cloud-iap"></a>
### NHN Cloud IAP { #61-2023-07-25-nhn-cloud-iap }

<a id="61-2023-07-25-nhn-cloud-iap-improved"></a>
#### Improved
* Improved the feature to send payment details

<a id="60-2023-07-11"></a>
## 1.6.0 (2023. 07. 11.) { #60-2023-07-11 }

<a id="60-2023-07-11-nhn-cloud-ocr"></a>
### NHN Cloud OCR { #60-2023-07-11-nhn-cloud-ocr }

<a id="60-2023-07-11-nhn-cloud-ocr-added-features"></a>
#### Added Features
* Added OCR (ID Card Recognizer)

<a id="50-2023-06-27"></a>
## 1.5.0 (2023. 06. 27.) { #50-2023-06-27 }

<a id="50-2023-06-27-nhn-cloud-push"></a>
### NHN Cloud Push { #50-2023-06-27-nhn-cloud-push }

<a id="50-2023-06-27-nhn-cloud-push-improved"></a>
#### Improved
* Improved the token registration feature
    * Provided the option to register a token regardless of the app's notification permissions.

<a id="50-2023-06-27-symboluploaderv003"></a>
### SymbolUploader(v0.0.3) { #50-2023-06-27-symboluploaderv003 }
* Improved stability

<a id="40-2023-05-30"></a>
## 1.4.0 (2023. 05. 30.) { #40-2023-05-30 }

<a id="40-2023-05-30-common"></a>
### Common { #40-2023-05-30-common }

<a id="40-2023-05-30-common-improved"></a>
#### Improved
* Added the SPM(swift package manager) deployment method

<a id="40-2023-05-30-nhn-cloud-iap"></a>
### NHN Cloud IAP { #40-2023-05-30-nhn-cloud-iap }

<a id="40-2023-05-30-nhn-cloud-iap-added-features"></a>
#### Added Featrues
* Added a feature to send payment details 
    * You can view payment details on the Transaction tab in the IAP console.

<a id="40-2023-05-30-symboluploaderv002"></a>
### SymbolUploader(v0.0.2) { #40-2023-05-30-symboluploaderv002 }
* Improved run script
    * Added support for Cocoapods, SPM

<a id="31-2023-05-19---hotfix"></a>
## 1.3.1 (2023. 05. 19.) - Hotfix { #31-2023-05-19---hotfix }

<a id="31-2023-05-19---hotfix-nhn-cloud-push"></a>
### NHN Cloud Push { #31-2023-05-19---hotfix-nhn-cloud-push }

<a id="31-2023-05-19---hotfix-nhn-cloud-push-improved"></a>
#### Improved
* Improved the token registration feature
    * When registering a token, if the notification setting of the app is disabled, `NHNCloudPushErrorPermissionDenied` is returned again.
    
<a id="30-2023-02-28"></a>
## 1.3.0 (2023. 02. 28.) { #30-2023-02-28 }

<a id="30-2023-02-28-common"></a>
### Common { #30-2023-02-28-common }

<a id="30-2023-02-28-common-improved"></a>
#### Improved
* Improved stability

<a id="21-2023-01-31"></a>
## 1.2.1 (2023. 01. 31.) { #21-2023-01-31 }

<a id="21-2023-01-31-nhn-cloud-push"></a>
### NHN Cloud Push { #21-2023-01-31-nhn-cloud-push }

<a id="21-2023-01-31-nhn-cloud-push-improved"></a>
#### Improved
* Improved token registration function

<a id="21-2023-01-31-nhn-cloud-ocr"></a>
### NHN Cloud OCR { #21-2023-01-31-nhn-cloud-ocr }

<a id="21-2023-01-31-nhn-cloud-ocr-improved"></a>
#### Improved
* Improved credit card recognition performance
* Improved stability

<a id="20-2022-11-29"></a>
## 1.2.0 (2022. 11. 29.) { #20-2022-11-29 }

<a id="20-2022-11-29-nhn-cloud-logger"></a>
### NHN Cloud Logger { #20-2022-11-29-nhn-cloud-logger }

<a id="20-2022-11-29-nhn-cloud-logger-added-features"></a>
#### Added Features
* Added support for Logger for government agencies

<a id="20-2022-11-29-nhn-cloud-push"></a>
### NHN Cloud Push { #20-2022-11-29-nhn-cloud-push }

<a id="20-2022-11-29-nhn-cloud-push-improved"></a>
#### Improved
* Improved sending push events

<a id="20-2022-11-29-nhn-cloud-ocr"></a>
### NHN Cloud OCR { #20-2022-11-29-nhn-cloud-ocr }

<a id="20-2022-11-29-nhn-cloud-ocr-improved"></a>
#### Improved
* Improved UI

<a id="10-2022-10-25"></a>
## 1.1.0 (2022. 10. 25.) { #10-2022-10-25 }

<a id="10-2022-10-25-common"></a>
### Common { #10-2022-10-25-common }

<a id="10-2022-10-25-common-improvements"></a>
#### Improvements
* Improved stability

<a id="10-2022-10-25-nhn-cloud-iap"></a>
### NHN Cloud IAP { #10-2022-10-25-nhn-cloud-iap }

<a id="10-2022-10-25-nhn-cloud-iap-added-features"></a>
#### Added Features
* [All stores] Added APIs for activated subscription query and unconsumed purchase query

<a id="10-2022-10-25-nhn-cloud-ocr"></a>
### NHN Cloud OCR { #10-2022-10-25-nhn-cloud-ocr }

<a id="10-2022-10-25-nhn-cloud-ocr-added-features"></a>
#### Added Features
* Added OCR(Credit Card Recognizer)

<a id="00-2022-07-12"></a>
## 1.0.0 (2022. 07. 12.) { #00-2022-07-12 }

<a id="00-2022-07-12-common"></a>
### Common { #00-2022-07-12-common }

<a id="00-2022-07-12-common-improvements"></a>
#### Improvements
* Improved stability
* Changed the module name to NHN Cloud SDK
	* TOAST SDK has been deprecated.

<a id="300-2022-03-29"></a>
## 0.30.0 (2022. 03. 29.) { #300-2022-03-29 }

<a id="300-2022-03-29-toast-iap"></a>
### TOAST IAP { #300-2022-03-29-toast-iap }

<a id="300-2022-03-29-toast-iap-added-features"></a>
#### Added Features
* Added a property to check whether the payment is sandbox payment or not (sandboxPayment) to ToastPurchaseResult

<a id="292-2021-11-23"></a>
## 0.29.2 (2021. 11. 23.) { #292-2021-11-23 }

<a id="292-2021-11-23-toast-push"></a>
### TOAST Push { #292-2021-11-23-toast-push }

<a id="292-2021-11-23-toast-push-improvements"></a>
#### Improvements
* Improved stability

<a id="291-2021-10-26"></a>
## 0.29.1 (2021. 10. 26.) { #291-2021-10-26 }

<a id="291-2021-10-26-toast-iap"></a>
### TOAST IAP { #291-2021-10-26-toast-iap }

<a id="291-2021-10-26-toast-iap-improvements"></a>
#### Improvements
* Improved stability

<a id="290-2021-07-06"></a>
## 0.29.0 (2021. 07. 06.) { #290-2021-07-06 }

<a id="290-2021-07-06-common"></a>
### Common { #290-2021-07-06-common }

<a id="290-2021-07-06-common-improvements"></a>
#### Improvements
* Improved stability

<a id="290-2021-07-06-toast-iap"></a>
### TOAST IAP { #290-2021-07-06-toast-iap }

<a id="290-2021-07-06-toast-iap-added-features"></a>
#### Added Features
* Added a monthly payment limit feature

<a id="280-2021-05-25"></a>
## 0.28.0 (2021. 05. 25.) { #280-2021-05-25 }

<a id="280-2021-05-25-common"></a>
### Common { #280-2021-05-25-common }

<a id="280-2021-05-25-common-improvements"></a>
#### Improvements
* Added xcframework
    * Added support for arm Simulator

<a id="280-2021-05-25-toast-logger"></a>
### TOAST Logger { #280-2021-05-25-toast-logger }

<a id="280-2021-05-25-toast-logger-crashreporter-buildinfo-20210525"></a>
#### CrashReporter (BuildInfo 20210525)
* Improved the way to classify architectures
    * Fixed an issue where iOS14 Core Library is not symbolicated

<a id="272-2021-03-23"></a>
## 0.27.2 (2021. 03. 23.) { #272-2021-03-23 }

<a id="272-2021-03-23-common"></a>
### Common { #272-2021-03-23-common }

<a id="272-2021-03-23-common-improvements"></a>
#### Improvements
* Improved stability

<a id="272-2021-03-23-toast-logger"></a>
### TOAST Logger { #272-2021-03-23-toast-logger }

<a id="272-2021-03-23-toast-logger-symboluploader-v001"></a>
#### SymbolUploader (v0.0.1)
* Added SymbolUploader

<a id="271-2020-11-24"></a>
## 0.27.1 (2020. 11. 24.) { #271-2020-11-24 }

<a id="271-2020-11-24-toast-iap"></a>
### TOAST IAP { #271-2020-11-24-toast-iap }

<a id="271-2020-11-24-toast-iap-improvements"></a>
#### Improvements
* Subscription product resubscription error revision (iOS 14 )
- Changed ToastProductsResponse to return nil when failing to get product info from the Appstore

<a id="271-2020-11-24-toast-push"></a>
### TOAST Push { #271-2020-11-24-toast-push }

<a id="271-2020-11-24-toast-push-improvements"></a>
#### Improvements
* Improved problem where callback did not occur upon a token disable request and there were no registered tokens

<a id="270-2020-09-11"></a>
## 0.27.0 (2020. 09. 11.) { #270-2020-09-11 }

<a id="270-2020-09-11-toast-iap"></a>
### TOAST IAP { #270-2020-09-11-toast-iap }

<a id="270-2020-09-11-toast-iap-added-features"></a>
#### Added Features
* Add localized product information (localizedTitle, localizedDescription) to ToastProduct

<a id="270-2020-09-11-toast-iap-improvements"></a>
#### Improvements
* Handled iOS 14 beta changes
     * Fixed an issue where payment failure Delegate is not received

<a id="270-2020-09-11-toast-push"></a>
### TOAST Push { #270-2020-09-11-toast-push }

<a id="270-2020-09-11-toast-push-improvements"></a>
#### Improvements
* Improved stability

<a id="260-2020-07-28"></a>
## 0.26.0 (2020. 07. 28.) { #260-2020-07-28 }

<a id="260-2020-07-28-toast-push"></a>
### TOAST Push { #260-2020-07-28-toast-push }

<a id="260-2020-07-28-toast-push-added-features"></a>
#### Added Features
* User tag feature support

<a id="251-2020-07-03"></a>
## 0.25.1 (2020. 07. 03.) { #251-2020-07-03 }

<a id="251-2020-07-03-toast-logger"></a>
### TOAST Logger { #251-2020-07-03-toast-logger }

<a id="251-2020-07-03-toast-logger-improvements"></a>
#### Improvements
* Improved stability

<a id="251-2020-07-03-toast-push"></a>
### TOAST Push { #251-2020-07-03-toast-push }

<a id="251-2020-07-03-toast-push-improvements"></a>
#### Improvements
* Improved stability

<a id="250-2020-06-23"></a>
## 0.25.0 (2020. 06. 23.) { #250-2020-06-23 }

<a id="250-2020-06-23-common"></a>
### Common { #250-2020-06-23-common }

<a id="250-2020-06-23-common-improvements"></a>
#### Improvements
* Improved stability

<a id="250-2020-06-23-toast-push"></a>
### TOAST Push { #250-2020-06-23-toast-push }

<a id="250-2020-06-23-toast-push-improvements"></a>
#### Improvements
* Separate notification options setting interface

<a id="241-2020-05-26"></a>
## 0.24.1 (2020. 05. 26.) { #241-2020-05-26 }

<a id="241-2020-05-26-toast-push"></a>
### TOAST Push { #241-2020-05-26-toast-push }

<a id="241-2020-05-26-toast-push-improvements"></a>
#### Improvements
* Improved token registration function

<a id="240-2020-04-28"></a>
## 0.24.0 (2020. 04. 28.) { #240-2020-04-28 }

<a id="240-2020-04-28-common"></a>
### Common { #240-2020-04-28-common }
* Raised the minimum supported version for TOAST SDK (iOS 8.0 -> iOS 9.0)
* Improved stability

<a id="240-2020-04-28-toast-iap"></a>
### TOAST IAP { #240-2020-04-28-toast-iap }

<a id="240-2020-04-28-toast-iap-added-features"></a>
#### Added Features
* Added Optional Delegate to allow you to choose whether to proceed with the promotional payment

<a id="240-2020-04-28-toast-push"></a>
### TOAST Push { #240-2020-04-28-toast-push }

<a id="240-2020-04-28-toast-push-improvements"></a>
#### Improvements
* Improved stability

<a id="230-2020-03-24"></a>
## 0.23.0 (2020. 03. 24.) { #230-2020-03-24 }

<a id="230-2020-03-24-toast-logger"></a>
### TOAST Logger { #230-2020-03-24-toast-logger }

<a id="230-2020-03-24-toast-logger-improvements"></a>
#### Improvements
* Fixed an issue where CrashReport CallStack could contain invalid strings

<a id="230-2020-03-24-toast-push"></a>
### TOAST Push { #230-2020-03-24-toast-push }

<a id="230-2020-03-24-toast-push-added-features"></a>
#### Added Features
* Added notification option setting function
     * At initialization, it is possible to set whether to expose foreground notifications, use badge icons, and use notification sounds.

<a id="221-2020-02-25"></a>
## 0.22.1 (2020. 02. 25.) { #221-2020-02-25 }

<a id="221-2020-02-25-toast-push"></a>
### TOAST Push { #221-2020-02-25-toast-push }

<a id="221-2020-02-25-toast-push-improvements"></a>
#### Improvements
* Improved token registration function
    * If a user ID is not set at the time of initial token registration, it is registered using the device identifier.
    * If you set or change the user ID after registering the token, the token information is updated.

<a id="220-2020-02-11"></a>
## 0.22.0 (2020. 02. 11.) { #220-2020-02-11 }

<a id="220-2020-02-11-toast-iap"></a>
### TOAST IAP { #220-2020-02-11-toast-iap }

<a id="220-2020-02-11-toast-iap-improvements"></a>
#### Improvements
* Improved stability

<a id="210-2019-12-24"></a>
## 0.21.0 (2019. 12. 24.) { #210-2019-12-24 }

<a id="210-2019-12-24-toast-logger"></a>
### TOAST Logger { #210-2019-12-24-toast-logger }

<a id="210-2019-12-24-toast-logger-improvements"></a>
#### Improvements
* Added data to improve the classification method of crash occurrence location

<a id="210-2019-12-24-toast-iap"></a>
### TOAST IAP { #210-2019-12-24-toast-iap }

<a id="210-2019-12-24-toast-iap-improvements"></a>
#### Improvements
* Added API security function
* Improved stability
* Defined Swift interface additionally

<a id="201-2019-12-04"></a>
## 0.20.1 (2019. 12. 04.) { #201-2019-12-04 }

<a id="201-2019-12-04-common"></a>
### Common { #201-2019-12-04-common }

<a id="201-2019-12-04-common-improvements"></a>
#### Improvements

* Improved initialization logic

<a id="200-2019-11-26"></a>
## 0.20.0 (2019. 11. 26.) { #200-2019-11-26 }

<a id="200-2019-11-26-toast-push"></a>
### TOAST Push { #200-2019-11-26-toast-push }

<a id="200-2019-11-26-toast-push-improvements"></a>
#### Improvements

* Changed token registration/deletion result notification to callback structure, delete delegate
* Added a feature to re-register tokens with previously registered agreement information
* Separated the VoIP function into a submodule
* Defined Swift interface additionally

<a id="193-2019-10-29"></a>
## 0.19.3 (2019. 10. 29.) { #193-2019-10-29 }

<a id="193-2019-10-29-common"></a>
### Common { #193-2019-10-29-common }

<a id="193-2019-10-29-common-bug-fixes"></a>
#### Bug Fixes

* Fixed a linker error that occurs under Xcode 11

<a id="192-2019-10-25"></a>
## 0.19.2 (2019. 10. 25.) { #192-2019-10-25 }

<a id="192-2019-10-25-toast-push"></a>
### TOAST Push { #192-2019-10-25-toast-push }

<a id="192-2019-10-25-toast-push-improvements"></a>
#### Improvements

* Supports migration of (old) TCPushSDK

<a id="191-2019-10-18"></a>
## 0.19.1 (2019. 10. 18.) { #191-2019-10-18 }

<a id="191-2019-10-18-toast-push"></a>
### TOAST Push { #191-2019-10-18-toast-push }

<a id="191-2019-10-18-toast-push-improvements"></a>
#### Improvements

* Improved token registration function

<a id="190-2019-10-15"></a>
## 0.19.0 (2019. 10. 15.) { #190-2019-10-15 }

<a id="190-2019-10-15-toast-push"></a>
### TOAST Push { #190-2019-10-15-toast-push }

<a id="190-2019-10-15-toast-push-added-features"></a>
#### Added Features

* Added notification feature for notification execution

<a id="180-2019-10-01"></a>
## 0.18.0 (2019. 10. 01.) { #180-2019-10-01 }

<a id="180-2019-10-01-common"></a>
### Common { #180-2019-10-01-common }

<a id="180-2019-10-01-common-improvements"></a>
#### Improvements

* Handles iOS 13 / Xcode 11

<a id="180-2019-10-01-toast-iap"></a>
### TOAST IAP { #180-2019-10-01-toast-iap }

<a id="180-2019-10-01-toast-iap-added-features"></a>
#### Added Features

* Added user data setting function when requesting a purchase

<a id="180-2019-10-01-toast-iap-improvements"></a>
#### Improvements

* Changed to return only the restored payment after performing the restore function

<a id="180-2019-10-01-toast-push"></a>
### TOAST Push { #180-2019-10-01-toast-push }

<a id="180-2019-10-01-toast-push-improvements"></a>
#### Improvements

* Changed the Nullability property of the ToastPushConfiguration object
* Deleted the sourceType and extension properties of the ToastPushMedia object by improving the rich message generation logic
* Supports Korean URLs in the source information of rich messages

<a id="180-2019-10-01-toast-push-bug-fixes"></a>
#### Bug Fixes

* Fixed a bug where rich messages were not displayed properly when the message reception/checking function is disabled in the console settings
* Fixed a bug where a device token could not be acquired in environments of iOS 13 or higher

<a id="170-2019-08-27"></a>
## 0.17.0 (2019. 08. 27.) { #170-2019-08-27 }

<a id="170-2019-08-27-common"></a>
### Common { #170-2019-08-27-common }

<a id="170-2019-08-27-common-improvements"></a>
#### Improvements
* Improved stability

<a id="170-2019-08-27-toast-iap"></a>
### TOAST IAP { #170-2019-08-27-toast-iap }

<a id="170-2019-08-27-toast-iap-added-features"></a>
#### Added Features

* Added auto-renewable consumable subscription products

<a id="170-2019-08-27-toast-iap-improvements"></a>
#### Improvements

* Fixed a problem that a valid product list was returned to invalidProducts when querying the product list

<a id="170-2019-08-27-toast-push"></a>
### TOAST Push { #170-2019-08-27-toast-push }

<a id="170-2019-08-27-toast-push-improvements"></a>
#### Improvements

* Improved so that the default notification sound is set when sending push messages without setting a notification sounds

<a id="161-2019-07-29"></a>
## 0.16.1 (2019. 07. 29.) { #161-2019-07-29 }

<a id="161-2019-07-29-common"></a>
### Common { #161-2019-07-29-common }

<a id="161-2019-07-29-common-improvements"></a>
#### Improvements
* Fixed an issue where the country code cannot be obtained

<a id="160-2019-07-23"></a>
## 0.16.0 (2019. 07. 23.) { #160-2019-07-23 }

<a id="160-2019-07-23-toast-logger"></a>
### TOAST Logger { #160-2019-07-23-toast-logger }

<a id="160-2019-07-23-toast-logger-improvements"></a>
#### Improvements
* Improved to include symbol string in CrashReport CallStack for binaries with symbols
* Fixed an issue where CrashReport Reason is not displayed

<a id="160-2019-07-23-toast-iap"></a>
### TOAST IAP { #160-2019-07-23-toast-iap }

<a id="160-2019-07-23-toast-iap-improvements"></a>
#### Improvements

* Fixed an issue where the status changes from successful payment status to previous payment status
* Fixed an issue where payment was requested when in-app purchases were not allowed
* Improved promotional payment

<a id="160-2019-07-23-toast-push"></a>
### TOAST Push { #160-2019-07-23-toast-push }

<a id="160-2019-07-23-toast-push-improvements"></a>
#### Improvements

* Changed message/action receiving delegate

<a id="150-2019-06-25"></a>
## 0.15.0 (2019. 06. 25.) { #150-2019-06-25 }

<a id="150-2019-06-25-toast-iap"></a>
### TOAST IAP { #150-2019-06-25-toast-iap }

<a id="150-2019-06-25-toast-iap-improvements"></a>
#### Improvements

* Added reprocessing logic for incomplete payment when requesting query for new payment, promotion payment, or unconsumed history

<a id="150-2019-06-25-toast-push"></a>
### TOAST Push { #150-2019-06-25-toast-push }

<a id="150-2019-06-25-toast-push-added-features"></a>
#### Added Features

* Added country code and language code setting function during initialization
* Added token information update function
* Added notification option setting function

<a id="150-2019-06-25-toast-push-improvements"></a>
#### Improvements

* Changed the default settings of notification options
    * Changed to not display notifications while the app is running
        * For the same behavior as before, check [here](./push-ios/#_6).

<a id="141-2019-05-16"></a>
## 0.14.1 (2019. 05. 16.) { #141-2019-05-16 }

<a id="141-2019-05-16-toast-iap"></a>
### TOAST IAP { #141-2019-05-16-toast-iap }

<a id="141-2019-05-16-toast-iap-improvements"></a>
#### Improvements

* Improved an issue where the user purchases the same product as the reprocessing payment case being processed, it is processed as the product owned by the user

<a id="141-2019-05-16-toast-push"></a>
### TOAST Push { #141-2019-05-16-toast-push }

<a id="141-2019-05-16-toast-push-improvements"></a>
#### Improvements

* Fixed a bug in which the event occurrence time was incorrectly collected according to the device's calendar setting

<a id="140-2019-05-14"></a>
## 0.14.0 (2019. 05. 14.) { #140-2019-05-14 }

<a id="140-2019-05-14-common"></a>
### Common { #140-2019-05-14-common }

<a id="140-2019-05-14-common-improvements"></a>
#### Improvements

* Integrated network-related error codes
* Improved stability

<a id="140-2019-05-14-toast-iap"></a>
### TOAST IAP { #140-2019-05-14-toast-iap }

<a id="140-2019-05-14-toast-iap-improvements"></a>
#### Improvements

* Improved purchase restore function
    * Added a function to restore missing payments based on AppStore purchase history
    * Added restore failure error codes
* Added whether it is store request (promotion) or not to the payment result class
* Expanded reprocessing targets
* Improved payment flow

<a id="140-2019-05-14-toast-push"></a>
### TOAST Push { #140-2019-05-14-toast-push }

<a id="140-2019-05-14-toast-push-improvements"></a>
#### Improvements

* Improved stability
* Added message ID information to payload information passed to the message-receiving delegate
* In the case of VoIP where agreement to receive advertising messages or night-time advertising messages is unnecessary, messages are received regardless of the agreement for message reception.

<a id="130-2019-03-26"></a>
## 0.13.0 (2019. 03. 26.) { #130-2019-03-26 }

<a id="130-2019-03-26-common"></a>
### Common { #130-2019-03-26-common }

<a id="130-2019-03-26-common-improvements"></a>
#### Improvements

* Improved usability of Public Class
  * Add Description
  * Support Nullability, NSCoding, NSCopying

<a id="130-2019-03-26-toast-core"></a>
### TOAST Core { #130-2019-03-26-toast-core }

<a id="130-2019-03-26-toast-core-improvements"></a>
#### Improvements

* Added internal exception handling

<a id="130-2019-03-26-toast-logger"></a>
### TOAST Logger { #130-2019-03-26-toast-logger }

<a id="130-2019-03-26-toast-logger-added-features"></a>
#### Added Features

* Support for crash analysis of devices using arm64e architecture
* Changed PLCrashReporter Dependency

<a id="130-2019-03-26-toast-logger-improvements"></a>
#### Improvements

* Changed Configuration Interface
  * Deprecate
    * configurationWithProjectKey
  * Add
    * configurationWithAppKey

* Fixed an issue where the UserID of the transferred log may not be updated depending on the user ID setting time

<a id="130-2019-03-26-toast-iap"></a>
### TOAST IAP { #130-2019-03-26-toast-iap }

<a id="130-2019-03-26-toast-iap-improvements"></a>
#### Improvements

* Added internal exception handling

<a id="130-2019-03-26-toast-push"></a>
### TOAST Push { #130-2019-03-26-toast-push }

<a id="130-2019-03-26-toast-push-added-features"></a>
#### Added Features

* Added token deletion API

<a id="124-2019-03-19"></a>
## 0.12.4 (2019. 03. 19.) { #124-2019-03-19 }

<a id="124-2019-03-19-toast-core"></a>
### TOAST Core { #124-2019-03-19-toast-core }

<a id="124-2019-03-19-toast-core-improvements"></a>
#### Improvements

* Added exception handling

<a id="123-2019-02-26"></a>
## 0.12.3 (2019. 02. 26.) { #123-2019-02-26 }

<a id="123-2019-02-26-toast-core-common"></a>
### TOAST Core, Common { #123-2019-02-26-toast-core-common }

<a id="123-2019-02-26-toast-core-common-improvements"></a>
#### Improvements

* Added exception handling for utility function

<a id="123-2019-02-26-toast-iap"></a>
### TOAST IAP { #123-2019-02-26-toast-iap }

<a id="123-2019-02-26-toast-iap-improvements"></a>
#### Improvements

* Added product information caching
* Added exception handling

<a id="122-2019-02-08---hotfix"></a>
## 0.12.2 (2019. 02. 08.) - Hotfix { #122-2019-02-08---hotfix }

<a id="122-2019-02-08---hotfix-toast-core"></a>
### TOAST Core { #122-2019-02-08---hotfix-toast-core }

<a id="122-2019-02-08---hotfix-toast-core-improvements"></a>
#### Improvements

* Added defense code to prevent intermittent crashes in ToastTransfer

<a id="121-2019-01-08"></a>
## 0.12.1 (2019. 01. 08.) { #121-2019-01-08 }

<a id="121-2019-01-08-toast-iap"></a>
### TOAST IAP { #121-2019-01-08-toast-iap }

<a id="121-2019-01-08-toast-iap-improvements"></a>
#### Improvements

* Fixed an issue where reprocessing of payments whose payment status is VerifyEnd did not work under certain circumstances

<a id="120-2018-12-27"></a>
## 0.12.0 (2018. 12. 27.) { #120-2018-12-27 }

<a id="120-2018-12-27-toast-core"></a>
### TOAST Core { #120-2018-12-27-toast-core }

<a id="120-2018-12-27-toast-core-improvements"></a>
#### Improvements

* Added defense code to prevent intermittent crashes in ToastTransfer

<a id="120-2018-12-27-toast-push"></a>
### TOAST Push { #120-2018-12-27-toast-push }

<a id="120-2018-12-27-toast-push-added-features"></a>
#### Added Features

* Added new features

<a id="120-2018-12-27-toast-iap"></a>
### TOAST IAP { #120-2018-12-27-toast-iap }

<a id="120-2018-12-27-toast-iap-improvements"></a>
#### Improvements

* Added exception handling of UserID Check logic to enable transaction processing reprocessed by Apple
* Added defense code to prevent intermittent crashes in ToastOperation


<a id="111-2018-12-04"></a>
## 0.11.1 (2018. 12. 04.) { #111-2018-12-04 }

<a id="111-2018-12-04-toast-iap"></a>
### TOAST IAP { #111-2018-12-04-toast-iap }

<a id="111-2018-12-04-toast-iap-added-features"></a>
#### Added Features

* Added new features


<a id="110-2018-11-20"></a>
## 0.11.0 (2018. 11. 20.) { #110-2018-11-20 }

<a id="110-2018-11-20-toast-log-crash"></a>
### TOAST Log & Crash { #110-2018-11-20-toast-log-crash }

<a id="110-2018-11-20-toast-log-crash-added-features"></a>
#### Added Features

* Added Network Insights function


<a id="90-2018-09-04"></a>
## 0.9.0 (2018. 09. 04.) { #90-2018-09-04 }

<a id="90-2018-09-04-toast-log-crash"></a>
### TOAST Log & Crash { #90-2018-09-04-toast-log-crash }

<a id="90-2018-09-04-toast-log-crash-added-features"></a>
#### Added Features

* Added new features
