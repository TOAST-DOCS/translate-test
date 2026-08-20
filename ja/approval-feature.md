<!-- pre-align:aligned sig=be0be57a5d82 -->

<a id="security-secure-key-manager-console-user-guide-approval-feature"></a>
## Security > Secure Key Manager > コンソール使用ガイド > 承認機能 { #security-secure-key-manager-console-user-guide-approval-feature }

国内外のセキュリティ認証審査(ISMS-P、ISOなど)で要求される安全な暗号化キー管理要件を満たすために使用するSecure Key Managerの承認機能について説明します。

**承認機能の有効化**方法と、承認機能有効化後の承認関連のロール設定と有効化前と有効化後の違い、そして**承認プロセス**について説明します。

![approval-feature](http://static.toastoven.net/prod_kms/2024-02-27-ja/approval-feature.png)

<a id="enable-approval-feature"></a>
## 承認機能の有効化 { #enable-approval-feature }

<a id="how-to-enable-approval-feature"></a>
### 承認機能有効化方法 { #how-to-enable-approval-feature }
組織管理画面のガバナンス設定で承認プロセス管理設定を利用してSecure Key Managerの承認機能を有効にします。

![console-guide-29](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-29.png)

<a id="set-up-roles-for-approval-feature"></a>
### 承認機能役割設定 { #set-up-roles-for-approval-feature }
Secure Key Managerのメンバー管理から承認者(APPROVAL ADMIN)、要請者(APPROVAL MEMBER)の役割を取得して承認手続きを進めます。

![console-guide-30](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-30.png)

<a id="differences-with-approval-feature-enabled"></a>
### 承認機能を有効にしたときの違い { #differences-with-approval-feature-enabled }
承認機能を有効にして承認者または要請者の役割を取得すると、Secure Key Managerに**承認リスト**と**キー保存場所管理**タブが追加されます。2つのタブは承認者、要請者のみアクセスできます。

![console-guide-31](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-31.png)

承認機能を有効にすると、キー保存場所でデータを追加、修正、削除できなくなり、変更リクエストを行うと**キー保存場所管理**タブに移動します。

![console-guide-32](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-32.png)

<a id="approval-process"></a>
## 承認プロセス { #approval-process }

<a id="make-approval-requests"></a>
### 承認リクエスト作成 { #make-approval-requests }
承認者と要請者は、**キー保存場所管理**タブでキー保存場所ごとに変更内容を承認リクエストできます。既存のキー保存場所と似た動作で追加、修正、削除を進めます。キー、認証情報の変更状態については次のように状態に表示されます。

![console-guide-33](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-33.png)

![console-guide-34](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-34.png)

キー保存場所の**承認リクエスト**ボタンで承認をリクエストし、該当プロジェクトの承認リクエストは**承認リスト**タブで確認できます。

![console-guide-35](http://static.toastoven.net/prod_kms/2024-09-25-en/console-guide-35.png)

<a id="apply-approval-requests"></a>
### 承認リクエストの反映 { #apply-approval-requests }
承認者は、**承認リスト**からキー保存場所の変更承認リクエストを確認し、**承認**または**拒否**を選択して反映するかどうかを決定します。

本人がリクエストした件については承認権限がありません。

![console-guide-36](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-36.png)

承認を押すとすぐにキー保存場所に反映されます。**キー保存場所**または**キー保存場所管理**タブで変更内容を確認できます。

![console-guide-37](http://static.toastoven.net/prod_kms/2023-03-28-en/console-guide-37.png)
