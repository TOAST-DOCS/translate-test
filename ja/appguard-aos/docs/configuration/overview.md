<!-- machine_translated: true -->

# 統合設定ファイル

<a id="overview"></a>
## 概要 { #overview }

統合設定ファイルは、保護作業に適用する機能別の設定を一つにまとめた JSON ファイルです。

保護作業を実行する際に、CLI の `--config` オプションで渡します。CLI の使用方法については、[CLI を使用した保護作業]({{ cli_page }})を参照してください。

```bash
--config /path/to/appguard.json
```

<a id="supported-version"></a>
## サポートバージョン { #supported-version }

統合設定ファイルは、次のバージョン以降から使用できます。

{% if variant == 'onprem' %}

| 区分 | 最小バージョン |
|------|-----------|
| Protector | 1.14.0.0 |
| NHN AppGuard CLI | 1.0.3 |

{% else %}

| 区分 | 最小バージョン |
|------|-----------|
| NHN AppGuard | 1.14.0.0 |

{% endif %}

統合設定ファイルのバージョンごとに使用できる機能は次のとおりです。

| 機能 | 設定名 | 統合設定ファイルバージョン |
|------|-----------|--------------------|
| リソース文字列難読化 | `resourceStringObfuscation` | 1.0 以上 |
| DEX 暗号化対象の指定 | `dexEncryption` | 1.0 以上 |

<a id="file-structure"></a>
## ファイル構造 { #file-structure }

設定ファイルは JSON で記述します。最上位に設定ファイルのバージョンを表す `version` と、機能別の設定を格納する `configs` を配置し、`configs` の下に使用する機能の設定を追加します。

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

| フィールド | タイプ | 必須 | 説明 |
|------|------|------|------|
| `version` | String | Y | 設定ファイルのバージョン |
| `configs` | Object | Y | 機能別の設定 |

機能別の記述方法および設定を省略した場合の動作については、[3.2 機能別設定](sections.md)を参照してください。

<a id="invalid-configuration-file-handling"></a>
## 無効な設定ファイルの処理 { #invalid-configuration-file-handling }

指定した設定ファイルの内容が定められた形式と異なる場合、保護作業は失敗します。

| 状況 | 動作 |
|------|------|
| 設定ファイルを指定しない | 各機能のデフォルト動作に従って保護作業を実行 |
| JSON 形式が不正 | 保護作業失敗 |
| サポートされていない `version` | 保護作業失敗 |
| 該当の `version` でサポートされていない機能名を記述した場合（タイポを含む） | 保護作業失敗 |
| 機能別設定の形式が不正 | 保護作業失敗 |

<a id="compatibility-with-existing-configuration-file"></a>
## 既存設定ファイルとの互換性 { #compatibility-with-existing-configuration-file }

これまでは、リソース文字列難読化の設定ファイルを `--resource-obfuscate` オプションで個別に渡していました。1.14.0.0 以降では、この設定を統合設定ファイルの `resourceStringObfuscation` に記述し、`--config` オプションで渡すことを推奨します。

既存の設定ファイルを統合設定ファイル形式に変換する方法については、[3.2 機能別設定](sections.md)を参照してください。

1.14.0.0 未満では、`--resource-obfuscate` と既存の設定ファイルをそのまま使用します。

```bash
# 1.14.0.0 以上
--config /path/to/appguard.json

# 1.14.0.0 未満
--resource-obfuscate /path/to/resource-obfuscation-rules.json
```

| オプション | 渡す設定ファイル | 備考 |
|------|--------------------|------|
| `--config` | 統合設定ファイル | 1.14.0.0 以降で使用 |
| `--resource-obfuscate` | リソース文字列難読化設定ファイル | 従来の方式（サポート終了予定） |

両方のオプションを同時に指定した場合は、`--config` で渡した統合設定ファイルが使用されます。

!!! warning "サポート終了予定"
    1.14.0.0 以降でも `--resource-obfuscate` をしばらくの間使用できます。将来的にサポートを終了する予定のため、統合設定ファイル（`--config`）に移行してください。

---