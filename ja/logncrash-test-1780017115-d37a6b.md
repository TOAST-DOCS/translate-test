## Log & Crash レポートテスト

この文書は、翻訳パイプラインが作業完了後にLog & Crash Searchにログを正常に送信しているかを確認するための短い韓国語サンプルです。

翻訳結果の品質ではなく、ジョブ(job)が終了した時に`jobId`、`sourcePrUrl`、`translationPrUrl`、`longDurationSec`のようなフィールドを含む一行のログが収集サーバーに到達したかを検証します。