## Game > Launching > コンソール使用ガイド

## Launchingデータ管理

モバイルアプリで使用するLaunchingデータの設定方法は、次のとおりです。

## 設定情報

Console画面の**設定情報**タブで現在のLaunching情報を照会できます。

![console_configuration_00](https://static.toastoven.net/prod_launching/ja/console_configuration_00.png)

> [参考]
> Launchingサービスを使用すると、上図のようにデフォルトでテンプレートデータを提供します。
> (実際のテンプレートデータは図とは異なる場合があります。)

### フォルダおよびキーの選択と変更

Launching情報の左側にあるエクスプローラウィンドウでフォルダやキーを選択すると、右側に該当フォルダとキー情報が表示されます。選択されたフォルダやキーの名前と説明を変更した後、**確認**ボタンをクリックすると、該当情報が変更されます。
![console_configuration_01](https://static.toastoven.net/prod_launching/ja/console_configuration_01.png)

> [参考]
> **確認**ボタンはConsole内で変更事項を反映したもので、修正された事項をサーバーに反映するには、**配布**タブで配布する必要があります。

> [参考]
> 異なるフォルダにあるキー名は同じ場合がありますが、同じフォルダ内ではキー名は重複できません。例えば、serverフォルダに名前が'ip'のキーは1つだけ許可されますが、clientという別のフォルダでは同じ名前の'ip'キーがありえます。

### キー形式の変更

キーを選択すると、右側に表示されるキー情報から形式を変更できます。配列形式に変更すると、該当キーで任意の文字列形式の値を追加したり削除できます。

![console_configuration_02](https://static.toastoven.net/prod_launching/ja/console_configuration_02.png)

### フォルダおよびキー作業

#### 追加

Launching情報の左側にあるエクスプローラウィンドウでフォルダを選択して右クリックすると現れるメニューで、フォルダおよびキーを追加したり、左側にあるエクスプローラウィンドウの上部にある**フォルダ追加/キー追加**ボタンをクリックしてフォルダおよびキーを追加できます。

![console_configuration_03](https://static.toastoven.net/prod_launching/ja/console_configuration_03.png)

#### コピー、貼り付けおよび削除

Launching情報の左側にあるエクスプローラウィンドウで、フォルダまたはキーを選択した後に現れるメニューで、**コピー/削除/貼り付け**ボタンをクリックして任意の作業を行うことができます。

![console_configuration_04](https://static.toastoven.net/prod_launching/ja/console_configuration_04.png)

> [参考]
> フォルダを削除すると、該当フォルダに属しているすべてのサブフォルダおよびキーが削除されます。

## ロジック

**ロジック**タブをクリックすると、登録されたLaunching情報を変更するためのサーバーロジック情報を確認できます。ロジックは固定されたLaunching情報を動的に変更するためのビジネスロジックを意味します。サーバーで動くため、モバイルアプリのアップデートをせずに変更されたLaunching情報を取得できます。

![console_logic_00](https://static.toastoven.net/prod_launching/ja/console_logic_00.png)

### ロジックの追加

サーバーロジックを追加するには、ロジックが動作する開始時刻および終了時刻、ロジックが適用される条件および結果を入力する必要があります。

条件には、最終結果がBooleanであるJavascriptの条件文を使用できます。
サーバーに登録されたLaunching情報およびLaunching照会APIのGETパラメータ値を一般変数として扱って使用できます。Launching情報は[launching.{folder}.{key}]形式で使用でき、それ以外はすべて一般変数として認識します。

結果はロジックの条件が合っている場合、 Launching情報を変更する設定で[launching.{folder}.{key}]形式で使用できます。

**適用期間**でロジックが適用される時間を設定でき、終了時刻を設定しないでロジックに継続して適用されるようにすることもできます。

![console_logic_01](https://static.toastoven.net/prod_launching/ja/console_logic_01.png)

> [参考]
> Launching情報で結果に指定したキーがない時は新たに追加する、あるいは既存情報を上書きします。

> [注意]
> ロジックの条件は最大1KBを超えられません。また、ロジック結果は1つ以上登録する必要があり、ロジック結果で設定するキーと結果値は最大255バイトを超えられません。

### ロジック修正

登録されたロジックをクリックすると、該当ロジックを修正できます。

![console_logic_02](https://static.toastoven.net/prod_launching/ja/console_logic_02.png)

#### ロジック実行 / 停止

ロジックリストで停止または実行するロジックのチェックボックスを選択した後、上部にある**実行 / 停止**ボタンをクリックしてロジックの状態を変更できます。停止状態のロジックはLaunching情報を修正しません。

#### ロジック削除

ロジックリストから削除するロジックのチェックボックスを選択した後、上部にある**削除**ボタンをクリックしてロジックを削除できます。

> [注意]
> ロジック実行/停止を含むすべての変更事項をサーバーに反映するには、**配布**タブで配布する必要があります。

### ロジックテスト

Launching情報をサーバーに配布する前にロジックをテストできます。Launching情報を呼び出す時、渡したGETパラメータとロジックの適用時刻を設定した後に**ロジックテスト**ボタンをクリックすると、下でロジックが適用されたLaunching情報をあらかじめ確認できます。

複数のパラメータを渡してテストする時は、パラメータの一番右にある**+**ボタンをクリックして、新しいパラメータを登録できます。

![console_logic_03](https://static.toastoven.net/prod_launching/ja/console_logic_03.png)

例えば、図のようにロジックを登録した後にテストを行うと、ロジック結果でテスト結果を確認できます。

ロジックの条件でパラメータ'launching.server.cds'の値が'TEST'の場合、[lauching.server.ip]の値に'127.0.0.1'を入れるように設定しました。ロジックテストの時にGETパラメータを'launching.server.cds'でTESTを設定し、テスト結果で[lauching.server.ip]に'127.0.0.1'値が入ったことを確認できます。

> [参考]
> ロジックテスト結果で黄色で処理された部分は、実際の原本Launching情報からロジックおよびGETパラメータで演算して追加または変更されたキーを意味します。

### サブキー

サブキーは、"launching."で始まり"."で組み合わされるキーで、サブキーを使用するとLaunching情報から一部のデータのみ取得できます。

次の図のようにサブキーを[launching.server]に指定すると、[launching.server]にあるデータのみ取得できます。

![console_logic_04](https://static.toastoven.net/prod_launching/ja/console_logic_04.png)

> [注意]
> 図のようにサブキーもGETパラメータで指定します。"subKey"をキーに設定したGETパラメータは、サブキーとして認識します。

### キーパターン

キーパターンは"$."で始まる特殊なキーで、ロジック条件および結果で使用できます。
全体またはサブキーを使用して伝達された最終結果であるLaunching情報のルートで、相対的な位置を指定します。

次の図のように、ロジックが登録されていると仮定します。

![console_logic_05](https://static.toastoven.net/prod_launching/ja/console_logic_05.png)

このような場合、サブキーを指定しなければロジックが適用されません。

しかしサブキー[launching.server]を指定して一部のデータのみ取得する場合、ロジック条件"$.cds === 'TEST'"を満たすことになり、"$.ip = '127.0.0.1'"により値が変更されます。

![console_logic_06](https://static.toastoven.net/prod_launching/ja/console_logic_06.png)

このようにサブキーおよびキーパターンを使用して、Launching情報を流動的に変更できます。

## インポート

**インポート**タブで、他のプロジェクトのLaunchingサービスに登録されたLaunching情報およびロジックをインポートしたり、**エクスポート**タブの**JSON形式でコピーする**で、コピーしたJSON形式のデータからインポートできます。

他のプロジェクトを選択した後に**インポート実行**ボタンをクリックして、Launching情報およびロジックをインポートできます。

**JSON形式からロード**メニューで、JSON形式のデータからLaunching情報およびロジックをインポートできます。

> [参考]
> **インポート**を実行した後、**設定情報/ロジック**タブでLaunching情報およびロジックを確認してテストできます。インポートを実行すると、**配布**タブで配布を行った時にサーバーに反映されます。

## エクスポート

**エクスポート**タブで、他のプロジェクトのLaunchingサービスにLaunching情報およびロジックをエクスポートしたり、JSON形式のデータにコピーできます。

他のプロジェクトを選択した後、**エクスポート実行**ボタンをクリックすると、Launching情報およびロジックをエクスポートできます。

**JSON形式でコピーする**メニューで、JSON形式のデータをコピーできます。

## 配布

**設定情報**および**ロジック**タブで修正した事項をサーバーに反映するには、**配布**タブで配布を行う必要があります。
**配布**タブでは、配布する前に図のようにLaunching情報およびロジック、説明の修正事項を確認できます。

![console_deploy_00](https://static.toastoven.net/prod_launching/ja/console_deploy_00.png)

**配布**ボタンをクリックして配布を行うとサーバーに反映され、モバイルアプリで変更されたLaunching情報を取得します。
**初期化**ボタンをクリックして、Consoleで修正した内容を元に戻すことができます。

配布を行うと、Consoleで修正する直前のLaunching情報とロジックをバックアップします。**配布**ボタンをクリックしたら、バックアップする名前を指定する必要があります。

### バックアップ履歴の確認

![console_deploy_01](https://static.toastoven.net/prod_launching/ja/console_deploy_01.png)

下部にあるバックアップ履歴で、現在までバックアップされた履歴を確認できます。

**設定情報/ロジック確認**ボタンをクリックしてバックアップされたLaunching情報とロジックを確認でき、復元または削除できます。
