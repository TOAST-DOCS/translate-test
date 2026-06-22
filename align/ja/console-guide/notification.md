## 通知

**Database > EasyCache > コンソール利用ガイド > 通知**

通知グループを使用して、パフォーマンス指標に関する通知を受け取ることができます。**通知タイプ**と**有効状態**を選択した後、監視対象ノードと通知を受け取るユーザーグループを指定します。**監視設定**で、通知を受け取るパフォーマンス指標のしきい値と条件を設定します。設定された指標が監視設定の条件を満たすと、関連付けられたユーザーグループに通知を送信します。通知グループに設定された通知タイプに応じて、SMSまたはメールで通知を送信します。

#### 通知グループの作成

![notification1.PNG](https://static.toastoven.net/prod_easycache/25.09.27/notification1.PNG)

❶: **通知グループ作成**をクリックすると、通知グループを作成できるポップアップ画面が表示されます。
❷: 通知を受け取る方法を選択します。
❸: **有効状態**を**いいえ**に選択した通知グループは、通知を送信しません。
❹: 監視する対象ノードを選択します。
❺: 通知を受け取るユーザーグループを選択します。

### 監視設定

監視設定は、監視項目、比較方法、しきい値及び持続時間で構成されます。監視項目のパフォーマンス指標値としきい値を比較して、条件を満たしているか判断します。条件を持続時間以上連続して満たすと、通知を送信します。例えば、CPU使用率のしきい値が90%以上で持続時間が5分である場合、該当の通知グループと連動したノードのCPU使用率が90%以上の状態が5分以上持続した時、ユーザーグループに定義されたユーザーに通知を送信します。もしCPU使用率が90%以上になっても、5分以内に90%未満に下がった場合は通知が発生しません。

#### 監視設定項目

監視可能なパフォーマンス指標項目は次のとおりです。

| カテゴリー | 項目 | 単位 |
| - | - | - | 
| CPU | CPU_USAGE | % | 
| CPU  | CPU_USAGE_IOWAIT | % | 
| CPU  | CPU_USAGE_NICE | % | 
| CPU  | CPU_USAGE_SYSTEM | % | 
| CPU  | CPU_USAGE_USER | % |
| CPU  | LOAD_AVG_1M |  |
| CPU  | LOAD_AVG_5M |  |
| CPU  | LOAD_AVG_15M |  |
| MEMORY | MEMORY_USAGE | % |
| MEMORY | MEMORY_USED | Bytes |
| MEMORY | MEMORY_FREE | Bytes |
| MEMORY | MEMORY_BUFFERS | Bytes |
| MEMORY | MEMORY_CACHED | Bytes |
| MEMORY | SWAP_USED | Bytes |
| MEMORY | SWAP_TOTAL | Bytes |
| NETWORK | NETWORK_SENT | Bytes/sec | 
| NETWORK | NETWORK_RECV | Bytes/sec |  
| STORAGE | STORAGE_FREE_BYTE | Bytes |  
| STORAGE  | STORAGE_IO_READ_TOTAL | Bytes/sec |  
| STORAGE  | STORAGE_IO_WRITE_TOTAL | Bytes/sec |  
| STORAGE  | STORAGE_IO_READ | % |  
| STORAGE  | STORAGE_IO_WRITE | Bytes |  
| STORAGE  | LINUX_DISK_FAULT |  |  
| REDIS | REDIS_CONNECTED_CLIENTS |  |  
| REDIS | REDIS_CONNECTED_SLAVES |  |  
| REDIS | REDIS_USED_MEMORY_RATE | % |  
| REDIS | REDIS_USED_MEMORY_RSS_RATE | % |  
| REDIS | REDIS_MEM_FRAGMENTATION_RATIO | % |  
| REDIS | REDIS_INSTANTANEOUS_OPS_PER_SEC | ops/sec |  
| REDIS | REDIS_HIT_RATE | % |  
| REDIS | REDIS_KEYS |  |  
| REDIS | REDIS_DELTA_BLOCKED_CLIENTS |  |  
| REDIS | REDIS_DELTA_NET_INPUT_BYTES | Bytes |  
| REDIS | REDIS_DELTA_NET_OUTPUT_BYTES | Bytes |  
| REDIS | REDIS_EXPIRED_KEYS |  |   
| REDIS | REDIS_EVICTED_KEYS |  |   
| REDIS | REDIS_KEYSPACE_HITS |  |   
| REDIS | REDIS_KEYSPACE_MISSES |  |     
| REDIS | REDIS_DELTA_CMDSTAT_GET_USEC_PER_CALL | ms |  
| REDIS | REDIS_DELTA_CMDSTAT_SET_USEC_PER_CALL | ms |  
| REDIS | REDIS_DELTA_CMDSTAT_GET_CALLS |  |  
| REDIS | REDIS_DELTA_CMDSTAT_SET_CALLS |  |  
| REDIS | REDIS_DELTA_CMDSTAT_HGET_CALLS |  |  
| REDIS | REDIS_DELTA_CMDSTAT_HSET_CALLS |  |  

#### 監視設定の追加

![notification2.PNG](https://static.toastoven.net/prod_easycache/25.09.27/notification2.PNG)

❶ **監視設定**を押すと、監視設定を変更できるポップアップ画面が表示されます。
❷ **監視設定追加**を押して、新規の監視設定を追加します。
❸ 監視する項目と比較方法、しきい値、持続時間を入力した後、**追加**をクリックします。

#### 監視設定の変更及び削除

![notification3.PNG](https://static.toastoven.net/prod_easycache/25.09.27/notification3.PNG)

❶ ボタンをクリックすると、追加された監視設定を変更できます。
❷ ボタンをクリックすると、追加された監視設定を削除できます。

### ユーザーグループ

通知を受け取るユーザーをグループとして管理できます。通知対象は必ずプロジェクトメンバーとして登録されている必要があります。ユーザーグループに属するユーザーがプロジェクトメンバーから除外されると、ユーザーグループに属していても通知を受け取ることができません。

!!! danger "注意"
実名認証を行っておらず、携帯電話情報がない場合、SMS通知を受け取ることはできません。

#### ユーザーグループの作成

![notification4.PNG](https://static.toastoven.net/prod_easycache/25.09.27/notification4.PNG)

❶ **ユーザーグループ作成**を押すと、ユーザーグループを作成できるポップアップ画面が表示されます。
❷ **通知方法**項目のプロジェクト全体メンバー項目を選択すると、プロジェクトに属する全員が自動的に反映されます。
❸ **通知方法**項目のユーザー指定項目を選択すると、ユーザーグループに通知対象リストが表示されます。
❹ **追加**を押すと、通知対象に追加できるプロジェクトのメンバーが表示されます。
❺ **確認**を押してユーザーグループを作成します。

#### ユーザーグループの修正及び削除

![notification5.PNG](https://static.toastoven.net/prod_easycache/25.09.27/notification5.PNG)

❶ ボタンをクリックすると、追加されたユーザーグループを修正できます。
❷ ボタンをクリックすると、追加されたユーザーグループを削除できます。