## Database > EasyCache > 開発者ガイド

## Clients 接続

* 同じVPC Subnetを利用するインスタンスのアプリケーションから接続できます。
* Redisを基盤に開発したEasyCacheは、多様な開発言語をサポートします。

### JAVA

* Jedisは、JAVA用のRedis Clientです。
* インストールした必要なJarファイルです。
    * jedis-2.9.0.jar
    * commons-pool2-2.4.2.jar
* 接続コード
 ```
 public static void main( String[] args ) {
    Jedis jedis = new Jedis("localhost", 6379);
    jedis.set("foo", "bar");
}
 ```
 
### PHP

* Predisは、PHP用のRedis Clientです。
* 接続コード
```
$client = new Predis\Client('tcp://127.0.0.1:6379');
$client->set('hogehoge','fugafuga');
```
OR
```
$client = new Predis\Client([
    'scheme' => 'tcp',
    'host'   => '192.168.10.33',
    'port'   => 6379,
]);
$client->set('hogehoge','fugafuga');
```

### PYTHON

* redis-pyは、PYTHON用のRedis Clientです。
* redis-pyは下記のようにインストールする必要があります。
```
$ pip install redis
```

* 接続コード
```
import redis

r = r = redis.StrictRedis(host='localhost', port=6379, db=0)
r.set('hoge', 'moge')
```
OR
```
import redis

pool = redis.ConnectionPool(host='localhost', port=6379, db=0)
r = redis.StrictRedis(connection_pool=pool)
r.set('hoge', 'moge')
```

## インスタンスからEasyCache for Redisサーバーに接続

* 同じVPC Subnet内からのみRedisサーバーに接続可能です。
* 同じVPC Subnetにあるインスタンスを作成します。
* Redis Clientを利用するには、各OSにRedisをインストールする必要があります。
    ```
    CentOS 場合
    yum -y install epel-release   
    yum -y install redis
    ```
* インストールが完了したら、正常にインストールできたかを確認します。
    ```
    redis-cli -v
    ```

* 接続したい複製グループを選択し、詳細情報で接続情報タブを押します。
 ![rep_de_005.PNG](https://static.toastoven.net/prod_easycache/20.02.21/rep_connection_info_ja.png)
* プライベート/公認コマンドから選択し、コピーボタンでコマンドをコピーして、インスタンスのコマンドウィンドウに貼り付けます。
* Redisサーバーに接続します。
* パスワードで表示ボタンを押すとパスワードが表示され、コピーボタンが有効になります。
* **コピー**ボタンを押すと、パスワードをコピーします。
* AUTHコマンドを利用して認証を行います。
    * AUTH {コピーしたパスワード}
    
## Restricted Redis commands

* 下記のコマンドを使用すると、サービスに致命的な影響を与える可能性があるため、使用できません。

  * BGREWRITEAOF
  * BGSAVE
  * CONFIG
  * DEBUG
  * MIGRATE
  * SAVE
  * SHUTDOWN
  * SLAVEOF
  * REPLICAOF
  * SYNC

* keyまたはアイテムが多数(数十万個以上)ある時に下記のようなコマンドを使用すると、性能が低下したり、システムが止まる場合があります。

  * KEYS
  * FLUSHALL, FLUSHDB
  * Delete Collections
  * Get All Collections

## メモリ管理

システムメモリの使用率が80%を超える場合、インスタンスのメモリが不足しないように次のような措置を取る必要があります。

* メモリ使用量をモニタリングする必要があります。 EasyCacheアラーム機能を確認してください。
* インスタンスにactivedefragの使用を設定します。
* インスタンスのmaxmemory限度を下げる必要があります。
* 適切なmaxmemory-policyを選択
   * 揮発性データを保存する場合は、volatile-*除去ポリシーの中から1つを選択します。揮発性ではないデータを保存する場合はallkeys-*ポリシーの中から1つを選択します。
* インスタンス拡張案内に従ってインスタンスの容量を増やします。
