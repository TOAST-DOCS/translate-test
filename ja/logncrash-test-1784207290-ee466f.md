## Log & Crash レポートテスト

このドキュメントは、翻訳パイプラインがタスク完了後に Log & Crash Search にログを正常に送信するかを確認するための短いサンプルです。

翻訳結果の品質ではなく、ジョブが完了したときに `jobId`、`sourcePrUrl`、`translationPrUrl`、`longDurationSec` などのフィールドを含む 1 行のログが収集サーバーに到達したかどうかを検証します。