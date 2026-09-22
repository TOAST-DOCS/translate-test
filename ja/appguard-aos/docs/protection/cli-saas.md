<!-- pre-align:aligned sig=2030b074147a -->

# CLIでの保護作業

<a id="overview"></a>
## 概要 { #overview }

Webコンソールを経由せずに、ビルド段階で保護作業が含まれるように、ビルド自動化のためのCLI(Command Line Interface)ビルドツールを提供します。
ダウンロードしたSDKファイルのCLIフォルダに、OS別(Windows、Mac、Linux)のサポートバイナリを確認できます。

Windowsや*nix系のOSに合わせてスクリプトファイル(AppGuard.cmd、AppGuard.sh)を提供します。スクリプトファイルを参照してCLIで実行してください。-hオプションを利用して、CLI自体で各オプションの説明を確認することもできます。
NHN AppGuard CLIのオプションは次のとおりです。必須オプションを全て設定しないと、CLIは動作しません。


!!! danger "権限設定"
    Linux、macOSでCLIを使用する際、一部の権限問題が発生する可能性があるため、実行権限が追加されているかを確認する必要があります。

<a id="cli-option"></a>
## CLIオプション { #cli-option }

必須オプションを全て設定しないと、CLIは動作しません。

| オプション | 説明 | 必須 |
|------|------|-----------|
| `-v` | Webコンソールで確認できるAppKey | Y |
| `-k` | キーストアファイルのフルパス | Y |
| `-m` | キーストアのパスワード | Y |
| `-a` | キーストアのエイリアス名 | Y |
| `-p` | キーストアのエイリアスパスワード | Y |
| `-n` | 元のAPKファイルのフルパス | Y |
| `-o` | 保護されたAPKファイルのダウンロードパス | Y |
| `--business`</br>`--enterprise`</br>`--game` | 保護機能ポリシー3つのうち1つを入力</br>- Businessポリシー適用: --business</br>- Enterpriseポリシー適用: --enterprise</br>- Gameポリシー適用: --game | Y |
| `--protectionVersion` | NHN AppGuardバージョン指定 | Y |
| `--as`</br>`--no-as` | --as : Google Play、ONE storeなどのストア署名方式を使用する場合</br>アプリ署名キー(SHA-256)入力</br>(最大10個の署名値を渡せます)</br></br>--no-as : apkまたはaabに署名された情報以外の署名を許可しない場合 | Y |
| `--google-pairip` | Google Play自動整合性保護</br>(PLAY_INTEGRITY)使用時の競合防止 | N |
| `--app-attestation` | NHN AppGuardアプリ証明の有効化 | N |
| `--obfuscate` | コード難読化の有効化 | N |
| `--resource-obfuscate` | リソース文字列難読化設定ファイルパス | N |

- アプリ証明を使用するには、AppGuard SDK 0.5.0以上が必要です。

<a id="build-cli-with-gradle"></a>
## Gradleを利用したCLIビルド { #build-cli-with-gradle }

CLIをGradleを利用してビルドする際は、Gradleに入力した引数がCLIに正しく渡されているかを確認する必要があります。

<a id="invalid-example-error-occurred"></a>
### 誤った例(エラー発生) { #invalid-example-error-occurred }

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

!!! danger "問題点"
    上記のように入力すると、Gradleの`-v RtnVWuGlFy4z4z9mr`という引数が、CLIでは`-v`と`RtnVWuGlFy4z4z9mr`に変わってしまいます。
    オプション値にスペースが追加され、文字列の両側が'(シングルクォーテーション)で囲まれるため、CLIでエラーが発生します。

<a id="valid-example"></a>
### 正しい例 { #valid-example }

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

!!! tip "解決方法"
    スペースと'(シングルクォーテーション)を削除し、オプションと値を続けて記述します。

---

