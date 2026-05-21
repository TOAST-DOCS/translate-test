## Machine Learning > AI EasyMaker > コンソール使用ガイド

## ノートブック

機械学習開発に必要な基本パッケージがインストールされているJupyter(ジュピター)ノートブックを作成および管理します。

### ノートブックリスト

ノートブックの状態が表示されます。主な状態は以下の表を参照してください。

| 状態               | 説明                                                                                                                              |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | ノートブックの作成がリクエストされた状態です。                                                                                                  |
| CREATE IN PROGRESS | ノートブックインスタンスを作成中の状態です。                                                                                           |
| ACTIVE (HEALTHY)   | ノートブックアプリケーションが正常に起動している状態です。                                                                            |
| ACTIVE (UNHEALTHY) | ノートブックアプリケーションが正常に起動していない状態です。ノートブックを再起動した後もこの状態が継続する場合はカスタマーサポートにお問い合わせください。 |
| STOPPED            | ノートブックを停止した状態です。                                                                                                       |

### TensorBoardの活用のための指標ログ保存

学習後TensorBoard画面で結果指標を確認するため、学習スクリプト作成時にTensorBoardログ保存スペースを指定された場所(`EM_TENSORBOARD_LOG_DIR`)に設定する必要があります。

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

![ハイパーパラメータ入力画面](http://static.toastoven.net/prod_ai_easymaker/console-guide_appendix_hyperparameter_ko.png)