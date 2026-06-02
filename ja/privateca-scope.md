# コンソール使用ガイド
**Management > Private CA > コンソール使用ガイド**

Private CAコンソールは、認証機関(certificate authority, CA)を中心に構成されており、すべてのリソース(証明書テンプレート、発行者、証明書、ACMEトークン)は特定のストレージに属します。コンソール画面は、左側にストレージリスト、右側に選択したストレージの詳細情報を表示するタブ構造になっています。

## Private CA使用フロー

Private CAで証明書を発行するまでの過程は次の通りです。

1. **ストレージ作成**: 証明書を管理するスペースを作ります。
2. **発行者作成**: 証明書に署名する認証機関(CA)を作ります。
    - Root CA: 最上位認証機関
    - Intermediate CA: Root CA下の中間認証機関
3. **証明書テンプレート作成**: 同じ設定で複数の証明書を発行する時に使用します。
4. **証明書発行**: 証明書テンプレートを通じて実際に使用する証明書を発行します。

!!! tip "知っておくべきこと"
    - **CA(certificate authority, 認証機関)**: 証明書を発行し署名する主体です。
    - **Root CA**: 自己署名した最上位証明書です。すべての信頼の出発点です。
    - **Intermediate CA**: Root CAによって署名された中間証明書です。実際のサーバー証明書発行に使用されます。

![Private CAコンソール画面](https://static.toastoven.net/prod2_translate-test/ja/privateca.png)

## 追加画像

![事前存在画像(PR未含)](../images/preexisting.png)

![外部スクリーンショット(PR未含)](http://static.toastoven.net/prod_ai_easymaker/console-guide_appendix_hyperparameter_ko.png)