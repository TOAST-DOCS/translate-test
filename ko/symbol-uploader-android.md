<!-- pre-align:aligned sig=d8574ae072bf -->

<a id="nhn-cloud-sdk-user-guide-log-crash-android-symbol-uploader"></a>
## NHN Cloud > SDK 사용 가이드 > Log & Crash > Android (Symbol Uploader) { #nhn-cloud-sdk-user-guide-log-crash-android-symbol-uploader }

<a id="prerequisites"></a>
## 사전 준비 { #prerequisites }

1. Android 프로젝트에 [NHN Cloud Logger를 추가](./log-collector-android/)합니다.
2. Android 앱에 네이티브 라이브러리가 포함되어 있는 경우 [NHN Cloud Crash Reporter for NDK를 추가](./log-collector-ndk/)합니다.
3. NHN Cloud 콘솔에서 **User Access Key ID**와 **Secret Access Key**를 발급받습니다.

<a id="library-setting"></a>
## 라이브러리 설정 { #library-setting }

프로젝트 수준의 `build.gradle` 파일에 NHN Cloud Gradle Plugin을 buildscript 의존성으로 추가합니다.

```groovy
buildscript {
    repositories {
        mavenCentral()
        google()
    }

    dependencies {
        // ...

        // Add the NHN Cloud Gradle Plugin
        classpath "com.toast.android:toast-gradle-plugin:0.1.0"
    }
}
```

앱 수준의 `build.gradle` 파일에 NHN Cloud Gradle Plugin을 적용합니다.

```groovy
// Apply the NHN Cloud Gradle Plugin
apply plugin: 'com.toast.android.toast-services'
```

<a id="configure-authentication-information"></a>
## 인증 정보 설정 { #configure-authentication-information }

파일 업로드 요청에는 NHN Cloud User Access Token이 필요합니다.
앱 수준의 Gradle 파일에서 `crashReporter`의 `auth` 블록을 설정합니다.

`userAccessKeyId`는 NHN Cloud 콘솔에서 발급받은 User Access Key ID, `secretAccessKey`는 함께 발급받은 Secret Access Key를 설정하는 항목입니다.
플러그인은 두 값을 사용해 User Access Token을 자동으로 발급합니다.
각 인증 정보의 발급 방법은 [User Access Key 토큰](https://docs.nhncloud.com/ko/nhncloud/ko/public-api/user-access-key-token/)을 참고하세요.

인증 방식은 다음 두 가지 중 하나를 선택할 수 있습니다.

| 방식 | 설정 항목 | 토큰 만료 시 동작 |
| --- | --- | --- |
| User Access Key ID와 Secret Access Key 사용(권장) | `userAccessKeyId`, `secretAccessKey` | 플러그인이 토큰을 새로 발급받아 업로드를 계속합니다. |
| 토큰 직접 입력 | `accessToken` | 플러그인이 토큰을 갱신할 수 없으므로 새 토큰을 직접 입력해야 합니다. |

<a id="use-user-access-key-id-and-secret-access-key"></a>
### User Access Key ID와 Secret Access Key 사용 { #use-user-access-key-id-and-secret-access-key }

Groovy DSL에서는 다음과 같이 설정합니다.

```groovy
toastServices {
    crashReporter {
        appKey "YOUR_APP_KEY"
        auth {
            userAccessKeyId "YOUR_USER_ACCESS_KEY_ID"
            secretAccessKey "YOUR_SECRET_ACCESS_KEY"
        }
    }
}
```

Kotlin DSL에서는 값을 대입하는 형식으로 설정합니다.

```kotlin
toastServices {
    crashReporter {
        appKey = "YOUR_APP_KEY"
        auth {
            userAccessKeyId = "YOUR_USER_ACCESS_KEY_ID"
            secretAccessKey = "YOUR_SECRET_ACCESS_KEY"
        }
    }
}
```

<a id="using-a-user-access-token-directly"></a>
### User Access Token 직접 사용 { #using-a-user-access-token-directly }

이미 발급받은 User Access Token을 직접 입력할 수도 있습니다.

```groovy
toastServices {
    crashReporter {
        appKey "YOUR_APP_KEY"
        auth {
            accessToken "YOUR_ACCESS_TOKEN"
        }
    }
}
```

`accessToken`은 `userAccessKeyId`, `secretAccessKey`와 함께 설정할 수 없습니다.
직접 입력한 토큰이 만료되면 새 토큰으로 변경해야 하므로 `userAccessKeyId`와 `secretAccessKey`를 설정하는 방식을 권장합니다.

<a id="authentication-information-rules"></a>
### 인증 정보 규칙 { #authentication-information-rules }

인증 정보에는 다음 규칙이 적용됩니다.

| 설정 상태 | 결과 |
| --- | --- |
| `userAccessKeyId`와 `secretAccessKey`를 모두 설정 | 정상 |
| `accessToken`만 설정 | 정상 |
| `accessToken`을 `userAccessKeyId` 또는 `secretAccessKey`와 함께 설정 | 오류 |
| `userAccessKeyId`와 `secretAccessKey` 중 하나만 설정 | 오류 |
| 인증 정보를 설정하지 않음 | 업로드 태스크 실행 시 오류 |

빈 문자열이나 공백만 있는 값은 설정하지 않은 것으로 처리됩니다.
인증 정보 없이 업로드 태스크가 등록되면 Gradle 설정 단계에서 경고가 출력되고, 해당 태스크를 실행하면 오류가 발생합니다.

<a id="enable-mappingtxt-file-upload"></a>
## mapping.txt 파일 업로드 설정 { #enable-mappingtxt-file-upload }

ProGuard 또는 R8으로 난독화된 스택 트레이스를 해석하려면 빌드 시 생성된 `mapping.txt` 파일을 NHN Cloud Log & Crash Search에 업로드해야 합니다.

앱 수준의 Gradle 파일에서 `mappingFileUploadEnabled`를 `true`로 설정합니다.

```groovy
toastServices {
    crashReporter {
        appKey "YOUR_APP_KEY"
        mappingFileUploadEnabled true
        auth {
            userAccessKeyId "YOUR_USER_ACCESS_KEY_ID"
            secretAccessKey "YOUR_SECRET_ACCESS_KEY"
        }
    }
}
```

`uploadMappingFile{BUILD_VARIANT}` 태스크는 다음 조건을 모두 만족할 때 등록됩니다.

- `mappingFileUploadEnabled`가 `true`입니다.
- 해당 Android build type의 `minifyEnabled`가 `true`입니다.

`mappingFileUploadEnabled`를 설정했는데 업로드 태스크가 표시되지 않으면 Android `buildTypes` 블록의 `minifyEnabled` 설정을 확인합니다.

<a id="enable-native-symbol-file-upload"></a>
## Native symbol 파일 업로드 설정 { #enable-native-symbol-file-upload }

NDK 비정상 종료의 스택 트레이스를 해석하려면 네이티브 바이너리의 심벌 파일을 NHN Cloud Log & Crash Search에 업로드해야 합니다.

앱 수준의 Gradle 파일에서 `nativeSymbolUploadEnabled`를 `true`로 설정합니다.

```groovy
toastServices {
    crashReporter {
        appKey "YOUR_APP_KEY"
        nativeSymbolUploadEnabled true
        auth {
            userAccessKeyId "YOUR_USER_ACCESS_KEY_ID"
            secretAccessKey "YOUR_SECRET_ACCESS_KEY"
        }
    }
}
```

설정을 활성화하면 `uploadSymbolFile{BUILD_VARIANT}` 태스크가 등록됩니다.
플러그인은 기본적으로 다음 디렉터리에서 빌드 변형별 `.so` 파일을 찾습니다.

```
{buildDir}/intermediates/merged_native_libs/{BUILD_VARIANT}/out/lib
```

다른 디렉터리를 사용하려면 `nativeLibsDir`을 설정합니다.

```groovy
toastServices {
    crashReporter {
        nativeSymbolUploadEnabled true
        nativeLibsDir file("src/main/jniLibs").absolutePath
    }
}
```

<a id="configure-build-variants"></a>
## 빌드 변형별 설정 { #configure-build-variants }

Build Type, Product Flavor, Variant에 따라 앱키와 업로드 여부, 인증 정보를 다르게 설정할 수 있습니다.

설정 우선순위는 다음과 같습니다.

```
Variant 전체 이름 > Product Flavor > Build Type > crashReporter 공통 설정
```

Groovy DSL 예시는 다음과 같습니다.

```groovy
toastServices {
    crashReporter {
        auth {
            userAccessKeyId "YOUR_USER_ACCESS_KEY_ID"
            secretAccessKey "YOUR_SECRET_ACCESS_KEY"
        }
        buildTypes {
            debug {
            }
            release {
                mappingFileUploadEnabled true
                nativeSymbolUploadEnabled false
            }
        }
        productFlavors {
            alpha {
                appKey "YOUR_ALPHA_APP_KEY"
            }
            real {
                appKey "YOUR_REAL_APP_KEY"
            }
            staging {
            }
            prod {
            }
        }
        variants {
            realProdRelease.nativeSymbolUploadEnabled = true
        }
    }
}
```

Kotlin DSL에서는 각 이름을 `create`로 등록합니다.

```kotlin
toastServices {
    crashReporter {
        auth {
            userAccessKeyId = "YOUR_USER_ACCESS_KEY_ID"
            secretAccessKey = "YOUR_SECRET_ACCESS_KEY"
        }
        buildTypes {
            create("release") {
                mappingFileUploadEnabled = true
                nativeSymbolUploadEnabled = false
            }
        }
        productFlavors {
            create("alpha") {
                appKey = "YOUR_ALPHA_APP_KEY"
            }
            create("real") {
                appKey = "YOUR_REAL_APP_KEY"
            }
        }
        variants {
            create("realProdRelease") {
                nativeSymbolUploadEnabled = true
            }
        }
    }
}
```

`auth`는 개별 항목이 아니라 블록 단위로 우선순위가 적용됩니다.
우선순위가 높은 설정에 `auth` 블록이 있으면 하위 설정의 인증 항목과 합쳐지지 않습니다.

<a id="execute-the-file-upload-task"></a>
## 파일 업로드 태스크 실행 { #execute-the-file-upload-task }

매핑 파일과 네이티브 심벌 파일은 빌드할 때 자동으로 업로드되지 않습니다.
먼저 대상 빌드 변형을 빌드한 다음 필요한 업로드 태스크를 명시적으로 실행합니다.

예를 들어 `release` 빌드 변형의 파일을 모두 업로드하려면 다음 명령을 실행합니다.

```bash
./gradlew app:assembleRelease \
    app:uploadMappingFileRelease \
    app:uploadSymbolFileRelease
```
