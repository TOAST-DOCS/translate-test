## Machine Learning > AI EasyMaker > Console Guide

## Notebook

Create and manage Jupyter notebooks with essential packages installed for machine learning development.

### Notebook List

The status of the notebook is displayed. Refer to the table below for major status values.

| Status             | Description                                                                                                                     |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | The state where notebook creation has been requested.                                                                           |
| CREATE IN PROGRESS | The state where a notebook instance is being created.                                                                           |
| ACTIVE (HEALTHY)   | The state where the notebook application is running normally.                                                                   |
| ACTIVE (UNHEALTHY) | The state where the notebook application is not running normally. If this state persists even after restarting the notebook, please contact customer support. |
| STOPPED            | The state where the notebook has been stopped.                                                                                 |

### Saving Metric Logs for TensorBoard Usage

To check the result metrics on the TensorBoard screen after training, when writing the training script, you must set the TensorBoard log storage location to the specified location (`EM_TENSORBOARD_LOG_DIR`).

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

![Hyperparameter input screen](http://static.toastoven.net/prod_ai_easymaker/console-guide_appendix_hyperparameter_ko.png)