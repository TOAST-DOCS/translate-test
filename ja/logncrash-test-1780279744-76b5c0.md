## Log & Crash レポートテスト

この文書は、翻訳パイプラインが作業完了後にLog & Crash Searchにログを正常に送信するかを確認するための短い韓国語サンプルです。

翻訳結果の品質ではなく、ジョブ(job)が終了したときに`jobId`、`sourcePrUrl`、`translationPrUrl`、`longDurationSec`のようなフィールドを含む1行のログが収集サーバーに到達したかを検証します。