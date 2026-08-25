# サポート環境

<a id="supported-platforms"></a>
## サポートプラットフォーム { #supported-platforms }

!!! tip "プラットフォーム要件"
    iOS 13以上

NHN AppGuard iOS SDKは、iOS 13以上のバージョンで動作します。

<a id="development-environment"></a>
## 開発環境 { #development-environment }

NHN AppGuardは、以下の開発環境をサポートしています。

<a id="native-environment"></a>
### ネイティブ開発 { #native-environment }
- Objective-C
- Swift

<a id="game-engine"></a>
### ゲームエンジン { #game-engine }
- Unity(Unity SDK)
- Unreal Engine(Unreal SDK)

<a id="cross-platform"></a>
### クロスプラットフォーム { #cross-platform }
- Flutter(Flutter SDK)
- React Native(React Native SDK)

<a id="required-framework"></a>
## 必須フレームワーク { #required-framework }

以下の必須フレームワークがプロジェクトに含まれている必要があります。

<a id="required-framework-list"></a>
### 必須フレームワーク一覧 { #required-framework-list }

| フレームワーク | 説明 |
|-----------|------|
| CoreTelephony.framework | 通信関連機能 |
| SystemConfiguration.framework | システム設定関連機能 |

!!! danger "フレームワークの追加"
    これらのフレームワークは、NHN AppGuardが正常に動作するために必ず必要です。
    
    Xcodeプロジェクトの**Build Phases** → **Link Binary With Libraries**で追加する必要があります。

