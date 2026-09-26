<!-- pre-align:aligned sig=70259b9e24c2 -->

<a id="security-secure-key-manager-console-user-guide"></a>
## Security > Secure Key Manager > コンソール使用ガイド { #security-secure-key-manager-console-user-guide }

コンソール使用ガイドではSecure Key Managerを使用するのに必要な基本的な内容を説明します。
- **キー保存場所の作成**
- **キーの作成**
- **認証情報の登録**
- **ユーザーデータの管理**
- **承認機能**

<a id="create-a-key-store"></a>
### キー保存場所の作成 { #create-a-key-store }
Secure Key Managerは、キー保存場所の単位として認証情報とキーを管理します。キー保存場所がない場合は次のような画面が表示されます。

![console-guide-01](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-01.png)

**キー保存場所追加**をクリックすると、キーの保存場所を作成できるウィンドウが表示されます。

![console-guide-02](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-02.png)

名前と説明を入力し、1つ以上の認証方法を選択します。**認証方式の組み合わせ**オプションは必須であり、有効にした認証方法が1つだけのときでも必ず選択する必要があります。

- **全て通過(AND)**: 有効にした全ての認証方法を通過すると認証に成功します(デフォルト値)。
- **1つのみ通過(OR)**: 有効にした認証方法のうち1つだけ通過しても認証に成功します。複数の認証方法を有効にした状態で、使用中の認証方式を別の方式へ段階的に移行する際の無停止マイグレーションの用途に役立ちます。

![console-guide-auth-mode](画像パス)

**追加**をクリックするとキーストアを作成します。作成したキーストアは次の図のようにキーストア一覧に表示されます。

![console-guide-03](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-03.png)

キーストア右上にある「さらに表示」ボタンをクリックして、詳細情報メニューから選択したキーストアの情報を確認できます。
![console-guide-01](http://static.toastoven.net/prod_kms/2024-02-27/console-guide-01.png)

キー保存場所リストでキー保存場所をクリックすると、次の図のようにキー保存場所を管理できるメニューが表示されます。

![console-guide-04](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-04.png)

<a id="create-a-key"></a>
### キーの作成 { #create-a-key }
Secure Key Managerは、キーを3つのタイプに区分します。機密データは文字列データを保存し、APIを使用した照会機能を提供します。対称鍵はAPIを使用したデータ暗号化/復号機能を提供します。非対称鍵はAPIを使用したデータ署名/検証機能を提供します。ユーザーは使用目的に合ったキータイプを選択してキーを作成できます。

**キー管理**メニューをクリックすると、次の図のようにキーを管理できる画面が表示されます。

![console-guide-05](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-05.png)

キー管理画面で**キー追加**をクリックすると、キーを作成できるウィンドウが表示されます。選択したキーのタイプに応じて、自由にデータを入力できます。

![console-guide-06](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-06.png)


![console-guide-07](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-07.png)


![console-guide-08](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-08.png)


機密データを選択すると名前、説明、データを入力できます。対称鍵/非対称鍵を選択すると名前、説明、ローテーション周期を入力できます。必須データを入力した後、**追加**をクリックするとキーを作成します。作成したキーは次の図のようにキー管理画面に表示されます。

![console-guide-09](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-09.png)

> [参考]
>
> NASサービスで暗号化ストレージを作成する際に設定したキーストアに対称鍵が保存されます。詳細は[NASユーザーガイド](https://docs.nhncloud.com/ko/Storage/NAS/ko/console-guide/#_2)を参照してください。

<a id="import-a-key"></a>
### キーのインポート { #import-a-key }
Secure Key Managerは、対称鍵(AES-256)をインポートする機能をサポートします。

![console-guide-10](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-10.png)

**キーデータ**領域にキー値を入力してアップロードできます。アップロード可能なキーの形式は次のとおりです。

```
0xXX, 0xXX, ..., 0xXX
```

上記のように32個のHex Stringをカンマ(`,`)またはスペース(` `)で区切って入力してキーをアップロードします。

<a id="register-authentication-information"></a>
### 認証情報の登録 { #register-authentication-information }
Secure Key Managerで作成したキーは、認証に成功したクライアントのみ使用できます。クライアント認証に使用する認証情報は**IPv4アドレス管理**、**MACアドレス管理**、**証明書管理**メニューで登録します。

<a id="register-authentication-information-register-ipv4-address"></a>
#### IPv4アドレスの登録
**IPv4アドレス管理**をクリックすると、次の図のようにクライアント認証に使用するIPv4アドレス管理画面が表示されます。

![console-guide-11](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-11.png)

**IPv4アドレス追加**をクリックすると、図のようにIPv4アドレスを追加できるウィンドウが表示されます。

![console-guide-12](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-12.png)

IPv4アドレス追加**をクリックすると、図のようにIPv4アドレスを追加できるウィンドウが表示されます。

![console-guide-38](http://static.toastoven.net/prod_kms/2023-09-26-en/console-guide-38.png)

クライアントIPv4アドレスと説明を入力した後、**追加**をクリックすると、IPv4アドレスを追加します。この時、IPv4アドレスにはクライアントがSecure Key Managerに接続する時に使用するIPv4アドレスを入力する必要があります。追加したIPv4アドレスは次の図のようにIPv4アドレス管理画面に表示されます。

![console-guide-13](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-13.png)

<a id="register-authentication-information-register-mac-address"></a>
#### MACアドレスの登録
**MACアドレス管理**をクリックすると、クライアント認証に使用するMACアドレス管理画面が表示されます。
![console-guide-14](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-14.png)

**MACアドレス追加**をクリックすると、MACアドレスを追加できるウィンドウが表示されます。

![console-guide-15](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-15.png)

クライアントMACアドレスと説明を入力した後、**追加**をクリックすると、MACアドレスを追加します。追加したMACアドレスはMACアドレス管理画面に表示されます。

![console-guide-16](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-16.png)

<a id="register-authentication-information-register-client-certificates"></a>
#### クライアント証明書の登録
**証明書管理**をクリックすると、クライアント認証に使用する証明書管理画面が表示されます。

![console-guide-17](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-17.png)

**証明書追加**をクリックすると、証明書を作成できるウィンドウが表示されます。

![console-guide-18](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-18.png)

証明書名、パスワード、説明を入力し、使用期間を選択した後、**追加**をクリックすると証明書を作成します。作成した証明書は次のように証明書管理画面に表示されます。証明書管理画面で**ダウンロード**アイコンをクリックすると証明書ファイルをダウンロードします。

![console-guide-19](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-19.png)

<a id="manage-user-data"></a>
### ユーザーデータの管理 { #manage-user-data }
Secure Key Managerは、ユーザーが作成したデータ(キー、認証情報)の詳細情報を提供します。ユーザーデータリストで**詳細情報アイコン**をクリックすると、次の図のように詳細情報が表示されます。

![console-guide-20](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-20.png)

<a id="manage-user-data-delete-user-data"></a>
#### ユーザーデータの削除

ユーザーが作成したデータの初期状態は**使用中**です。不要なデータを削除するには次の図のように**詳細情報**ウィンドウで**削除リクエスト**をクリックします。

![console-guide-21](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-21.png)

削除をリクエストすると、次の図のようにデータ状態が**削除予定**に変更されます。**削除予定**に変更されたデータは使用できず、7日後に完全に削除されます。

![console-guide-22](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-22.png)

**削除予定**状態のデータは**即時削除**をクリックして削除予定時間まで待たずにすぐに削除することができます。また、**削除キャンセル**をクリックして**使用中**状態に戻すこともできます。

![console-guide-23](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-23.png)

<a id="manage-user-data-rotate-symmetricasymmetric-keys"></a>
#### 対称鍵/非対称鍵のローテーション

Secure Key Managerでは対称鍵/非対称鍵をローテーションできます。次の図のように対称鍵/非対称鍵詳細情報ウィンドウで自動ローテーション周期を設定できます。ローテーション周期を「0」に設定すると、自動ローテーションを行いません。

![console-guide-24](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-24.png)

ローテーション周期に30以上の値を設定すると、次のローテーション日を表示し、ローテーション周期ごとにキーを自動的にローテーションします。

![console-guide-25](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-25.png)

対称鍵/非対称鍵詳細情報ウィンドウで**即時ローテーション**をクリックすると、キーを即時にローテーションできます。

![console-guide-26](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-26.png)

キーをローテーションすると、次の図のようにキーバージョンリストに新しいバージョンが追加されます。

![console-guide-27](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-27.png)

例外としてキーのインポートを行って作成したキーはSecure Key Managerで作成した対称鍵とは異なり、ローテーション機能を提供しません。照会時、次のようにキーローテーション領域が存在しません。

![console-guide-28](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-28.png)

<a id="approval-feature"></a>
### 承認機能 { #approval-feature }

<a id="approval-feature-enable-approval-feature"></a>
#### 承認機能の有効化
組織管理画面のガバナンス設定で承認プロセス管理設定を利用してSecure Key Managerの承認機能を有効にします。

![console-guide-29](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-29.png)

<a id="approval-feature-set-up-roles-for-approval-feature"></a>
#### 承認機能役割設定
Secure Key Managerのメンバー管理から承認者(APPROVAL ADMIN)、要請者(APPROVAL MEMBER)の役割を取得して承認手続きを進めます。

![console-guide-30](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-30.png)

<a id="approval-feature-differences-with-approval-feature-enabled"></a>
#### 承認機能を有効にしたときの違い
承認機能を有効にして承認者または要請者の役割を取得すると、Secure Key Managerに**承認リスト**と**キー保存場所管理**タブが追加されます。2つのタブは承認者、要請者のみアクセスできます。

![console-guide-31](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-31.png)

承認機能を有効にすると、キー保存場所でデータを追加、修正、削除できなくなり、変更リクエストを行うと**キー保存場所管理**タブに移動します。

![console-guide-32](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-32.png)

<a id="approval-feature-make-approval-requests"></a>
#### 承認リクエスト作成
承認者と要請者は、**キー保存場所管理**タブでキー保存場所ごとに変更内容を承認リクエストできます。既存のキー保存場所と似た動作で追加、修正、削除を進めます。キー、認証情報の変更状態については次のように状態に表示されます。

![console-guide-33](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-33.png)

![console-guide-34](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-34.png)

キー保存場所の**承認リクエスト**ボタンで承認をリクエストし、該当プロジェクトの承認リクエストは**承認リスト**タブで確認できます。

![console-guide-35](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-35.png)

<a id="approval-feature-apply-approval-requests"></a>
#### 承認リクエストの反映
承認者は、**承認リスト**からキー保存場所の変更承認リクエストを確認し、**承認**または**拒否**を選択して反映するかどうかを決定します。

![console-guide-36](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-36.png)

承認を押すとすぐにキー保存場所に反映されます。**キー保存場所**または**キー保存場所管理**タブで変更内容を確認できます。

![console-guide-37](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-37.png)
