<!-- pre-align:aligned sig=d558666785f8 -->

<a id="logs"></a>
## ログ { #logs }

**Security > Network Firewall > コンソール使用ガイド > ログ**

**ログ**タブでは、Network Firewallで生成されたログを検索できます。

<br>

<a id="search-logs"></a>
## ログを検索する { #search-logs }

<a id="traffic"></a>
### トラフィック { #traffic }

* Network Firewallを通過する際、許可または遮断ポリシーによって生成されたトラフィックログを検索します。
    * 照会は1か月単位で、最大3か月前までの過去データのみ検索可能です。
        * 最大保存ログ件数は800万件であり、トラフィックの量によって保存されるログの量が異なるため、過去のデータが照会されない場合があります。
    * 別途データ保存が必要な場合は、**オプション**タブの**ログ遠隔送信設定**をご参照ください。

<a id="audit"></a>
### Audit { #audit }

* ポリシーの作成及び削除など、Network Firewallの変更事項に関するログを検索します。
    * 照会は最大1か月単位で検索可能であり、組織サービスであるCloudTrailでも検索できます。

<br>

<a id="download-excel"></a>
## Excelダウンロード { #download-excel }

* **Excelダウンロード**をクリックして、トラフィックとAuditログの検索結果をダウンロードできます。
    * トラフィックログの最大ダウンロード件数は30万件です。
