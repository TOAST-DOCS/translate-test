<!-- pre-align:aligned sig=a88c32c1d251 -->

# CLI를 이용한 보호 작업

<a id="overview"></a>
## 개요 { #overview }

웹 콘솔을 거치지 않고 빌드 단계에 보호 작업이 포함될 수 있도록 빌드 자동화를 위한 CLI(command line interface) 도구를 제공합니다.

SDK 패키지의 CLI 폴더에 OS별(Windows, Mac, Linux) `appguard-cli` 바이너리가 포함되어 있습니다. `-h` 옵션을 이용해 각 옵션의 설명을 확인할 수 있습니다.

```bash
appguard-cli -h                    # 전체 도움말 확인
appguard-cli android -h            # Android 관련 상세 옵션 확인
```

<a id="command-structure"></a>
## 명령어 구조 { #command-structure }

```
appguard-cli <platform> [options]
```

| 플랫폼 | 설명 |
|--------|------|
| `android` | Android 앱 보호(APK/AAB) |
| `protector` | Protector 이미지 관리(On-Premise 전용) |
| `update` | CLI 업데이트 관리 |

<a id="android-app-protection-options"></a>
## Android 앱 보호 옵션 { #android-app-protection-options }

<a id="required-options"></a>
### 필수 옵션 { #required-options }

| 옵션 | 설명 |
|------|------|
| `-i, --input` | 입력 파일 경로(APK 또는 AAB) |
| `-o, --output` | 출력 디렉터리 또는 파일 경로 |
| `--appkey` | NHN AppGuard AppKey |
| `--plan` | 플랜(`business` / `enterprise` / `game`) |
| `--protector-version` | Protector 버전 |
| `--endpoint` | API Endpoint URL |

<a id="optional-options"></a>
### 선택 옵션 { #optional-options }

| 옵션 | 설명 | 기본값 |
|------|------|--------|
| `--app-attestation` | 앱 증명 활성화(앱 증명 사용 시 필수) | 생략 시 비활성 |
| `--additional-sign` | 추가 서명 해시(SHA256 해시 1~10개) | `none` |
| `--config` | 통합 설정 파일 경로 | 생략 시 비활성 |
| `--dry-run` | 실제 실행 없이 파라미터 확인 | 생략 시 비활성 |

- 통합 설정 파일(`--config`)을 사용하려면 CLI 1.0.3 이상, Protector 1.14.0.0 이상이 필요합니다. 자세한 내용은 [3. 통합 설정 파일](../configuration/overview.md)을 참고하세요.

<a id="security-options"></a>
### 보안 옵션 { #security-options }

| 옵션 | 설명 | 기본값 |
|------|------|--------|
| `--dex-obfuscate` | DEX 난독화(enterprise/game만) | 생략 시 비활성 |
| `--resource-obfuscate` | 리소스 문자열 난독화 설정 파일 경로(통합 설정 파일로 대체, 향후 지원 종료 예정) | 생략 시 비활성 |
| `--google-pairip` | Google PairIP | 생략 시 비활성 |

- `--resource-obfuscate`로 전달하던 리소스 문자열 난독화 설정은 통합 설정 파일의 `resourceStringObfuscation` 설정으로 통합되었습니다. Protector 1.14.0.0 이상에서는 `--config` 옵션 사용을 권장하며, `--resource-obfuscate`는 향후 지원을 종료할 예정입니다. 두 옵션을 함께 지정하면 `--config`로 전달한 통합 설정 파일을 사용합니다.

<a id="other-options"></a>
### 기타 옵션 { #other-options }

| 옵션 | 설명 | 기본값 |
|------|------|--------|
| `--show-startup-message` | 시작 메시지 표시 | 생략 시 비활성 |
| `--detection-popup-mode` | 탐지 팝업 모드(`detail` / `simple`) | `detail` |
| `--intune` | MS Intune 지원 | 생략 시 비활성 |

<!-- 
<a id="signing-options"></a>
### 서명 옵션 { #signing-options }

| 옵션 | 설명 |
|------|------|
| `--keystore` | Keystore 파일 경로 |
| `--keystore-key-alias` | Keystore Key alias |
| `--keystore-password` | Keystore 패스워드 |
| `--key-password` | Key alias 패스워드 |

서명 옵션을 생략하면 보호 작업 후 별도로 서명해야 합니다. [보호 작업 후 서명](#sign-after-protection)을 참고하세요.
-->

<a id="framework-options"></a>
### 프레임워크 옵션 { #framework-options }

| 옵션 | 설명 | 기본값 |
|------|------|--------|
| `--flutter` | Flutter 보호 | 생략 시 비활성 |
| `--flutter-app-library-name` | Flutter App 라이브러리명 | `libapp.so` |
| `--flutter-engine-library-name` | Flutter Engine 라이브러리명 | `libflutter.so` |
| `--react-native` | React Native 보호 | 생략 시 비활성 |
| `--jsbundle` | JS Bundle 파일명 | `index.android.bundle` |

<a id="store-options"></a>
### 스토어 옵션 { #store-options }

| 옵션 | 설명 | 기본값 |
|------|------|--------|
| `--ext-store` | 외부 스토어 | 생략 시 비활성 |
| `--amazon` | Amazon 스토어 | 생략 시 비활성 |
| `--huawei` | Huawei 스토어 | 생략 시 비활성 |

<a id="usage-examples"></a>
## 사용 예시 { #usage-examples }

<a id="basic-protection"></a>
### 기본 보호 { #basic-protection }

```bash
appguard-cli android \
  -i app.apk \
  -o ./output \
  --appkey YOUR_APP_KEY \
  --plan business \
  --protector-version 1.0.0 \
  --endpoint https://your-server.com
```

<a id="app-attestation-obfuscation"></a>
### 앱 증명 + 난독화 { #app-attestation-obfuscation }

```bash
appguard-cli android \
  -i app.apk \
  -o ./output \
  --appkey YOUR_APP_KEY \
  --plan enterprise \
  --protector-version 1.0.0 \
  --endpoint https://your-server.com \
  --dex-obfuscate \
  --app-attestation
```

<a id="specifying-the-output-path"></a>
### 출력 경로 지정 { #specifying-the-output-path }

출력 디렉터리만 지정하면 기본 파일명이 생성됩니다.

```bash
appguard-cli android -i app.apk -o ./output ...
# 결과: ./output/app_protected.apk
```

출력 파일명을 직접 지정할 수도 있습니다.

```bash
appguard-cli android -i app.apk -o ./output/my_protected_app.apk ...
# 결과: ./output/my_protected_app.apk
```

!!! warning "확장자 일치"
    입력 파일과 출력 파일의 확장자가 일치해야 합니다. (APK 입력 → APK 출력, AAB 입력 → AAB 출력)

<a id="dry-run-mode"></a>
### Dry-Run 모드 { #dry-run-mode }

`--dry-run` 옵션을 사용하면 실제 보호 작업 없이 파라미터만 확인할 수 있습니다.

```bash
appguard-cli android \
  -i app.apk \
  -o ./output \
  --appkey YOUR_APP_KEY \
  --plan business \
  --protector-version 1.0.0 \
  --dry-run
```

<a id="protector-management"></a>
## Protector 관리 { #protector-management }

On-Premise 환경에서는 보호 엔진(Protector) 이미지를 직접 관리합니다.

<a id="automatic-protector-pull"></a>
### 자동 Protector Pull { #automatic-protector-pull }

앱 보호 시 `--protector-version`을 지정하면 CLI가 자동으로 Protector 이미지를 관리합니다.

1. 서버에 해당 버전 존재 여부 확인
2. 없으면 NCR에서 자동 Pull
3. Pull 성공 후 보호 작업 진행

일반적으로 별도 관리가 필요 없습니다.

<a id="manual-protector-management"></a>
### 수동 Protector 관리 { #manual-protector-management }

수동으로 관리하려면 다음 명령어를 사용합니다.

```bash
# 버전 조회
appguard-cli protector --endpoint https://your-server.com --android --version

# 이미지 Pull
appguard-cli protector --endpoint https://your-server.com --android --pull 1.0.0
```

<a id="sign-after-protection"></a>
## 보호 작업 후 서명 { #sign-after-protection }

보호된 APK/AAB 파일은 서명되어 있지 않은 상태이기 때문에, 원본 앱 서명에 사용한 것과 동일한 Keystore로 반드시 재서명해야 합니다.

<a id="apk-signing"></a>
### APK 서명 { #apk-signing }

```bash
apksigner sign --ks <keystore 파일 경로> \
  --ks-pass pass:<keystore 비밀번호> \
  --ks-key-alias <key alias> \
  --key-pass pass:<key 비밀번호> \
  --out <서명된 APK 경로> \
  <보호된 APK 경로>

# 서명 확인
apksigner verify <서명된 APK 경로>
```

<a id="aab-signing"></a>
### AAB 서명 { #aab-signing }

```bash
jarsigner -verbose -sigalg SHA256withRSA -digestalg SHA-256 \
  -keystore <keystore 파일 경로> \
  -storepass <keystore 비밀번호> \
  -keypass <key 비밀번호> \
  <보호된 AAB 경로> \
  <key alias>

# 서명 확인
jarsigner -verify -verbose -certs <서명된 AAB 경로>
```

`apksigner`와 `jarsigner`는 Android SDK Build Tools에 포함되어 있습니다. Google Play App Signing을 사용하는 경우, 업로드 키로 서명해야 합니다.

<a id="cli-update"></a>
## CLI 업데이트 { #cli-update }

```bash
appguard-cli --version                        # 현재 CLI 버전 확인
appguard-cli update --list                    # 사용 가능한 CLI 버전 목록 조회
appguard-cli update --install VERSION         # 특정 버전으로 업데이트
appguard-cli update --auto-update             # 자동 업데이트 설정 확인
appguard-cli update --auto-update enable      # 자동 업데이트 활성화
appguard-cli update --auto-update disable     # 자동 업데이트 비활성화 (Default)
```

| 명령어 | 설명 | 예시 |
|--------|------|------|
| `--version` | 현재 설치된 CLI 버전 확인 | `appguard-cli --version` |
| `--list` | 배포 서버에서 사용 가능한 CLI 버전 목록 조회 및 표시 | `appguard-cli update --list` |
| `--install VERSION` | 지정된 버전으로 CLI 업데이트(예: `0.2.0`) | `appguard-cli update --install 0.2.0` |
| `--auto-update` | 현재 자동 업데이트 설정 상태 조회 | `appguard-cli update --auto-update` |
| `--auto-update enable` | 자동 업데이트 활성화(CLI 실행 시 자동 확인 및 업데이트) | `appguard-cli update --auto-update enable` |
| `--auto-update disable` | 자동 업데이트 비활성화(수동 업데이트만 가능) | `appguard-cli update --auto-update disable` |

- 자동 업데이트가 활성화되어 있다면 CLI 실행 시 업데이트가 우선 진행됩니다.
- 업데이트 실패, 배포 서버 접근 불가, 네트워크 타임아웃 시에는 무시하고 기존 버전으로 원래 작업을 계속합니다.

<a id="important-notes"></a>
## 주의사항 { #important-notes }

1. **Flutter와 React Native는 동시 사용 불가**
    ```
    Error: --flutter and --react-native cannot be used together.
    ```
2. **입력 파일 확장자는 플랫폼과 일치 필요**
    ```
    Android: .apk 또는 .aab
    ```
3. **출력 파일 경로 지정 시 입력 파일과 확장자 일치 필요**
    ```
    APK 입력 → APK 출력, AAB 입력 → AAB 출력
    ```

---
