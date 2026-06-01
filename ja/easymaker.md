## Machine Learning > AI EasyMaker > コンソール使用ガイド

## ノートブック

Machine Learning開発に必要なパッケージがインストールされているJupyterノートブックを作成して管理します。

### ノートブックリスト

ノートブックのステータスが表示されます。主なステータスは下記の表を参考してください。

| ステータス         | 説明                                                                                                                                   |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | ノートブック作成がリクエストされた状態です。                                                                                           |
| CREATE IN PROGRESS | ノートブックインスタンスを作成中の状態です。                                                                                           |
| ACTIVE (HEALTHY)   | ノートブックアプリケーションが正常に稼働中の状態です。                                                                                 |
| ACTIVE (UNHEALTHY) | ノートブックアプリケーションが正常に稼働していない状態です。ノートブックを再起動した後もこの状態が続く場合は、カスタマーサポートにお問い合わせください。 |
| STOPPED            | ノートブックを停止した状態です。                                                                                                       |

### TensorBoard活用のための指標ログ保存

学習後TensorBoard画面で結果指標を確認するため、学習スクリプト作成時にTensorBoardログ保存場所を指定された位置(`EM_TENSORBOARD_LOG_DIR`)に設定する必要があります。

<details>
<summary><strong>例</strong></summary>

```python
import tensorflow as tf

# TensorBoardログパス指定
tb_log = tf.keras.callbacks.TensorBoard(log_dir=os.environ.get("EM_TENSORBOARD_LOG_DIR"))

model = ... # モデル実装

model.fit(x_train, y_train, validation_data=(x_test, y_test),
        epochs=100, batch_size=20, callbacks=[tb_log])
```

</details>

### ハイパーパラメータ入力画面

![ハイパーパラメータ入力画面](https://static.toastoven.net/translate-test/ja/console-guide_appendix_hyperparameter_ko.png)