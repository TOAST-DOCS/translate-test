<!-- pre-align:aligned sig=924ab8b473ea -->

# ログ

**セキュリティ > Cloud Access > コンソール使用ガイド > ログ**

**ログ**タブでは、Cloud Accessサービスの運用中に発生するさまざまなログをリアルタイムで検索できます。

<br>

<a id="traffic"></a>
## トラフィック { #traffic }

![traffic_log.PNG](../../static/images/2025.06.24/traffic_log.png)

ユーザーがエージェントを使用してCloud Access経由でインスタンスに接続する際に発生する通信トラフィックログを検索できます。
* 過去最大3か月間、1か月単位でログを検索可能です。

<br>

<a id="audit"></a>
## 監査（Audit） { #audit }

![audit_log.PNG](../../static/images/2025.06.24/audit_log.png)

ポリシーの作成や削除など、Cloud Accessサービスの変更履歴に関するログを検索できます。
* 最大1か月単位で検索可能で、組織サービスである CloudTrail からも検索できます。

<br>

<a id="user"></a>
## ユーザー { #user }

![audit_log.PNG](../../static/images/2025.06.24/user_log.png)

ユーザーがCloud Accessを使用している間に、エージェントで発生したすべてのログを検索できます。

<br>

<a id="download-as-excel"></a>
## Excelダウンロード { #download-as-excel }

検索結果をExcelファイルとしてダウンロードできます。

<br>

!!! tip "ポイント"
    * トラフィックログは最大7日間または5万件まで保存され、いずれかの条件を超えると、古いログから順に削除（上書き）されます。
        * ログを長期間保存する必要がある場合は、**設定**タブの**ログのリモート送信設定**を利用することをおすすめします。