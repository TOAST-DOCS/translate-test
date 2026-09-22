<!-- machine_translated: true -->

# 機能別設定

統合設定ファイルの `configs` に記述できる機能別設定について説明します。

| 機能 | 設定名 | 記述しない場合 |
|------|-----------|--------------------|
| リソース文字列難読化 | `resourceStringObfuscation` | 難読化しない |
| DEX 暗号化対象指定 | `dexEncryption` | DEX 暗号化が有効化されている場合、全体を DEX 暗号化 |

<a id="resource-string-obfuscation-section"></a>
## リソース文字列難読化 { #resource-string-obfuscation-section }

`resourceStringObfuscation` 設定に、難読化する文字列リソース名のパターンを指定します。機能の説明については、[7. リソース文字列難読化](../resource-string-obfuscation/overview.md)を参照してください。

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

| フィールド | タイプ | 必須 | 説明 |
|------|------|------|------|
| `enabled` | Boolean | N | 機能の有効化状態（デフォルト: `true`） |
| `include` | String[] | Y | 難読化対象リソース名のパターン |
| `exclude` | String[] | N | 難読化除外リソース名のパターン（デフォルト: `[]`） |

リソース名が `include` にマッチし、かつ `exclude` にマッチしない場合にのみ難読化されます。`resourceStringObfuscation` 設定を記述しない場合、リソース文字列難読化は実行されません。

パターンルールと注意事項については、[7.2 設定ファイルの作成方法](../resource-string-obfuscation/config.md)を参照してください。

<a id="dex-encryption-section"></a>
## DEX 暗号化対象指定 { #dex-encryption-section }

DEX 暗号化は Enterprise プランでデフォルトで動作します。暗号化対象を制限するには、`dexEncryption` 設定にパッケージまたはクラスを指定します。指定した対象のみを暗号化し、それ以外は暗号化しません。

!!! warning "ANR 注意"
    暗号化対象の DEX が大きい場合、復号化に時間がかかり ANR が発生する可能性があります。`dexEncryption` 設定で暗号化対象を絞り込むと、復号化時間を短縮できます。

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

| フィールド | タイプ | 必須 | 説明 |
|------|------|------|------|
| `include` | String[] | Y | 暗号化対象クラスのパターン（空の場合はエラー） |
| `exclude` | String[] | N | 暗号化除外クラスのパターン（デフォルト: `[]`） |

クラスが `include` にマッチし、かつ `exclude` にマッチしない場合にのみ暗号化されます。`dexEncryption` 設定を記述した場合、`include` に対象を 1 つ以上指定する必要があります。全体を暗号化するには、`include` に `["*"]` を指定します。

<a id="pattern-rules"></a>
### パターンルール { #pattern-rules }

`dexEncryption` には、パッケージ名またはクラス名のみ指定できます。リソース文字列難読化のパターンルールとは異なります。

| パターン | 説明 | 例 |
|------|------|------|
| `*` | 全体マッチ | すべてのクラス |
| `com.example.*` | パッケージマッチ | `com.example` パッケージおよびすべてのサブパッケージのクラス |
| `com.example.TestClass` | クラスマッチ | `com.example.TestClass` のみマッチ |

`*` は単独で使用するか、`com.example.*` のようにパッケージ名の末尾に付けることができます。`com.*.sample` や `com.exa*` のように他の位置に使用すると、保護処理が失敗します。

クラスを指定すると、内部クラスも合わせて暗号化または除外されます。たとえば `com.example.TestClass` を指定すると、`com.example.TestClass$InnerClass` も同様に処理されます。

<a id="behavior-by-configuration"></a>
### 設定別動作 { #behavior-by-configuration }

DEX 暗号化を実行する際の設定に応じた動作は次のとおりです。

| 状況 | 動作 |
|------|------|
| 統合設定ファイルを指定しない | 全体 DEX 暗号化 |
| `dexEncryption` 設定を記述しない | 全体 DEX 暗号化 |
| `include` に `["*"]` のみ指定 | 全体 DEX 暗号化 |
| `include`、`exclude` で対象を指定 | 指定したクラスのみ部分暗号化 |
| `include` が空 | 保護処理失敗 |
| 指定したパターンにマッチするクラスがない | 保護処理失敗 |
| `dexEncryption` の設定形式が誤っている | 保護処理失敗 |

<a id="proguard-guide"></a>
### ProGuard(R8) 使用時の注意事項 { #proguard-guide }

この注意事項は、**部分暗号化**（`include`/`exclude` で対象を指定した場合）にのみ該当します。全体暗号化はパッケージ・クラス名に依存しないため、影響を受けません。

部分暗号化は、`include`/`exclude` に指定した**パッケージ・クラス名**を基に暗号化対象を検索します。アプリに ProGuard(R8) 難読化を併用すると、パッケージ・クラス名が変更されて暗号化対象から除外される場合があります。

```text
例) com.example.Sample  ──(ProGuard 適用)──▶  a.a.A
```

たとえば `include` に `com.example.*` を指定していても、ProGuard が `com.example` パッケージ名を変更すると、該当クラスは `com.example.*` にマッチしなくなり暗号化されません。

暗号化対象のパッケージ名が難読化後も維持されるよう、`proguard-rules.pro` に以下を追加します。

```proguard
-keeppackagenames com.example.**
```

例の `com.example` は、実際の部分暗号化対象パッケージ名に変更してください。`include` に `com.example.TestClass` のようにクラスを指定した場合は、`-keep class com.example.TestClass` を追加して、クラスが削除または名前変更されないようにします。

設定を適用した後、対象クラスが実際に暗号化されているか確認してください。

ProGuard 設定の詳細については、[9.2 ProGuard 適用時の確認事項](../testing/proguard.md)も参照してください。

---