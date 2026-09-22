<!-- machine_translated: true -->

<!-- pre-align:aligned sig=2030b074147a -->

# Protection by CLI

<a id="overview"></a>
## Overview { #overview }

Provide a command line interface (CLI) build tool for build automation, allowing you to include protection tasks in your build steps without going through the web console.
You can check the supported binaries for each OS (Windows, Mac, and Linux) in the CLI folder of the downloaded SDK file.

Provide a script file (AppGuard.cmd, AppGuard.sh) suitable for Windows or \*nix family operating systems. You can run the script file from the CLI. You can also check the description of each option in the CLI itself using the -h option.
The following are the options for NHN AppGuard CLI. You must set all required options to work CLI.


!!! danger "Permissions Settings"
    When using CLI on Linux and macOS, you may have some permission issues and must check whether the execution permission has been added.

<a id="cli-option"></a>
## CLI Option { #cli-option }

You must set all required options to work CLI.

| Options | Description | Required |
|------|------|-----------|
| `-v` | Full Path of the Keystore File to be Found in the Web Console | Y |
| `-k` | Full path to the keystore file | Y |
| `-m` | Keystore Password | Y | 
| `-a` | Keystore Alias Name | Y | 
| `-p` | Keystore Alias Password | Y | 
| `-n` | Full Path of the Original APK File | Y 
| `-o` | Download Path of Protected APK File | Y |
| `--business`</br>`--enterprise`</br>`--game` | Enter one of the three protection feature policies</br>\- Apply Business Policy: --business</br>\- Apply Enterprise Policy: --enterprise</br>\- Apply Game Policy: --game | Y | | 
| `--protectionVersion` | Specify NHN AppGuard Version | Y |
| `--as`</br>`--no-as` | --as : When using store signing methods such as Google Play and ONE store</br> Enter an app signature key (SHA-256) </br>(Up to 10 signature values can be transferred)</br></br>--no-as: If you do not allow signatures other than those signed to apk or aab | Y |
| `--google-pairip` | Prevents conflicts when using Google Play Automatic Integrity Protection</br>(PLAY_INTEGRITY) | N |
| `--app-attestation` | Enables NHN AppGuard app attestation authentication | N |
| `--obfuscate` | Enables code obfuscation | N |
| `--resource-obfuscate` | Resource string obfuscation configuration file path</br>(replaced by the unified configuration file; end of support planned) | N |
| `--config` | Unified configuration file path | N |

- AppGuard SDK 0.5.0 or later is required to use app-attestation.

- NHN AppGuard 1.14.0.0 or later is required to use the unified configuration file (`--config`). For more information, see [3. Unified Configuration File](../configuration/overview.md).
- The resource string obfuscation settings previously passed via `--resource-obfuscate` have been consolidated into the `resourceStringObfuscation` setting in the unified configuration file. We recommend that you use the `--config` option in NHN AppGuard 1.14.0.0 or later. Support for `--resource-obfuscate` will be discontinued in the future. If both options are specified together, the unified configuration file passed via `--config` is used.

<a id="build-cli-with-gradle"></a>
## Build CLI with Gradle { #build-cli-with-gradle }

When building a CLI using Gradle, make sure the factors entered in Gradle are well passed over with the CLI.

<a id="invalid-example-error-occurred"></a>
### Invalid Example (Error Occurred) { #invalid-example-error-occurred }

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

!!! danger "Problem"
    If you enter as shown above, the Gradle index `-v RtnVWuGlFy4z4z9mr` is changed to `-v` and `RtnVWuGlFy4z4z9mr` in CLI.
    A space is added to the option value and both sides of the string are wrapped with '(small mark), resulting in an error in the CLI.

<a id="valid-example"></a>
### Valid Example { #valid-example }

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

!!! tip "Solution"
    Write options and values ​​by concatenating them, removing spaces and ' (single quotes).

---

