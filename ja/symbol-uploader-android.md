<!-- machine_translated: true -->

<!-- pre-align:aligned sig=d8574ae072bf -->

<a id="nhn-cloud-sdk-user-guide-log-crash-android-symbol-uploader"></a>
## NHN Cloud > SDK使用ガイド > Log & Crash > Android (Symbol Uploader) { #nhn-cloud-sdk-user-guide-log-crash-android-symbol-uploader }

<a id="prerequisites"></a>
## 事前準備 { #prerequisites }

1. Android プロジェクトに [NHN Cloud Logger を追加](./log-collector-android/)します。
2. Android アプリにネイティブライブラリが含まれている場合は、[NHN Cloud Crash Reporter for NDK を追加](./log-collector-ndk/)します。
3. NHN Cloud コンソールで **User Access Key ID** と **Secret Access Key** を発行します。

<a id="library-setting"></a>
## ライブラリ設定 { #library-setting }

プロジェクトレベルの `build.gradle` ファイルに NHN Cloud Gradle Plugin を buildscript の依存性として追加します。

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

アプリレベルの `build.gradle` ファイルに NHN Cloud Gradle Plugin を適用します。

```groovy
// Apply the NHN Cloud Gradle Plugin
apply plugin: 'com.toast.android.toast-services'
```

<a id="configure-authentication-information"></a>
## 認証情報の設定 { #configure-authentication-information }

ファイルのアップロード要請には NHN Cloud User Access Token が必要です。
アプリレベルの Gradle ファイルで `crashReporter` の `auth` ブロックを設定します。

`userAccessKeyId` は NHN Cloud コンソールで発行した User Access Key ID、`secretAccessKey` は同時に発行した Secret Access Key を設定する項目です。
プラグインは両方の値を使用して User Access Token を自動で発行します。
各認証情報の発行方法については、[User Access Keyトークン](https://docs.nhncloud.com/ja/nhncloud/ja/public-api/user-access-key-token/)を参照してください。

認証方式は次の 2 つの中から選択できます。

| 方式 | 設定項目 | トークン有効期限切れ時の動作 |
| --- | --- | --- |
| User Access Key ID と Secret Access Key を使用（推奨） | `userAccessKeyId`、`secretAccessKey` | プラグインがトークンを新たに発行し、アップロードを継続します。 |
| トークンの直接入力 | `accessToken` | プラグインがトークンを更新できないため、新しいトークンを直接入力する必要があります。 |

<a id="use-user-access-key-id-and-secret-access-key"></a>
### User Access Key IDとSecret Access Keyの使用 { #use-user-access-key-id-and-secret-access-key }

Groovy DSLでは、次のように設定します。

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

Kotlin DSLでは、値を代入する形式で設定します。

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
### User Access Token の直接使用 { #using-a-user-access-token-directly }

既に発行済みの User Access Token を直接入力することもできます。

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

`accessToken` は `userAccessKeyId`、`secretAccessKey` と同時に設定することはできません。
直接入力したトークンが有効期限切れになると新しいトークンに変更する必要があるため、`userAccessKeyId` と `secretAccessKey` を設定する方式を推奨します。

<a id="authentication-information-rules"></a>
### 認証情報のルール { #authentication-information-rules }

認証情報には次のルールが適用されます。

| 設定状態 | 結果 |
| --- | --- |
| `userAccessKeyId` と `secretAccessKey` の両方を設定 | 正常 |
| `accessToken` のみ設定 | 正常 |
| `accessToken` を `userAccessKeyId` または `secretAccessKey` と共に設定 | エラー |
| `userAccessKeyId` と `secretAccessKey` のいずれか一方のみ設定 | エラー |
| 認証情報を設定しない | アップロードタスク実行時にエラー |

空文字列または空白のみの値は、設定されていないものとして処理されます。
認証情報なしでアップロードタスクが登録された場合、Gradle の設定フェーズで警告が出力され、該当タスクを実行するとエラーが発生します。

<a id="enable-mappingtxt-file-upload"></a>
## mapping.txt ファイルアップロード設定 { #enable-mappingtxt-file-upload }

ProGuard または R8 で難読化されたスタックトレースを解析するには、ビルド時に生成された `mapping.txt` ファイルを NHN Cloud Log & Crash Search にアップロードする必要があります。

アプリレベルの Gradle ファイルで `mappingFileUploadEnabled` を `true` に設定します。

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

`uploadMappingFile{BUILD_VARIANT}` タスクは、次の条件をすべて満たした場合に登録されます。

- `mappingFileUploadEnabled`が`true`です。
- 該当する Android build type の`minifyEnabled`が`true`です。

`mappingFileUploadEnabled` を設定したにもかかわらずアップロードタスクが表示されない場合は、Android の `buildTypes` ブロックの `minifyEnabled` 設定を確認します。

<a id="enable-native-symbol-file-upload"></a>
## Native symbol ファイルアップロード設定 { #enable-native-symbol-file-upload }

NDK の異常終了のスタック トレースを解析するには、ネイティブ バイナリのシンボル ファイルを NHN Cloud Log & Crash Search にアップロードする必要があります。

アプリレベルの Gradle ファイルで `nativeSymbolUploadEnabled` を `true` に設定します。

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

設定を有効化すると、`uploadSymbolFile{BUILD_VARIANT}` タスクが登録されます。
プラグインはデフォルトで、次のディレクトリからビルドバリアント別の `.so` ファイルを検索します。

```
{buildDir}/intermediates/merged_native_libs/{BUILD_VARIANT}/out/lib
```

別のディレクトリを使用するには、`nativeLibsDir` を設定します。

```groovy
toastServices {
    crashReporter {
        nativeSymbolUploadEnabled true
        nativeLibsDir file("src/main/jniLibs").absolutePath
    }
}
```

<a id="configure-build-variants"></a>
## ビルドバリアントごとの設定 { #configure-build-variants }

Build Type、Product Flavor、Variantに応じて、アプリキー、アップロードの有無、認証情報をそれぞれ異なる設定にできます。

設定の優先順位は次のとおりです。

```
Variant 全体名 > Product Flavor > Build Type > crashReporter 共通設定
```

Groovy DSL の例は次のとおりです。

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

Kotlin DSL では、各名前を `create` で登録します。

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

`auth`は個別項目ではなく、ブロック単位で優先順位が適用されます。
優先順位の高い設定に`auth`ブロックがある場合、下位設定の認証項目とは統合されません。

<a id="execute-the-file-upload-task"></a>
## ファイルアップロードタスク実行 { #execute-the-file-upload-task }

マッピングファイルとネイティブシンボルファイルは、ビルド時に自動的にアップロードされません。
まず対象のビルドバリアントをビルドし、次に必要なアップロードタスクを明示的に実行します。

例えば、`release` ビルドバリアントのファイルをすべてアップロードするには、次のコマンドを実行します。

```bash
./gradlew app:assembleRelease \
    app:uploadMappingFileRelease \
    app:uploadSymbolFileRelease
```
