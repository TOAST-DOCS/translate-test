<!-- machine_translated: true -->

<!-- pre-align:aligned sig=fe1bf114a926 -->

# Protection Using CLI

<a id="overview"></a>
## Overview { #overview }

Provides a CLI (command line interface) tool for build automation, allowing the protection process to be integrated into the build stage without going through the web console.

The SDK package's CLI folder contains `appguard-cli` binaries for each OS (Windows, Mac, and Linux). Use the `-h` option to view descriptions of each option.

```bash
appguard-cli -h                    # View full help
appguard-cli android -h            # View detailed Android options
```

<a id="command-structure"></a>
## Command Structure { #command-structure }

```
appguard-cli <platform> [options]
```

| Platform | Description |
|--------|------|
| `android` | Android app protection (APK/AAB) |
| `protector` | Protector image management (On-Premise only) |
| `update` | CLI update management |

<a id="android-app-protection-options"></a>
## Android App Protection Options { #android-app-protection-options }

<a id="required-options"></a>
### Required Options { #required-options }

| Option | Description |
|------|------|
| `-i, --input` | Input file path (APK or AAB) |
| `-o, --output` | Output directory or file path |
| `--appkey` | AppGuard Appkey |
| `--plan` | Plan (`business` / `enterprise` / `game`) |
| `--protector-version` | Protector version |
| `--endpoint` | API endpoint URL |

<a id="optional-options"></a>
### Optional Options { #optional-options }

| Option | Description | Default |
|------|------|--------|
| `--app-attestation` | Enable app attestation **(required when using app attestation)** | Disabled if omitted |
| `--additional-sign` | Additional signature hash (1–10 SHA256 hashes) | `none` |
| `--config` | Integration configuration file path | Disabled if omitted |
| `--dry-run` | Verify parameters without actual execution | Disabled if omitted |

- To use the integrated configuration file (`--config`), CLI 1.0.3 or later and Protector 1.14.0.0 or later are required. For more information, see [3. Integrated Configuration File](../configuration/overview.md).

<a id="security-options"></a>
### Security Options { #security-options }

| Option | Description | Default |
|------|------|--------|
| `--dex-obfuscate` | DEX obfuscation (enterprise/game only) | Disabled if omitted |
| `--resource-obfuscate` | Resource string obfuscation config file path (replaced by the integrated configuration file; support will be discontinued in the future) | Disabled if omitted |
| `--google-pairip` | Google PairIP | Disabled if omitted |

- The resource string obfuscation settings previously passed via `--resource-obfuscate` have been consolidated into the `resourceStringObfuscation` setting in the unified configuration file. For Protector 1.14.0.0 and later, we recommend that you use the `--config` option. Support for `--resource-obfuscate` will be discontinued in the future. If both options are specified, the unified configuration file passed via `--config` is used.

<a id="other-options"></a>
### Other Options { #other-options }

| Option | Description | Default |
|------|------|--------|
| `--show-startup-message` | Display startup message | Disabled if omitted |
| `--detection-popup-mode` | Detection popup mode (`detail` / `simple`) | `detail` |
| `--intune` | MS Intune support | Disabled if omitted |

<!-- 
<a id="signing-options"></a>
### Signing Options { #signing-options }

| Option | Description |
|------|------|
| `--keystore` | Keystore file path |
| `--keystore-key-alias` | Keystore key alias |
| `--keystore-password` | Keystore password |
| `--key-password` | Key alias password |

If signing options are omitted, you must sign the app separately after the protection process. For more information, see [Sign After Protection](#sign-after-protection).
-->

<a id="framework-options"></a>
### Framework Options { #framework-options }

| Option | Description | Default |
|------|------|--------|
| `--flutter` | Flutter protection | Disabled if omitted |
| `--flutter-app-library-name` | Flutter app library name | `libapp.so` |
| `--flutter-engine-library-name` | Flutter engine library name | `libflutter.so` |
| `--react-native` | React Native protection | Disabled if omitted |
| `--jsbundle` | JS bundle file name | `index.android.bundle` |

<a id="store-options"></a>
### Store Options { #store-options }

| Option | Description | Default |
|------|------|--------|
| `--ext-store` | External store | Disabled if omitted |
| `--amazon` | Amazon store | Disabled if omitted |
| `--huawei` | Huawei store | Disabled if omitted |

<a id="usage-examples"></a>
## Usage Examples { #usage-examples }

<a id="basic-protection"></a>
### Basic Protection { #basic-protection }

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
### App Attestation + Obfuscation { #app-attestation-obfuscation }

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
### Specifying the Output Path { #specifying-the-output-path }

If only the output directory is specified, a default file name is generated.

```bash
appguard-cli android -i app.apk -o ./output ...
# Result: ./output/app_protected.apk
```

You can also specify the output file name directly.

```bash
appguard-cli android -i app.apk -o ./output/my_protected_app.apk ...
# Result: ./output/my_protected_app.apk
```

!!! warning "Extension Match"
    The input and output file extensions must match. (APK input → APK output, AAB input → AAB output)

<a id="dry-run-mode"></a>
### Dry-Run Mode { #dry-run-mode }

Use the `--dry-run` option to verify parameters without performing the actual protection process.

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
## Protector Management { #protector-management }

In an On-Premise environment, the protection engine (Protector) images are managed directly.

<a id="automatic-protector-pull"></a>
### Automatic Protector Pull { #automatic-protector-pull }

When `--protector-version` is specified during app protection, the CLI automatically manages the Protector image.

1. Checks whether the specified version exists on the server.
2. If not, automatically pulls it from NCR.
3. Proceeds with the protection process after a successful pull.

In general, no separate management is required.

<a id="manual-protector-management"></a>
### Manual Protector Management { #manual-protector-management }

To manage manually, use the following commands.

```bash
# Check version
appguard-cli protector --endpoint https://your-server.com --android --version

# Pull image
appguard-cli protector --endpoint https://your-server.com --android --pull 1.0.0
```

<a id="sign-after-protection"></a>
## Sign After Protection { #sign-after-protection }

Since the protected APK/AAB file is unsigned, it **must** be re-signed using the same keystore used to sign the original app.

<a id="apk-signing"></a>
### APK Signing { #apk-signing }

```bash
apksigner sign --ks <keystore file path> \
  --ks-pass pass:<keystore password> \
  --ks-key-alias <key alias> \
  --key-pass pass:<key password> \
  --out <signed APK path> \
  <protected APK path>

# Verify signature
apksigner verify <signed APK path>
```

<a id="aab-signing"></a>
### AAB Signing { #aab-signing }

```bash
jarsigner -verbose -sigalg SHA256withRSA -digestalg SHA-256 \
  -keystore <keystore file path> \
  -storepass <keystore password> \
  -keypass <key password> \
  <protected AAB path> \
  <key alias>

# Verify signature
jarsigner -verify -verbose -certs <signed AAB path>
```

`apksigner` and `jarsigner` are included in the Android SDK Build Tools. If you are using Google Play App Signing, sign with the upload key.

<a id="cli-update"></a>
## CLI Update { #cli-update }

```bash
appguard-cli --version                        # Check current CLI version
appguard-cli update --list                    # List available CLI versions
appguard-cli update --install VERSION         # Update to a specific version
appguard-cli update --auto-update             # Check auto-update settings
appguard-cli update --auto-update enable      # Enable auto-update
appguard-cli update --auto-update disable     # Disable auto-update (default)
```

| Command | Description | Example |
|--------|------|------|
| `--version` | Check the currently installed CLI version | `appguard-cli --version` |
| `--list` | Retrieve and display the list of available CLI versions from the distribution server | `appguard-cli update --list` |
| `--install VERSION` | Update the CLI to the specified version (e.g., `0.2.0`) | `appguard-cli update --install 0.2.0` |
| `--auto-update` | Check the current auto-update setting | `appguard-cli update --auto-update` |
| `--auto-update enable` | Enable auto-update (automatically checks and updates when the CLI is run) | `appguard-cli update --auto-update enable` |
| `--auto-update disable` | Disable auto-update (manual updates only) | `appguard-cli update --auto-update disable` |

- If auto-update is enabled, the update will be performed first when the CLI is run.
- If the update fails, the distribution server is unreachable, or a network timeout occurs, the error is ignored and the CLI continues with the existing version.

<a id="important-notes"></a>
## Important Notes { #important-notes }

1. **Flutter and React Native cannot be used simultaneously.**
    ```
    Error: --flutter and --react-native cannot be used together.
    ```
2. **The input file extension must match the platform.**
    ```
    Android: .apk or .aab
    ```
3. **When specifying an output file path, the extension must match the input file.**
    ```
    APK input → APK output, AAB input → AAB output
    ```

---

