## Machine Learning > AI EasyMaker > Console Guide

## Notebook

Create and manage Jupyter notebooks with essential packages for machine learning development pre-installed.

### Notebook List

The status of the notebook is displayed. Refer to the table below for the main statuses.

| Status             | Description                                                                                                                                     |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | The notebook creation has been requested.                                                                                                      |
| CREATE IN PROGRESS | The notebook instance is being created.                                                                                                        |
| ACTIVE (HEALTHY)   | The notebook application is running normally.                                                                                                  |
| ACTIVE (UNHEALTHY) | The notebook application is not running normally. If this status persists even after restarting the notebook, contact customer support.      |
| STOPPED            | The notebook has been stopped.                                                                                                                 |

### Storing Metric Logs for TensorBoard Usage

To check result metrics on the TensorBoard screen after training, when writing training scripts, you must set the TensorBoard log storage space to the designated location (`EM_TENSORBOARD_LOG_DIR`).

<details>
<summary><strong>Example</strong></summary>

```python
import tensorflow as tf

# Specify TensorBoard log path
tb_log = tf.keras.callbacks.TensorBoard(log_dir=os.environ.get("EM_TENSORBOARD_LOG_DIR"))

model = ... # Model implementation

model.fit(x_train, y_train, validation_data=(x_test, y_test),
        epochs=100, batch_size=20, callbacks=[tb_log])
```

</details>

### Hyperparameter Input Screen

![하이퍼파리미터 입력 화면](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/en/console-guide_appendix_hyperparameter_ko.png)