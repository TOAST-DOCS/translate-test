## Machine Learning > AI EasyMaker > コンソール使用ガイド

## ノートブック

機械学習開発に必要な必須パッケージがインストールされている Jupyter ノートブックを作成および管理します。

### ノートブックリスト

ノートブックのステータスが表示されます。主要なステータスは次の表を参照してください。

| ステータス         | 説明                                                                                                                              |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | ノートブック生成がリクエストされた状態です。                                                                                      |
| CREATE IN PROGRESS | ノートブックインスタンスを作成中の状態です。                                                                                     |
| ACTIVE (HEALTHY)   | ノートブックアプリケーションが正常に動作している状態です。                                                                        |
| ACTIVE (UNHEALTHY) | ノートブックアプリケーションが正常に動作していない状態です。ノートブックを再起動してもこのステータスが続く場合は、カスタマーサポートにお問い合わせください。 |
| STOPPED            | ノートブックを停止した状態です。                                                                                                 |

### TensorBoard活用のためのメトリクスログ保存

学習後に TensorBoard 画面で結果メトリクスを確認するために、学習スクリプト作成時に TensorBoard ログ保存スペースを指定された場所(`EM_TENSORBOARD_LOG_DIR`)に設定する必要があります。

<details>
<summary><strong>例</strong></summary>

```python
import tensorflow as tf

# TensorBoard ログディレクトリ指定
tb_log = tf.keras.callbacks.TensorBoard(log_dir=os.environ.get("EM_TENSORBOARD_LOG_DIR"))

model = ... # モデル実装

model.fit(x_train, y_train, validation_data=(x_test, y_test),
        epochs=100, batch_size=20, callbacks=[tb_log])
```

</details>

### ハイパーパラメータ入力画面

![ハイパーパラメータ入力画面](http://static.toastoven.net/prod_ai_easymaker/console-guide_appendix_hyperparameter_ko.png)