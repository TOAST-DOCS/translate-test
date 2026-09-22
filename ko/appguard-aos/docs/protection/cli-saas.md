<!-- pre-align:aligned sig=2030b074147a -->

# CLI를 통한 보호 작업

<a id="overview"></a>
## 개요 { #overview }

웹 콘솔을 거치지 않고 빌드 단계에 보호 작업이 포함될 수 있도록 빌드 자동화를 위한 CLI(command line interface) 빌드 툴을 제공합니다.
다운로드한 SDK 파일의 CLI 폴더에 OS별(Windows, Mac, Linux) 지원 바이너리를 확인할 수 있습니다.

Windows나 *nix 계열 운영체제에 맞게 스크립트 파일(AppGuard.cmd, AppGuard.sh)을 제공합니다. 스크립트 파일을 참고해 CLI에서 실행하면 됩니다. -h 옵션을 이용해 CLI 자체에서 각 옵션의 설명을 확인할 수도 있습니다.
NHN AppGuard CLI의 옵션은 아래와 같습니다. 필수 옵션을 모두 설정해야 CLI가 동작합니다.


!!! danger "권한 설정"
    Linux, macOS에서 CLI 사용 시 일부 권한 문제가 있을 수 있어 실행 권한이 추가되었는지 확인해야 합니다.

<a id="cli-option"></a>
## CLI 옵션 { #cli-option }

필수 옵션을 모두 설정해야 CLI가 동작합니다.

| 옵션 | 설명 | 필수 여부 |
|------|------|-----------|
| `-v` | 웹 콘솔에서 확인할 수 있는 Appkey | Y |
| `-k` | 키스토어 파일의 전체 경로 | Y |
| `-m` | 키스토어 비밀번호 | Y |
| `-a` | 키스토어 앨리어스명 | Y |
| `-p` | 키스토어 앨리어스 비밀번호 | Y |
| `-n` | 원본 APK 파일의 전체 경로 | Y |
| `-o` | 보호된 APK 파일의 다운로드 경로 | Y |
| `--business`</br>`--enterprise`</br>`--game` | 보호 기능 정책 세 가지 중 하나를 입력</br>- Business 정책 적용: --business</br>- Enterprise 정책 적용: --enterprise</br>- Game 정책 적용: --game | Y |
| `--protectionVersion` | NHN AppGuard 버전 지정 | Y |
| `--as`</br>`--no-as` | --as : Google Play, 원스토어 등의 스토어 서명 방식을 사용하는 경우</br> 앱 서명 키(SHA-256) 입력 </br>(최대 10개의 서명 값 전달 가능)</br></br>--no-as : apk 또는 aab에 서명된 정보 외의 서명을 허용하지 않을 경우 | Y |
| `--google-pairip` | Google Play 자동 무결성 보호</br>(PLAY_INTEGRITY) 사용 시 충돌 방지 | N |
| `--app-attestation` | NHN AppGuard 앱 증명 활성화 | N |
| `--obfuscate` | 코드 난독화 활성화 | N |
| `--resource-obfuscate` | 리소스 문자열 난독화 설정 파일 경로</br>(통합 설정 파일로 대체, 향후 지원 종료 예정) | N |
| `--config` | 통합 설정 파일 경로 | N |

- 앱 증명을 사용하려면 AppGuard SDK 0.5.0 이상이 필요합니다.
- 통합 설정 파일(`--config`)을 사용하려면 NHN AppGuard 1.14.0.0 이상이 필요합니다. 자세한 내용은 [3. 통합 설정 파일](../configuration/overview.md)을 참고하세요.
- `--resource-obfuscate`로 전달하던 리소스 문자열 난독화 설정은 통합 설정 파일의 `resourceStringObfuscation` 설정으로 통합되었습니다. NHN AppGuard 1.14.0.0 이상에서는 `--config` 옵션 사용을 권장하며, `--resource-obfuscate`는 향후 지원을 종료할 예정입니다. 두 옵션을 함께 지정하면 `--config`로 전달한 통합 설정 파일을 사용합니다.

<a id="build-cli-with-gradle"></a>
## Gradle을 이용한 CLI 빌드 { #build-cli-with-gradle }

CLI를 Gradle을 이용해 빌드할 때는 Gradle에 입력한 인자들이 CLI로 잘 전달되는지 확인해야 합니다.

<a id="invalid-example-error-occurred"></a>
### 잘못된 예시(오류 발생) { #invalid-example-error-occurred }

```gradle
def apkDir = "$rootProject.rootDir/apkpath"
def apkFullName = 'test_app.apk'
def apkName = apkFullName.substring(0, apkFullName.lastIndexOf('.'))
def protectedApkFullName = apkFullName.replace(apkName, apkName + '-appGuard')
def keyStore = "$rootProject.rootDir/keystore/appguard.keystore"
def appguardArgs = [
    "-n '$apkDir$apkFullName'",
    "-o '$apkDir$protectedApkFullName'",
    "-k '$keyStore'",
    "-m ${System.getenv('APPGUARD_KEY_STORE_PASSWORD')}",
    "-a ${System.getenv('APPGUARD_KEY_STORE_ALLIAS')}",
    "-p ${System.getenv('APPGUARD_KEY_STORE_ALLIAS_PASSWORD')}",
    "-v RtnVWuGlFy4z4z9mr",
    "--game"
]
```

!!! danger "문제점"
    위와 같이 입력하면 Gradle의 `-v RtnVWuGlFy4z4z9mr` 인자가 CLI에는 `-v`와 `RtnVWuGlFy4z4z9mr`로 바뀝니다. 
    옵션 값에 공백이 추가되고 문자열 양쪽이 '(작은따옴표)로 감싸져 CLI에서 오류가 발생합니다.

<a id="valid-example"></a>
### 올바른 예시 { #valid-example }

```gradle
def apkDir = "$rootProject.rootDir/apkpath"
def apkFullName = 'test_app.apk'
def apkName = apkFullName.substring(0, apkFullName.lastIndexOf('.'))
def protectedApkFullName = apkFullName.replace(apkName, apkName + '-appGuard')
def keyStore = "$rootProject.rootDir/keystore/appguard.keystore"
def appguardArgs = [
    "-n$apkDir$apkFullName",
    "-o$apkDir$protectedApkFullName",
    "-k$keyStore",
    "-m${System.getenv('APPGUARD_KEY_STORE_PASSWORD')}",
    "-a${System.getenv('APPGUARD_KEY_STORE_ALLIAS')}",
    "-p${System.getenv('APPGUARD_KEY_STORE_ALLIAS_PASSWORD')}",
    "-vRtnVWuGlFy4z4z9mr",
    "--game"
]
```

!!! tip "해결 방법"
    공백과 '(작은따옴표)를 제거하여 옵션과 값을 붙여서 작성합니다.

---
