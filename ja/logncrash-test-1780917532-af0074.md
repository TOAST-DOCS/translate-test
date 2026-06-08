## Log & Crash レポートテスト

この文書は、翻訳パイプラインが作業完了後に Log & Crash Search にログを正常に送信されるかを確認するための短い韓国語サンプルです。

翻訳結果の品質ではなく、ジョブが終了した時に `jobId`、`sourcePrUrl`、`translationPrUrl`、`longDurationSec` などのフィールドを含む1行のログが収集サーバーに到達したかを検証します。