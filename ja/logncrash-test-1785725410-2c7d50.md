## Log & Crash レポート テスト

このドキュメントは、翻訳パイプラインが作業完了後に Log & Crash Search にログを正常に送信しているかを確認するための短い日本語サンプルです。

翻訳結果の品質ではなく、ジョブ (job) が終了したとき、`jobId`、`sourcePrUrl`、`translationPrUrl`、`longDurationSec` などのフィールドを含む1行のログが収集サーバーに到達したかを検証します。