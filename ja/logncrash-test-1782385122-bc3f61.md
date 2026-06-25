## Log & Crash レポートテスト

このドキュメントは、翻訳パイプラインがジョブ完了後に Log & Crash Search へログを正常に送信するかどうかを確認するための短い韓国語サンプルです。

翻訳結果の品質ではなく、ジョブが終了したときに `jobId`、`sourcePrUrl`、`translationPrUrl`、`longDurationSec` などのフィールドを含む1行のログが収集サーバーに到達したかどうかを検証します。