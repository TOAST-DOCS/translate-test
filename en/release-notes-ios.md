<!-- machine_translated: true -->

<!-- pre-align:aligned sig=499fcf966eda -->

<a id="nhn-cloud-sdk-user-guide-release-notes-ios"></a>
## NHN Cloud > SDK User Guide > Release Notes > iOS { #nhn-cloud-sdk-user-guide-release-notes-ios }

<a id="100-2026-09-15"></a>
## 1.10.0 (September 15, 2026) { #100-2026-09-15 }

<a id="100-2026-09-15-nhn-cloud-logger"></a>
### NHN Cloud Logger { #100-2026-09-15-nhn-cloud-logger }

<a id="100-2026-09-15-nhn-cloud-logger-improved"></a>
#### Feature Updates

* Changed Log & Crash Search API Domain
    * The log collection API domain changed from api-logncrash.cloud.toast.com to api-logncrash.nhncloudservice.com.
    * The settings API domain changed from setting-logncrash.cloud.toast.com to api-setting-logncrash.nhncloudservice.com.

<a id="100-2026-09-15-symboluploaderv005"></a>
### SymbolUploader(v0.0.5) { #100-2026-09-15-symboluploaderv005 }

<a id="100-2026-09-15-symboluploaderv005-added-features"></a>
#### Added Features

* Applied Log & Crash Search Symbol API v3
    * Starting from v0.0.5, User Access Token authentication is required.
      * Authentication using appKey alone is not supported; User Access Token authentication is required.
      * You can configure a User Access Token directly or have one issued automatically by using a User Access Key and Secret Access Key.
      * For more information, refer to [Apply NHN Cloud Symbol Uploader](https://docs.nhncloud.com/en/nhncloud-sdk/en/log-collector-ios/#apply-nhn-cloud-symbol-uploader).

<a id="100-2026-09-15-nhn-cloud-push"></a>
### NHN Cloud Push { #100-2026-09-15-nhn-cloud-push }

<a id="100-2026-09-15-nhn-cloud-push-improved"></a>
#### Feature Updates

* Changed Push API domain
    * The token API and user tag API domain has been changed from api-push.cloud.toast.com to push.api.nhncloudservice.com.
* Improved Notification Hub metrics transfer method
    * Improved so that the same metrics are not counted twice even if metrics transfer is retried.

<a id="100-2026-09-15-nhn-cloud-push-bugfix"></a>
#### Bug Fixes

* Fixed an issue where Notification Hub token updates failed
    * Fixed an issue where token registration always failed after changing the user ID.

<a id="100-2026-09-15-nhn-cloud-ocr"></a>
### NHN Cloud OCR { #100-2026-09-15-nhn-cloud-ocr }

<a id="100-2026-09-15-nhn-cloud-ocr-improved"></a>
#### Feature Updates

* Changed OCR API Domain
    * The OCR API domain has been changed from ocr.api.nhncloudservice.com to api-ocr.nhncloudservice.com.
* Improved error delivery for PublicKey acquisition failures
    * Improved the system to deliver PublicKey acquisition failure errors that occur before Delegate registration after Delegate registration is complete.

<a id="100-2026-09-15-nhn-cloud-ocr-bugfix"></a>
#### Bug Fixes

* Fixed an issue where the Default UI icon aspect ratio was distorted

<a id="90-2025-04-29"></a>
## 1.9.0 (April 29, 2025) { #90-2025-04-29 }

<a id="90-2025-04-29-nhn-cloud-push"></a>
### NHN Cloud Push { #90-2025-04-29-nhn-cloud-push }

<a id="90-2025-04-29-nhn-cloud-push-added-features"></a>
#### Added Features

* Added Notification Hub
    * You can use Notification Hub in the NHNCloudPush SDK.
    * You can use it by setting the `NHNCloudPushServiceTypeNotificationHub` value for the `serviceType` property of `NHNCloudPushConfiguration`.

<a id="86-2024-11-15"></a>
## 1.8.6 (November 15, 2024) { #86-2024-11-15 }

<a id="86-2024-11-15-nhn-cloud-push"></a>
### NHN Cloud Push { #86-2024-11-15-nhn-cloud-push }

<a id="86-2024-11-15-nhn-cloud-push-improved"></a>
#### Feature Updates

* Added API to set device ID 

<a id="85-2024-10-08"></a>
## 1.8.5 (October 8, 2024) { #85-2024-10-08 }

<a id="85-2024-10-08-nhn-cloud-iap"></a>
### NHN Cloud IAP { #85-2024-10-08-nhn-cloud-iap }

<a id="85-2024-10-08-nhn-cloud-iap-improved"></a>
#### Feature Updates

* Improved the payment details transmission feature

<a id="84-2024-09-11"></a>
## 1.8.4 (September 11, 2024) { #84-2024-09-11 }

<a id="84-2024-09-11-nhn-cloud-push"></a>
### NHN Cloud Push { #84-2024-09-11-nhn-cloud-push }

<a id="84-2024-09-11-nhn-cloud-push-improved"></a>
#### Feature Updates

* Fixed duplicate notification issue (iOS 18 Beta)
    * Improved so that duplicate notifications are not received when an application is in the foreground in iOS 18 (OS bugs).

<a id="83-2024-07-23"></a>
## 1.8.3(July 23, 2024) { #83-2024-07-23 }

<a id="83-2024-07-23-common"></a>
### Common { #83-2024-07-23-common }

<a id="83-2024-07-23-common-improved"></a>
#### Feature Updates

* Stability improvements

<a id="82-2024-06-25"></a>
## 1.8.2 (June 25, 2024) { #82-2024-06-25 }

<a id="82-2024-06-25-common"></a>
### Common { #82-2024-06-25-common }

<a id="82-2024-06-25-common-improved"></a>
#### Feature Updates

* Improved stability

<a id="81-2024-02-27"></a>
## 1.8.1 (February 27, 2024) { #81-2024-02-27 }

<a id="81-2024-02-27-common"></a>
### Common { #81-2024-02-27-common }

<a id="81-2024-02-27-common-improved"></a>
#### Feature Updates

* Applied Privacy manifest

<a id="81-2024-02-27-nhn-cloud-push"></a>
### NHN Cloud Push { #81-2024-02-27-nhn-cloud-push }

<a id="81-2024-02-27-nhn-cloud-push-improved"></a>
#### Feature Updates

* Fixed an issue where message click actions do not work immediately in certain environments

<a id="80-2024-01-23"></a>
## 1.8.0 (January 23, 2024) { #80-2024-01-23 }

<a id="80-2024-01-23-nhn-cloud-iap"></a>
### NHN Cloud IAP { #80-2024-01-23-nhn-cloud-iap }

<a id="80-2024-01-23-nhn-cloud-iap-improved"></a>
#### Feature Updates

* Improved payment verification methods
    * Improved to enable (old) receipt verification in new SDKs
        * [(New) Receipt verification + Notification V2](/Mobile%20Service/IAP/en/console-apple-guide/#new-receipt-verification-notification-v2)
        * [(Old) Receipt verification + Notification V1 (Deprecated)](/Mobile%20Service/IAP/en/console-apple-guide/#old-receipt-verification-notification-v1-soon-to-be-deprecated)

<a id="71-2023-12-19"></a>
## 1.7.1 (December 19, 2023) { #71-2023-12-19 }

<a id="71-2023-12-19-common"></a>
### Common { #71-2023-12-19-common }

<a id="71-2023-12-19-common-improved"></a>
#### Feature Updates

* Signature applied
    * Applied the `NHN Cloud Corp.` signature to the binaries being distributed.

<a id="71-2023-12-19-logger"></a>
### Logger { #71-2023-12-19-logger }

<a id="71-2023-12-19-logger-improved"></a>
#### Feature Updates

* Improved NetworkInsight stability for Instance Logger

<a id="71-2023-12-19-symboluploaderv004"></a>
### SymbolUploader(v0.0.4) { #71-2023-12-19-symboluploaderv004 }

<a id="71-2023-12-19-symboluploaderv004-improved"></a>
#### Feature Updates

* Stability improvements

<a id="70-2023-11-14"></a>
## 1.7.0 (November 14, 2023) { #70-2023-11-14 }

<a id="70-2023-11-14-common"></a>
### Common { #70-2023-11-14-common }

<a id="70-2023-11-14-common-improved"></a>
#### Feature Updates

* Raised the minimum supported version
    * 9.0 > 11.0
* Ended support for architectures
    *  i386, armv7s, armv7

<a id="70-2023-11-14-nhn-cloud-iap"></a>
### NHN Cloud IAP { #70-2023-11-14-nhn-cloud-iap }

<a id="70-2023-11-14-nhn-cloud-iap-improved"></a>
#### Feature Updates

* Changed payment verification methods - [(New) Receipt verification + Notification V2](/Mobile%20Service/IAP/en/console-apple-guide/#new-receipt-verification-notification-v2)

<a id="62-2023-08-29"></a>
## 1.6.2 (August 29, 2023) { #62-2023-08-29 }

<a id="62-2023-08-29-common"></a>
### Common { #62-2023-08-29-common }

<a id="62-2023-08-29-common-improved"></a>
#### Feature Updates

* Fixed an issue where CountryCode is not obtained

<a id="62-2023-08-29-nhn-cloud-ocr"></a>
### NHN Cloud OCR { #62-2023-08-29-nhn-cloud-ocr }

<a id="62-2023-08-29-nhn-cloud-ocr-added-features"></a>
#### Added Features

* Added recognition area data to credit card/ID card recognition results

<a id="61-2023-07-25"></a>
## 1.6.1 (July 25, 2023) { #61-2023-07-25 }

<a id="61-2023-07-25-nhn-cloud-iap"></a>
### NHN Cloud IAP { #61-2023-07-25-nhn-cloud-iap }

<a id="61-2023-07-25-nhn-cloud-iap-improved"></a>
#### Feature Updates

* Improved the feature to send payment details

<a id="60-2023-07-11"></a>
## 1.6.0 (July 11, 2023) { #60-2023-07-11 }

<a id="60-2023-07-11-nhn-cloud-ocr"></a>
### NHN Cloud OCR { #60-2023-07-11-nhn-cloud-ocr }

<a id="60-2023-07-11-nhn-cloud-ocr-added-features"></a>
#### Added Features

* Added OCR (ID Card Recognizer)

<a id="50-2023-06-27"></a>
## 1.5.0 (June 27, 2023) { #50-2023-06-27 }

<a id="50-2023-06-27-nhn-cloud-push"></a>
### NHN Cloud Push { #50-2023-06-27-nhn-cloud-push }

<a id="50-2023-06-27-nhn-cloud-push-improved"></a>
#### Feature Updates

* Improved the token registration feature
    * Provided the option to register a token regardless of the app's notification permissions.

<a id="50-2023-06-27-symboluploaderv003"></a>
### SymbolUploader(v0.0.3) { #50-2023-06-27-symboluploaderv003 }

* Stability improvements

<a id="40-2023-05-30"></a>
## 1.4.0 (May 30, 2023) { #40-2023-05-30 }

<a id="40-2023-05-30-common"></a>
### Common { #40-2023-05-30-common }

<a id="40-2023-05-30-common-improved"></a>
#### Feature Updates

* Added the SPM(swift package manager) deployment method

<a id="40-2023-05-30-nhn-cloud-iap"></a>
### NHN Cloud IAP { #40-2023-05-30-nhn-cloud-iap }

<a id="40-2023-05-30-nhn-cloud-iap-added-features"></a>
#### Added Features

* Added the feature to send payment details
    * You can view payment details from the Transaction tab in the IAP console.

<a id="40-2023-05-30-symboluploaderv002"></a>
### SymbolUploader(v0.0.2) { #40-2023-05-30-symboluploaderv002 }

* Improved run script 
    * Added support for Cocoapods and SPM

<a id="31-2023-05-19---hotfix"></a>
## 1.3.1 (May 19, 2023) - Hotfix { #31-2023-05-19---hotfix }

<a id="31-2023-05-19---hotfix-nhn-cloud-push"></a>
### NHN Cloud Push { #31-2023-05-19---hotfix-nhn-cloud-push }

<a id="31-2023-05-19---hotfix-nhn-cloud-push-improved"></a>
#### Feature Updates

* Improved the token registration feature
    * When registering a token, if the notification setting of the app is disabled, `NHNCloudPushErrorPermissionDenied` is returned again.
    
<a id="30-2023-02-28"></a>
## 1.3.0 (February 28, 2023) { #30-2023-02-28 }

<a id="30-2023-02-28-common"></a>
### Common { #30-2023-02-28-common }

<a id="30-2023-02-28-common-improved"></a>
#### Feature Updates

* Improved stability

<a id="21-2023-01-31"></a>
## 1.2.1 (January 31, 2023) { #21-2023-01-31 }

<a id="21-2023-01-31-nhn-cloud-push"></a>
### NHN Cloud Push { #21-2023-01-31-nhn-cloud-push }

<a id="21-2023-01-31-nhn-cloud-push-improved"></a>
#### Feature Updates

* Improved token registration function

<a id="21-2023-01-31-nhn-cloud-ocr"></a>
### NHN Cloud OCR { #21-2023-01-31-nhn-cloud-ocr }

<a id="21-2023-01-31-nhn-cloud-ocr-improved"></a>
#### Feature Updates

* Improved credit card recognition performance
* Improved stability

<a id="20-2022-11-29"></a>
## 1.2.0 (November 29, 2022) { #20-2022-11-29 }

<a id="20-2022-11-29-nhn-cloud-logger"></a>
### NHN Cloud Logger { #20-2022-11-29-nhn-cloud-logger }

<a id="20-2022-11-29-nhn-cloud-logger-added-features"></a>
#### Added Features

* Added support for Logger for public institutions

<a id="20-2022-11-29-nhn-cloud-push"></a>
### NHN Cloud Push { #20-2022-11-29-nhn-cloud-push }

<a id="20-2022-11-29-nhn-cloud-push-improved"></a>
#### Feature Updates

* Improved sending push events

<a id="20-2022-11-29-nhn-cloud-ocr"></a>
### NHN Cloud OCR { #20-2022-11-29-nhn-cloud-ocr }

<a id="20-2022-11-29-nhn-cloud-ocr-improved"></a>
#### Feature Updates

* Improved UI

<a id="10-2022-10-25"></a>
## 1.1.0 (October 25, 2022) { #10-2022-10-25 }

<a id="10-2022-10-25-common"></a>
### Common { #10-2022-10-25-common }

<a id="10-2022-10-25-common-improvements"></a>
#### Feature Updates

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
## 1.0.0 (July 12, 2022) { #00-2022-07-12 }

<a id="00-2022-07-12-common"></a>
### Common { #00-2022-07-12-common }

<a id="00-2022-07-12-common-improvements"></a>
#### Feature Updates

* Improved stability
* Changed the module name to NHN Cloud SDK
	* TOAST SDK has been deprecated.

<a id="300-2022-03-29"></a>
## 0.30.0 (March 29, 2022) { #300-2022-03-29 }

<a id="300-2022-03-29-toast-iap"></a>
### TOAST IAP { #300-2022-03-29-toast-iap }

<a id="300-2022-03-29-toast-iap-added-features"></a>
#### Added Features

* Added a sandbox payment flag to ToastPurchaseResult (sandboxPayment)

<a id="292-2021-11-23"></a>
## 0.29.2 (November 23, 2021) { #292-2021-11-23 }

<a id="292-2021-11-23-toast-push"></a>
### TOAST Push { #292-2021-11-23-toast-push }

<a id="292-2021-11-23-toast-push-improvements"></a>
#### Feature Updates

* Stability improvements

<a id="291-2021-10-26"></a>
## 0.29.1 (October 26, 2021) { #291-2021-10-26 }

<a id="291-2021-10-26-toast-iap"></a>
### TOAST IAP { #291-2021-10-26-toast-iap }

<a id="291-2021-10-26-toast-iap-improvements"></a>
#### Feature Updates

* Improved stability

<a id="290-2021-07-06"></a>
## 0.29.0 (July 6, 2021) { #290-2021-07-06 }

<a id="290-2021-07-06-common"></a>
### Common { #290-2021-07-06-common }

<a id="290-2021-07-06-common-improvements"></a>
#### Feature Updates

* Improved stability

<a id="290-2021-07-06-toast-iap"></a>
### TOAST IAP { #290-2021-07-06-toast-iap }

<a id="290-2021-07-06-toast-iap-added-features"></a>
#### Added Features

* Added a monthly payment limit feature

<a id="280-2021-05-25"></a>
## 0.28.0 (May 25, 2021) { #280-2021-05-25 }

<a id="280-2021-05-25-common"></a>
### Common { #280-2021-05-25-common }

<a id="280-2021-05-25-common-improvements"></a>
#### Feature Updates

* Added xcframework
    * Added support for arm Simulator

<a id="280-2021-05-25-toast-logger"></a>
### TOAST Logger { #280-2021-05-25-toast-logger }

<a id="280-2021-05-25-toast-logger-crashreporter-buildinfo-20210525"></a>
#### CrashReporter (BuildInfo 20210525)

* Improved the way to classify architectures
    * Fixed an issue where iOS14 Core Library is not symbolicated

<a id="272-2021-03-23"></a>
## 0.27.2 (March 23, 2021) { #272-2021-03-23 }

<a id="272-2021-03-23-common"></a>
### Common { #272-2021-03-23-common }

<a id="272-2021-03-23-common-improvements"></a>
#### Feature Updates

* Improved stability

<a id="272-2021-03-23-toast-logger"></a>
### TOAST Logger { #272-2021-03-23-toast-logger }

<a id="272-2021-03-23-toast-logger-symboluploader-v001"></a>
#### SymbolUploader (v0.0.1)

* Added SymbolUploader

<a id="271-2020-11-24"></a>
## 0.27.1 (November 24, 2020) { #271-2020-11-24 }

<a id="271-2020-11-24-toast-iap"></a>
### TOAST IAP { #271-2020-11-24-toast-iap }

<a id="271-2020-11-24-toast-iap-improvements"></a>
#### Feature Updates

* Subscription product resubscription error revision (iOS 14 )
- Changed ToastProductsResponse to return nil when failing to get product info from the Appstore

<a id="271-2020-11-24-toast-push"></a>
### TOAST Push { #271-2020-11-24-toast-push }

<a id="271-2020-11-24-toast-push-improvements"></a>
#### Feature Updates

* Improved problem where callback did not occur upon a token disable request and there were no registered tokens

<a id="270-2020-09-11"></a>
## 0.27.0 (September 11, 2020) { #270-2020-09-11 }

<a id="270-2020-09-11-toast-iap"></a>
### TOAST IAP { #270-2020-09-11-toast-iap }

<a id="270-2020-09-11-toast-iap-added-features"></a>
#### Added Features

* Add localized product information (localizedTitle, localizedDescription) to ToastProduct

<a id="270-2020-09-11-toast-iap-improvements"></a>
#### Feature Updates

* Handled iOS 14 beta changes
     * Fixed an issue where payment failure Delegate is not received

<a id="270-2020-09-11-toast-push"></a>
### TOAST Push { #270-2020-09-11-toast-push }

<a id="270-2020-09-11-toast-push-improvements"></a>
#### Feature Updates

* Improved stability

<a id="260-2020-07-28"></a>
## 0.26.0 (July 28, 2020) { #260-2020-07-28 }

<a id="260-2020-07-28-toast-push"></a>
### TOAST Push { #260-2020-07-28-toast-push }

<a id="260-2020-07-28-toast-push-added-features"></a>
#### Added Features

* User tag feature support

<a id="251-2020-07-03"></a>
## 0.25.1 (July 3, 2020) { #251-2020-07-03 }

<a id="251-2020-07-03-toast-logger"></a>
### TOAST Logger { #251-2020-07-03-toast-logger }

<a id="251-2020-07-03-toast-logger-improvements"></a>
#### Feature Updates

* Improved stability

<a id="251-2020-07-03-toast-push"></a>
### TOAST Push { #251-2020-07-03-toast-push }

<a id="251-2020-07-03-toast-push-improvements"></a>
#### Feature Updates

* Improved stability

<a id="250-2020-06-23"></a>
## 0.25.0 (June 23, 2020) { #250-2020-06-23 }

<a id="250-2020-06-23-common"></a>
### Common { #250-2020-06-23-common }

<a id="250-2020-06-23-common-improvements"></a>
#### Feature Updates

* Improved stability

<a id="250-2020-06-23-toast-push"></a>
### TOAST Push { #250-2020-06-23-toast-push }

<a id="250-2020-06-23-toast-push-improvements"></a>
#### Feature Updates

* Separate notification options setting interface

<a id="241-2020-05-26"></a>
## 0.24.1 (May 26, 2020) { #241-2020-05-26 }

<a id="241-2020-05-26-toast-push"></a>
### TOAST Push { #241-2020-05-26-toast-push }

<a id="241-2020-05-26-toast-push-improvements"></a>
#### Feature Updates

* Improved token registration function

<a id="240-2020-04-28"></a>
## 0.24.0 (April 28, 2020) { #240-2020-04-28 }

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
#### Feature Updates

* Improved stability

<a id="230-2020-03-24"></a>
## 0.23.0 (March 24, 2020) { #230-2020-03-24 }

<a id="230-2020-03-24-toast-logger"></a>
### TOAST Logger { #230-2020-03-24-toast-logger }

<a id="230-2020-03-24-toast-logger-improvements"></a>
#### Feature Updates

* Fixed an issue where CrashReport CallStack could contain invalid strings

<a id="230-2020-03-24-toast-push"></a>
### TOAST Push { #230-2020-03-24-toast-push }

<a id="230-2020-03-24-toast-push-added-features"></a>
#### Added Features

* Added notification option setting function
     * At initialization, it is possible to set whether to expose foreground notifications, use badge icons, and use notification sounds.

<a id="221-2020-02-25"></a>
## 0.22.1 (February 25, 2020) { #221-2020-02-25 }

<a id="221-2020-02-25-toast-push"></a>
### TOAST Push { #221-2020-02-25-toast-push }

<a id="221-2020-02-25-toast-push-improvements"></a>
#### Feature Updates

* Improved token registration function
    * If a user ID is not set at the time of initial token registration, it is registered using the device identifier.
    * If you set or change the user ID after registering the token, the token information is updated.

<a id="220-2020-02-11"></a>
## 0.22.0 (February 11, 2020) { #220-2020-02-11 }

<a id="220-2020-02-11-toast-iap"></a>
### TOAST IAP { #220-2020-02-11-toast-iap }

<a id="220-2020-02-11-toast-iap-improvements"></a>
#### Feature Updates

* Improved stability

<a id="210-2019-12-24"></a>
## 0.21.0 (December 24, 2019) { #210-2019-12-24 }

<a id="210-2019-12-24-toast-logger"></a>
### TOAST Logger { #210-2019-12-24-toast-logger }

<a id="210-2019-12-24-toast-logger-improvements"></a>
#### Feature Updates

* Added data to improve the classification method of crash occurrence location

<a id="210-2019-12-24-toast-iap"></a>
### TOAST IAP { #210-2019-12-24-toast-iap }

<a id="210-2019-12-24-toast-iap-improvements"></a>
#### Feature Updates

* Added API security function
* Improved stability
* Defined Swift interface additionally

<a id="201-2019-12-04"></a>
## 0.20.1 (December 4, 2019) { #201-2019-12-04 }

<a id="201-2019-12-04-common"></a>
### Common { #201-2019-12-04-common }

<a id="201-2019-12-04-common-improvements"></a>
#### Feature Updates

* Improved initialization logic

<a id="200-2019-11-26"></a>
## 0.20.0 (November 26, 2019) { #200-2019-11-26 }

<a id="200-2019-11-26-toast-push"></a>
### TOAST Push { #200-2019-11-26-toast-push }

<a id="200-2019-11-26-toast-push-improvements"></a>
#### Feature Updates

* Changed token registration/deletion result notification to callback structure, delete delegate
* Added a feature to re-register tokens with previously registered agreement information
* Separated the VoIP function into a submodule
* Defined Swift interface additionally

<a id="193-2019-10-29"></a>
## 0.19.3 (October 29, 2019) { #193-2019-10-29 }

<a id="193-2019-10-29-common"></a>
### Common { #193-2019-10-29-common }

<a id="193-2019-10-29-common-bug-fixes"></a>
#### Bug Fixes

* Fixed a linker error that occurs under Xcode 11

<a id="192-2019-10-25"></a>
## 0.19.2 (October 25, 2019) { #192-2019-10-25 }

<a id="192-2019-10-25-toast-push"></a>
### TOAST Push { #192-2019-10-25-toast-push }

<a id="192-2019-10-25-toast-push-improvements"></a>
#### Feature Updates

* Supports migration of (old) TCPushSDK

<a id="191-2019-10-18"></a>
## 0.19.1 (October 18, 2019) { #191-2019-10-18 }

<a id="191-2019-10-18-toast-push"></a>
### TOAST Push { #191-2019-10-18-toast-push }

<a id="191-2019-10-18-toast-push-improvements"></a>
#### Feature Updates

* Improved token registration function

<a id="190-2019-10-15"></a>
## 0.19.0 (October 15, 2019) { #190-2019-10-15 }

<a id="190-2019-10-15-toast-push"></a>
### TOAST Push { #190-2019-10-15-toast-push }

<a id="190-2019-10-15-toast-push-added-features"></a>
#### Added Features

* Added notification feature for notification execution

<a id="180-2019-10-01"></a>
## 0.18.0 (October 1, 2019) { #180-2019-10-01 }

<a id="180-2019-10-01-common"></a>
### Common { #180-2019-10-01-common }

<a id="180-2019-10-01-common-improvements"></a>
#### Feature Updates

* Handles iOS 13 / Xcode 11

<a id="180-2019-10-01-toast-iap"></a>
### TOAST IAP { #180-2019-10-01-toast-iap }

<a id="180-2019-10-01-toast-iap-added-features"></a>
#### Added Features

* Added user data setting function when requesting a purchase

<a id="180-2019-10-01-toast-iap-improvements"></a>
#### Feature Updates

* Changed to return only the restored payment after performing the restore function

<a id="180-2019-10-01-toast-push"></a>
### TOAST Push { #180-2019-10-01-toast-push }

<a id="180-2019-10-01-toast-push-improvements"></a>
#### Feature Updates

* Changed the Nullability property of the ToastPushConfiguration object
* Deleted the sourceType and extension properties of the ToastPushMedia object by improving the rich message generation logic
* Supports Korean URLs in the source information of rich messages

<a id="180-2019-10-01-toast-push-bug-fixes"></a>
#### Bug Fixes

* Fixed a bug where rich messages were not displayed properly when the message reception/checking function is disabled in the console settings
* Fixed a bug where a device token could not be acquired in environments of iOS 13 or higher

<a id="170-2019-08-27"></a>
## 0.17.0 (August 27, 2019) { #170-2019-08-27 }

<a id="170-2019-08-27-common"></a>
### Common { #170-2019-08-27-common }

<a id="170-2019-08-27-common-improvements"></a>
#### Feature Updates

* Improved stability

<a id="170-2019-08-27-toast-iap"></a>
### TOAST IAP { #170-2019-08-27-toast-iap }

<a id="170-2019-08-27-toast-iap-added-features"></a>
#### Added Features

* Added auto-renewable consumable subscription products

<a id="170-2019-08-27-toast-iap-improvements"></a>
#### Feature Updates

* Fixed a problem that a valid product list was returned to invalidProducts when querying the product list

<a id="170-2019-08-27-toast-push"></a>
### TOAST Push { #170-2019-08-27-toast-push }

<a id="170-2019-08-27-toast-push-improvements"></a>
#### Feature Updates

* Improved so that the default notification sound is set when sending push messages without setting a notification sounds

<a id="161-2019-07-29"></a>
## 0.16.1 (July 29, 2019) { #161-2019-07-29 }

<a id="161-2019-07-29-common"></a>
### Common { #161-2019-07-29-common }

<a id="161-2019-07-29-common-improvements"></a>
#### Feature Updates

* Fixed an issue where the country code cannot be obtained

<a id="160-2019-07-23"></a>
## 0.16.0 (July 23, 2019) { #160-2019-07-23 }

<a id="160-2019-07-23-toast-logger"></a>
### TOAST Logger { #160-2019-07-23-toast-logger }

<a id="160-2019-07-23-toast-logger-improvements"></a>
#### Feature Updates

* Improved to include symbol string in CrashReport CallStack for binaries with symbols
* Fixed an issue where CrashReport Reason is not displayed

<a id="160-2019-07-23-toast-iap"></a>
### TOAST IAP { #160-2019-07-23-toast-iap }

<a id="160-2019-07-23-toast-iap-improvements"></a>
#### Feature Updates

* Fixed an issue where the status changes from successful payment status to previous payment status
* Fixed an issue where payment was requested when in-app purchases were not allowed
* Improved promotional payment

<a id="160-2019-07-23-toast-push"></a>
### TOAST Push { #160-2019-07-23-toast-push }

<a id="160-2019-07-23-toast-push-improvements"></a>
#### Feature Updates

* Changed message/action receiving delegate

<a id="150-2019-06-25"></a>
## 0.15.0 (June 25, 2019) { #150-2019-06-25 }

<a id="150-2019-06-25-toast-iap"></a>
### TOAST IAP { #150-2019-06-25-toast-iap }

<a id="150-2019-06-25-toast-iap-improvements"></a>
#### Feature Updates

* Added reprocessing logic for incomplete payment when requesting query for new payment, promotion payment, or unconsumed history

<a id="150-2019-06-25-toast-push"></a>
### TOAST Push { #150-2019-06-25-toast-push }

<a id="150-2019-06-25-toast-push-added-features"></a>
#### Added Features

* Added country code and language code setting function during initialization
* Added token information update function
* Added notification option setting function

<a id="150-2019-06-25-toast-push-improvements"></a>
#### Feature Updates

* Changed the default settings of notification options
    * Changed to not display notifications while the app is running
        * For the same behavior as before, check [here](./push-ios/#_6).

<a id="141-2019-05-16"></a>
## 0.14.1 (May 16, 2019) { #141-2019-05-16 }

<a id="141-2019-05-16-toast-iap"></a>
### TOAST IAP { #141-2019-05-16-toast-iap }

<a id="141-2019-05-16-toast-iap-improvements"></a>
#### Feature Updates

* Improved an issue where the user purchases the same product as the reprocessing payment case being processed, it is processed as the product owned by the user

<a id="141-2019-05-16-toast-push"></a>
### TOAST Push { #141-2019-05-16-toast-push }

<a id="141-2019-05-16-toast-push-improvements"></a>
#### Feature Updates

* Fixed a bug in which the event occurrence time was incorrectly collected according to the device's calendar setting

<a id="140-2019-05-14"></a>
## 0.14.0 (May 14, 2019) { #140-2019-05-14 }

<a id="140-2019-05-14-common"></a>
### Common { #140-2019-05-14-common }

<a id="140-2019-05-14-common-improvements"></a>
#### Feature Updates

* Integrated network-related error codes
* Improved stability

<a id="140-2019-05-14-toast-iap"></a>
### TOAST IAP { #140-2019-05-14-toast-iap }

<a id="140-2019-05-14-toast-iap-improvements"></a>
#### Feature Updates

* Improved purchase restore function
    * Added a function to restore missing payments based on AppStore purchase history
    * Added restore failure error codes
* Added whether it is store request (promotion) or not to the payment result class
* Expanded reprocessing targets
* Improved payment flow

<a id="140-2019-05-14-toast-push"></a>
### TOAST Push { #140-2019-05-14-toast-push }

<a id="140-2019-05-14-toast-push-improvements"></a>
#### Feature Updates

* Improved stability
* Added message ID information to payload information passed to the message-receiving delegate
* In the case of VoIP where agreement to receive advertising messages or night-time advertising messages is unnecessary, messages are received regardless of the agreement for message reception.

<a id="130-2019-03-26"></a>
## 0.13.0 (March 26, 2019) { #130-2019-03-26 }

<a id="130-2019-03-26-common"></a>
### Common { #130-2019-03-26-common }

<a id="130-2019-03-26-common-improvements"></a>
#### Feature Updates

* Improved usability of Public Class
  * Add Description
  * Support Nullability, NSCoding, NSCopying

<a id="130-2019-03-26-toast-core"></a>
### TOAST Core { #130-2019-03-26-toast-core }

<a id="130-2019-03-26-toast-core-improvements"></a>
#### Feature Updates

* Added internal exception handling

<a id="130-2019-03-26-toast-logger"></a>
### TOAST Logger { #130-2019-03-26-toast-logger }

<a id="130-2019-03-26-toast-logger-added-features"></a>
#### Added Features

* Support for crash analysis of devices using arm64e architecture
* Changed PLCrashReporter Dependency

<a id="130-2019-03-26-toast-logger-improvements"></a>
#### Feature Updates

* Configuration Interface changes
  * Deprecate
    * configurationWithProjectKey
  * Add
    * configurationWithAppKey
* Fixed an issue where the UserID of logs being sent might not be updated depending on when the UserID was set

<a id="130-2019-03-26-toast-iap"></a>
### TOAST IAP { #130-2019-03-26-toast-iap }

<a id="130-2019-03-26-toast-iap-improvements"></a>
#### Feature Updates

* Added internal exception handling

<a id="130-2019-03-26-toast-push"></a>
### TOAST Push { #130-2019-03-26-toast-push }

<a id="130-2019-03-26-toast-push-added-features"></a>
#### Added Features

* Added token deletion API

<a id="124-2019-03-19"></a>
## 0.12.4 (March 19, 2019) { #124-2019-03-19 }

<a id="124-2019-03-19-toast-core"></a>
### TOAST Core { #124-2019-03-19-toast-core }

<a id="124-2019-03-19-toast-core-improvements"></a>
#### Feature Updates

* Added exception handling

<a id="123-2019-02-26"></a>
## 0.12.3 (February 26, 2019) { #123-2019-02-26 }

<a id="123-2019-02-26-toast-core-common"></a>
### TOAST Core, Common { #123-2019-02-26-toast-core-common }

<a id="123-2019-02-26-toast-core-common-improvements"></a>
#### Feature Updates

* Added exception handling for utility features

<a id="123-2019-02-26-toast-iap"></a>
### TOAST IAP { #123-2019-02-26-toast-iap }

<a id="123-2019-02-26-toast-iap-improvements"></a>
#### Feature Updates

* Added product information caching
* Added exception handling

<a id="122-2019-02-08---hotfix"></a>
## 0.12.2 (February 8, 2019) - Hotfix { #122-2019-02-08---hotfix }

<a id="122-2019-02-08---hotfix-toast-core"></a>
### TOAST Core { #122-2019-02-08---hotfix-toast-core }

<a id="122-2019-02-08---hotfix-toast-core-improvements"></a>
#### Feature Updates

* Added defense code to prevent intermittent crashes in ToastTransfer

<a id="121-2019-01-08"></a>
## 0.12.1 (January 8, 2019) { #121-2019-01-08 }

<a id="121-2019-01-08-toast-iap"></a>
### TOAST IAP { #121-2019-01-08-toast-iap }

<a id="121-2019-01-08-toast-iap-improvements"></a>
#### Feature Updates

* Fixed an issue where reprocessing of payments whose payment status is VerifyEnd did not work under certain circumstances

<a id="120-2018-12-27"></a>
## 0.12.0 (December 27, 2018) { #120-2018-12-27 }

<a id="120-2018-12-27-toast-core"></a>
### TOAST Core { #120-2018-12-27-toast-core }

<a id="120-2018-12-27-toast-core-improvements"></a>
#### Feature Updates

* Added defense code to prevent intermittent crashes in ToastTransfer

<a id="120-2018-12-27-toast-push"></a>
### TOAST Push { #120-2018-12-27-toast-push }

<a id="120-2018-12-27-toast-push-added-features"></a>
#### Added Features

* Added Push support

<a id="120-2018-12-27-toast-iap"></a>
### TOAST IAP { #120-2018-12-27-toast-iap }

<a id="120-2018-12-27-toast-iap-improvements"></a>
#### Feature Updates

* Added exception handling of UserID Check logic to enable transaction processing reprocessed by Apple
* Added defense code to prevent intermittent crashes in ToastOperation


<a id="111-2018-12-04"></a>
## 0.11.1 (December 4, 2018) { #111-2018-12-04 }

<a id="111-2018-12-04-toast-iap"></a>
### TOAST IAP { #111-2018-12-04-toast-iap }

<a id="111-2018-12-04-toast-iap-added-features"></a>
#### Added Features

* Added IAP support

<a id="110-2018-11-20"></a>
## 0.11.0 (November 20, 2018) { #110-2018-11-20 }

<a id="110-2018-11-20-toast-log-crash"></a>
### TOAST Log & Crash { #110-2018-11-20-toast-log-crash }

<a id="110-2018-11-20-toast-log-crash-added-features"></a>
#### Added Features

* Added the Network Insights feature


<a id="90-2018-09-04"></a>
## 0.9.0 (September 4, 2018) { #90-2018-09-04 }

<a id="90-2018-09-04-toast-log-crash"></a>
### TOAST Log & Crash { #90-2018-09-04-toast-log-crash }

<a id="90-2018-09-04-toast-log-crash-added-features"></a>
#### Added Features

* Added support for Log & Crash Search
