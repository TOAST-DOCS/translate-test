## Machine Learning > AI EasyMaker > Console Guide

## Notebook

Create and manage Jupyter laptop with essential packages installed for machine learning development.

### Notebook list

Laptop status is displayed. See the table below for main statuses.

| Status             | Description                                                                                                                       |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| CREATE REQUESTED   | Laptop creation is requested.                                                                                                     |
| CREATE IN PROGRESS | Laptop instance is in the process of creation.                                                                                    |
| ACTIVE (HEALTHY)   | Laptop application is in normal operation.                                                                                        |
| ACTIVE (UNHEALTHY) | Laptop application is not operating properly. If this condition persists after restarting the laptop, please contact customer service center. |
| STOPPED            | Laptop is in a stopped state.                                                                                                     |

### TensorBoard log storage for indicator metrics

To check training results on the TensorBoard screen after training, you must set the TensorBoard log storage location to the specified location (`EM_TENSORBOARD_LOG_DIR`) when writing the training script.

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

### Hyperparameter input screen

![Hyperparameter input screen](http://static.toastoven.net/prod_ai_easymaker/console-guide_appendix_hyperparameter_ko.png)