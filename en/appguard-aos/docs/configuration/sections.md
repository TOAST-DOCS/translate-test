<!-- machine_translated: true -->

# Feature-Specific Settings

This section describes the feature-specific settings that you can write under `configs` in the unified configuration file.

| Feature | Setting Name | If Not Specified |
|------|-----------|--------------------|
| Resource string obfuscation | `resourceStringObfuscation` | No obfuscation |
| DEX encryption target specification | `dexEncryption` | All DEX files are encrypted when DEX encryption is enabled |

<a id="resource-string-obfuscation-section"></a>
## Resource String Obfuscation { #resource-string-obfuscation-section }

In the `resourceStringObfuscation` setting, specify the string resource name patterns to obfuscate. For a description of this feature, see [7. Resource String Obfuscation](../resource-string-obfuscation/overview.md).

```json
{
  "version": "1.0",
  "configs": {
    "resourceStringObfuscation": {
      "enabled": true,
      "include": ["secret_key", "secret_*", "*secret*"],
      "exclude": ["secret_debug_*"]
    }
  }
}
```

| Field | Type | Required | Description |
|------|------|------|------|
| `enabled` | Boolean | N | Whether the feature is enabled (default: `true`) |
| `include` | String[] | Y | Resource name patterns to obfuscate |
| `exclude` | String[] | N | Resource name patterns to exclude from obfuscation (default: `[]`) |

A resource is obfuscated only if its name matches a pattern in `include` and does not match any pattern in `exclude`. If the `resourceStringObfuscation` setting is not specified, no resource string obfuscation is performed.

For pattern rules and cautions, see [7.2 How to Write the Configuration File](../resource-string-obfuscation/config.md).

<a id="dex-encryption-section"></a>
## DEX Encryption Target Specification { #dex-encryption-section }

DEX encryption runs by default on the Enterprise plan. To restrict the encryption targets, specify packages or classes in the `dexEncryption` setting. Only the specified targets are encrypted; the rest are not.

!!! warning "ANR Caution"
    If the DEX file to be encrypted is large, the decryption time increases and may cause an ANR. You can reduce the decryption time by narrowing the encryption targets using the `dexEncryption` setting.

```json
{
  "version": "1.0",
  "configs": {
    "dexEncryption": {
      "include": ["com.nhnent.appguard.*"],
      "exclude": ["com.nhnent.appguard.debug.*"]
    }
  }
}
```

| Field | Type | Required | Description |
|------|------|------|------|
| `include` | String[] | Y | Class patterns to encrypt (an error occurs if empty) |
| `exclude` | String[] | N | Class patterns to exclude from encryption (default: `[]`) |

A class is encrypted only if it matches a pattern in `include` and does not match any pattern in `exclude`. If the `dexEncryption` setting is specified, you must specify at least one target in `include`. To encrypt all classes, specify `["*"]` in `include`.

<a id="pattern-rules"></a>
### Pattern Rules { #pattern-rules }

Only package names or class names can be specified in `dexEncryption`. These pattern rules differ from those for resource string obfuscation.

| Pattern | Description | Example |
|------|------|------|
| `*` | Matches everything | All classes |
| `com.example.*` | Package match | Classes in the `com.example` package and all sub-packages |
| `com.example.TestClass` | Class match | Matches only `com.example.TestClass` |

`*` can be used alone or appended to the end of a package name, as in `com.example.*`. Using it in any other position — for example, `com.*.sample` or `com.exa*` — causes the protection task to fail.

When you specify a class, its inner classes are also encrypted or excluded. For example, specifying `com.example.TestClass` applies the same treatment to `com.example.TestClass$InnerClass`.

<a id="behavior-by-configuration"></a>
### Behavior by Configuration { #behavior-by-configuration }

The following table describes the behavior when DEX encryption is performed, depending on the configuration.

| Condition | Behavior |
|------|------|
| No unified configuration file specified | All DEX files are encrypted |
| `dexEncryption` setting is not specified | All DEX files are encrypted |
| Only `["*"]` specified in `include` | All DEX files are encrypted |
| Targets specified using `include` and `exclude` | Only the specified classes are partially encrypted |
| `include` is empty | Protection task fails |
| No class matches the specified patterns | Protection task fails |
| `dexEncryption` configuration format is invalid | Protection task fails |

<a id="proguard-guide"></a>
### Cautions When Using ProGuard (R8) { #proguard-guide }

These cautions apply only to **partial encryption** (when targets are specified using `include`/`exclude`). Full encryption is not affected because it is independent of package and class names.

Partial encryption identifies the targets to encrypt by the **package and class names** specified in `include`/`exclude`. If ProGuard (R8) obfuscation is also applied to the app, package and class names may change, causing the intended targets to be excluded from encryption.

```text
Example) com.example.Sample  ──(ProGuard applied)──▶  a.a.A
```

For example, even if `com.example.*` is specified in `include`, if ProGuard changes the `com.example` package name, the classes in that package no longer match `com.example.*` and are not encrypted.

To ensure that the target package names are preserved after obfuscation, add the following to `proguard-rules.pro`.

```proguard
-keeppackagenames com.example.**
```

Replace `com.example` in the example with the actual package name of the partial encryption target. If a class is specified in `include` — for example, `com.example.TestClass` — add `-keep class com.example.TestClass` to prevent the class from being removed or renamed.

After applying the configuration, verify that the target classes are actually encrypted.

For more information about ProGuard configuration, see [9.2 Checklist for Applying ProGuard](../testing/proguard.md).