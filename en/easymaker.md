## Machine Learning > AI EasyMaker > Console User Guide

## Notebook

Create and manage Jupyter notebooks with essential packages installed for machine learning development.

### Notebook List

The status of notebooks is displayed. Refer to the table below for major status types.

| Status             | Description                                                                                                                                          |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | A notebook creation has been requested.                                                                                                             |
| CREATE IN PROGRESS | A notebook instance is being created.                                                                                                               |
| ACTIVE (HEALTHY)   | The notebook application is running normally.                                                                                                       |
| ACTIVE (UNHEALTHY) | The notebook application is not running normally. If this status persists after restarting the notebook, contact customer support.              |
| STOPPED            | The notebook has been stopped.                                                                                                                      |

### Saving Metric Logs for TensorBoard Utilization

To check result metrics on the TensorBoard screen after training, you must set the TensorBoard log storage location to the designated path (`EM_TENSORBOARD_LOG_DIR`) when writing training scripts.

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

![Hyperparameter Input Screen](https://static.toastoven.net/translate-test/en/console-guide_appendix_hyperparameter_ko.png)