<!-- pre-align:aligned sig=72d665d34e38 -->

<a id="management-certificate-manager-console-user-guide"></a>
## Management > Certificate Manager > コンソール使用ガイド { #management-certificate-manager-console-user-guide }
コンソール使用ガイドではCertificate Managerを使用するのに必要な基本的な内容を説明します。
* 通知グループ
* 証明書
* ドメイン
* ユーザーデータ
* 証明書照会/ダウンロードAPI資格関連

<a id="notification-group"></a>
## 通知グループ { #notification-group }

Certificate Managerは、通知グループ単位で有効期限の通知周期を設定し、通知を受け取る対象者を管理します。

![20260728_alarm_group_01_en.png](http://static.toastoven.net/prod_certificate_manager/2026-07-28/20260728_alarm_group_01_en.png)

<a id="creating-notification-groups"></a>
### 通知グループ作成 { #creating-notification-groups }

1. 通知グループメイン画面で**+グループ作成**ボタンをクリックします。
![20260728_alarm_group_02_en.png](http://static.toastoven.net/prod_certificate_manager/2026-07-28/20260728_alarm_group_02_en.png)
2. **グループ作成**ウィンドウでグループ名を入力します。すでに存在する名前は指定できません。
3. 通知を使用するかどうかを選択します。通知グループに属しているユーザーに有効期限の通知を含むすべての通知を送信するかどうかを選択できます。
4. **追加**ボタンをクリックします。

<a id="detail-page"></a>
### 詳細情報 { #detail-page }

1. 通知グループメイン画面で**詳細情報**ボタンをクリックすると、通知グループ名と通知使用有無、管理データが表示されます。**管理data**は該当通知グループに連携されている証明書、ドメイン、ユーザーデータを意味します。
2. **修正**ボタンをクリックして通知グループの名前および通知を使用するかどうかを変更できます。

![20260728_alarm_group_03_en.png](http://static.toastoven.net/prod_certificate_manager/2026-07-28/20260728_alarm_group_03_en.png)

<a id="notification-setup"></a>
### 通知設定 { #notification-setup }

1. 通知グループメイン画面で**通知設定**ボタンをクリックします。
2. 基本に設定されている通知ポリシーがないため、**通知設定**ウィンドウで通知ポリシーを追加すると、有効期限の通知を受け取ることができます。
![20260728_alarm_group_04_en.png](http://static.toastoven.net/prod_certificate_manager/2026-07-28/20260728_alarm_group_04_en.png)

<a id="adding-notifications"></a>
### 通知追加 { #adding-notifications }

1. **通知設定**ウィンドウ左下の**+**ボタンをクリックします。
![20260728_alarm_group_05_en.png](http://static.toastoven.net/prod_certificate_manager/2026-07-28/20260728_alarm_group_05_en.png)
2. **通知開始D-day**で、証明書、ドメイン、データ有効期限の何日前から通知を送信するかを指定します。
3. **通知周期**で、何日間隔で通知を送信するかを指定します。
4. **受信グループ**で通知を受け取る受信グループを選択します。受信グループはプロジェクト設定で編集できます。
5. **管理**列で**-**ボタンをクリックして通知ポリシーを削除できます。
6. **通知開始D-day**と**通知周期**は重複して設定できません。
7. **完了**ボタンをクリックします。
![20260728_alarm_group_06_en.png](http://static.toastoven.net/prod_certificate_manager/2026-07-28/20260728_alarm_group_06_en.png)

<a id="certificate"></a>
## 証明書 { #certificate }

証明書のドメイン名(例：\*.toast.com)と有効期限を入力すると、連携した通知グループの通知ポリシーに従ってユーザーに通知を送信します。

証明書ファイル(.pem)をアップロードすると、証明書ファイルから下記の項目を自動的に収集します。
* Domains [CN(CommonName) + SAN(SubjectAlternativeNames)]
* 作成日
* 有効期限
* 証明書の署名方式(例: sha256RSA)
* 認証機関(例：Digicert)

証明書のインストール情報を登録する場合、証明書インストール情報のIPと、ポートから証明書をインポートし、Certificate Managerに登録した証明書と有効期限を比較します。
Certificate Managerに登録した証明書の有効期限より、自動収集した証明書インストール情報の有効期限が前の場合、証明書の交換が必要という通知を送信します。

<a id="main-page"></a>
### メイン画面 { #main-page }
メイン画面では証明書リストや有効期限までの残り日数などを確認できます。

![certificate-1.png](http://static.toastoven.net/prod_certificate_manager/202511/certificate-1-en.png)

* 既に登録している証明書のリストを確認および検索できます。
* 証明書ファイルがアップロードされると、自動で抽出されたDomains [CN(CommonName) + SAN(SubjectAlternativeNames)]情報を確認できます。
* 有効期限までの残り日数を確認できます。
* 有効期限を過ぎたデータは赤色で、有効期限までの残り日数が30日以下のデータはオレンジ色で表示されます。

<a id="creating-certificates"></a>
### 証明書の作成 { #creating-certificates }

1. 証明書メイン画面で**+証明書の追加**ボタンをクリックすると、**証明書の追加**ウィンドウが表示されます。
![certificate-2.png](http://static.toastoven.net/prod_certificate_manager/202511/certificate-2-en.png)
2. **通知グループ**で連携する通知グループを選択します。作成された通知グループがない時はリストに表示されず、証明書を作成できません。
3. **名前**に証明書名を入力します。
    * 証明書名は、プロジェクト内で重複して登録できません。
    * 証明書名は、英字、日本語、数字を組み合わせて自由に構成できます。
    * 特殊記号は(-, _, ., *)のみ使用できます。
4. **証明書登録**で証明書ファイルを登録します。<br>
   証明書は必須項目です。
    * 証明書は、秘密鍵と証明書で構成された.pem形式のファイルです。
    * サポートする証明書ファイル(.pem)形式は[**問題解決ガイド > 証明書ファイルフォーマット変換**](./troubleshooting-guide/#converting-certificate-file-formats)をご覧ください。
    * 証明書ファイルは最大512KBまでアップロードできます。
5. **パスフレーズ**(passphrase)に、証明書ファイル内に含まれる秘密鍵の**パスフレーズ**を入力します。
6. **追加**ボタンをクリックします。
7. [Network > Load Balancer](/Network/Load%20Balancer/ja/overview) サービスと連携する場合は、証明書ファイルの**パスフレーズ**を削除する必要があります。
   * 次のコマンドを使用してパスフレーズを削除できます。
    ```bash
    openssl rsa -in my_private_input.key -out my_private_output.key
    ```

<a id="certificate-detail-page"></a>
### 詳細画面 { #certificate-detail-page }

1. 証明書メイン画面で**詳細情報**ボタンをクリックすると、証明書ファイル情報を確認できます。
    * **(自動収集)**が表示されたフィールドは証明書ファイルから自動収集された項目を意味します。証明書ファイルが登録されていない場合は「-」と表示されます。
      ![certificate-3-1.png](http://static.toastoven.net/prod_certificate_manager/202511/certificate-3-1-en.png)
2. **修正**ボタンをクリックすると、証明書情報の修正や、証明書ファイルのアップロードを行うことができます。
    * 証明書名は修正できません。証明書名を修正するには、登録している証明書を削除して新たに作成する必要があります。
    * 1つの証明書には、1つの証明書ファイルのみアップロードできます。
    * 既存の証明書ファイルを更新する場合、新しい証明書ファイルのDomains [CN(CommonName) + SAN(SubjectAlternativeNames)]が、既存の証明書ファイルのDomainsと同一である必要があります。
      ![certificate-3-2.png](http://static.toastoven.net/prod_certificate_manager/202511/certificate-3-2-en.png)

<a id="creating-certificate-usageinstallation-information"></a>
### 証明書使用情報、インストール情報作成 { #creating-certificate-usageinstallation-information }

1. 証明書メイン画面で**証明書の使用情報**ボタンをクリックすると、証明書の使用およびインストール情報を確認できます。デフォルト値では何も登録されていません。
![certificate-4.png](http://static.toastoven.net/prod_certificate_manager/202511/certificate-4-1-en.png)
2. **修正**ボタンをクリックすると、次のような画面を確認できます。
![certificate-5.png](http://static.toastoven.net/prod_certificate_manager/202511/certificate-4-2-en.png)
3. 証明書の使用情報を追加する方法は、次の2つがあります。
    * **ユーザー追加**: 右上にある**+ 追加**ボタンをクリックすると、情報を入力できるフィールドが表示されます。
![certificate-6.png](http://static.toastoven.net/prod_certificate_manager/202511/certificate-4-3-en.png)
    * **読み込み**: 右上にある**読み込み**ボタンをクリックして、他の証明書の使用情報を読み込むことができます。
        1. **読み込み**ボタンをクリックすると、証明書検索ウィンドウが表示されます。
![certificate-9.png](http://static.toastoven.net/prod_certificate_manager/202511/certificate-4-4-en.png)
        2. 検索ウィンドウで、読み込む証明書名を検索します。
![certificate-10.png](http://static.toastoven.net/prod_certificate_manager/202511/certificate-4-5-en.png)
        3. **確認**を押すと、該当の証明書の使用情報一覧が自動的に読み込まれます。
![certificate-11.png](http://static.toastoven.net/prod_certificate_manager/202511/certificate-4-6-en.png)
4. 証明書使用情報の名前を入力します。
    * 使用情報のドメイン名は、証明書ファイルのアップロード時に自動登録されたDomains [CN(CommonName) + SAN(SubjectAlternativeNames)]に含まれている必要があります。
5. **通知使用有無**で証明書使用情報の通知を使用するかどうかを選択します。
6. 証明書インストール情報を入力するには証明書インストール情報の横にある**+追加**ボタンをクリックします。
![certificate-7.png](http://static.toastoven.net/prod_certificate_manager/202511/certificate-4-8-en.png)
    * **IPアドレス**と**ポート番号**を入力します。証明書の自動収集を使用する場合、入力したIPアドレスとポート番号で証明書をダウンロードして有効期限を比較します。
    * IPアドレスがプライベートIP(例：192.168.0.1, 172.20.0.1, 10.0.0.1)の場合、証明書をダウンロードできず、自動収集失敗通知が送信される場合があります。
7. **完了**ボタンをクリックすると、設定した証明書の使用およびインストール情報が保存されます。

<a id="page-of-certificate-usage-information"></a>
### 証明書使用情報画面 { #page-of-certificate-usage-information }
証明書メイン画面で**証明書使用情報**ボタンをクリックすると、証明書使用およびインストール情報を確認できます。
右上の全体/使用/未使用で証明書使用情報の通知使用有無を選択して確認できます。

![certificate-8.png](http://static.toastoven.net/prod_certificate_manager/202511/certificate-4-7-en.png)

<a id="domain"></a>
## ドメイン { #domain }
DNSの最上位ドメイン名(例：toast.com)と有効期限を入力すると、連携した通知グループの通知ポリシーに合わせてユーザーに通知を送信します。

ドメインの「自動収集」機能を使用する場合、whoisサーバーからドメイン情報を自動収集します。
自動収集する項目は次のとおりです。
* 作成日
* 有効期限
* 登録者(registrar)(例：Gabia, Inc.)
* 登録機関(registrant、ドメインの実所有者)
* ネームサーバー

<a id="domain-main-page"></a>
### メイン画面 { #domain-main-page }

登録したドメインリストの確認、検索ができます。

![domain-1.png](http://static.toastoven.net/prod_certificate_manager/202002/domain-1.png)

有効期限まで何日残っているかを確認できます。

有効期限を過ぎたデータは赤色で、有効期限までの残り日数が30日以下のデータはオレンジ色で表示されます。

<a id="creating-domains"></a>
### ドメイン作成 { #creating-domains }

1. ドメインメイン画面で**+ ドメイン追加**ボタンをクリックします。
![domain-2.png](http://static.toastoven.net/prod_certificate_manager/202002/domain-2.png)
2. **ドメイン追加**ウィンドウで連携する通知グループを選択します。通知グループがない場合はリストに表示されず、ドメインを作成できません。
3. **上位ドメイン情報**の下の**名前**に上位ドメイン名を入力します。上位ドメイン名は重複して登録できません。
4. **有効期限**にドメインの有効期限を入力します。
5. **タイプ**でタイプを選択します。
    * **サービス用**はDNSサーバーにドメインを登録してサービスで使用する場合です。
    * **防御用**は、実サービスで使用しないが、サービスの信頼性などの目的でドメインを購入して確保する場合です。
6. **通知使用有無**を選択します。該当ドメインの通知を送信するかどうかを選択します。**未使用**を選択すると該当ドメインの通知が全て送信されません。
7. **自動収集**で項目を自動的に収集するかどうかを選択します。**使用**を選択するとwhoisサーバーから下記の項目を収集します。
    * 作成日
    * 有効期限
    * 登録者(registrar、例：Gabia, Inc.)
    * 登録機関(registrant、ドメインの実所有者)
    * ネームサーバー
8. **サブドメイン情報**でサブドメインの自動収集をするかどうか、およびサブドメイン名を入力します。
    * サブドメインの自動収集を使用する場合、該当ドメインでpingを呼び出し、レスポンスが成功するかどうかを確認します。
    * サブドメイン名は上位ドメインに属している必要があります。
        * サブドメイン名は上位ドメインと同じか、'.[上位ドメイン名]'で終わる必要があります。
        * 例：上位ドメイン名が'toast.com'の場合、サブドメイン名には'toast.com'および'www.toast.com'、'www2.toast.com'などを入力できます。
9. **追加**ボタンをクリックすると、設定したドメイン情報を保存できます。

<a id="domain-detail-page"></a>
### 詳細画面 { #domain-detail-page }

1. ドメインメイン画面で**詳細情報**ボタンをクリックすると、ドメインとサブドメインの情報および自動収集された情報が表示されます。
2. フィールド名の後ろに**(自動収集)**と表示されたフィールドは自動収集された項目を意味します。自動収集された情報がない場合は**-**と表示されます。
3. **修正**ボタンをクリックして上位ドメイン情報を修正したり、登録されたサブドメインの削除またはサブドメインの追加を行うことができます。
    * 上位ドメイン名は修正できません。上位ドメイン名を修正する必要がある場合は、登録したドメインを削除し、新たに作成する必要があります。

![domain-3.png](http://static.toastoven.net/prod_certificate_manager/202002/domain-3.png)

<a id="user-data"></a>
## ユーザーデータ { #user-data }

有効期限があるデータ(例：ライセンスキー)を入力すると、連携した通知グループの通知ポリシーに応じてユーザーに通知を送信します。
特定ユーザーグループに周期的に通知を送信する時に活用できます。

<a id="user-data-main-page"></a>
### メイン画面 { #user-data-main-page }

登録したユーザーデータのリストの確認、検索を行うことができます。有効期限までの残り日数を確認できます。
有効期限を過ぎたデータは赤色で、有効期限までの残り日数が30日以下のデータはオレンジ色で表示されます。

![userdata-1.png](http://static.toastoven.net/prod_certificate_manager/202002/userdata-1.png)

<a id="creating-user-data"></a>
### ユーザーデータの作成 { #creating-user-data }

ユーザーデータメイン画面で**+ ユーザーデータ追加**ボタンをクリックすると、次のような画面が表示されます。

![userdata-2.png](http://static.toastoven.net/prod_certificate_manager/202002/userdata-2.png)

* 連携する通知グループを選択します。通知グループが作成されていない場合、選択可能な通知グループが表示されず、ユーザーデータを作成できません。
* ユーザーデータ名を入力します。ユーザーデータ名は重複して登録できません。
* 通知を送信するかどうかを選択します。該当ユーザーデータに対する通知を送信するかどうかを選択できます。該当フィールドを**未使用**に選択する場合、該当ユーザーデータに対する通知が全て送信されません。
* ユーザーデータの有効期限を入力します。
* **追加**ボタンをクリックすると、ユーザーデータ情報が保存されます。

<a id="user-data-detail-page"></a>
### 詳細画面 { #user-data-detail-page }

ユーザーデータメイン画面で**詳細情報**ボタンをクリックすると、保存していたユーザーデータの情報が表示されます。

**修正**ボタンをクリックしてユーザーデータの情報を修正できます。

![userdata-3.png](http://static.toastoven.net/prod_certificate_manager/202002/userdata-3.png)
