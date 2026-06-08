## Machine Learning > AI EasyMaker > Console Guide

## Notebook

You can create and manage Jupyter notebooks with essential packages pre-installed for machine learning development.

### Notebook List

The status of notebooks is displayed. See the table below for the main statuses.

| Status             | Description                                                                                                                                    |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | Notebook creation has been requested.                                                                                                         |
| CREATE IN PROGRESS | The notebook instance is being created.                                                                                                       |
| ACTIVE (HEALTHY)   | The notebook application is running normally.                                                                                                 |
| ACTIVE (UNHEALTHY) | The notebook application is not running normally. If this status persists even after restarting the notebook, contact customer support. |
| STOPPED            | The notebook is stopped.                                                                                                                      |

### Saving Metric Logs for TensorBoard Use

To view result metrics in the TensorBoard screen after training, you must set the TensorBoard log storage location to the designated path (`EM_TENSORBOARD_LOG_DIR`) when writing training scripts.

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

![Hyperparameter input screen](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/en/console-guide_appendix_hyperparameter_ko.png)