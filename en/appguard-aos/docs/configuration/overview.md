<!-- machine_translated: true -->

<!-- pre-align:aligned sig=899d793daadd -->

# Unified Configuration File

<a id="overview"></a>
## Overview { #overview }

The unified configuration file is a JSON file that consolidates feature-specific settings to apply to protection tasks.

When performing a protection task, pass the file using the `--config` option of the CLI. For information on how to use the CLI, see [Protection Tasks Using the CLI]({{ cli_page }}).

```bash
--config /path/to/appguard.json
```

<a id="supported-version"></a>
## Supported Versions { #supported-version }

The unified configuration file is available starting from the following versions.

{% if variant == 'onprem' %}

| Item | Minimum Version |
|------|-----------|
| Protector | 1.14.0.0 |
| NHN AppGuard CLI | 1.0.3 |

{% else %}

| Item | Minimum Version |
|------|-----------|
| NHN AppGuard | 1.14.0.0 |

{% endif %}

The features available by unified configuration file version are as follows:

| Feature | Setting Name | Unified Configuration File Version |
|------|-----------|--------------------|
| Resource string obfuscation | `resourceStringObfuscation` | 1.0 or later |
| DEX encryption target specification | `dexEncryption` | 1.0 or later |

<a id="file-structure"></a>
## File Structure { #file-structure }

The configuration file is written in JSON. At the top level, include `version` to indicate the configuration file version and `configs` to hold feature-specific settings. Add the settings for the features you want to use under `configs`.

```json
{
  "version": "1.0",
  "configs": {
    "resourceStringObfuscation": {
      "enabled": true,
      "include": ["secret_key", "secret_*", "*secret*"],
      "exclude": ["secret_debug_*"]
    },
    "dexEncryption": {
      "include": ["com.nhnent.appguard.*"],
      "exclude": ["com.nhnent.appguard.debug.*"]
    }
  }
}
```

| Field | Type | Required | Description |
|------|------|------|------|
| `version` | String | Y | Version of the configuration file |
| `configs` | Object | Y | Feature-specific settings |

For information on how to write each feature's settings and the behavior when settings are omitted, see [3.2 Feature-Specific Settings](sections.md).

<a id="invalid-configuration-file-handling"></a>
## Invalid Configuration File Handling { #invalid-configuration-file-handling }

If the contents of the specified configuration file do not conform to the defined format, the protection task fails.

| Situation | Behavior |
|------|------|
| No configuration file specified | Protection task is performed according to the default behavior of each feature |
| Invalid JSON format | Protection task fails |
| Unsupported `version` | Protection task fails |
| A feature name not supported in the given `version` is specified (including typos) | Protection task fails |
| Invalid format in feature-specific settings | Protection task fails |

<a id="compatibility-with-existing-configuration-file"></a>
## Compatibility with Existing Configuration Files { #compatibility-with-existing-configuration-file }

Previously, the resource string obfuscation configuration file was passed separately using the `--resource-obfuscate` option. In version 1.14.0.0 or later, we recommend that you write this setting in `resourceStringObfuscation` in the unified configuration file and pass it using the `--config` option.

For information on how to convert an existing configuration file to the unified configuration file format, see [3.2 Feature-Specific Settings](sections.md).

In versions earlier than 1.14.0.0, use `--resource-obfuscate` and the existing configuration file as before.

```bash
# 1.14.0.0 or later
--config /path/to/appguard.json

# Earlier than 1.14.0.0
--resource-obfuscate /path/to/resource-obfuscation-rules.json
```

| Option | Configuration File Passed | Notes |
|------|--------------------|------|
| `--config` | Unified configuration file | Available in version 1.14.0.0 or later |
| `--resource-obfuscate` | Resource string obfuscation configuration file | Legacy method (end of support scheduled) |

If both options are specified together, the unified configuration file passed with `--config` is used.

!!! warning "End of Support Scheduled"
    The `--resource-obfuscate` option remains available for the time being in version 1.14.0.0 or later. Support will be discontinued in the future, so switch to the unified configuration file (`--config`).

---