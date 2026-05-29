## Machine Learning > AI EasyMaker > Console Guide

## Notebook

Create and manage Jupyter notebooks with essential packages for machine learning development pre-installed.

### Notebook List

The status of notebooks is displayed. Refer to the table below for key statuses.

| Status             | Description                                                                                                                       |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | Notebook creation has been requested.                                                                                             |
| CREATE IN PROGRESS | Notebook instance is being created.                                                                                              |
| ACTIVE (HEALTHY)   | Notebook application is running normally.                                                                                        |
| ACTIVE (UNHEALTHY) | Notebook application is not running normally. If this status persists after restarting the notebook, contact customer support. |
| STOPPED            | Notebook has been stopped.                                                                                                       |

### Saving Metric Logs for TensorBoard

To view result metrics on the TensorBoard screen after training, you must set the TensorBoard log storage location to the specified path (`EM_TENSORBOARD_LOG_DIR`) when writing training scripts.

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

![Hyperparameter Input Screen](https://static.toastoven.net/prod_translate/en/console-guide_appendix_hyperparameter_ko.png)