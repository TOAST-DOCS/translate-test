<!-- machine_translated: true -->

<!-- pre-align:aligned sig=4aaf1d63e79e -->

<a id="security-ddos-guard-l7-ddos-security-configuration-guide"></a>
## Security > DDoS Guard > L7 DDoSセキュリティ設定ガイド { #security-ddos-guard-l7-ddos-security-configuration-guide }

ここでは、L7 DDoS攻撃に効果的に対応するためのセキュリティ設定方法を説明します。

<a id="background"></a>
## 1. 背景 { #background }

* L7 Slow DDoS攻撃の継続的な増加
    * Slowloris、Slow Readなど、ネットワーク帯域幅ではなくアプリケーション層のセッションを長時間占有する攻撃が頻繁に発生しています。
    * 全体のトラフィック量が少なくても、Webサーバーの Connection/Session リソースを急速に枯渇させ、正常なユーザーのアクセスを遮断します。
* 検出難易度の上昇
    * HTTPS暗号化トラフィック内に正常なHTTPリクエストに見せかけて流入するため、単純なL3/L4しきい値(Threshold)ベースのDDoS装置だけでは対応に限界があります。

<a id="purpose"></a>
## 2. 目的 { #purpose }

* 総合的な防御体制の構築
    * サーバー、ネットワーク、アプリケーションなど多重レイヤーのセキュリティポリシーを策定します。
* Webサーバーリソース枯渇の緩和
    * セッションベースの攻撃が流入した際、接続数および待機時間の設定によりサーバーリソースを保護します。
* サービスの可用性(Availability)の確保
    * 適切なセッション維持時間および最大接続数の管理を通じて、正常なサービスの維持を図ります。

<a id="security-measures"></a>
## 3. セキュリティ対策 { #security-measures }

* Webサーバーハードニング(Web Server Hardening)
    * KeepAliveTimeout、RequestReadTimeout、client_body_timeoutなどのセッション設定を最適化し、異常な接続によるリソース占有を最小限に抑えます。
* DDoS装置の国家ベース先行遮断設定
    * 遮断基準: L7 DDoS攻撃によりWebサービスの遅延または障害(アクセス不可)が発生した場合に適用します。
    * 国家基準: 緊急事態発生時に、国内および主要サービス国(例: 韓国、日本など)を除いた海外送信元IPアドレス帯域全体を遮断します。
    * 復旧手順: 攻撃トラフィックの減少および事態収束を確認した後、国家遮断ポリシーを解除して正常サービス状態に復元します。

<a id="security-checklist"></a>
## 4. セキュリティチェックリスト { #security-checklist }

<a id="nginx"></a>
### Nginx { #nginx }

| 番号 | 区分 | 項目 | 確認 | 備考 |
| --- | --- | --- | ---- | ---- |
| 1 | セキュリティソリューション | WEB Firewallを構築・運用しているか？ |  |  |
| 2 | システム | リクエスト速度制限(Rate Limit)が設定されているか？ |  |  |
| 3 | システム | 同時接続制限(Connection Limit)が設定されているか？ |  |  |
| 4 | システム | リクエスト本文サイズ制限が設定されているか？ |  |  |
| 5 | システム | バッファサイズ制限が設定されているか？ |  |  |
| 6 | システム | Keep-Alive制限が設定されているか？ |  |  |
| 7 | システム | リクエスト待機時間制限が設定されているか？ |  |  |
| 8 | システム | HTTP Method制限が設定されているか？ |  |  |
| 9 | システム | 異常なUser-Agentブロックが設定されているか？ |  |  |
| 10 | システム | ステータスモニタリングが設定されているか？ |  |  |
| 11 | システム | キャッシュ設定がされているか？ |  |  |

<a id="apache"></a>
### Apache { #apache }

| 番号 | 区分 | 項目 | 確認 | 備考 |
| --- | --- | --- | ---- | ---- |
| 1 | セキュリティソリューション | WEB Firewallを構築・運用しているか？ |  |  |
| 2 | システム | mod_evasiveが設定されているか？ |  |  |
| 3 | システム | mod_qosが設定されているか？ |  |  |
| 4 | システム | KeepAlive制限が設定されているか？ |  |  |
| 5 | システム | リクエスト本文サイズ制限が設定されているか？ |  |  |
| 6 | システム | Timeout調整が設定されているか？ |  |  |
| 7 | システム | HTTP Method制限が設定されているか？ |  |  |
| 8 | システム | User-Agentフィルタリングが設定されているか？ |  |  |
| 9 | システム | リクエスト速度制限(mod_ratelimit)が設定されているか？ |  |  |
| 10 | システム | ログフォーマット強化が設定されているか？ |  |  |

<a id="netty"></a>
### Netty { #netty }

| 番号 | 区分 | 項目 | 確認 | 備考 |
| --- | --- | --- | ---- | ---- |
| 1 | セキュリティソリューション | WEB Firewallを構築・運用しているか？ |  |  |
| 2 | システム | リクエスト速度制限(Rate Limit)が適用されているか？ |  |  |
| 3 | システム | 同時接続数制限(Connection Limit)が適用されているか？ |  |  |
| 4 | システム | リクエスト本文サイズ制限が設定されているか？ |  |  |
| 5 | システム | ヘッダー/バッファサイズ制限が設定されているか？ |  |  |
| 6 | システム | Keep-Alive / Idle Timeoutが設定されているか？ |  |  |
| 7 | システム | リクエスト処理時間制限が設定されているか？ |  |  |
| 8 | システム | HTTP Method制限が設定されているか？ |  |  |
| 9 | システム | 異常なUser-Agentブロックのロジックがあるか？ |  |  |
| 10 | システム | ステータスモニタリングおよびMetrics収集がされているか？ |  |  |
| 11 | システム | キャッシュまたはレスポンス最適化の適用有無 |  |  |

<a id="security-configuration-guide"></a>
## 5. セキュリティ設定ガイド { #security-configuration-guide }

セキュリティ設定時にWebサービスの障害を最小限に抑えるには、環境を考慮する必要があります。

<a id="security-configuration-guide-nginx"></a>
### Nginx { #security-configuration-guide-nginx }

| 番号 | 項目 | 設定方法 | 内容 | 優先度 | 例 |
| --- | --- | --- | ---- | ---- | ---- |
| 1 | リクエスト速度制限(Rate Limit) | limit_req_zone / limit_req 設定 | IPごとの1秒あたりリクエスト数制限により、過剰なHTTPリクエストを防御 | 必須 | http {<BR>   limit_req_zone $binary_remote_addr zone=req_limit_per_ip:10m rate=5r/s; <BR>} server {<BR>   limit_req zone=req_limit_per_ip burst=10 nodelay; <BR>} |
| 2 | 同時接続制限(Connection Limit) | limit_conn_zone / limit_conn 設定 | 1つのIPから同時に確立できる接続数を制限 | 必須 | http {<BR>   limit_conn_zone $binary_remote_addr zone=conn_limit_per_ip:10m; <BR>} server {<BR>   limit_conn conn_limit_per_ip 10; <BR>} |
| 3 | リクエスト本文サイズ制限 | client_max_body_size 設定 | 大容量POSTリクエストによるリソース枯渇を防止 | 必須 | client_max_body_size 1m; |
| 4 | バッファサイズ制限 | client_body_buffer_size、client_header_buffer_size 設定 | リクエストヘッダー・本文のバッファ使用量を制限(Slowloris攻撃防御) | 必須 | client_body_buffer_size 16k; <BR>client_header_buffer_size 1k; |
| 5 | Keep-Alive制限 | keepalive_timeout 設定 | クライアントのセッション占有時間を制限 | 必須 | keepalive_timeout 10s; |
| 6 | リクエスト待機時間制限 | client_header_timeout、send_timeout 設定 | 遅いリクエスト(Slow HTTP)攻撃を防御 | 必須 | client_header_timeout 10s; <BR>send_timeout 10s; |
| 7 | HTTP Method制限 | if文で許可されたメソッドのみに制限 | 不要なメソッド(TRACE、PUTなど)のリクエストを遮断 | 推奨 | if ($request_method !~ ^(GET\|POST\|HEAD)$) { return 444; } |
| 8 | 異常なUser-Agentブロック | 正規表現でUser-Agentをフィルタリング | スキャナー、ボット、curlなど自動化ツールのアクセスを遮断 | 推奨 | if ($http_user_agent ~* (masscan\|curl\|python\|nmap)) { return 403; } |
| 9 | ステータスモニタリング | stub_status 設定 | リアルタイムのリクエスト数/セッション数を確認(運用点検用) | 推奨 | location /nginx_status {<BR>   stub_status;<BR>   allow 127.0.0.1;<BR>   deny all; <BR>} |
| 10 | キャッシュ設定 | proxy_cache 設定 | 同一リクエストのキャッシュによりバックエンドの負荷を軽減 | 推奨 | proxy_cache_path /tmp/nginx_cache levels=1:2 keys_zone=my_cache:10m; <BR>location / {<BR>   proxy_cache my_cache;<BR>   proxy_cache_use_stale error timeout updating; <BR>} |

<a id="security-configuration-guide-apache"></a>
### Apache { #security-configuration-guide-apache }

| 番号 | 項目 | 設定方法 | 内容 | 優先度 | 例 |
| --- | --- | --- | ---- | ---- | ---- |
| 1 | mod_evasive 設定 | yum install mod_evasive 後、/etc/httpd/conf.d/mod_evasive.conf を設定 | 短時間に多数のリクエストを送信したIPを自動遮断 | 必須 | DOSPageCount 2 <BR>DOSSiteCount 50 <BR>DOSBlockingPeriod 10 |
| 2 | mod_qos 設定 | yum install mod_qos 後、/etc/httpd/conf.d/mod_qos.conf を設定 | IPごとの最大接続数およびリクエスト数を制限 | 必須 | QS_SrvMaxConnPerIP 10 <BR>QS_SrvMaxConnClose 20 <BR>QS_SrvRequestRate 5 |
| 3 | KeepAlive制限 | KeepAliveTimeout 設定 | 長時間の接続維持を防止 | 必須 | KeepAlive On <BR>MaxKeepAliveRequests 100 <BR>KeepAliveTimeout 5 |
| 4 | リクエスト本文サイズ制限 | LimitRequestBody 設定 | 大容量POSTリクエストを制限 | 必須 | LimitRequestBody 1048576 |
| 5 | Timeout調整 | Timeout、RequestReadTimeout 設定 | 遅いリクエスト/レスポンスを遮断 | 必須 | Timeout 10 <BR>RequestReadTimeout header=10-20,MinRate=500 |
| 6 | HTTP Method制限 | <LimitExcept\> ブロックを使用 | 許可されたメソッドのみを許可 | 必須 | <LimitExcept GET POST HEAD\><BR>   Deny from all <BR></LimitExcept\> |
| 7 | User-Agentフィルタリング | SetEnvIfNoCase + Deny | 異常なUser-Agentを遮断 | 推奨 | SetEnvIfNoCase User-Agent "curl" bad_bot <BR>Order Allow,Deny <BR>Allow from all <BR>Deny from env=bad_bot |
| 8 | リクエスト速度制限(mod_ratelimit) | mod_ratelimit を使用 | レスポンス送信速度の制限により過剰なリクエストを抑制 | 推奨 | SetOutputFilter RATE_LIMIT <BR>SetEnv rate-limit 400 |
| 9 | ログフォーマット強化 | LogFormat を修正 | リクエスト、レスポンスサイズ、User-Agentを含めてトレーサビリティを強化 | 推奨 | LogFormat "%h %l %u %t \\"%r\\" %>s %b \\"%{Referer}i\\" \\"%{User-Agent}i\\"" combined |

<a id="security-configuration-guide-netty"></a>
### Netty { #security-configuration-guide-netty }

| 番号 | 項目 | 設定方法 | 内容 | 優先度 | 例 | 備考 |
| --- | --- | --- | ---- | ---- | ---- | ---- |
| 1 | リクエスト速度制限(Rate Limit) | ChannelHandler / Redis / Guava RateLimiter | IPベースのリクエスト数制限 | 必須 | `SimpleRateTracker(5, 10)` | 1秒あたり5〜15個まで許可 |
| 2 | 同時接続制限(Connection Limit) | ChannelGroup / Atomic Counter | IPごとの同時接続を制限 | 必須 | `MAX_CONN_PER_IP = 10` | IPあたりの同時接続数を10個に制限 |
| 3 | リクエスト本文サイズ制限 | HttpObjectAggregator | 大容量POST攻撃を防止 | 必須 | `new HttpObjectAggregator(1024 * 1024)` | POST Bodyリクエストを1MBに制限 |
| 4 | バッファサイズ制限 | HttpServerCodec 設定 | ヘッダー/ライン長を制限 | 必須 | `new HttpServerCodec(4096, 1024, 8192)` | 異常に大きなHeader/URIリクエストを制限(line 4096 / header 1024 / chunk 8192) |
| 5 | Keep-Alive制限 | IdleStateHandler | アイドルセッションイベントを発生 | 必須 | `new IdleStateHandler(10, 10, 10)` | 10秒間イベントが発生しない場合にイベントを発生(読み取り/書き込み/読み取り&書き込み) |
| 6 | リクエスト時間制限 | ReadTimeoutHandler / WriteTimeoutHandler | Slowloris対応 | 必須 | `new ReadTimeoutHandler(10)`<BR>`new WriteTimeoutHandler(10)` |  |
| 7 | HTTP Method制限 | ChannelInboundHandler | 許可されたメソッドのみ処理 | 推奨 | `if (!(request.method().equals(HttpMethod.GET)`<BR>`  \|\| request.method().equals(HttpMethod.POST)`<BR>`  \|\| request.method().equals(HttpMethod.HEAD))) {`<BR>`  ctx.close();`<BR>`  return;`<BR>`}` | GET、POST、HEAD Methodのみ許可 |
| 8 | User-Agentブロック | HandlerでHeaderを検査 | スキャナー/ボットを遮断 | 推奨 | `String ua = request.headers().get("User-Agent");`<BR> `if(ua != null && ua.matches(".(masscan\|curl\|python\|nmap).")) {`<BR>`  ctx.close();`<BR>`  return;`<BR>`}` | masscan/curl/python/nmapパターンを検出 |
| 9 | ステータスモニタリング | Micrometer / Prometheus | TPS、接続数をモニタリング | 推奨 |  |  |
| 10 | キャッシュ設定 | Caffeine / Redis | バックエンドの負荷を軽減 | 推奨 |  |  |

<a id="load-balancer"></a>
### Load Balancer { #load-balancer }

| 番号 | 項目 | 設定方法 | 内容 | 例 | 備考 |
| --- | --- | --- | ---- | ---- | ---- |
| 1 | セッション接続制限 | 接続制限設定 | リスナーが同時に維持するTCPセッション数を指定 | `デフォルト値 : 60,000` <BR>`サービス特性に応じて段階的な調整が必要` |  |
| 2 | Keep-Alive制限 | Keep-Aliveタイムアウト設定 | クライアントおよびサーバーとのセッション維持時間を秒単位で指定 | `デフォルト値 : 300秒` |  |
| 3 | 異常なリクエスト自動ブロック | 無効なリクエスト遮断設定 | HTTPリクエストヘッダーに無効な文字が含まれている場合に遮断 | `デフォルト値 : 有効` |  |