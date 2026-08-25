<!-- pre-align:aligned sig=3c0b72517c71 -->

# 지원 환경

<a id="supported-platforms"></a>
## 지원 플랫폼 { #supported-platforms }

!!! tip "플랫폼 요구사항"
    iOS 13 이상

NHN AppGuard iOS SDK는 iOS 13 이상의 버전에서 동작합니다.

<a id="development-environment"></a>
## 개발 환경 { #development-environment }

NHN AppGuard는 다음 개발 환경을 지원합니다.

<a id="native-environment"></a>
### 네이티브 개발 { #native-environment }
- Objective-C
- Swift

<a id="game-engine"></a>
### 게임 엔진 { #game-engine }
- Unity(Unity SDK)
- Unreal Engine(Unreal SDK)

<a id="cross-platform"></a>
### 크로스 플랫폼 { #cross-platform }
- Flutter(Flutter SDK)
- React Native(React Native SDK)

<a id="required-framework"></a>
## 필수 프레임워크 { #required-framework }

다음 필수 프레임워크 목록이 프로젝트에 포함되어야 합니다.

<a id="required-framework-list"></a>
### 필수 프레임워크 목록 { #required-framework-list }

| 프레임워크 | 설명 |
|-----------|------|
| CoreTelephony.framework | 통신 관련 기능 |
| SystemConfiguration.framework | 시스템 설정 관련 기능 |

!!! danger "프레임워크 추가"
    이 프레임워크들은 NHN AppGuard가 정상적으로 동작하기 위해 반드시 필요합니다.
    
    Xcode 프로젝트의 **Build Phases** → **Link Binary With Libraries**에서 추가해야 합니다.