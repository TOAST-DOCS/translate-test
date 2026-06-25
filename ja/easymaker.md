## Machine Learning > AI EasyMaker > コンソール使用ガイド

## ノートパソコン

機械学習開発に必要なパッケージがインストールされている Jupyter ノートパソコンを作成および管理します。

### ノートパソコン一覧

ノートパソコンのステータスが表示されます。主なステータスについては、以下の表を参照してください。

| ステータス         | 説明                                                                                                                              |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | ノートパソコンの作成がリクエストされた状態です。                                                                                  |
| CREATE IN PROGRESS | ノートパソコンのインスタンスを作成中の状態です。                                                                                  |
| ACTIVE (HEALTHY)   | ノートパソコンのアプリケーションが正常に稼働中の状態です。                                                                        |
| ACTIVE (UNHEALTHY) | ノートパソコンのアプリケーションが正常に稼働していない状態です。ノートパソコンを再起動しても、この状態が続く場合はカスタマーサポートにお問い合わせください。 |
| STOPPED            | ノートパソコンを停止した状態です。                                                                                                |

### TensorBoard 活用のための指標ログ保存

学習後に TensorBoard 画面で結果指標を確認するために、学習スクリプト作成時に TensorBoard のログ保存先を指定の場所（`EM_TENSORBOARD_LOG_DIR`）に設定する必要があります。

<details>
<summary><strong>例</strong></summary>

```python
import tensorflow as tf

# TensorBoard ログパスを指定
tb_log = tf.keras.callbacks.TensorBoard(log_dir=os.environ.get("EM_TENSORBOARD_LOG_DIR"))

model = ... # モデルの実装

model.fit(x_train, y_train, validation_data=(x_test, y_test),
        epochs=100, batch_size=20, callbacks=[tb_log])
```

</details>

### ハイパーパラメータ入力画面

![ハイパーパラメータ入力画面](https://static.toastoven.net/prod2_translate-test/ja/console-guide_appendix_hyperparameter_ko.png)