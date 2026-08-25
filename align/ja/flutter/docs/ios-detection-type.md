<a id="ios-detection"></a>
## iOS検出 { #ios-detection }

<a id="content-of-the-callback-function"></a>
### コールバック関数の内容 { #content-of-the-callback-function }

検出イベント発生時、JSON文字列をコールバック関数に渡します。

以下はJSON文字列の例です。

```json
{ 
  "info" : {
    "type" : 2,
    "data" : "100047" 
  }
}
```

- type:対応タイプ
- data:検出タイプ

<a id="correspondence-type"></a>
### 対応タイプ { #correspondence-type }


| 対応タイプ(type) | 説明 |
| --- | --- |
|1  | ログだけ残してアプリを終了しないイベント(detected) |
|2  | アプリをすぐに終了する必要がある検出イベント(blocked) |
|4  | 条件ブロックポリシーによるブロックイベント |

<a id="detection-type"></a>
### 検出タイプ { #detection-type }

<a id="detection-type-cheating-tools"></a>
#### チートツール

| 検出タイプ(data) | 説明 |
| --- | --- |
| 10010 | GameGuardian |
|  10013|GameHacker  |
|10095  | Jailed Tweak |
|10072 |Tweak |
|10035 |GamePlayer |
| 10036|Flex |
| 10037|MemSearch |
|10062 |GameGem |

<a id="detection-type-simulators"></a>
#### シミュレータ

| 検出タイプ(data) | 説明 |
| --- | --- |
| 20096 | シミュレータ |

<a id="detection-type-tampering"></a>
#### 改ざん

| 検出タイプ(data) | 説明 |
| --- | --- |
|40071 | IPA復号|
|40070 |IPA改ざん |
|40038 |Code改ざん |
|40003 |NHN AppGuard改ざん |
|40124|Info.plist改ざん |

<a id="detection-type-debugger"></a>
#### デバッガ
| 検出タイプ(data) | 説明 |
| --- | --- |
|50031 |デバッガ(Native)|
|50033 |デバッガ |
|50126 |IPAダンプ検出|

<a id="detection-type-jailbreaking"></a>
#### 脱獄

| 検出タイプ(data) | 説明 |
| --- | --- |
|100047 |脱獄|

<a id="detection-type-hooking"></a>
#### フッキング

| 検出タイプ(data) | 説明 |
| --- | --- |
| 110097|C API Hooking | 
| 110098| Obj-C API Hooking|
| 110099| User Function Hooking|
|110101 | NHN AppGuard Function Hooking|


<a id="detection-type-blacklist"></a>
#### ブラックリスト

| 検出タイプ(data) | 説明 |
| --- | --- |
| 900090|ブラックリスト | 

<a id="detection-type-screen-capture"></a>
#### 画面キャプチャ
| 検出タイプ(data) | 説明 |
| --- | --- |
| 200145|画面キャプチャ | 

<a id="detection-type-screen-recording"></a>
#### 画面録画
| 検出タイプ(data) | 説明 |
| --- | --- |
| 210146|画面録画 | 

<a id="detection-type-vpn"></a>
#### VPN

<!-- TODO: translate body -->

<a id="detection-type-macro-tool"></a>
#### マクロツール

<!-- TODO: translate body -->

<!-- pre-align: ko에 대응 섹션 없음 — 검토 필요 (位置操作 (location manipulation) has no counterpart in the ko outline; ko contains VPN and マクロツール at this position, neither of which matches) -->
<!-- pre-align: ko에 대응 섹션 없음 — 검토 필요 (位置操作 (location spoofing) has no corresponding ko heading in the source outline) -->
<a id="detection-type-notification"></a>
#### 通知
| 検出タイプ(data) | 説明 |
| --- | --- |
| -60017|ユーザーコールバック登録成功 | 
