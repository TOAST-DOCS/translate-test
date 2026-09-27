<!-- pre-align:aligned sig=82c2a3411707 -->

<a id="nhn-cloud-sdk-user-guide-overview"></a>
## NHN Cloud > SDK User Guide > Overview { #nhn-cloud-sdk-user-guide-overview }

NHN Cloud SDK is an integrated library that lets you conveniently apply various service libraries of [NHN Cloud](https://nhncloud.com/). When you use NHN Cloud services to develop an application, you can apply them all at once without applying each library of individual services.
Although the SDK provides an integrated development environment for many services, you can save storage space by selecting only the required features. NHN Cloud SDK is a library optimized for each programming language and platform of your choice, and provides familiar development environment.

> Currently, NHN Cloud SDK provides development environment for iOS, Android, and Windows C++. More programming languages and platforms are to be supported in the future.

<a id="supported-services"></a>
## Supported Services { #supported-services }

NHN Cloud SDK provides the following services:

- [Log & Crash Search](https://www.nhncloud.com/service/data-analytics/log-crash-search)
- [IAP](https://www.nhncloud.com/service/mobile-service/iap)
- [Push](https://www.nhncloud.com/service/notification/push)
- [OCR](https://www.nhncloud.com/service/ai-service/ocr)

> Services providing individual SDK are to be supported for development via NHN Cloud SDK.

<a id="features"></a>
## Features { #features }

- Supports build environment that uses Gradle for Android and CocoaPods for iOS.
- Lets you select and apply the whole or part of the services, depending on the needs.
- Improved the inconvenience of SDK that was separately provided by individual services.

<a id="getting-started-with-nhn-cloud-sdk"></a>
## Getting Started with NHN Cloud SDK { #getting-started-with-nhn-cloud-sdk }

<a id="android"></a>
### Android { #android }

NHN Cloud Android SDK is deployed on **mavenCentral** and requires only simple Gradle settings for use.

- [Get started for Android](./getting-started-android)

<a id="ios"></a>
### iOS { #ios }

NHN Cloud iOS SDK is released on **Github** and requires only simple **Cocoapods**, **Carthage**, **Swift Package Manager** settings for use.

- [Get started for iOS](./getting-started-ios)

<a id="windows-c"></a>
### Windows C++ { #windows-c }

NHN Cloud Windows C++ SDK supports Windows 7, 10 (32/64 bits) and 11 (64bits) environments.

- [Get started for Windows C++](./getting-started-windows)

<a id="log-crash"></a>
## Log & Crash { #log-crash }

This service provides capability to send logs to a collector server of Log & Crash Search. You can check the collected logs by clicking the **Log & Crash Search** menu on NHN Cloud console.

- [Find out Log & Crash Search Service](https://nhncloud.com/service/data-analytics/log-crash-search)

<a id="main-features"></a>
### Main Features { #main-features }

| Feature      | Description                                       |
| ------- | ---------------------------------------- |
| Sending Logs   | Sends logs to a collector server.                        |
| View and Search | Provides features to view logs or search for logs that meet criteria in NHN Cloud Console. |
| Crash Reports | When an unexpected crash occurs, sends the crash logs to a collector server of Log & Crash Search. |

<a id="user-guides"></a>
### User Guides { #user-guides }

- User Guide for [Log & Crash > Android](./log-collector-android)
- User Guide for [Log & Crash > iOS](./log-collector-ios)
- User Guide for [Log & Crash > Windows C++](./log-collector-windows)

<a id="nhn-cloud-iap"></a>
## NHN Cloud IAP { #nhn-cloud-iap }

This service provides integrated mobile in-app payment (IAP) service.

- [Find out IAP Service](https://www.nhncloud.com/service/mobile-service/iap)

<a id="nhn-cloud-iap-main-features"></a>
### Main Features { #nhn-cloud-iap-main-features }

| Feature | Description |
| -- | -- |
| General Payment | Provides features to sell one-time products. |
| Subscription Payment | Provides features to sell subscription products. |
| Re-processing | Provides features to restore incompletely-terminated purchase process. |

<a id="nhn-cloud-iap-user-guides"></a>
### User Guides { #nhn-cloud-iap-user-guides }

- User Guide for [IAP > Android](./iap-android)
- User Guide for [IAP > iOS](./iap-ios)

<a id="nhn-cloud-push"></a>
## NHN Cloud Push { #nhn-cloud-push }

NHN Cloud Push SDK allows you to apply push notification service easily.
On console, you can send the notification message in a stable manner and check the result.

<a id="nhn-cloud-push-user-guides"></a>
### User Guides { #nhn-cloud-push-user-guides }

- User Guide for [Push > Android](./push-android)
- User Guide for [Push > iOS](./push-ios)
