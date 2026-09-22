<!-- machine_translated: true -->

<!-- pre-align:aligned sig=a88c32c1d251 -->

# CLIを利用した保護作業

<a id="overview"></a>
## 概要 { #overview }

Webコンソールを経由せず、ビルド段階に保護作業を組み込めるよう、ビルド自動化のためのCLI(Command Line Interface)ツールを提供します。

SDKパッケージのCLIフォルダにOS別(Windows、Mac、Linux)の`appguard-cli`バイナリが含まれています。`-h`オプションを使用して、各オプションの説明を確認できます。

```bash
appguard-cli -h                    # 全てのヘルプを確認
appguard-cli android -h            # Android関連の詳細オプションを確認
```

<a id="command-structure"></a>
## コマンド構造 { #command-structure }

```
appguard-cli <platform> [options]
```

| プラットフォーム | 説明 |
|--------|------|
| `android` | Androidアプリ保護 (APK/AAB) |
| `protector` | Protectorイメージ管理 (オンプレミス専用) |
| `update` | CLIアップデート管理 |

<a id="android-app-protection-options"></a>
## Androidアプリ保護オプション { #android-app-protection-options }

<a id="required-options"></a>
### 必須オプション { #required-options }

| オプション | 説明 |
|------|------|
| `-i, --input` | 入力ファイルパス (APKまたはAAB) |
| `-o, --output` | 出力ディレクトリまたはファイルパス |
| `--appkey` | AppGuard AppKey |
| `--plan` | プラン (`business` / `enterprise` / `game`) |
| `--protector-version` | Protectorバージョン |
| `--endpoint` | API Endpoint URL |

<a id="optional-options"></a>
### 任意オプション { #optional-options }

| オプション | 説明 | デフォルト値 |
|------|------|--------|
| `--app-attestation` | アプリ証明の有効化 **(アプリ証明使用時は必須)** | 省略時は無効 |
| `--additional-sign` | 追加署名ハッシュ (SHA256ハッシュ1～10個) | `none` |
| `--config` | 統合設定ファイルのパス | 省略時は無効 |
| `--dry-run` | 実際の実行なしでパラメータを確認 | 省略時は無効 |

- 統合設定ファイル (`--config`) を使用するには、CLI 1.0.3 以上、Protector 1.14.0.0 以上が必要です。詳細については、[3. 統合設定ファイル](../configuration/overview.md)を参照してください。

<a id="security-options"></a>
### セキュリティオプション { #security-options }

| オプション | 説明 | デフォルト値 |
|------|------|--------|
| `--dex-obfuscate` | DEX難読化 (enterprise/gameのみ) | 省略時は無効 |
| `--resource-obfuscate` | リソース文字列難読化設定ファイルパス（統合設定ファイルへ移行、今後サポート終了予定） | 省略時は無効 |
| `--google-pairip` | Google PairIP | 省略時は無効 |

- `--resource-obfuscate` で指定していたリソース文字列の難読化設定は、統合設定ファイルの `resourceStringObfuscation` 設定に統合されました。Protector 1.14.0.0 以降では `--config` オプションの使用をお勧めします。`--resource-obfuscate` は今後サポート終了予定です。両方のオプションを同時に指定した場合は、`--config` で指定した統合設定ファイルが使用されます。

<a id="other-options"></a>
### その他のオプション { #other-options }

| オプション | 説明 | デフォルト値 |
|------|------|--------|
| `--show-startup-message` | 起動メッセージを表示 | 省略時は無効 |
| `--detection-popup-mode` | 検知ポップアップモード (`detail` / `simple`) | `detail` |
| `--intune` | MS Intuneサポート | 省略時は無効 |

<!-- 
<a id="signing-options"></a>
### 署名オプション { #signing-options }

| オプション | 説明 |
|------|------|
| `--keystore` | Keystoreファイルパス |
| `--keystore-key-alias` | Keystore Key alias |
| `--keystore-password` | Keystoreパスワード |
| `--key-password` | Key aliasパスワード |

署名オプションを省略した場合、保護作業後に別途署名する必要があります。[保護作業後の署名](#sign-after-protection)をご参照ください。
-->

<a id="framework-options"></a>
### フレームワークオプション { #framework-options }

| オプション | 説明 | デフォルト値 |
|------|------|--------|
| `--flutter` | Flutter保護 | 省略時は無効 |
| `--flutter-app-library-name` | Flutter Appライブラリ名 | `libapp.so` |
| `--flutter-engine-library-name` | Flutter Engineライブラリ名 | `libflutter.so` |
| `--react-native` | React Native保護 | 省略時は無効 |
| `--jsbundle` | JS Bundleファイル名 | `index.android.bundle` |

<a id="store-options"></a>
### ストアオプション { #store-options }

| オプション | 説明 | デフォルト値 |
|------|------|--------|
| `--ext-store` | 外部ストア | 省略時は無効 |
| `--amazon` | Amazonストア | 省略時は無効 |
| `--huawei` | Huaweiストア | 省略時は無効 |

<a id="usage-examples"></a>
## 使用例 { #usage-examples }

<a id="basic-protection"></a>
### 基本保護 { #basic-protection }

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
### アプリ証明 + 難読化 { #app-attestation-obfuscation }

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
### 出力パス指定 { #specifying-the-output-path }

出力ディレクトリのみ指定すると、デフォルトのファイル名が作成されます。

```bash
appguard-cli android -i app.apk -o ./output ...
# 結果：./output/app_protected.apk
```

出力ファイル名を直接指定することもできます。

```bash
appguard-cli android -i app.apk -o ./output/my_protected_app.apk ...
# 結果：./output/my_protected_app.apk
```

!!! warning "拡張子の一致"
    入力ファイルと出力ファイルの拡張子が一致する必要があります。(APK入力 → APK出力、AAB入力 → AAB出力)

<a id="dry-run-mode"></a>
### Dry-Runモード { #dry-run-mode }

`--dry-run`オプションを使用すると、実際の保護作業を行わずにパラメータのみを確認できます。

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
## Protector管理 { #protector-management }

オンプレミス環境では、保護エンジン(Protector)イメージを直接管理します。

<a id="automatic-protector-pull"></a>
### 自動Protector Pull { #automatic-protector-pull }

アプリ保護時に`--protector-version`を指定すると、CLIが自動的にProtectorイメージを管理します。

1. サーバーに該当バージョンが存在するか確認
2. 存在しない場合はNCRから自動Pull
3. Pull成功後に保護作業を実行

通常、別途管理する必要はありません。

<a id="manual-protector-management"></a>
### 手動Protector管理 { #manual-protector-management }

手動で管理するには、次のコマンドを使用します。

```bash
# バージョン確認
appguard-cli protector --endpoint https://your-server.com --android --version

# イメージPull
appguard-cli protector --endpoint https://your-server.com --android --pull 1.0.0
```

<a id="sign-after-protection"></a>
## 保護作業後の署名 { #sign-after-protection }

保護されたAPK/AABファイルは署名されていない状態であるため、元のアプリの署名に使用したものと同じKeystoreで**必ず**再署名する必要があります。

<a id="apk-signing"></a>
### APK署名 { #apk-signing }

```bash
apksigner sign --ks <Keystoreファイルパス> \
  --ks-pass pass:<Keystoreパスワード> \
  --ks-key-alias <key alias> \
  --key-pass pass:<Keyパスワード> \
  --out <署名済みAPKパス> \
  <保護されたAPKパス>

# 署名確認
apksigner verify <署名済みAPKパス>
```

<a id="aab-signing"></a>
### AAB署名 { #aab-signing }

```bash
jarsigner -verbose -sigalg SHA256withRSA -digestalg SHA-256 \
  -keystore <Keystoreファイルパス> \
  -storepass <Keystoreパスワード> \
  -keypass <Keyパスワード> \
  <保護されたAABパス> \
  <key alias>

# 署名確認
jarsigner -verify -verbose -certs <署名済みAABパス>
```

`apksigner`と`jarsigner`はAndroid SDK Build Toolsに含まれています。Google Play App Signingを使用する場合は、アップロードキーで署名する必要があります。

<a id="cli-update"></a>
## CLIアップデート { #cli-update }

```bash
appguard-cli --version                        # 現在のCLIバージョンを確認
appguard-cli update --list                    # 使用可能なCLIバージョン一覧を照会
appguard-cli update --install VERSION         # 特定のバージョンにアップデート
appguard-cli update --auto-update             # 自動アップデート設定を確認
appguard-cli update --auto-update enable      # 自動アップデートを有効化
appguard-cli update --auto-update disable     # 自動アップデートを無効化 (デフォルト)
```

| コマンド | 説明 | 例 |
|--------|------|------|
| `--version` | 現在インストールされているCLIバージョンを確認 | `appguard-cli --version` |
| `--list` | 配布サーバーで使用可能なCLIバージョン一覧を照会及び表示 | `appguard-cli update --list` |
| `--install VERSION` | 指定されたバージョンにCLIをアップデート (例：`0.2.0`) | `appguard-cli update --install 0.2.0` |
| `--auto-update` | 現在の自動アップデート設定状態を照会 | `appguard-cli update --auto-update` |
| `--auto-update enable` | 自動アップデートを有効化 (CLI実行時に自動確認及びアップデート) | `appguard-cli update --auto-update enable` |
| `--auto-update disable` | 自動アップデートを無効化 (手動アップデートのみ可能) | `appguard-cli update --auto-update disable` |

- 自動アップデートが有効になっている場合、CLI実行時にアップデートが優先して行われます。
- アップデートの失敗、配布サーバーへのアクセス不可、ネットワークタイムアウト時には無視して既存のバージョンで元の作業を継続します。

<a id="important-notes"></a>
## 注意事項 { #important-notes }

1. **FlutterとReact Nativeは同時使用不可**
    ```
    Error: --flutter and --react-native cannot be used together.
    ```
2. **入力ファイルの拡張子はプラットフォームと一致させること**
    ```
    Android：.apkまたは.aab
    ```
3. **出力ファイルパスの指定時は入力ファイルと拡張子を一致させること**
    ```
    APK入力 → APK出力、AAB入力 → AAB出力
    ```

---

