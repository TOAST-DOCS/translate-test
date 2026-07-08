<a id="network-colocation-gateway-console-user-guide"></a>
## Network > Colocation Gateway > コンソール使用ガイド { #network-colocation-gateway-console-user-guide }

コンソールで**Colocation Gateway**サービスを使用する方法を説明します。

<a id="colocation-gateway"></a>
## コロケーションゲートウェイ { #colocation-gateway }

<a id="create-a-colocation-gateway"></a>
### コロケーションゲートウェイの作成 { #create-a-colocation-gateway }

**コロケーションゲートウェイ**を作成する方法は次のとおりです。

> [参考] NHN Cloud Zoneに事前に登録されたVPCのみオンプレミスネットワークと通信できます。オンプレミスネットワークと通信を行いたいVPCはコロケーションゲートウェイ作成前に必ずNHN Cloudサポート[1:1お問い合わせ](https://www.nhncloud.com/kr/support/inquiry)までお問い合わせください。<br>
> [注意] NHN Cloud Zoneに事前に登録されていないVPCを選択してコロケーションゲートウェイを作成すると、オンプレミスネットワークとの通信はできず、同じNHN Cloud Zoneに接続された他のVPCとの通信のみ可能です。

1. **Network > Colocation Gateway**に移動します。
2. **コロケーションゲートウェイ作成**ボタンをクリックすると、作成画面が表示されます。
3. **コロケーションゲートウェイ**に使用する**名前**を入力します。
4. **VPC**を選択します。<br>
 選択されたVPCをNHN Cloud Zoneに接続します。<br>
   VPCは1個のNHN Cloud Zoneのみ接続できます。
5. **NHN Cloud Zone**を選択します。
6. **確認**ボタンをクリックします。

<a id="view-a-colocation-gateway"></a>
### コロケーションゲートウェイの照会 { #view-a-colocation-gateway }

作成したコロケーションゲートウェイは**Network > Colocation Gateway**画面で確認できます。コロケーションゲートウェイを選択すると、下部にコロケーションゲートウェイ情報が表示されます。

<a id="modify-a-colocation-gateway"></a>
### コロケーションゲートウェイの変更 { #modify-a-colocation-gateway }

コロケーションゲートウェイを変更する方法は次のとおりです。**名前**、**説明**のみ変更できます。

1. **Network > Colocation Gateway**に移動します。
2. **コロケーションゲートウェイ変更**ボタンをクリックし、変更画面で項目を変更します。

<a id="delete-a-colocation-gateway"></a>
### コロケーションゲートウェイの削除 { #delete-a-colocation-gateway }

コロケーションゲートウェイを削除するには**Network > Colocation Gateway**画面で削除するコロケーションゲートウェイを選択し、コロケーションゲートウェイ削除ボタンをクリックします。

<a id="route"></a>
### ルート { #route }

コロケーションゲートウェイから流入したすべてのトラフィックを処理するVMインスタンスのPortおよび仮想IPポートを指定できます。ルートのゲートウェイとなるVMインスタンスにはNetwork Virtual Appliance VMをバッチしてVMインスタンス内部でトラフィックを制御し、ピアリング機能を利用して他のVPCにトラフィックを伝達できます。<br>
* ピアリングでハブ&スポーク(Hub & Spoke)形式のVPC接続を構成し、ハブVPCにあるNetwork Virtual Applianceですべてのトラフィックを制御する状況で顧客のオンプレミスネットワークをハブVPCにスポークとして追加するためにコロケーションゲートウェイのルート機能を活用できます。 

> [参考]現在は韓国(ピョンチョン)、韓国(パンギョ)リージョンでのみ機能が提供されます。
<a id="route-create-a-route"></a>
#### ルートの作成

1. ルート設定を行いたいコロケーションゲートウェイを選択
2. 下部タブでルートを選択
3. **ルート作成**を選択
4. ゲートウェイを選択し、確認ボタンをクリックします。
   > [参考]ゲートウェイはインスタンスと仮想IPのみ選択が可能です。<br>
<a id="route-delete-a-route"></a>
#### ルートの削除

1. ルート設定を削除したいコロケーションゲートウェイを選択
2. ルートを選択
3. **ルート削除**ボタンをクリックします。

<a id="use-a-colocation-gateway"></a>
## コロケーションゲートウェイの使用 { #use-a-colocation-gateway }

オンプレミスネットワークにパケットを送信するには**Network > Routing**でルーティングパスを追加する必要があります。

<a id="configure-a-route-for-a-colocation-gateway"></a>
### コロケーションゲートウェイルート設定 { #configure-a-route-for-a-colocation-gateway }

1. **Network > Routing**に移動します。
2. **コロケーションゲートウェイ**を作成した**VPC**の**ルーティングテーブル**を選択します。
3. 下部に表示される**ルーティングテーブル**情報から**ルート**タブを選択します。
4. **ルート作成**ボタンをクリックすると、作成画面が表示されます。
5. **対象CIDR**を入力します。<br>
 オンプレミスネットワークCIDRまたは同じHN Cloud Zoneに接続した他のVPCのCIDR
6. **ゲートウェイ**の**ゲートウェイ選択**リストから**TRANSIT_GATEWAY**を選択します。<br>
   > [参考] TRANSIT_GATEWAY項目はコロケーションゲートウェイ作成を利用して作成できます。
