<!-- pre-align:aligned sig=f4b3b577c934 -->

# Cloud Accessトラブルシューティング

**Security > Cloud Access > トラブルシューティング**

<br>

<a id="connected-agent-but-cannot-access-the-instance"></a>
## エージェントは接続されましたが、インスタンスにアクセスできません { #connected-agent-but-cannot-access-the-instance }

ログイン後、インスタンスに接続するには以下の設定を追加する必要があります。

* ルート設定
    * 詳細は[コンソール使用ガイド - 始める](./console-user-guide/cloud-access-start/)を参照してください。
* ACLポリシー設定
    * 内部インスタンスへのアクセス時に適用されるアクセス制御ポリシーです。**ACLポリシー** タブでIPを許可する必要があります。
* Security Groups設定
    * インスタンスのセキュリティグループで送信元IPを許可する必要があります。

<br>

<a id="after-entering-information-to-add-a-connection-a-failure-message-will-be-displayed-during-verification"></a>
## 接続追加のための情報入力後、検証時に失敗メッセージが表示されます。 { #after-entering-information-to-add-a-connection-a-failure-message-will-be-displayed-during-verification }

Cloud Accessエージェントはパブリック及び公共クラウドの両方に接続できます。トレイアイコンメニューの**設定 - クラウド環境設定**で、接続を追加しようとする環境であるか確認してください。

<br>

<a id="im-a-windows-user-but-biometric-authentication-is-not-working"></a>
## Windowsユーザーですが、生体認証が使用できません { #im-a-windows-user-but-biometric-authentication-is-not-working }

Cloud Accessの生体認証機能は、指紋や顔認識が可能なデバイスでのみ使用可能です。生体認証がない場合は、**アカウント > ログインオプション** メニューでPINを設定後、生体認証の代替として使用可能です。

<br>

<a id="the-user-account-is-created-but-nothing-appears-when-clicking-the-add-user-object-button"></a>
## ユーザーアカウントは作成済みだが、「ユーザーオブジェクト追加」ボタンを押しても項目が表示されません { #the-user-account-is-created-but-nothing-appears-when-clicking-the-add-user-object-button }

以下の場合、ユーザーオブジェクト追加リストに表示されません。

* ユーザーアカウントを作成した直後から認証完了まで
    * 認証が完了してはじめてIPを確認できます。
* ユーザーアカウント作成時にIPタイプを動的IP(dynamic IP)に設定したユーザーアカウント

<br>

<a id="password-policy-is-enabled-but-login-is-possible-with-an-invalid-password"></a>
## パスワードポリシーを「使用する」に設定したのに、条件に合わないパスワードでもログインできてしまいます { #password-policy-is-enabled-but-login-is-possible-with-an-invalid-password }

パスワードポリシーを**使用**に設定して保存しても、既存のユーザーや既にパスワードを変更したユーザーアカウントには当該ポリシーが適用されません。
パスワードポリシーは、**初期パスワードの強制変更**オプションを選択した場合にのみ、新たに作成されたユーザーアカウントに適用されます。この場合、該当するユーザーアカウントのパスワードを初期化し、ポリシーに準拠したパスワードを使用するように案内してください。

<br>

<a id="force-initial-password-change-is-enabled-but-the-change-screen-does-not-appear-on-login"></a>
## 初期パスワードの強制変更を設定しましたが、ログイン時に変更画面が表示されません { #force-initial-password-change-is-enabled-but-the-change-screen-does-not-appear-on-login }

**初期パスワード強制変更**オプションを選択した場合にのみ、新しく作成されたユーザーアカウントに設定が適用されます。設定前に作成されたユーザーアカウントや、既存のアカウントでオプションを変更した場合には、設定は反映されません。その場合は該当ユーザーアカウントのパスワードを初期化した後に変更を行ってください。

<br>

<a id="clicking-the-link-account-button-shows-a-popup-saying-no-activated-services"></a>
## アカウント連携ボタンをクリックすると「有効なサービスがありません」というポップアップが表示されます { #clicking-the-link-account-button-shows-a-popup-saying-no-activated-services }

Cloud Accessサービスが無効化されていると、アカウント連携はできません。サービスを有効化してから連携を再度追加するか、不要な連携であれば削除してください。

<br>

<a id="after-activating-services-in-both-pangyo-and-pyeongchon-regions-deactivating-a-single-region-is-not-supported"></a>
## パンギョとピョンチョンリージョンの両方でサービスを有効化した後、どちらか一方だけを無効化することができません { #after-activating-services-in-both-pangyo-and-pyeongchon-regions-deactivating-a-single-region-is-not-supported }

現在はすべてのリージョンが同時に無効化される仕様となっており、特定のリージョンのみを個別に無効化する機能はサポートされていません。
特定のリージョンでのみ利用したい場合は、サービスを一度無効化した上で、使用したいリージョンでのみ再度有効化してください（個別リージョンの削除機能は今後追加予定です）。

<br>

!!! tip "問題が解決しない場合"
    トラブルシューティングの案内に従って進めたにもかかわらず問題が解決しない場合は、NHN Cloudサポートまでお問い合わせください。
    * [オンライン1:1お問い合わせ](https://www.nhncloud.com/kr/support/inquiry?alias=tab16_15)
    * 代表電話: 1588-7967(営業時間:月～金10:00～19:00)