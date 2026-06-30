## Compute > Monitoring > コンソール使用ガイド

## インスタンス状態確認

インスタンス状態を確認するには、まず**Compute > Monitoring > Server Details**でモニタリングするインスタンスを追加します。

**Server名**からサーバーを選択し、 **追加** ボタンをクリックすると詳細情報を確認できます。情報の確認をやめるには、右側にある**削除** ボタンをクリックします。サーバー詳細情報で確認できる情報は次のとおりです。

- Server名：サーバー名前
- IP： IPアドレス
- vCPU： CPU使用量
- メモリ：メモリ使用量
- Disk読み込み：毎秒読み込むディスクバイト
- Disk書き込み：毎秒書き込むディスクバイト
- Network In：毎秒受信するネットワークバイト
- Network Out：毎秒転送するネットワークバイト
- 状態：サーバー状態
- 使用時間：サーバー駆動時間

サーバー状態グラフを見るには**Graph** タブを選択します。

![[図2サーバー状態グラフ]](http：//static.toastoven.net/prod_infrastructure/monitoring/img_102.jpg)

検索期間に応じてグラフに表示されるデータの周期が1分、 5分、 30分、 2時間に自動変更されます。情報の確認をやめるには、サーバーグラフがある場合、**削除** ボタンをクリックします。

> [注意]  
> モニタリングデータの保管周期は最大1か月です。したがってグラフの期間は1か月を超えられません。

## アラームログ確認

**Compute > Monitoring > Alarm Logs**でアラームログリストを確認できます。

ユーザーが登録した臨界値を超えると、発送されたアラームリストを確認できます。特定VMに対するアラームログを確認したい場合は、サーバー名またはIPアドレスを入力後、 **検索** ボタンをクリックします。

## アラーム登録

 **Compute > Monitoring > Alarm Setting**で**追加**をクリックするとアラームを登録できます。

**Alarm追加** ウィンドウでアラームを登録するサーバーを追加して、臨界値と受信者を指定します。

### Server名選択

アラームを登録するサーバーを検索して追加します。

### 臨界値選択

アラームを受け取るインスタンスのシステムリソース、および臨界値を設定します。サポートするマトリックス(metric)にはCPU使用量、メモリ使用量、ディスク使用量、ネットワーク使用量、およびサーバー状態(server status)があります。各マトリックス(metric)の説明と入力が必要な臨界値の形式は次のとおりです。

|パラメータ|	説明|
|---|---|
|CPU|	CPU使用量を意味します。 0～100(%)の間の値を入力する必要があります。|
|メモリ|	メモリ使用量を意味します。 MB単位の絶対値を入力します。|
|Disk Read|	ディスク読み込み使用量を意味します。インスタンスに接続した各々のディスクについてバイト単位の絶対値を入力します。|
|Disk Write|	ディスク書き込み使用量を意味します。インスタンスに接続した各々のディスクについてについてバイト単位の絶対値を入力します。|
|Network In|	受信したネットワーク使用量を意味します。インスタンスに接続した各々のイーサネットインターフェイスについてバイト単位の絶対値を入力します。|
|Network Out|	転送したネットワーク使用量を意味します。インスタンスに接続した各々のイーサネットインターフェイスについてバイト単位の絶対値を入力します。|
|Serverダウン|	サーバーの状態を意味します。ここで言うサーバーの状態は、外部と通信が可能な状態を正常と判断します。該当のMetricは別途の値を入力する必要がありません。|

> [注意]  
> **Server Down**を使用するには、別途のMonitoringエージェントを該当インスタンスにインストールする必要があり、該当インスタンスは外部と通信が可能なネットワークに接続されている必要があります。

1. **Server名**からサーバーを選択し、 **追加** ボタンをクリックします。
2. **+ Alarm追加**をクリックします。
3. **計量** リストから、設定するマトリックスを選択します。
4. **臨界値**から条件を選択し、臨界値を指定します。
5. アラーム受信者を設定するために**受信者**で**編集** ボタンをクリックします。
6. **受信者** ダイアログボックスが現れたらプロジェクトメンバーを追加します。

### 受信者設定

アラームを受け取るプロジェクトメンバーを選択し、アラームを受け取る方法を選択します。

**受信者** 入力ボックスにプロジェクトメンバーEメールを入力し、**追加** ボタンをクリックします。

![[図6 Receiver設定]](http：//static.toastoven.net/prod_infrastructure/monitoring/img_106.png)

## アラーム修正、削除

**Compute > Monitoring > Alarm Setting**でアラームの修正や削除ができます。

アラームを修正するにはリストから修正したいアラーム設定をクリックします。アラーム登録とは異なり、1度にアラームを1つだけ修正できます。残りはアラーム登録と同じです。  
登録したアラームは必要に応じて活性化、または非活性化できます。活性化または非活性化したいアラームをリストから選択した後、**活性/非活性** ボタンをクリックすると、そのアラームを活性化または非活性化できます。
登録したアラームが必要なくなった時は**削除** ボタンをクリックして、そのアラームを削除できます。

## モニタリングエージェントのインストール

モニタリングエージェントはServer Down Metricを使用する時のみ必要です。

### エージェントのダウンロード

[TOAST Downloads](https：//docs.toast.com/en/Download/)ページの**Compute > Monitoring**で**Agent** ファイルをダウンロードします。

```
[root@host-192-168-0-7 ~]# wget http：//static.toastoven.net/toastcloud/sdk_download/monitor/tcc/agent-centos-0.0.2.tgz
--2014-09-17 11：35：31--  http：//static.toastoven.net/toastcloud/sdk_download/monitor/tcc/agent-centos-0.0.2.tgz
Connecting to http：//static.toastoven.net... connected.
HTTP request sent、 awaiting response... 200 OK
Length： 168329 (164K) [application/x-gzip]
Saving to： “agent-centos-0.0.2.tgz”

100%[=======================================================>]
168、329     --.-K/s   in 0.005s

2014-09-17 11：35：31 (35.6 MB/s) - “agent-centos-0.0.2.tgz” saved [168329/168329]
```

### エージェントのインストール

モニタリングエージェントは必ずルート(root)権限でインストールする必要があります。インストールするには、ダウンロードしたファイルを解凍し、 'install.sh'を実行します。

```
[root@host-192-168-0-7 ~]# tar -zxvf agent-centos-0.0.2.tgz
./agent/
./agent/ssl/
./agent/ssl/cert.pem
./agent/ssl/.svn/
./agent/ssl/.svn/entries
./agent/ssl/.svn/text-base/
./agent/ssl/.svn/text-base/key.pem.svn-base
./agent/ssl/.svn/text-base/cert.pem.svn-base
./agent/ssl/.svn/tmp/
./agent/ssl/.svn/tmp/text-base/
./agent/ssl/.svn/tmp/prop-base/
./agent/ssl/.svn/tmp/props/
./agent/ssl/.svn/prop-base/
./agent/ssl/.svn/props/
./agent/ssl/.svn/all-wcprops
./agent/ssl/key.pem
./agent/conf.d/
./agent/conf.d/client.json
./agent/conf.d/rabbitmq.json
./agent/jq
./agent/sensu.repo
./agent/install.sh
./agent/plugins/
./agent/plugins/vm_checks_update.rb
./agent/plugins/VERSION
[root@host-192-168-0-7 ~]# cd agent
[root@host-192-168-0-7 ~]# sh install.sh
```

### エージェント状態確認

'service sensu-client status'コマンドを入力し、下記のように'is running'と表示されたら、正常に動作しているということです。

```
[root@host-192-168-0-7 ~]# /etc/init.d/sensu-client status
sensu-client (pid 9223) is running...
```

もし上の状態ではない場合、 'service sensu-client start'コマンドを利用して、手動で開始できます。

```
[root@host-192-168-0-7 ~]# /etc/init.d/sensu-client start
Starting sensu-client [ OK ]
```

### 注意事項
モニタリングエージェントはオープンソースのプロジェクトであるsensuを利用しました。したがって、ユーザーインスタンスに既に別のsensuエージェントがインストールされていたら、TOASTのモニタリングエージェントを使用できません。  
また /etc/sensu内のファイルを任意で変更または削除する場合、正しく動作しない場合があります。


