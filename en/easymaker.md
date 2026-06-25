## Machine Learning > AI EasyMaker > Console Guide

## Notebook

Create and manage Jupyter laptop with essential packages installed for machine learning development.

### Notebook List

The status of the notebook is displayed. For key statuses, refer to the table below.

| Status             | Description                                                                                                                                                                              |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | Laptop creation is requested.                                                                                                                                                            |
| CREATE IN PROGRESS | Laptop instance is in the process of creation.                                                                                                                                           |
| ACTIVE (HEALTHY)   | Laptop application is in normal operation.                                                                                                                                               |
| ACTIVE (UNHEALTHY) | Laptop application is not operating properly. If this condition persists after restarting the laptop, please contact customer service center. |
| STOPPED            | The notebook has been stopped.                                                                                                                                                           |

### Save Metric Logs for TensorBoard

To check result metrics on the TensorBoard screen after training, you must set the TensorBoard log storage location to the designated path (`EM_TENSORBOARD_LOG_DIR`) when writing the training script.

<details>
<summary><strong>Example</strong></summary>

```python
import tensorflow as tf

# Specify the TensorBoard log path
tb_log = tf.keras.callbacks.TensorBoard(log_dir=os.environ.get("EM_TENSORBOARD_LOG_DIR"))

model = ... # Model implementation

model.fit(x_train, y_train, validation_data=(x_test, y_test),
        epochs=100, batch_size=20, callbacks=[tb_log])
```

</details>

### Hyperparameter Input Screen

![Hyperparameter input screen](https://static.toastoven.net/prod2_translate-test/en/console-guide_appendix_hyperparameter_ko.png)