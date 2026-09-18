<!-- machine_translated: true -->

<!-- pre-align:aligned sig=d8574ae072bf -->

<a id="nhn-cloud-sdk-user-guide-log-crash-android-symbol-uploader"></a>
## NHN Cloud > SDK User Guide > Log & Crash > Android (Symbol Uploader) { #nhn-cloud-sdk-user-guide-log-crash-android-symbol-uploader }

<a id="prerequisites"></a>
## Prerequisites { #prerequisites }

1. [Add NHN Cloud Logger to your Android project](/nhncloud/en/nhncloud-sdk/log-collector-android/).
2. If your Android app contains native libraries, [add NHN Cloud Crash Reporter for NDK](/nhncloud/en/nhncloud-sdk/log-collector-ndk/).
3. In the NHN Cloud Console, issue a **User Access Key ID** and **Secret Access Key**.

<a id="library-setting"></a>
## Library Setting { #library-setting }

Add the NHN Cloud Gradle Plugin as a buildscript dependency to your project-level `build.gradle` file.

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

Apply the NHN Cloud Gradle Plugin to your app-level `build.gradle` file.

```groovy
// Apply the TOAST Gradle Plugin
apply plugin: 'com.toast.android.toast-services'
```

<a id="configure-authentication-information"></a>
## Configure Authentication Information { #configure-authentication-information }

File upload requests require an NHN Cloud User Access Token.
Configure the `auth` block of `crashReporter` in your app-level Gradle file.

`userAccessKeyId` is the User Access Key ID issued from the NHN Cloud Console, and `secretAccessKey` is the Secret Access Key issued along with it.
The plugin uses these two values to automatically issue a User Access Token.
For information on how to issue each set of authentication information, see [User Access Key Token](https://docs.nhncloud.com/en/nhncloud/en/public-api/user-access-key-token/).

You can choose one of the following two authentication methods:

| Method | Setting | Behavior when token expires |
| --- | --- | --- |
| Use User Access Key ID and Secret Access Key (recommended) | `userAccessKeyId`, `secretAccessKey` | The plugin issues a new token and continues the upload. |
| Enter token directly | `accessToken` | The plugin cannot renew the token, so you must manually enter a new token. |

<a id="use-user-access-key-id-and-secret-access-key"></a>
### Use User Access Key ID and Secret Access Key { #use-user-access-key-id-and-secret-access-key }

In Groovy DSL, configure the settings as follows.

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

In Kotlin DSL, configure the settings by assigning values.

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
### Using a User Access Token Directly { #using-a-user-access-token-directly }

You can also directly enter a User Access Token that you have already been issued.

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

`accessToken` cannot be configured together with `userAccessKeyId` and `secretAccessKey`.
Because you must replace an expired directly entered token with a new one, we recommend configuring `userAccessKeyId` and `secretAccessKey` instead.

<a id="authentication-information-rules"></a>
### Authentication Information Rules { #authentication-information-rules }

The following rules apply to authentication information.

| Setting State | Result |
| --- | --- |
| Both `userAccessKeyId` and `secretAccessKey` are set | Normal |
| Only `accessToken` is set | Normal |
| `accessToken` is set together with `userAccessKeyId` or `secretAccessKey` | Error |
| Only one of `userAccessKeyId` or `secretAccessKey` is set | Error |
| Authentication information is not set | Error when the upload task runs |

Values that are empty strings or contain only whitespace are treated as not set.
If an upload task is registered without authentication information, a warning is displayed during the Gradle configuration phase, and an error occurs when that task is run.

<a id="enable-mappingtxt-file-upload"></a>
## mapping.txt File Upload Settings { #enable-mappingtxt-file-upload }

To interpret obfuscated stack traces from ProGuard or R8, you must upload the `mapping.txt` file generated during the build to NHN Cloud Log & Crash Search.

Set `mappingFileUploadEnabled` to `true` in your app-level Gradle file.

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

`uploadMappingFile{BUILD_VARIANT}` task is registered when all of the following conditions are met.

- `mappingFileUploadEnabled` is `true`.
- `minifyEnabled` for the Android build type is `true`.

If you set `mappingFileUploadEnabled` but the upload task is not displayed, check the `minifyEnabled` setting in the Android `buildTypes` block.

<a id="enable-native-symbol-file-upload"></a>
## Native Symbol File Upload Settings { #enable-native-symbol-file-upload }

To interpret stack traces from NDK crashes, you must upload the symbol files of native binaries to NHN Cloud Log & Crash Search.

Set `nativeSymbolUploadEnabled` to `true` in your app-level Gradle file.

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

When you enable the setting, the `uploadSymbolFile{BUILD_VARIANT}` task is registered.
By default, the plugin looks for `.so` files per build variant in the following directories:

```
{buildDir}/intermediates/merged_native_libs/{BUILD_VARIANT}/out/lib
```

To use a different directory, set `nativeLibsDir`.

```groovy
toastServices {
    crashReporter {
        nativeSymbolUploadEnabled true
        nativeLibsDir file("src/main/jniLibs").absolutePath
    }
}
```

<a id="configure-build-variants"></a>
## Configure Build Variants { #configure-build-variants }

Depending on the Build Type, Product Flavor, and Variant, you can configure the AppKey, upload settings, and authentication information differently.

The setting priority is as follows.

```
Variant Full Name > Product Flavor > Build Type > crashReporter Common Settings
```

Groovy DSL examples are as follows.

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

In Kotlin DSL, register each name with `create`.

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

`auth` priority is applied at the block level, not to individual items.
If a higher-priority setting has an `auth` block, it is not merged with the authentication items of lower-priority settings.

<a id="execute-the-file-upload-task"></a>
## Execute the File Upload Task { #execute-the-file-upload-task }

Mapping files and native symbol files are not automatically uploaded during a build.
First, build the target build variant, and then explicitly run the required upload task.

For example, to upload all files for the `release` build variant, run the following command.

```bash
./gradlew app:assembleRelease \
    app:uploadMappingFileRelease \
    app:uploadSymbolFileRelease
```
