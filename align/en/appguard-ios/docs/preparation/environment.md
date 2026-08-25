<!-- pre-align:aligned sig=3c0b72517c71 -->

# Supported Environment

<a id="supported-platforms"></a>
## Supported Platforms { #supported-platforms }

<!-- TODO: translate body -->

<!-- pre-align: ko에 대응 섹션 없음 — 검토 필요 (Renders as 'Unsupported platform', which is semantically opposite to k1 '지원 플랫폼' (Supported Platforms); antonymy disqualifies it as a translation match) -->
<!-- pre-align: ko에 대응 섹션 없음 — 검토 필요 (No ko counterpart — 'Unsupported platform' does not correspond to any heading in the ko outline) -->
<a id="development-environment"></a>
## Development Environment { #development-environment }

NHN AppGuard supports the following development environments:

<a id="native-environment"></a>
### Native Environment { #native-environment }
- Objective-C
- Swift

<a id="game-engine"></a>
### Game Engine { #game-engine }
- Unity (Unity SDK)
- Unreal Engine (Unreal SDK)

<a id="cross-platform"></a>
### Cross Platform { #cross-platform }
- Flutter (Flutter SDK)
- React Native (React Native SDK)

<a id="required-framework"></a>
## Required Framework { #required-framework }

The following required framework list should be included in the project:

<a id="required-framework-list"></a>
### Required Framework List { #required-framework-list }

| Framework | Description |
|-----------|------|
| CoreTelephony.framework | Communication-related features |
| SystemConfiguration.framework | System configuration-related features |

!!! danger "Add Framework"
These frameworks are required to work NHN AppGuard normally.
    
    Add it from **Build Phases** → **Link Binary With Libraries** of the Xcode project.
