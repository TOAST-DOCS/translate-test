<a id="ai.easymaker.console.guide"></a>

## Machine Learning > AI EasyMaker > Console Guide

<a id="dashboard"></a>

## Dashboard

You can check the usage status of all AI EasyMaker resources in the Dashboard.

<a id="dashboard.service.usage.status"></a>

### Service Usage Status

Displays the number of resources in use by resource type.

- Notebooks: Number of notebooks in ACTIVE (HEALTHY) status
- Training: Number of completed training jobs
- Hyperparameter Tuning: Number of completed hyperparameter tuning jobs
- Endpoints: Number of endpoints in ACTIVE status

<a id="dashboard.service.monitoring"></a>

### Service Monitoring

- Displays the top 3 endpoints with the most API calls.
- When you select an endpoint, you can view the API success/failure metrics for the subordinate endpoint stages.

<a id="dashboard.resource.usage"></a>

### Resource Usage

- You can check the most used resources by CPU and GPU core type.
- When you hover your mouse pointer over a metric, resource information is displayed.

<a id="notebook"></a>

## Notebook

Create and manage Jupyter notebooks with essential packages installed for machine learning development.

<a id="notebook.create"></a>

### Create Notebook

Create a Jupyter notebook.

- **Image**: Select the OS image to be installed on the notebook instance.
    - **Core Type**: The CPU and GPU core type of the image is displayed.
    - **Framework**: The framework installed on the image is displayed.
        - TENSORFLOW: Image with TensorFlow deep learning framework installed.
        - PYTORCH: Image with PyTorch deep learning framework installed.
        - PYTHON: Image with only Python language installed without any deep learning framework.
    - **Framework Version**: The version of the framework installed on the image is displayed.
    - **Python Version**: The Python version installed on the image is displayed.

- **Notebook Information**
    - Enter the name and description of the notebook.
    - Select the instance type for the notebook. The specifications of the instance are determined by the selected type.

- **Storage**
    - Specify the boot storage and data storage size for the notebook.
        - Boot storage is where the Jupyter notebook and default virtual environment are installed. This storage is reset when you restart the notebook.
        - Data storage is block storage mounted on the `/root/easymaker` directory path. Data in this storage is retained even after restarting the notebook.
    - The storage size of a created notebook cannot be changed, so you must specify a sufficient storage size at creation time.
    - If needed, you can attach an **NHN Cloud NAS** to connect to the notebook.
        - Mount Directory Name: Enter the name of the directory to mount on the notebook.
        - NHN Cloud NAS Path: Enter the directory path in the format `nas://{NAS ID}:/{path}`.

!!! tip "Note"
    Notebook creation may take a few minutes.
    When creating resources for the first time, additional time is required for service environment configuration.

!!! danger "Caution"
    Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.

<a id="notebook.list"></a>

### Notebook List

The notebook list is displayed. When you select a notebook from the list, you can view detailed information and modify it.

- **Name**: The notebook name is displayed. Click **Change** on the detail screen to change the name.
- **Status**: The notebook status is displayed. Refer to the table below for major statuses.

    | Status             | Description                                                                                                                                          |
    | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED   | Notebook creation has been requested.                                                                                                               |
    | CREATE IN PROGRESS | The notebook instance is being created.                                                                                                             |
    | ACTIVE (HEALTHY)   | The notebook application is running normally.                                                                                                       |
    | ACTIVE (UNHEALTHY) | The notebook application is not running normally. If this status persists after restarting the notebook, contact customer support.                 |
    | STOP IN PROGRESS   | The notebook is being stopped.                                                                                                                      |
    | STOPPED            | The notebook has been stopped.                                                                                                                      |
    | START IN PROGRESS  | The notebook is being started.                                                                                                                      |
    | REBOOT IN PROGRESS | The notebook is being rebooted.                                                                                                                     |
    | DELETE IN PROGRESS | The notebook is being deleted.                                                                                                                      |
    | CREATE FAILED      | Notebook creation failed. If creation continues to fail, contact customer support.                                                                  |
    | STOP FAILED        | Notebook stop failed. Try again.                                                                                                                    |
    | START FAILED       | Notebook start failed. Try again.                                                                                                                   |
    | REBOOT FAILED      | Notebook reboot failed. Try again.                                                                                                                  |
    | DELETE FAILED      | Notebook deletion failed. Try again.                                                                                                                |

- **Actions > Open Jupyter Notebook**: Click the **Open Jupyter Notebook** button to open the notebook in a new browser window. The notebook is accessible only to users logged in to the console.

- **Monitoring**: When you select a notebook, you can view the monitoring target instance list and basic metric charts in the **Monitoring** tab of the detail screen.
    - The **Monitoring** tab is disabled when the notebook is being created or has ongoing tasks.

<a id="notebook.user.virtual.run.environment.configuration"></a>

### User Virtual Execution Environment Configuration

AI EasyMaker notebook instances provide a default Conda virtual environment with various libraries and kernels required for machine learning.
The default Conda virtual environment is reset and runs when you stop and start the notebook. However, virtual environments and external libraries installed by users in arbitrary paths are not automatically reset, so they are not retained when the notebook is stopped and started.
To resolve this issue, you must create virtual environments in the `/root/easymaker/custom-conda-envs` directory path and install external libraries in the created virtual environment.
AI EasyMaker notebook instances support initialization and operation of virtual environments created in the `/root/easymaker/custom-conda-envs` directory path when the notebook is stopped and started.

Follow the guide below to configure your user virtual environment.

1. Click **Open Jupyter Notebook** > **Jupyter Notebook > Launcher > Terminal** from the console notebook menu.
2. Navigate to the `/root/easymaker/custom-conda-envs` path.

        cd /root/easymaker/custom-conda-envs

3. To create a virtual environment named `easymaker_env` with Python 3.8, execute the `conda create` command as follows:

        conda create --prefix ./easymaker_env python=3.8

4. You can verify the created virtual environment with the `conda env list` command.

        (base) root@nb-xxxxxx-0:~# conda env list
        # conda environments:
        #
                                /opt/intel/oneapi/intelpython/latest
                                /opt/intel/oneapi/intelpython/latest/envs/2022.2.1
        base                *   /opt/miniconda3
        easymaker_env           /root/easymaker/custom-conda-envs/easymaker_env

<a id="notebook.user.script"></a>

### User Script

You can register scripts to be automatically executed when the notebook is stopped and started in the `/root/easymaker/cont-init.d` path.
Scripts are executed in ascending alphanumeric order.

- Script Location and Permissions
    - Only files located in the `/root/easymaker/cont-init.d` path are executed.
    - Only scripts with execute permissions are executed.
- Script Content
    - The first line of the script must start with `#!`.
    - Scripts are executed with root privileges.
- Script execution logs are saved in the following locations:
    - Script exit code: `/root/easymaker/cont-init.d/{SCRIPT}.exitcode`
    - Script standard output and standard error stream: `/root/easymaker/cont-init.d/{SCRIPT}.output`
    - Full execution log: `/root/easymaker/cont-init.output`

<a id="notebook.stop"></a>

### Stop Notebook

Stop a running notebook or start a stopped notebook.

1. Select the notebook you want to start or stop from the notebook list.
2. Click **Start Notebook** or **Stop Notebook**.
3. The requested action cannot be canceled. Click **OK** to proceed.

!!! tip "Note"
    Starting and stopping the notebook may take a few minutes.

!!! danger "Caution"
    Virtual environments and external libraries created by users may be reset when you stop and start the notebook.
    To maintain virtual environments and external libraries when starting the notebook after stopping, refer to [User Virtual Execution Environment Configuration](#notebook.user.virtual.run.environment.configuration) to configure your user virtual environment.

<a id="notebook.instance.type.change"></a>

### Change Notebook Instance Type

Change the instance type of a created notebook.
The instance type can only be changed to an instance type with the same core type as the existing instance.

1. Select the notebook for which you want to change the instance type.
2. If the notebook is in a running state (ACTIVE), click **Stop Notebook** to stop the notebook.
3. Click **Change Instance Type**.
4. Select the instance type to change to and click OK.

!!! tip "Note"
    Changing the instance type may take a few minutes.

<a id="notebook.reboot"></a>

### Reboot Notebook

If you encounter issues while using the notebook, or if the status is normal (ACTIVE) but you cannot access the notebook,
you can reboot the notebook.

1. Select the notebook to reboot.
2. Click **Reboot Notebook**.
3. The requested deletion action cannot be canceled. Click **OK** to proceed.

!!! danger "Caution"
    Virtual environments and external libraries created by users may be reset when you reboot the notebook.
    To maintain virtual environments and external libraries when rebooting the notebook, refer to [User Virtual Execution Environment Configuration](#notebook.user.virtual.run.environment.configuration) to configure your user virtual environment.

<a id="notebook.delete"></a>

### Delete Notebook

Delete a created notebook.

1. Select the notebook to delete from the list.
2. Click **Delete Notebook**.
3. The requested deletion action cannot be canceled. Click **OK** to proceed.

!!! tip "Note"
    When you delete a notebook, the boot storage and data storage are deleted.
    Connected NHN Cloud NAS is not deleted and must be deleted individually from **NHN Cloud NAS**.

<a id="experiment"></a>

## Experiment

Experiments manage related training by grouping them together as experiments.

<a id="experiment.create"></a>

### Create Experiment

1. Click **Create Experiment**.
2. Enter the experiment name and description, then click **Confirm**.

!!! tip "Note"
    Creating an experiment may take several minutes.
    When creating resources for the first time, additional time is required to set up the service environment.

<a id="experiment.list"></a>

### Experiment List

The experiment list is displayed. When you select an experiment from the list, you can view detailed information and modify the information.

- **Status**: The status of the experiment is displayed. Refer to the table below for major statuses.

    | Status             | Description                                              |
    | ------------------ | -------------------------------------------------------- |
    | CREATE REQUESTED   | The experiment creation has been requested.              |
    | CREATE IN PROGRESS | The experiment is being created.                         |
    | CREATE FAILED      | The experiment creation failed. Please try again.        |
    | ACTIVE             | The experiment has been created successfully.            |

- **Actions**
    - Click **Go to TensorBoard** to open TensorBoard in a new browser window where you can view statistical information about the training included in the experiment. TensorBoard is accessible only to users logged into the console.
    - **Retry**: If the experiment status is failed, you can click **Retry** to recover the experiment.
- **Training**: When you select training, the **Training** tab in the displayed detail screen shows a list of training included in the experiment.

<a id="experiment.delete"></a>

### Delete Experiment

Delete an experiment.

1. Select the experiment to delete.
2. Click **Delete Experiment**. You cannot delete an experiment if it is in the creation state.
3. The requested deletion cannot be canceled. Click **Confirm** to proceed.

!!! tip "Note"
    You cannot delete an experiment if there are pipeline schedules associated with it, or if there are training, hyperparameter tuning, or pipeline executions in progress or being created.
    Delete resources associated with the experiment before deleting the experiment.
    Associated resources can be viewed in the detail screen at the bottom that appears when you click the experiment you want to delete.

<a id="training"></a>

## Training

Provides an environment where you can train machine learning algorithms and view training results through statistics.

<a id="training.create"></a>

### Create Training

Set up the training environment by selecting the instance and OS image on which training will be performed, then proceed with training by entering algorithm information and input/output data paths.

- **Training Template**: To load a training template and configure training information, select 'Use' and then select the training template to load.
- **Basic Information**: Select basic information about the training and the experiment that will contain the training.
    - **Training Name**: Enter the training name.
    - **Training Description**: Enter a description.
    - **Experiment**: Select the experiment that will contain the training. An experiment groups related trainings. If no experiment has been created, click **Add** to create an experiment.
- **Algorithm Information**: Enter information about the algorithm you want to train.
    - **Algorithm Type**: Select the algorithm type.
        - **NHN Cloud Provided Algorithm**: Uses algorithms provided by AI EasyMaker. For detailed information on provided algorithms, see the [NHN Cloud Provided Algorithm Guide](./algorithm-guide/#) documentation.
            - **Algorithm**: Select the algorithm.
            - **Hyperparameters**: Enter the hyperparameter values required for training. For detailed information on hyperparameters by algorithm, see the [NHN Cloud Provided Algorithm Guide](./algorithm-guide/#) documentation.
            - **Algorithm Metrics**: Information about metrics generated by the algorithm is displayed.
        - **Custom Algorithm**: Uses an algorithm written by the user.
            - **Algorithm Path**
                - **NHN Cloud Object Storage**: Enter the path of NHN Cloud Object Storage where the algorithm is saved.<br>
                    - Enter the directory path in the format obs://{Object Storage API endpoint}/{containerName}/{path}.
                    - When using NHN Cloud Object Storage, refer to [Appendix > 1. Adding AI EasyMaker System Account Permission to NHN Cloud Object Storage](#appendix.1.object.storage.account.permission) to configure permissions. If the required permissions are not set, model creation will fail.
                - **NHN Cloud NAS**: Enter the NHN Cloud NAS path where the algorithm is saved. <br>
                    Enter the directory path in the format nas://{NAS ID}:/{path}.

            - **Entry Point**
                - The entry point is the entry point of algorithm execution where training begins. Enter the entry point filename.
                - The entry point file must exist in the algorithm path.
                - If you create **requirements.txt** in the same path, Python packages required by the script will be installed.
            - **Hyperparameters**
                - To add parameters for training, click the **+ button** to enter parameters in Key-Value format. Up to 100 parameters can be entered.
                - The entered hyperparameters are passed as execution arguments when the entry point is executed. For detailed usage instructions, see [Appendix > 3. Hyperparameters](#appendix.3.hyperparameter).

- **Image**: Select the image of the instance according to the environment in which training should be executed.

- **Training Resource Information**
    - **Training Instance Type**: Select the instance type to run training on.
    - **Number of Distributed Nodes**: Enter the number of nodes for distributed training. Distributed training can be enabled through configuration in the algorithm code. For more details, see [Appendix > 6. Distributed Training Configuration by Framework](#appendix.6.framework.training.settings).
    - **Use torchrun**: Select whether to use torchrun supported by the Pytorch framework. For more details, see [Appendix > 8. How to Use torchrun](#appendix.8.torchrun.usage).
    - **Number of Processes per Node**: If using torchrun, enter the number of processes per node. When using torchrun, distributed training is possible by running multiple processes on a single node. The number of processes affects memory usage.
- **Input Data**
    - **Data Set**: Enter the data set to run training on. Up to 10 data sets can be configured.
        - Data set name: Enter the data set name.
        - Data path: Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Checkpoint**: If you want to continue training from a saved checkpoint, enter the checkpoint storage path.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
- **Output Data**
    - **Output Data**: Enter the data storage path to save the training execution results.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Checkpoint**: If the algorithm provides a checkpoint, enter the checkpoint storage path.
        - The generated checkpoint can be used to resume training from the previous training.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
- **Additional Settings**
    - **Data Storage Size**: Enter the data storage size of the instance to run training on.
        - Used only when using NHN Cloud Object Storage. You must specify a sufficient size so that all data required for training can be stored.
    - **Maximum Training Time**: Specify the maximum wait time until training is completed. Training that exceeds the maximum wait time will be terminated.
    - **Log Management**: Logs generated during training progress can be saved to the NHN Cloud Log & Crash service.
        - For more details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! danger "Caution"
    - Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.
    - If you delete input data before training is completed, training may fail.

<a id="training.list"></a>

### Training List

The training list is displayed. When you select a training from the list, you can view detailed information and change the information.

- **Training Time**: The time the training was in progress is displayed.
- **Status**: The status of the training is displayed. Refer to the table below for major statuses.

    | Status                                         | Description                                                                                                                             |
    | -------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED                             | Status where training creation has been requested.                                                                                   |
    | CREATE IN PROGRESS                           | Status where resources required for training are being created.                                                                      |
    | RUNNING                                      | Status where training is in progress.                                                                                                     |
    | STOPPED                                      | Status where training has been stopped at the user's request.                                                                                      |
    | COMPLETE                                     | Status where training has been completed normally.                                                                             |
    | STOP IN PROGRESS                             | Status where training is being stopped.                                                                                                     |
    | FAIL TRAIN                                   | Status where training has failed during progress. Detailed failure information can be found through Log & Crash Search logs if log management is enabled. |
    | CREATE FAILED                                | Status where training creation has failed. If creation continues to fail, contact customer support.                                             |
    | FAIL TRAIN IN PROGRESS, COMPLETE IN PROGRESS | Status where resources used for training are being cleaned up.                                                                                     |

- **Actions**
    - **TensorBoard Shortcut**: Opens TensorBoard where you can view statistical information about the training in a new browser window.<br/>
        For information on how to save TensorBoard logs, see [Appendix > 5. Saving Metrics Logs for TensorBoard Usage](#appendix.5.tensorboard.store.metric.log). TensorBoard can only be accessed by users logged into the console.
    - **Stop Training**: You can stop the training in progress.

- **Hyperparameters**: When you select a training, you can view the hyperparameter values configured for the training in the **Hyperparameters** tab of the detailed screen that appears.

- **Monitoring**: When you select a training, you can view the list of monitoring target instances and basic metric charts in the **Monitoring** tab of the detailed screen that appears.
    - The **Monitoring** tab is disabled when training is in the creation state.

<a id="training.copy"></a>

### Copy Training

Create a new training with the same settings as an existing training.

1. Select the training you want to copy.
2. Click **Copy Training**.
3. The training creation screen is displayed with the same settings as the existing training.
4. If there is information you want to change, change it and then click **Create Training** to create the training.

<a id="training.model.create"></a>

### Create Model from Training

Create a model from training that is in a completed state.

1. Select the training you want to create a model from.
2. Click **Create Model**. Only training in the COMPLETE state can be created as a model.
3. You are redirected to the model creation page. After confirming the contents, click **Create Model** to create the model. For more details on model creation, see the [Model](#model) documentation.

<a id="training.delete"></a>

### Delete Training

Delete training.

1. Select the training you want to delete.
2. Click **Delete Training**. Training in progress can be stopped and then deleted.
3. The requested deletion operation cannot be canceled. Click **Confirm** to proceed.

!!! tip "Note"
    If a model created from the training you want to delete exists, you cannot delete the training. Delete the model first, then delete the training.

<a id="hyperparameter.tuning"></a>

## Hyperparameter Tuning

Hyperparameter tuning is the process of optimizing hyperparameter values to maximize the prediction accuracy of a model. If you do not use this feature, you must manually adjust hyperparameters by running many training tasks directly to find optimal values.

<a id="hyperparameter.tuning.create"></a>

### Create Hyperparameter Tuning

How to configure a hyperparameter tuning job.

- **Training Template**
    - **Use**: Select whether to use a training template. When using a training template, some configuration values of hyperparameter tuning are pre-filled with predefined values.
    - **Training Template**: Select a training template to use for automatically entering some configuration values for hyperparameter tuning.
- **Basic Information**
    - **Hyperparameter Tuning Name**: Enter the name of the hyperparameter tuning job.
    - **Description**: Enter a description for the hyperparameter tuning job if needed.
    - **Experiment**: Select an experiment to include the hyperparameter tuning. Experiments group related hyperparameter tuning. If no experiment has been created, click **Add** to create one.
- **Tuning Strategy**
    - **Strategy Name**: Select a strategy to use for finding optimal hyperparameters.
    - **Random Seed**: Determines random number generation. Set it to a fixed value for reproducible results.
- **Algorithm Information**: Enter information about the algorithm you want to train.
    - **Algorithm Type**: Select the algorithm type.
        - **NHN Cloud Provided Algorithm**: Use algorithms provided by AI EasyMaker. For detailed information about provided algorithms, see the [NHN Cloud Provided Algorithm Guide](./algorithm-guide/#) document.
            - **Algorithm**: Select an algorithm.
            - **Hyperparameter Spec**: Enter the range of hyperparameter values to use for hyperparameter tuning. For detailed information about hyperparameters by algorithm, see the [NHN Cloud Provided Algorithm Guide](./algorithm-guide/#) document.
                - **Name**: Define which hyperparameter to tune. This is determined by algorithm.
                - **Type**: Select the data type of the hyperparameter. This is determined by algorithm.
                - **Value/Range**
                    - **Min**: Define the minimum value.
                    - **Max**: Define the maximum value.
                    - **Step**: Determines the change size of hyperparameter values when using the "Grid" tuning strategy.
            - **Algorithm Metric**: Information about metrics generated by the algorithm is displayed.
        - **Custom Algorithm**: Use an algorithm you have created.
            - **Algorithm Path**
                - **NHN Cloud Object Storage**: Enter the path of NHN Cloud Object Storage where the algorithm is stored.
                    - Enter the directory path in the format obs://{Object Storage API endpoint}/{containerName}/{path}.
                    - When using NHN Cloud Object Storage, refer to [Appendix > 1. Add AI EasyMaker System Account Permission to NHN Cloud Object Storage](#appendix.1.object.storage.account.permission) to set permissions. If you do not set the required permissions, model creation will fail.
                - **NHN Cloud NAS**: Enter the path of NHN Cloud NAS where the algorithm is stored.
                    - Enter the directory path in the format nas://{NAS ID}:/{path}.
            - **Entry Point**
                - The entry point is the entry point of algorithm execution where training begins. Enter the entry point file name.
                - The entry point file must exist in the algorithm path.
                - If you create **requirements.txt** in the same path, Python packages required by the script will be installed.
            - **Hyperparameter Spec**
                - **Name**: Define which hyperparameter to tune.
                - **Type**: Select the data type of the hyperparameter.
                - **Value/Range**
                    - **Min**: Define the minimum value.
                    - **Max**: Define the maximum value.
                    - **Step**: Determines the change size of hyperparameter values when using the "Grid" tuning strategy.
                    - **Comma-separated values**: Tune hyperparameters using static values (e.g., sgd, adam).
- **Image**: Select the image of the instance according to the environment where training should be executed.
- **Training Resource Information**
    - **Training Instance Type**: Select the instance type to run training.
    - **Number of Training Instances**: The number of instances to perform training. The number of training instances is 'number of distributed nodes × number of parallel training'.
    - **Number of Distributed Nodes**: Enter the number of nodes to perform distributed training. Distributed training can be enabled through configuration in the algorithm code. For details, see [Appendix > 6. Framework-Specific Distributed Training Settings](#appendix.6.framework.training.settings).
    - **Number of Parallel Training**: Enter the number of trainings to perform in parallel simultaneously.
    - **Use torchrun**: Select whether to use torchrun supported by the PyTorch framework. For details, see [Appendix > 8. How to Use torchrun](#appendix.8.torchrun.usage).
    - **Number of Processes per Node**: When using torchrun, enter the number of processes per node. When using torchrun, multiple processes run on a single node to enable distributed training. The number of processes affects memory usage.
- **Input Data**
    - **Dataset**: Enter the dataset to run training. You can set up to 10 datasets.
        - Dataset Name: Enter the dataset name.
        - Data Path: Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Checkpoint**: If you want to resume training from a saved checkpoint, enter the checkpoint storage path.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
- **Output Data**
    - **Output Data**: Enter the data storage path to save the training execution results.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Checkpoint**: If the algorithm provides a checkpoint, enter the checkpoint storage path.
        - The created checkpoint can be used when resuming training from previous training.
        - Enter the NHN Cloud Object Storage or NHN Cloud NAS path.
- **Metric**
    - **Metric Name**: Define which metric to collect from the logs output by the training code.
    - **Metric Format**: Enter a regular expression to use for collecting metrics. The training algorithm must output metrics that match the regular expression.
- **Target Metric**
    - **Metric Name**: Select which metric to optimize.
    - **Target Metric Type**: Select the optimization type.
    - **Target Value**: When the target metric reaches this value, the tuning job terminates.
- **Tuning Resource Configuration**
    - **Maximum Number of Failed Training**: Define the maximum number of failed training. When the number of failed training reaches this value, tuning terminates as failed.
    - **Maximum Number of Training**: Define the maximum number of training. Tuning runs until the number of automatically executed training reaches this value.
- **Training Early Stopping**
    - **Name**: If the model does not improve even though training continues, training is terminated early.
    - **Minimum Number of Training**: Define how many training runs to get the target metric value from when calculating the median.
    - **Start Step**: Set from which training step early stopping applies.
- **Additional Settings**
    - **Data Storage Size**: Enter the data storage size of the instance where training will be executed.
        - Used only when using NHN Cloud Object Storage. You must specify a sufficiently large size to store all data needed for training.
    - **Maximum Elapsed Time**: Specify the maximum elapsed time until training is completed. Training that exceeds the maximum elapsed time is terminated.
    - **Log Management**: Logs generated during training can be saved to the NHN Cloud Log & Crash service.
        - For details, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! danger "Warning"
    - Only NHN Cloud NAS created from the same project as AI EasyMaker can be used.
    - If you delete input data before training is completed, training may fail.

<a id="hyperparameter.tuning.list"></a>

### Hyperparameter Tuning List

The hyperparameter tuning list is displayed. You can select a hyperparameter tuning from the list to view detailed information and make changes.

- **Elapsed Time**: Displays the time spent on hyperparameter tuning.
- **Completed Training**: Indicates the number of completed training runs among those automatically generated by hyperparameter tuning.
- **Training in Progress**: Indicates the number of training runs currently in progress.
- **Failed Training**: Indicates the number of failed training runs.
- **Best Training**: Displays the target metric information of the training run that recorded the best target metric value among those automatically generated by hyperparameter tuning.
- **Status**: Displays the status of the hyperparameter tuning. For major statuses, refer to the table below.

    | Status | Description |
    | --- | --- |
    | CREATE REQUESTED | State when hyperparameter tuning creation has been requested. |
    | CREATE IN PROGRESS | State when resources required for hyperparameter tuning are being created. |
    | RUNNING | State when hyperparameter tuning is in progress. |
    | STOPPED | State when hyperparameter tuning has been stopped at user's request. |
    | COMPLETE | State when hyperparameter tuning has completed successfully. |
    | STOP IN PROGRESS | State when hyperparameter tuning is being stopped. |
    | FAIL HYPERPARAMETER TUNING | State when hyperparameter tuning fails during progress. Detailed failure information can be found in Log & Crash Search logs if log management is enabled. |
    | CREATE FAILED | State when hyperparameter tuning creation has failed. If creation continues to fail, contact customer support. |
    | FAIL HYPERPARAMETER TUNING IN PROGRESS, COMPLETE IN PROGRESS, STOP IN PROGRESS | State when resources used for hyperparameter tuning are being cleaned up. |

- **Status Details**: Content inside parentheses in the `COMPLETE` state represents detailed status information. For major details, refer to the table below.

    | Details | Description |
    | --- | --- |
    | GoalReached | Detailed information when hyperparameter tuning training reaches the target value and completes. |
    | MaxTrialsReached | Detailed information when hyperparameter tuning reaches the maximum number of training runs and completes. |
    | SuggestionEndReached | Detailed information when the search algorithm of hyperparameter tuning has explored all hyperparameters. |

- **Actions**
    - **TensorBoard Shortcut**: Opens TensorBoard showing statistical information of training in a new browser window.<br/>
        For information on how to save metric logs for TensorBoard, refer to [Appendix > 5. Saving Metric Logs for TensorBoard Utilization](#appendix.5.tensorboard.store.metric.log). TensorBoard can only be accessed by users logged into the console.
    - **Stop Hyperparameter Tuning**: You can stop hyperparameter tuning that is in progress.

- **Monitoring**: When you select hyperparameter tuning, you can view the monitoring target instance list and basic metric charts in the **Monitoring** tab of the detailed screen that is displayed.
    - The **Monitoring** tab is disabled while hyperparameter tuning is in the creation state.

<a id="hyperparameter.tuning.training.list"></a>

### Learning Job List in Hyperparameter Tuning

A learning job list automatically generated by hyperparameter tuning is displayed. You can select a learning job from the list to view detailed information.

- **Target Metric Value**: Displays the target metric value.
- **Status**: Shows the status of the learning job automatically generated by hyperparameter tuning. For the main statuses, refer to the table below.

    | Status              | Description                                                                                                                                                              |
    | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
    | CREATED             | The learning job has been created.                                                                                                                                       |
    | RUNNING             | The learning job is in progress.                                                                                                                                         |
    | SUCCEEDED           | The learning job has completed successfully.                                                                                                                             |
    | KILLED              | The learning job has been stopped by the system.                                                                                                                         |
    | FAILED              | The learning job failed during execution. For detailed failure information, you can check the Log & Crash Search logs if log management is enabled.                       |
    | METRICS_UNAVAILABLE | The target metric cannot be collected.                                                                                                                                   |
    | EARLY_STOPPED       | The learning job was stopped early because the performance (target metric) did not improve further during execution.                                                    |

<a id="hyperparameter.tuning.copy"></a>

### Copy Hyperparameter Tuning

Creates a new hyperparameter tuning with the same settings as an existing hyperparameter tuning.

1. Select the hyperparameter tuning you want to copy.
2. Click **Copy Hyperparameter Tuning**.
3. The hyperparameter tuning creation screen appears with the same settings as the existing hyperparameter tuning.
4. If there is any information you want to change, modify it and then click **Create Hyperparameter Tuning** to create the hyperparameter tuning.

<a id="hyperparameter.tuning.model.create"></a>

### Create Model from Hyperparameter Tuning

Creates a model from the best learning job of a completed hyperparameter tuning.

1. Select the hyperparameter tuning from which you want to create a model.
2. Click **Create Model**. Only hyperparameter tunings in the completed (COMPLETE) status can be used to create a model.
3. You will be taken to the model creation page. After confirming the information, click **Create Model** to create the model.
   For more details on model creation, refer to the [Model](#model) documentation.

<a id="hyperparameter.tuning.delete"></a>

### Delete Hyperparameter Tuning

Deletes hyperparameter tuning.

1. Select the hyperparameter tuning you want to delete.
2. Click **Delete Hyperparameter Tuning**. In-progress hyperparameter tunings can be stopped and then deleted.
3. The requested deletion cannot be canceled. Click **Confirm** to proceed.

!!! tip "Note"
    If there is a model created from the hyperparameter tuning you want to delete, you cannot delete the hyperparameter tuning. Delete the model first, then delete the hyperparameter tuning.

<a id="training.template"></a>

## Training Templates

By creating training templates in advance, you can reuse the values you've entered in the template when creating training or tuning hyperparameters.

<a id="training.template.create"></a>

### Create Training Template

For information about what can be configured in a training template, see [Create Training](#training.create).

<a id="training.template.list"></a>

### Training Template List

A list of training templates is displayed. When you select a training template from the list, you can view detailed information and modify it.

- **Actions**
    - **Modify**: You can change the training template information.
- **Hyperparameters**: When you select a training template, you can view the hyperparameter names configured in the training template in the **Hyperparameters** tab on the details screen.

<a id="training.template.copy"></a>

### Copy Training Template

Create a new training template with the same settings as an existing training template.

1. Select the training template you want to copy.
2. Click **Copy Training Template**.
3. The training template creation screen is displayed with the same settings as the existing training template.
4. If you need to change any settings, modify them and click **Create Training Template** to create the training template.

<a id="training.template.delete"></a>

### Delete Training Template

Delete a training template.

1. Select the training template you want to delete.
2. Click **Delete Training Template**.
3. The requested deletion cannot be canceled. Click **Confirm** to proceed.

<a id="model"></a>

## Model

You can manage models from AI EasyMaker training results or external models as artifacts.

<a id="model.create"></a>

### Create Model

- **Basic Information**: Enter basic information about the model.
    - **Name**: Enter the model name.
        - If the model's framework type is PyTorch, you must enter a model name that matches the PyTorch model name.
    - **Description**: Enter a description of the model.
- **Framework Information**: Enter framework information about the model.
    - **Framework**: Select the framework for the model.
    - **Framework Version**: Enter the version of the model framework.
- **Model Information**: Enter the repository where the model artifacts are stored.
    - **Model Artifact**: Select the repository where the model artifacts are stored.
        - **NHN Cloud Object Storage**: Enter the Object Storage path where model artifacts are stored.
            - Enter the directory path in the format `obs://{Object Storage API endpoint}/{containerName}/{path}`.
            - When using NHN Cloud Object Storage, refer to [Appendix > 1. Add AI EasyMaker System Account Permissions to NHN Cloud Object Storage](#appendix.1.object.storage.account.permission) to configure permissions. If permissions are not set, you will not be able to access model artifacts and model creation will fail.
        - **NHN Cloud NAS**: Enter the NHN Cloud NAS path where model artifacts are stored.
            - Enter the directory path in the format `nas://{NAS ID}:/{path}`.
    - **Parameters**: Enter parameter information for the model.
        - **Parameter Name**: Enter the parameter name of the model.
        - **Parameter Value**: Enter the parameter value of the model.

!!! tip "Note"
    Values entered as model parameters are used when serving the model. Parameters can be used as arguments and environment variables.
    Arguments are used with the parameter names as entered, while environment variables convert the parameter names to screaming snake case.

!!! tip "Note"
    When creating a HuggingFace model, you can create the model by entering the HuggingFace model ID as a parameter.
    The HuggingFace model ID can be found in the URL of the HuggingFace model page.
    For more information, refer to [Appendix > 11. Framework-specific Serving Notes](#appendix.11.framework.note).

!!! danger "Caution"
    Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.

!!! danger "Caution"
    HuggingFace model file types are restricted to safetensors.
    Safetensors is a safe and efficient machine learning model file format developed by HuggingFace.
    Other file formats are not supported.

!!! danger "Caution"
    When creating TensorFlow (Triton), PyTorch (Triton), or ONNX (Triton) models, the model artifact path you enter must contain model files and `config.pbtxt` files in a structure that can be executed by Triton.
    Refer to the examples below.
    <details>
    <summary><strong>Example</strong></summary>

        model_name/
        ├── config.pbtxt                              # Model configuration file
        └── 1/                                        # Version 1 directory
            └── model.savedmodel/                     # TensorFlow SavedModel directory
                ├── saved_model.pb                    # Metagraph and checkpoint data
                └── variables/                        # Model weights directory
                    ├── variables.data-00000-of-00001
                    └── variables.index

    </details>

<a id="model.list"></a>

### Model List

The model list is displayed. Select a model in the list to view detailed information and make changes.

- **Name**: The model name and description are displayed. You can change the model name and description by clicking **Edit**.
- **Model Artifact Path**: The repository where the model artifacts are stored is displayed.
- **Status**: The status of the model is displayed. Refer to the table below for major statuses.

    | Status             | Description                                                                          |
    | ------------------ | ------------------------------------------------------------------------------------ |
    | CREATE REQUESTED   | The state when model creation has been requested.                                    |
    | CREATE IN PROGRESS | The state when creating resources required for the model.                            |
    | DELETE IN PROGRESS | The state when the model is being deleted.                                           |
    | ACTIVE             | The state when the model has been created successfully.                              |
    | CREATE FAILED      | The state when model creation failed. If creation continues to fail, contact support. |
    | DELETE FAILED      | The state when model deletion failed. Try again.                                     |

- **Training Name**: For models created from training, the name of the training it is based on is displayed.
- **Training ID**: For models created from training, the ID of the training it is based on is displayed.
- **Framework**: Framework information of the model is displayed.
- **Parameters**: Parameters of the model are displayed. Parameters are used for inference.

<a id="model.endpoint.create"></a>

### Create Endpoint from Model

Creates an endpoint that can serve the selected model.

1. Select the model you want to create as an endpoint from the list.
2. Click **Create Endpoint**.
3. Navigate to the **Create Endpoint** page. After reviewing the content, click **Create Endpoint**.
   For more information about endpoint creation, refer to the [Endpoint](#endpoint) documentation.

<a id="model.batch.inference.create"></a>

### Create Batch Inference from Model

Creates a batch inference that performs batch inference with the selected model and allows you to view inference results statistically.

1. Select the model you want to create as batch inference from the list.
2. Click **Create Batch Inference**.
3. Navigate to the **Create Batch Inference** page. After reviewing the content, click **Create Batch Inference**.
   For more information about batch inference creation, refer to the [Batch Inference](#batch.inference) documentation.

<a id="model.delete"></a>

### Delete Model

Deletes a model.

1. Select the model you want to delete from the list.
2. Click **Delete Model**.
3. The requested delete operation cannot be canceled. Click **Confirm** to proceed.

!!! tip "Note"
    If an endpoint created from the model you want to delete exists, you cannot delete the model.
    To delete, first delete the endpoint created from that model, then delete the model.

<a id="model.evaluation"></a>

## Model Evaluation

Measure the model's performance and compare performance across multiple models.

<a id="model.evaluation.create"></a>

### Create Model Evaluation

Batch inference is automatically generated during the model evaluation process.

- **Basic Information**: Enter basic information about the model evaluation.
    - **Name**: Enter the name of the model evaluation.
    - **Description**: Enter the description of the model evaluation.
- **Model Information**: Enter information about the model to be evaluated.
    - **Model**: Select the model to evaluate. Only classification and regression models are supported.
    - **Class Name**: Enter the class name of the model.
- **Model Evaluation Instance Information**
    - **Instance Type**: Select the instance type to run the model evaluation. This is used for data preprocessing and evaluation calculation tasks.
- **Input Data**: Input data is used to compare predicted values and ground truth generated through batch inference. You need fields used in inference and the ground truth field.
    - **Data Path**: Enter the path where the input data is located.
        - **Input Data Format**: Select the format of the input data. CSV and JSONL formats are supported, and file extensions must be .csv and .jsonl respectively.
        - **Evaluation Target Field**: Enter the field name of the ground truth label.
- **Batch Inference Output Data**
    - **Data Path**: Enter the path where the batch inference results will be saved.
- **Batch Inference Information**
    - **Instance Type**: Select the instance type to run the batch inference.
    - **Number of Instances**: Enter the number of instances to perform batch inference.
    - **Number of Pods**: Enter the number of pods for batch inference.
    - **Batch Size**: Enter the number of data samples processed simultaneously in a single inference operation.
    - **Inference Time Limit (seconds)**: Enter the time limit for batch inference. Set the maximum allowed time for a single inference request to be processed and results returned.
- **Additional Settings**
    - **Maximum Progress Time**: Specify the maximum progress time until the model evaluation is completed. Model evaluations that exceed the maximum progress time will be terminated.
    - **Log Management**: Logs generated during model evaluation can be saved to the NHN Cloud Log & Crash service.
        - For more information, refer to [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! danger "Caution"
    - Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.
    - The size of input data used in model evaluation must be 20GB or less.
    - The number of classes in classification model evaluation must be 50 or less.

<a id="model.evaluation.list"></a>

### Model Evaluation List

The model evaluation list is displayed. When you select a model evaluation from the list, you can check detailed information and change the information.

- **Name**: The name of the model evaluation is displayed.
- **Model**: The name of the model used in the model evaluation is displayed.
- **Status**: The status of the model evaluation is displayed. See the table below for the main statuses.

    | Status                                                  | Description                                                                                                           |
    |---------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
    | CREATE REQUESTED                                        | The status when model evaluation creation is requested.                                                               |
    | CREATE IN PROGRESS                                      | The status when model evaluation is being created.                                                                    |
    | CREATE FAILED                                           | The status when model evaluation creation fails. Please try again.                                                    |
    | RUNNING                                                 | The status when model evaluation is in progress.                                                                      |
    | COMPLETE IN PROGRESS, FAIL MODEL EVALUATION IN PROGRESS | The status when resources used in model evaluation are being cleaned up.                                               |
    | COMPLETE                                                | The status when model evaluation is completed successfully.                                                           |
    | STOP IN PROGRESS                                        | The status when model evaluation is being stopped.                                                                    |
    | STOPPED                                                 | The status when model evaluation is stopped by user request.                                                          |
    | FAIL MODEL EVALUATION                                   | The status when model evaluation fails. Detailed failure information can be checked through Log & Crash Search logs when log management is enabled. |
    | DELETE IN PROGRESS                                      | The status when model evaluation is being deleted.                                                                    |

- **Actions**
    - **Stop**: You can stop the model evaluation in progress.

<a id="model.evaluation.classification.metric"></a>

### Classification Model Evaluation Metrics

- **PR AUC**: The area under the Precision-Recall (PR) curve. It is effective for measuring model classification performance on imbalanced datasets.
- **ROC AUC**: The area under the ROC curve (Recall-False Positive Rate). The closer to 1, the better the performance.
- **Log Loss**: A loss value calculated by applying a logarithmic function to the difference between predicted probability and actual ground truth. Lower values indicate more reliable model predictions.
- **F1 Score**: The harmonic mean of precision and recall. It is useful when there is class imbalance, and the closer to 1, the better.
- **Precision**: The ratio of actual positives among those predicted as positive. It focuses on reducing False Positives.
- **Recall**: The ratio of actual positives that the model correctly predicts as positive. It is important in reducing False Negatives.
- **Precision-Recall Curve**: A curve that visualizes the relationship between precision and recall at various threshold values. It is referenced when adjusting the model's threshold.
- **ROC Curve**: Shows the relationship between recall and false positive rate at various threshold values. It is used for setting classification thresholds or comparing models.
- **Precision-Recall Curve by Threshold**: A graph showing how precision and recall change at specific threshold values. It is referenced when setting actual operational standards.
- **Confusion Matrix**: A matrix that classifies prediction results into four types: TP, FP, FN, and TN. It allows easy identification of error types by class.

<a id="model.evaluation.regression.metric"></a>

### Regression Model Evaluation Metrics

- **MAE (mean absolute error)**: The average of the absolute values of the differences between actual and predicted values. It intuitively shows the magnitude of prediction errors.
- **MAPE (mean absolute percentage error)**: The average of the ratios of prediction errors divided by actual values. Since it is ratio-based, it may be unsuitable for data with values close to zero.
- **R-squared (coefficient of determination)**: Indicates how well the model explains actual data. The closer to 1, the higher the explanatory power.
- **RMSE (root mean squared error)**: The square root of the average of squared errors. It is more sensitive to large errors and allows results to be interpreted on a scale identical to actual units.
- **RMSLE (root mean squared logarithmic error)**: Calculated as the difference between log-transformed actual and predicted values. It is insensitive to differences in value magnitude, making it useful for evaluating exponentially growing data.

<a id="model.evaluation.compare"></a>

### Compare Model Evaluations

Compare evaluation metrics of multiple models.

1. Select the model evaluations you want to compare from the list.
2. Click **Compare**.

<a id="model.evaluation.delete"></a>

### Delete Model Evaluation

Delete a model evaluation.

1. Select the model evaluation you want to delete.
2. Click **Delete**. Model evaluations in progress can be deleted after being stopped.
3. The requested deletion cannot be canceled. Click **Confirm** to proceed.

<a id="endpoint"></a>

## Endpoint

Create and manage endpoints to serve models.

<a id="endpoint.create"></a>

### Creating an Endpoint

- **Enable API Gateway Service**
    - AI EasyMaker endpoints create and manage API endpoints through NHN Cloud API Gateway service. You must enable the API Gateway service to use endpoint functionality.
    - For more details and pricing information about API Gateway service, see the following:
        - [API Gateway Service Guide](https://docs.nhncloud.com/ko/Application%20Service/API%20Gateway/ko/overview/)
        - [API Gateway Pricing](https://www.nhncloud.com/kr/pricing/by-service?c=Application%20Service&s=API%20Gateway)
- **Endpoint**: Choose whether to add a stage to a new or existing endpoint.
    - **Create as new endpoint**: Creates a new endpoint. A new service and default stage endpoint are created in API Gateway.
    - **Add new stage to existing endpoint**: A new stage endpoint is created in the API Gateway service of the existing endpoint. Select the existing endpoint to which you want to add the stage.
- **Endpoint Name**: Enter the endpoint name. Endpoint names must be unique.
- **Stage Name**: When adding a new stage to an existing endpoint, enter the new stage name. Stage names must be unique.
- **Description**: Enter the endpoint stage description.
- **Instance Information**: Enter instance information where the model will be served.
    - **Instance Type**: Select the instance type.
    - **Number of Instances**: Enter the number of instances to run.
    - **Auto Scaler**: Auto Scaler is a feature that automatically adjusts the number of nodes based on resource usage policies. Auto Scaler is configured on a per-stage basis.
        - **Enable/Disable**: Choose whether to enable Auto Scaler. When enabled, the number of instances scales in or out based on instance load.
        - **Minimum Number of Nodes**: Minimum number of nodes that can be scaled down.
        - **Maximum Number of Nodes**: Maximum number of nodes that can be scaled up.
        - **Scale Down**: Set whether node scale-down is active.
        - **Resource Usage Threshold**: The threshold value for resource usage that serves as the criteria for scale-down.
        - **Threshold Maintenance Time (minutes)**: Duration to maintain resource usage below the threshold for nodes targeted for scale-down.
        - **Scale-Down Delay Time After Scale-Up (minutes)**: Delay time before monitoring begins for nodes targeted for scale-down after scaling up nodes.
- **Stage Information**: Enter information about the model artifacts to deploy to the endpoint. If you deploy the same model across multiple stage resources, requests are distributed for processing.
    - **Model**: Select the model to deploy to the endpoint. If you have not created a model, create one first. For framework-specific serving notes, see [Appendix > 11. Framework-Specific Serving Notes](#appendix.11.framework.note).
    - **Resource Allocation (%)**: Enter the resources to allocate to the model. Allocates actual resource usage of instances as a fixed percentage.
        - **cpu**: Enter the CPU allocation. Enter this value when directly allocating instead of using allocation ratio (%).
        - **memory**: Enter the Memory allocation. Enter this value when directly allocating instead of using allocation ratio (%).
        - **gpu**: Enter the GPU allocation. Enter this value when directly allocating instead of using allocation ratio (%).
    - **Description**: Enter the stage resource description.
    - **Pod Auto Scaler**: A feature that automatically adjusts the number of pods based on the model's request volume. Auto Scaler is configured on a per-model basis.
        - **Enable/Disable**: Choose whether to enable Auto Scaler. When enabled, the number of pods scales in or out based on model load.
        - **Scale-Up Unit**: Enter the pod scale-up unit.
            - **CPU**: The number of pods is adjusted based on CPU usage.
            - **Memory**: The number of pods is adjusted based on Memory usage.
        - **Threshold Value**: The threshold value per scale-up unit at which pods will be scaled up.
    - **Resource Information**: You can verify the actual resources being used. Based on the allocation quota of the model you entered, actual resource usage is allocated to each model. For more details, see [Appendix > 9. Resource Information](#appendix.9.resource.info).

!!! tip "Note"
    AI EasyMaker service provides endpoints based on the OIP (Open Inference Protocol) specification. For endpoint API specification details, see [Appendix > 10. Endpoint API Specification](#appendix.10.endpoint.api.specification).
    To use a separate endpoint, create and use a new resource by referring to the resource created in API Gateway service.
    For more details about OIP specification, see [OIP Specification](https://github.com/kserve/open-inference-protocol).

!!! tip "Note"
    Endpoint creation may take a few minutes.
    When creating resources for the first time, additional time is required to configure the service environment.

!!! tip "Note"
    Creating a new endpoint creates a new API Gateway service.
    Adding a new stage to an existing endpoint creates a new stage in the API Gateway service.
    If you exceed the default quota specified in the [API Gateway Service Resource Policy](https://docs.nhncloud.com/ko/nhncloud/ko/resource-policy/#api-gateway), you may not be able to create endpoints in AI EasyMaker. In this case, the issue can be resolved by adjusting the API Gateway service resource quota.

<a id="endpoint.list"></a>

### Endpoint List

A list of endpoints is displayed. When you select an endpoint from the list, you can view detailed information and make changes.

- **Default Stage URL**: Displays the URL of the default stage among the endpoint's stages.
- **Status**: The status of the endpoint. Refer to the table below for major statuses.

    | Status | Description |
    | --- | --- |
    | CREATE REQUESTED | The endpoint creation has been requested. |
    | CREATE IN PROGRESS | The endpoint is being created. |
    | UPDATE IN PROGRESS | Some stages of the endpoint have ongoing operations.<br/>You can check the operation status for each stage in the endpoint stage list. |
    | DELETE IN PROGRESS | The endpoint is being deleted. |
    | ACTIVE | The endpoint is operating normally. |
    | CREATE FAILED | Endpoint creation failed.<br/>You must delete the endpoint and create it again. If creation failures persist, contact customer support. |
    | UPDATE FAILED | Some stages of the endpoint are not operating normally. You must delete the problematic stage and create it again. |

- **API Gateway Status**: Displays the API Gateway status information of the endpoint's default stage. Refer to the table below for major statuses.

    | Status | Description |
    | --- | --- |
    | CREATE IN PROGRESS | API Gateway resources are being created. |
    | STAGE DEPLOYING | The API Gateway default stage is being deployed. |
    | ACTIVE | The API Gateway default stage has been successfully deployed and is active. |
    | NOT FOUND: STAGE | The default stage of the endpoint cannot be found.<br/>Check if the stage exists in the API Gateway console.<br/>If the stage has been deleted, the deleted API Gateway stage cannot be recovered. You must delete the endpoint and create it again. |
    | NOT FOUND: STAGE DEPLOY RESULT | The deployment status of the endpoint's default stage cannot be found.<br/>Check if the default stage is deployed in the API Gateway console. |
    | STAGE DEPLOY FAIL | API Gateway default stage deployment failed. |

<a id="endpoint.stage.create"></a>

### Create Endpoint Stage

Adds a new stage to an existing endpoint. You can create a new stage and test it without affecting the default stage.

1. Click the **endpoint name** in the endpoint list.
2. Click **+ Create Stage**.
3. Adding a new stage to an existing endpoint is automatically selected, and the configuration method is the same as endpoint creation.
4. Requested deletion operations cannot be canceled. Click **Confirm** to proceed.

<a id="endpoint.stage.list"></a>

### Endpoint Stage List

A list of stages created under the endpoint is displayed. You can select a stage from the list to view its detailed information.

- **Status**: The status of the endpoint stage is displayed. Refer to the table below for major statuses.

    | Status             | Description                                                              |
    | ------------------ | ------------------------------------------------------------------------ |
    | CREATE REQUESTED   | The creation of the endpoint stage has been requested.                   |
    | CREATE IN PROGRESS | The endpoint stage is being created.                                     |
    | DEPLOY IN PROGRESS | A model is being deployed to the endpoint stage.                         |
    | DELETE IN PROGRESS | The endpoint stage is being deleted.                                     |
    | ACTIVE             | The endpoint stage is operating normally.                                |
    | CREATE FAILED      | The endpoint stage creation failed. Please try again.                    |
    | DEPLOY FAILED      | The endpoint stage deployment failed. Please try creating it again.      |

- **API Gateway Status**: The stage status of the API Gateway where the endpoint stage is deployed is displayed.
- **Stage Default Stage**: Whether this is the default stage is displayed.
- **Stage URL**: The stage URL of the API Gateway where the model is served is displayed.
- **View API Gateway Settings**: To view the settings that AI EasyMaker deployed to the API Gateway stage, click **View Settings**.
- **View API Gateway Statistics**: To view the API statistics of the endpoint, click **View Statistics**.
- **Instance Type**: The endpoint instance type on which the model is served is displayed.
- **Running Work Node/Pod Count**: The number of nodes and pods used by the endpoint is displayed.
- **Stage Resources**: Information about the model artifacts deployed to the stage is displayed.
- **Monitoring**: When you select an endpoint stage, you can view the list of monitoring target instances and basic metric charts in the **Monitoring** tab of the detailed screen that appears.
    - The **Monitoring** tab is disabled when the endpoint stage is in the creation state.
- **API Statistics**: When you select an endpoint stage, you can view the API statistics information of the endpoint stage in the **API Statistics** tab of the detailed screen that appears.
    - The **API Statistics** tab is disabled when the endpoint stage is in the creation state.

!!! danger "Caution"
    When AI EasyMaker creates an endpoint or endpoint stage, it creates an API Gateway service and stage for the endpoint.
    If you directly modify the API Gateway service and stage created by AI EasyMaker in the API Gateway service console, please refer to the following precautions.

    1. Do not delete the API Gateway service and stage created by AI EasyMaker. If you do, the API Gateway information may not be displayed correctly for the endpoint, and changes to the endpoint may not be applied to the API Gateway.
    2. Do not modify or delete the resources in the API Gateway resource path entered when creating the endpoint. If you delete them, inference API calls to the endpoint may fail.
    3. Do not add resources under the API Gateway resource path entered when creating the endpoint. Resources added may be deleted when adding or modifying endpoint stages.
    4. Do not disable or change the URL of the **Backend Endpoint URL Override** setting in the API Gateway resource path in the API Gateway stage settings. If you change it, inference API calls to the endpoint may fail.
       Aside from the precautions above, you can use other features provided by API Gateway as needed.
       For more information about using API Gateway, refer to the [API Gateway Console Guide](https://docs.nhncloud.com/ko/Application%20Service/API%20Gateway/ko/console-guide/).

!!! tip "Keep in Mind"
    If the endpoint stage settings of AI EasyMaker are not deployed to the API Gateway stage due to a temporary issue, it is displayed as 'Deployment Failed' status.
    In this case, you can manually deploy the API Gateway stage by selecting the stage from the stage list > clicking **View API Gateway Settings** in the detailed screen at the bottom > clicking **Deploy Stage**.
    If the deployment status is not recovered with the above guide, please contact customer support.

<a id="endpoint.stage.resource.create"></a>

### Stage Resource Creation

Add new resources to an existing endpoint stage.

- **Model**: Select the model you want to deploy to the endpoint. If you haven't created a model yet, create one first.
- **Resource Allocation (%)**: Enter the resources to allocate to the model. Allocates the instance's actual resource usage at a fixed ratio.
    - **CPU**: Enter the CPU allocation quota. Enter this if you want to allocate directly without using the allocation ratio (%).
    - **Memory**: Enter the Memory allocation quota. Enter this if you want to allocate directly without using the allocation ratio (%).
- **Pod Count**: Enter the number of pods for the stage resource.
- **Description**: Enter a description for the stage resource.
- **Pod Auto Scaler**: A feature that automatically adjusts the number of pods based on the model's request volume. The auto scaler is configured per model.
    - **Enable/Disable**: Choose whether to enable the auto scaler. When enabled, the number of pods will scale in or out based on the model load.
    - **Scale Unit**: Enter the pod scale unit.
        - **CPU**: The number of pods is adjusted based on CPU usage.
        - **Memory**: The number of pods is adjusted based on Memory usage.
    - **Threshold Value**: The threshold value for the scale unit at which pods will be scaled up.

<a id="endpoint.stage.resource.list"></a>

### Stage Resource List

A list of resources created under the endpoint stage is displayed.

- **Status**: Displays the status of the stage resource. Refer to the table below for major statuses.

    | Status             | Description                                                   |
    | ------------------ | ------------------------------------------------------------- |
    | CREATE REQUESTED   | The stage resource creation has been requested.               |
    | CREATE IN PROGRESS | The stage resource is being created.                          |
    | DELETE IN PROGRESS | The stage resource is being deleted.                          |
    | ACTIVE             | The stage resource has been deployed successfully.            |
    | CREATE FAILED      | The stage resource creation failed. Please try again.         |

- **Model Name**: The name of the model deployed to the stage.
- **API Gateway Resource Path**: The inference URL of the model deployed to the stage. You can request inference using the displayed URL. For more details, see [Appendix > 10. Endpoint API Specification](#appendix.10.endpoint.api.specification).
- **Pod Count**: Displays the number of healthy pods in use and the total number of pods for the resource.

<a id="endpoint.inference.call"></a>

### Endpoint Inference Invocation

1. Click on a stage in **Endpoint** > **Endpoint Stage** to display the stage details screen at the bottom.
2. In the Stage Resource tab of the details screen, confirm the API Gateway resource path.
3. Call the API Gateway resource path using HTTP POST method to invoke the inference API.
    - The request and response specifications of the inference API vary depending on the algorithm created by the user.

            // Inference API example: Request
            curl --location --request POST '{API Gateway resource path}' \
            --header 'Content-Type: application/json' \
            --data-raw '{
                "instances": [
                    [6.8,  2.8,  4.8,  1.4],
                    [6.0,  3.4,  4.5,  1.6]
                ]
            }'

            // Inference API example: Response
            {
                "predictions" : [
                    [
                        0.337502569,
                        0.332836747,
                        0.329660654
                    ],
                    [
                        0.337530434,
                        0.332806051,
                        0.329663515
                    ]
                ]
            }

<a id="endpoint.stage.resource.delete"></a>

### Delete Stage Resource

1. Click on the **Endpoint Name** in the endpoint list to go to the endpoint stage list.
2. In the endpoint stage list, click on the endpoint stage where the stage resource to be deleted is deployed. The stage details screen will be displayed at the bottom.
3. In the **Stage Resource** tab of the details screen, select the stage resource to delete.
4. Click **Delete Stage Resource**.
5. The requested deletion operation cannot be undone. Click **Confirm** to proceed.

<a id="endpoint.default.stage.change"></a>

### Change Default Endpoint Stage

Change the default stage of an endpoint to another stage.
To change the model of an endpoint without service interruption, AI EasyMaker recommends deploying the model using the stage feature.

1. The stage currently operating as the actual service runs on the default stage.
2. When replacing with a new model, add a new stage to the existing endpoint.
3. Verify that there are no issues with the endpoint service using the replaced model in the new stage.
4. Click **Change Default Stage**.
5. Select the new stage to be changed to the default stage from the stage to change.
6. The change request operation cannot be undone. Click **Confirm** to proceed.
7. The selected stage will be changed to the default stage, and the resources of the existing default stage will be automatically deleted.

<a id="endpoint.stage.delete"></a>

### Delete Endpoint Stage

1. Click on the **Endpoint Name** in the endpoint list to go to the endpoint stage list.
2. In the endpoint stage list, select the endpoint stage to delete. The default stage cannot be deleted.
3. Click **Delete Stage**.
4. The requested deletion operation cannot be undone. Click **Confirm** to proceed.

!!! danger "Caution"
    When you delete an endpoint stage in AI EasyMaker, the stage of the API Gateway service where the endpoint stage is deployed will also be deleted.
    If there are APIs in operation on the API Gateway stage being deleted, API calls will not be possible, so please proceed with caution.

<a id="endpoint.delete"></a>

### Delete Endpoint

Delete an endpoint.

1. Select the endpoint you want to delete from the endpoint list.
2. If there are stages other than the default stage under the endpoint, the endpoint cannot be deleted. First delete other stages and then delete the endpoint.
3. Click **Delete Endpoint**.
4. The requested deletion operation cannot be undone. Click **Confirm** to proceed.

!!! danger "Caution"
    When you delete an endpoint in AI EasyMaker, the API Gateway service where the endpoint is deployed will also be deleted.
    If there are APIs in operation on the API Gateway service being deleted, API calls will not be possible, so please proceed with caution.

<a id="batch.inference"></a>

## Batch Inference

AI EasyMaker provides an environment where you can perform batch inference with models and check inference results through statistics.

<a id="batch.inference.create"></a>

### Create Batch Inference

Set up the environment where batch inference will be performed by selecting an instance and OS image, and proceed with batch inference by entering the paths of input/output data to be inferred.

- **Basic Information**: Enter basic information about the batch inference.
    - **Batch Inference Name**: Enter the name of the batch inference.
    - **Batch Inference Description**: Enter a description.
- **Instance Information**
    - **Instance Type**: Select the instance type to run the batch inference.
    - **Number of Instances**: The number of instances to perform batch inference.
- **Model Information**
    - **Model**: Select the model for batch inference. If you have not created a model, create one first.
    - **Number of Pods**: Enter the number of pods for the model.
    - **Resource Information**: You can check the resources actually used by the model. The actual usage is divided and allocated to each pod according to the number of pods entered. For more information, see [Appendix > 9. Resource Information](#appendix.9.resource.info).
- **Input Data**
    - **Data Path**: Enter the path of the data to execute batch inference.
        - Enter an NHN Cloud Object Storage or NHN Cloud NAS path.
    - **Input Data Type**: Select the type of data to execute batch inference.
        - **JSON**: Use valid JSON data in the file as input values.
        - **JSONL**: Use JSON Lines files where each line consists of valid JSON as input values.
            - Reference: [https://jsonlines.org/](https://jsonlines.org/)
    - **Glob Pattern**
        - **Include Files**: Enter a set of files to include in the input data using a Glob pattern.
        - **Exclude Files**: Enter a set of files to exclude from the input data using a Glob pattern.
- **Output Data**
    - **Output Data**: Enter the data storage path where the execution result of batch inference will be saved.
        - Enter an NHN Cloud Object Storage or NHN Cloud NAS path.
- **Additional Settings**
    - **Batch Options**
        - **Batch Size**: Enter the number of data samples processed simultaneously in a single inference task.
        - **Inference Time Limit (seconds)**: Enter the time limit for batch inference. You can set the maximum allowed time for a single inference request to be processed and results to be returned.
    - **Data Storage Size**: Enter the data storage size for the instance to run batch inference.
        - Only used when using NHN Cloud Object Storage. You must specify a sufficient size to store all data required for batch inference.
    - **Maximum Batch Inference Time**: Specify the maximum waiting time until batch inference is completed. Batch inference that exceeds the maximum waiting time will be terminated.
    - **Log Management**: Logs that occur during batch inference can be saved to the NHN Cloud Log & Crash Search service.
        - For more information, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! tip "Note"
    - When using Glob pattern, **exclude Glob pattern** is applied with priority.
    - You must appropriately set **batch size** and **inference time limit** depending on the performance of the model performing batch inference. If the entered settings are incorrect, batch inference may not perform sufficiently.

!!! danger "Caution"
    - Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.
    - If you delete input data before batch inference is completed, batch inference may fail.
    - When using Glob pattern, if the value is not entered appropriately, input data cannot be found and batch inference may not work normally.

!!! danger "Caution"
    Batch inference using GPU instances allocates GPU instances according to the number of pods.
    If `number of pods / number of GPUs` is not evenly divisible, unallocated GPUs may occur.
    Since unallocated GPUs are not used in batch inference, set the number of pods appropriately to efficiently use GPU instances.

<a id="batch.inference.list"></a>

### Batch Inference List

The batch inference list is displayed. When you select a batch inference from the list, you can check detailed information and modify the information.

- **Inference Elapsed Time**: The time during which batch inference was performed is displayed.
- **Status**: The status of batch inference is displayed. Refer to the table below for major statuses.

    | Status                                                   | Description                                                                                                                                   |
    | ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
    | CREATE REQUESTED                                       | The state in which batch inference creation has been requested.                                                                                                    |
    | CREATE IN PROGRESS                                     | The state in which resources required for batch inference are being created.                                                                                        |
    | RUNNING                                                | The state in which batch inference is in progress.                                                                                                      |
    | STOPPED                                                | The state in which batch inference has been stopped at the user's request.                                                                                       |
    | COMPLETE                                               | The state in which batch inference has been completed normally.                                                                                              |
    | STOP IN PROGRESS                                       | The state in which batch inference is being stopped.                                                                                                      |
    | FAIL BATCH INFERENCE                                   | The state in which batch inference has failed during execution. Detailed failure information can be checked through Log & Crash Search logs if log management is enabled. |
    | CREATE FAILED                                          | The state in which batch inference creation has failed. If creation continues to fail, contact customer support.                                              |
    | FAIL BATCH INFERENCE IN PROGRESS, COMPLETE IN PROGRESS | The state in which resources used for batch inference are being cleaned up.                                                                                      |

- **Operations**
    - **Stop**: You can stop the running batch inference.
- **Monitoring**: When you select batch inference, you can check the monitoring target instance list and basic metric charts in the **Monitoring** tab of the detailed screen displayed.
    - The **Monitoring** tab is disabled when batch inference is in the creation state.

<a id="batch.inference.copy"></a>

### Copy Batch Inference

Create a new batch inference with the same settings as an existing batch inference.

1. Select the batch inference to copy.
2. Click **Copy Batch Inference**.
3. The batch inference creation screen is displayed with the same settings as the existing batch inference.
4. If there is information you want to change settings for, change it and click **Create Batch Inference** to create the batch inference.

<a id="batch.inference.delete"></a>

### Delete Batch Inference

Delete batch inference.

1. Select the batch inference to delete.
2. Click **Delete Batch Inference**. Running batch inference can be deleted after stopping.
3. The requested delete operation cannot be canceled. Click **Confirm** to proceed.

<a id="personal.image"></a>

## Personal Images

You can run notebooks, training, and hyperparameter tuning using customized container images.
Only personal images derived from the notebook/deep learning images provided by AI EasyMaker can be used when creating resources in AI EasyMaker.
Refer to the table below for AI EasyMaker's base images.

<a id="personal.image.notebook.image"></a>

#### Notebook Images

| Image Name                          | Core Type | Framework | Framework Version | Python Version | Image Address                                                                                            |
| ------------------------------------ | -------- | ---------- | --------------- | ----------- | ------------------------------------------------------------------------------------------------------ |
| Ubuntu 22.04 CPU Python Notebook     | CPU      | Python     | 3.10.12         | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/python-notebook:3.10.12-cpu-py310-ubuntu2204    |
| Ubuntu 22.04 GPU Python Notebook     | GPU      | Python     | 3.10.12         | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/python-notebook:3.10.12-gpu-py310-ubuntu2204    |
| Ubuntu 22.04 CPU PyTorch Notebook    | CPU      | PyTorch    | 2.0.1           | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-notebook:2.0.1-cpu-py310-ubuntu2204     |
| Ubuntu 22.04 GPU PyTorch Notebook    | GPU      | PyTorch    | 2.0.1           | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-notebook:2.0.1-gpu-py310-ubuntu2204     |
| Ubuntu 22.04 CPU TensorFlow Notebook | CPU      | TensorFlow | 2.12.0          | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-notebook:2.12.0-cpu-py310-ubuntu2204 |
| Ubuntu 22.04 GPU TensorFlow Notebook | GPU      | TensorFlow | 2.12.0          | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-notebook:2.12.0-gpu-py310-ubuntu2204 |

<a id="personal.image.deep.learning.image"></a>

#### Deep Learning Images

| Image Name                          | Core Type | Framework | Framework Version | Python Version | Image Address                                                                                         |
| ------------------------------------ | -------- | ---------- | --------------- | ----------- | --------------------------------------------------------------------------------------------------- |
| Ubuntu 22.04 CPU PyTorch Training    | CPU      | PyTorch    | 2.0.1           | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-train:2.0.1-cpu-py310-ubuntu2204     |
| Ubuntu 22.04 GPU PyTorch Training    | GPU      | PyTorch    | 2.0.1           | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/pytorch-train:2.0.1-gpu-py310-ubuntu2204     |
| Ubuntu 22.04 CPU TensorFlow Training | CPU      | TensorFlow | 2.12.0          | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-train:2.12.0-cpu-py310-ubuntu2204 |
| Ubuntu 22.04 GPU TensorFlow Training | GPU      | TensorFlow | 2.12.0          | 3.10        | fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/tensorflow-train:2.12.0-gpu-py310-ubuntu2204 |

!!! tip "Note"
    Only NHN Container Registry (NCR) can be connected as the container registry service where personal images are stored (as of December 2023).

!!! danger "Caution"
    Only personal images derived from the base images provided by AI EasyMaker can be used.

<a id="personal.image.create"></a>

### Creating Personal Images

The following document guides you on how to create a container image using the Docker tool based on AI EasyMaker's base image and use personal images for notebooks in AI EasyMaker.

1. Create a Dockerfile for your personal image.

        FROM fb34a0a4-kr1-registry.container.nhncloud.com/easymaker/python-notebook:3.10.12-cpu-py310-ubuntu2204 as easymaker-notebook
        RUN conda create -n example python=3.10
        RUN conda activate example
        RUN pip install torch torchvision

2. Build the personal image and push to the container registry
    Build the image using the Dockerfile and save (push) the image to the NCR registry.

        docker build -t {image name}:{tag} .
        docker tag {image name}:{tag} {NCR registry address}/{image name}:{tag}
        docker push {NCR registry address}/{image name}:{tag}

        (Example)
        docker build -t custom-training:v1 .
        docker tag custom-training:v1 example-kr1-registry.container.nhncloud.com/registry/custom-training:v1
        docker push example-kr1-registry.container.nhncloud.com/registry/custom-training:v1

3. Create the image pushed (saved) to NCR as a personal image in AI EasyMaker.

    1. Navigate to the **Images** menu in the AI EasyMaker console.
    2. Click the **Create Image** button and enter information about the created image.
        - Name, Description: Enter the name and description for the image.
        - Address: Enter the registry image address.
        - Type: Enter the type of the container image. Select **Notebook** or **Training**.
        - Account: Select the account for AI EasyMaker notebook/training nodes to access your registry repository.
            - Create New: Register a new registry account.
                - Name, Description: Enter the name and description for the registry account.
                - Category: Select the container registry service.
                - ID: Enter the ID for the registry repository.
                - Password: Enter the password for the registry repository.
            - Use Existing Account: Select an already registered registry account.

4. Create a notebook with the personal image you created.
    1. Navigate to the **Notebooks** menu. Click the **Create Notebook** button to go to the notebook creation page.
    2. Click the **Personal Images** tab in the image information section.
    3. Select the personal image to use as the notebook container image.
    4. Enter the other notebook information and create it. The notebook will run with the personal image.

!!! tip "Note"
    Personal images can be used to create resources for notebooks, training, and hyperparameter tuning.

!!! tip "Note"
    Only NHN Container Registry (NCR) service can be connected as the container registry service (as of December 2023).
    For the account ID and password for the NCR service, enter the following values:
    ID: User Access Key of the NHN Cloud user account
    Password: User Secret Key of the NHN Cloud user account

<a id="registry.account"></a>

## Registry Account

For AI EasyMaker to pull images from your registry where private images are stored and run containers, you must log in to your registry.
Once you save login information with a registry account, it can be reused for images linked to that registry account.
To manage registry accounts, navigate to the **Image** menu in the AI EasyMaker console and select the **Registry Account** tab.

<a id="registry.account.create"></a>

### Create Registry Account

Create a new registry account.

- Name: Enter the name of the registry account.
- Description: Enter a description of the registry account.
- Category: Select a container registry service.
- ID: Enter the ID of the registry account.
- Password: Enter the password of the registry account.

<a id="registry.account.modify"></a>

### Modify Registry Account

<a id="registry.account.modify.account.modify"></a>

#### Modify Registry ID and Password

- Click the **Modify Registry Account** button.
- Enter the new ID and password, then click the **Confirm** button.

!!! tip "Note"
    When you change a registry account, the updated ID and password will be used to access the registry service when using images linked to that account.
    If you enter an incorrect registry ID or password, authentication will fail during private image pull, causing resource creation to fail.

!!! danger "Warning"
    Modifying the ID and password may cause problems if there are resources being created with private images linked to the registry account, or if there are ongoing training or hyperparameter tuning tasks.
    Be careful when modifying the ID and password.

<a id="registry.account.modify.account.info.modify"></a>

#### Modify Registry Account Name and Description

1. Select the account to change from the registry account list.
2. Click the **Change** button in the lower screen.
3. Change the name and description, then click the **Confirm** button.

<a id="registry.account.delete"></a>

### Delete Registry Account

Select the registry account to delete from the list and click the **Delete Registry Account** button.

!!! tip "Note"
    Registry accounts linked to images cannot be deleted. To delete them, you must first delete the linked images and then delete the registry account.

<a id="pipeline"></a>

## Pipeline

ML Pipeline is a feature for managing and executing portable and scalable machine learning workflows.
Using the Kubeflow Pipelines (KFP) Python SDK, you can write components and pipelines, compile pipelines into intermediate representation YAML, and run them in AI EasyMaker.
Most pipelines aim to generate one or more ML artifacts, such as datasets, models, and evaluation metrics.

!!! tip "Note"
    A **pipeline** is a definition of a workflow that combines one or more components to form a directed acyclic graph (DAG).
    - Each component runs a single container during execution, which can generate ML artifacts.
    - Components can receive inputs and produce outputs. There are two types of I/O: parameters and artifacts.
    - Parameters are useful for passing small amounts of data between components.
    - Artifact types are for ML artifact outputs such as datasets, models, and metrics. They provide a convenient mechanism for storing in object storage.

!!! tip "Note"
    Console output that occurs while running a pipeline is not provided.
    Send pipeline code logs to Log & Crash Search using [the SDK's Log transmission feature](./sdk-guide/#feature.lncs.log.send).

!!! tip "Note"
    Kubeflow Pipelines (KFP) official documentation
    - [KFP User Guide](https://www.kubeflow.org/docs/components/pipelines/user-guides/)
    - [KFP SDK Reference](https://kubeflow-pipelines.readthedocs.io/ko/stable/)

<a id="pipeline.upload"></a>

### Upload Pipeline

Upload a pipeline.

- **Name**: Enter the pipeline name.
- **Description**: Enter a description.
- **File Registration**: Select the YAML file to upload.

!!! tip "Note"
    Pipeline upload may take several minutes.
    When creating resources for the first time, additional time is required to configure the service environment.

<a id="pipeline.list"></a>

### Pipeline List

The pipeline list is displayed. When you select a pipeline from the list, you can view detailed information and modify it.

- **Status**: The status of the pipeline is displayed. Refer to the table below for major statuses.

    | Status             | Description                                    |
    |--------------------|------------------------------------------------|
    | CREATE REQUESTED   | Pipeline creation has been requested.          |
    | CREATE IN PROGRESS | Pipeline creation is in progress.              |
    | CREATE FAILED      | Pipeline creation failed. Please try again.    |
    | ACTIVE             | Pipeline has been successfully created.        |

<a id="pipeline.graph"></a>

### Pipeline Graph

The pipeline graph is displayed. When you select a node in the graph, you can view detailed information.

The graph is a visual representation of the pipeline. Each node in the graph represents a step in the pipeline, and arrows indicate the parent/child relationships between pipeline components represented by each step.

<a id="pipeline.delete"></a>

### Delete Pipeline

Delete a pipeline.

1. Select the pipeline to delete.
2. Click **Delete Pipeline**. Pipelines being created cannot be deleted.
3. The requested deletion cannot be canceled. Click **Delete** to proceed.

!!! tip "Note"
    If a schedule exists that was created from the pipeline you want to delete, you cannot delete the pipeline. Delete the pipeline schedule first, then delete the pipeline.

<a id="pipeline.run"></a>

## Pipeline Execution

You can run and manage uploaded pipelines in AI EasyMaker.

<a id="pipeline.run.create"></a>

### Create Pipeline Run

Execute a pipeline.

- **Basic Information**
    - **Name**: Enter the pipeline run name.
    - **Description**: Enter a description.
    - **Pipeline**: Select the pipeline to execute.
    - **Experiment**: Select the experiment that will contain the pipeline run. An experiment groups related pipeline runs. If no experiment has been created, click **Add** to create one.
- **Run Information**
    - **Run Parameters**: If there are input parameters defined in the pipeline, enter their values.
    - **Run Type**: Select the pipeline run type. If you select **One-time**, the pipeline runs only once. To run the pipeline repeatedly on a schedule, select **Schedule Settings** and refer to [Create Pipeline Schedule](#pipeline.recurring.run.create) to configure the schedule.
- **Instance Information**
    - **Instance Type**: Select the instance type to run the pipeline.
    - **Number of Instances**: Enter the number of instances to use for the pipeline run.
- **Additional Settings**
    - **Boot Storage Size**: Enter the boot storage size for the instance running the pipeline.
    - **NHN Cloud NAS**: You can connect **NHN Cloud NAS** to the instance running the pipeline.
        - **Mount Directory Name**: Enter the directory name to mount on the instance.
        - **NAS Path**: Enter the path in the format `nas://{NAS ID}:/{path}`.
    - **Log Management**: You can save logs generated during pipeline execution to the NHN Cloud Log & Crash Search service.
        - For more information, refer to [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! tip "Note"
    Creating a pipeline run may take several minutes.
    When creating resources for the first time, additional time is required for service environment configuration.

!!! danger "Caution"
    Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.

<a id="pipeline.run.list"></a>

### Pipeline Run List

The pipeline run list is displayed. When you select a pipeline run from the list, you can view detailed information and modify the information.

- **Status**: The status of the pipeline run is displayed. Refer to the table below for major statuses.

    | Status                        | Description                                                                                    |
    |-------------------------------|------------------------------------------------------------------------------------------------|
    | CREATE REQUESTED              | Pipeline run creation has been requested.                                                      |
    | CREATE IN PROGRESS            | Pipeline run creation is in progress.                                                          |
    | CREATE FAILED                 | Pipeline run creation failed. Please try again.                                                |
    | RUNNING                       | Pipeline run is in progress.                                                                  |
    | COMPLETE IN PROGRESS          | Resources used for the pipeline run are being cleaned up.                                      |
    | COMPLETE                      | Pipeline run completed successfully.                                                           |
    | STOP IN PROGRESS              | Pipeline run is being stopped.                                                                |
    | STOPPED                       | Pipeline run was stopped by user request.                                                      |
    | FAIL PIPELINE RUN IN PROGRESS | Resources used for the pipeline run are being cleaned up.                                      |
    | FAIL PIPELINE RUN             | Pipeline run failed. For detailed failure information, check the Log & Crash Search logs if log management is enabled. |

- **Actions**
    - **Stop**: You can stop an ongoing pipeline run.
- **Monitoring**: When you select a pipeline run from the list, you can view the monitoring target instance list and basic metric charts in the **Monitoring** tab of the detail screen displayed.
    - The **Monitoring** tab is disabled when the pipeline run is in the creation state.

<a id="pipeline.run.graph"></a>

### Pipeline Run Graph

The pipeline run graph is displayed. When you select a node in the graph, you can view detailed information.

The graph is a visual representation of the pipeline execution. This graph shows the steps that have already been executed and the step currently being executed during the pipeline run, and the parent/child relationships between pipeline components displayed as steps are represented by arrows. Each node in the graph represents a step in the pipeline.

Through detailed information for each node, you can download generated artifacts.

!!! danger "Caution"
    Pipeline artifacts are retained for 120 days. Artifacts older than 120 days are automatically deleted.

<a id="pipeline.run.stop"></a>

### Stop Pipeline Run

Stop an ongoing pipeline run.

1. Select the pipeline run to stop from the list.
2. Click **Stop Run**.
3. The requested operation cannot be canceled. Click **Confirm** to proceed.

!!! tip "Note"
    Stopping a pipeline run may take several minutes.

<a id="pipeline.run.copy"></a>

### Copy Pipeline Run

Create a new pipeline run with the same settings as an existing pipeline run.

1. Select the pipeline run to copy.
2. Click **Copy Pipeline Run**.
3. The pipeline run creation screen is displayed with the same settings as the existing pipeline run.
4. If there are any settings you want to change, change them and click **Create Pipeline Run**.

<a id="pipeline.run.delete"></a>

### Delete Pipeline Run

Delete a pipeline run.

1. Select the pipeline run to delete.
2. Click **Delete Pipeline Run**. An ongoing pipeline run cannot be deleted.
3. The requested deletion operation cannot be canceled. Click **Delete** to proceed.

<a id="pipeline.schedule"></a>

## Pipeline Schedule

You can create and manage schedules to periodically execute uploaded pipelines in AI EasyMaker.

<a id="pipeline.recurring.run.create"></a>

### Create Pipeline Schedule

Create a schedule to periodically execute a pipeline.

For settings available when creating a pipeline schedule, refer to other items not listed below in [Create Pipeline Run](#pipeline.run.create).

- **Run Information**
    - **Run Type**: Select the pipeline run type. If you select **Schedule**, the pipeline will be executed periodically. To run the pipeline only once, select **One-time**.
    - **Trigger Type**: Select the pipeline execution trigger type. You can choose **Time interval** or **Cron expression**.
        - To run the pipeline repeatedly using time interval settings, select **Time interval** and enter a number and time unit.
        - To run the pipeline repeatedly using a Cron expression, select **Cron expression** and enter the Cron expression.
    - **Concurrent Execution Settings**: Depending on the trigger period (**Time interval** or **Cron expression**), a new pipeline run may be created before a previously created pipeline run completes. You can limit the number of parallel executions by specifying the maximum number of concurrent runs.
    - **Start Time**: Set the start time of the pipeline schedule. If not entered, pipeline runs will be created according to the configured interval.
    - **End Time**: Set the end time of the pipeline schedule. If not entered, pipeline runs will be created until stopped.
    - **Catchup Missing Runs**: Determine whether to catch up if pipeline runs fall behind schedule.
        - For example, if the pipeline schedule is temporarily paused and then restarted, setting this to **Enabled** will catch up on missed pipeline runs.
        - If the pipeline handles backfill internally, set this to **Disabled** to prevent duplicate backfill operations.

!!! tip "Note"
    Creating a pipeline schedule may take several minutes.
    When creating a resource for the first time, additional time is required to configure the service environment.

!!! tip "Note"
    Cron expressions use six space-separated fields to represent time.
    For more information, refer to the [Cron Expression Format](https://pkg.go.dev/github.com/robfig/cron#hdr-CRON_Expression_Format) documentation.

<a id="pipeline.recurring.run.list"></a>

### Pipeline Schedule List

The pipeline schedule list is displayed. When you select a pipeline schedule from the list, you can view detailed information and change the settings.

- **Status**: The status of the pipeline schedule is displayed. Refer to the table below for major statuses.

    | Status                           | Description                                          |
    |-------------------------------|---------------------------------------------|
    | CREATE REQUESTED              | Pipeline schedule creation has been requested.                     |
    | CREATE FAILED                 | Pipeline schedule creation failed. Please try again.           |
    | ENABLED                       | Pipeline schedule has started normally.                  |
    | ENABLED(EXPIRED)              | Pipeline schedule has started normally but has passed the configured end time. |
    | DISABLED                      | Pipeline schedule has been stopped at the user's request.              |

- **Run Management**: When you select a pipeline schedule from the list, you can view the list of runs created by the pipeline schedule in the **Run Management** tab of the detailed screen.

<a id="pipeline.recurring.run.start.stop"></a>

### Start and Stop Pipeline Schedule

Stop a started pipeline schedule or start a stopped pipeline schedule.

1. Select the pipeline schedule to start or stop from the list.
2. Click **Start Schedule** or **Stop Schedule**.

<a id="pipeline.recurring.run.copy"></a>

### Copy Pipeline Schedule

Create a new pipeline schedule with the same settings as an existing pipeline schedule.

1. Select the pipeline schedule to copy.
2. Click **Copy Pipeline Schedule**.
3. The pipeline schedule creation screen appears with the same settings as the existing pipeline schedule.
4. If there are settings you want to change, make the changes and click **Create Pipeline Schedule**.

<a id="pipeline.recurring.run.delete"></a>

### Delete Pipeline Schedule

Delete a pipeline schedule.

1. Select the pipeline schedule to delete.
2. Click **Delete Pipeline Schedule**.
3. The requested delete operation cannot be cancelled. To proceed, click **Delete**.

!!! tip "Note"
    You cannot delete a pipeline schedule if runs created by that schedule are still in progress. Delete the pipeline schedule after the pipeline runs are completed.

<a id="rag"></a>

## RAG

RAG (Retrieval-Augmented Generation) is a technology that vectorizes and stores user documents, searches for content related to questions, and increases the accuracy of LLM (Large Language Model) responses. AI EasyMaker allows you to create and manage RAG systems by integrating vector stores, embedding models, and LLMs.

<a id="rag.create"></a>

### Create RAG

Create a new RAG.

- **API Gateway Service Activation**
    - AI EasyMaker RAG uses NHN Cloud API Gateway service to create and manage API endpoints. You must enable the API Gateway service to use RAG functionality.
    - For more information about the API Gateway service and pricing, see the following:
        - [API Gateway Service Guide](https://docs.nhncloud.com/ko/Application%20Service/API%20Gateway/ko/overview/)
        - [API Gateway Service Pricing](https://www.nhncloud.com/kr/pricing/by-service?c=Application%20Service&s=API%20Gateway)
- **Basic Settings**
    - **Name**: Enter the RAG name. RAG names must be unique.
    - **Description**: Enter a description for the RAG.
    - **Instance Type**: Select the instance type to run the RAG endpoint.
    - **Number of Instances**: Enter the number of instances to run the RAG endpoint.
    - **Prompt**: The prompt to be used in the RAG endpoint. Click **View Details** to see the full content of the prompt.
- **Vector Store Settings**
    - **Vector Store Type**: Select the vector store type.
        - **RDS for PostgreSQL**
            - **Enable RDS for PostgreSQL**
                - AI EasyMaker RAG uses NHN Cloud RDS for PostgreSQL to create and manage vector stores. If you select this option, you must enable RDS for PostgreSQL.
                - For more information about RDS for PostgreSQL and pricing, see the following:
                    - [RDS for PostgreSQL Guide](https://docs.nhncloud.com/ko/Database/RDS%20for%20PostgreSQL/ko/overview/)
                    - [RDS for PostgreSQL Service Pricing](https://www.nhncloud.com/kr/pricing/by-service?c=Database&s=RDS%20for%20PostgreSQL)
            - **Instance Type**: Select the instance type to use in RDS for PostgreSQL.
            - **Storage Type**: Select the storage type to use in RDS for PostgreSQL.
            - **Storage Size**: The storage size to use in RDS for PostgreSQL.
            - **User ID**: Enter the user ID to use for PostgreSQL connection.
            - **Password**: Enter the password to use for PostgreSQL connection.
            - **Confirm Password**: Re-enter the password to confirm it.
            - **VPC ID**: Enter the VPC ID to use in RDS for PostgreSQL.
            - **Subnet ID**: Enter the subnet ID to use in RDS for PostgreSQL.
        - **PostgreSQL Instance**: Use the NHN Cloud PostgreSQL Instance you created as a vector store.
            - **User ID**: Enter the user ID that can access the PostgreSQL Instance.
            - **Password**: Enter the password that can access the PostgreSQL Instance.
            - **VPC ID**: Enter the VPC ID of the PostgreSQL Instance.
            - **Subnet ID**: Enter the subnet ID of the PostgreSQL Instance.
            - **PostgreSQL Instance IP**: Enter the IP address of the PostgreSQL Instance.
    - **Ingestion Settings**
        - **Data Path**: Enter the data path where documents to be collected in the vector store are stored.
    - **Embedding Model**
        - **Model**: Select the embedding model to use when vectorizing documents and queries.
        - **Instance Type**: The instance type to run the embedding model.
        - **Number of Instances**: Enter the number of instances to run the embedding model.
- **LLM Settings**
    - **Model**: Select the LLM to use when generating responses.
    - **Instance Type**: The instance type to run the LLM.
    - **Number of Instances**: The number of instances to run the LLM.
- **Additional Settings**
    - **Log Management**: You can save logs generated during RAG execution to the NHN Cloud Log & Crash Search service.
        - For more information, see [Appendix > 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Guide](#appendix.2.lncs.service.usage.guide.and.log.inquiry.guide).

!!! tip "Tips"
    File formats, sizes, and quantities available for ingestion may be restricted. For more information, see [Ingestion Synchronization](#rag.ingestion.sync).

!!! danger "Caution"
    When using PostgreSQL Instance, set the port to `15432`.
    For how to create an instance, see [PostgreSQL Instance](https://docs.nhncloud.com/ko/Compute/Instance/ko/component-guide/#postgresql-instance).
    Configure the security group to allow access on port `15432` from the instance's subnet range.

!!! danger "Caution"
    Only NHN Cloud NAS created in the same project as AI EasyMaker can be used.

<a id="rag.list"></a>

### RAG List

View and manage the list of created RAGs. When you select a RAG from the list, you can view detailed information.

- **Status**: The status of the RAG. For major statuses, see the table below.

| Status | Description |
| --- | --- |
| CREATE REQUESTED | The RAG creation has been requested. |
| CREATE IN PROGRESS | RAG creation is in progress. |
| ACTIVE | The RAG is operating normally. |
| UPDATE IN PROGRESS | Document ingestion is in progress in the RAG. |
| DELETE IN PROGRESS | RAG deletion is in progress. |
| CREATE FAILED | RAG creation has failed.<br/>Delete the RAG and create it again. If creation failure persists, contact customer support. |
| UPDATE FAILED | Document ingestion has failed in the RAG.<br/>Try **Ingestion Synchronization** again. If update failure persists, contact customer support. |
| DELETE FAILED | RAG deletion has failed.<br/>Try deletion again. If deletion failure persists, contact customer support. |

- **API Gateway Status**: Deployment status information of the API Gateway default stage.

| Status | Description |
| --- | --- |
| DEPLOYING | The API Gateway default stage is being deployed. |
| COMPLETE | The API Gateway default stage has been successfully deployed and is active. |
| FAILURE | API Gateway default stage deployment has failed. |

- **Ingestion History**: When you select a RAG, you can view the execution history of document collection tasks in the **Ingestion History** tab on the detailed screen.
- **API Statistics**: When you select a RAG, you can view API statistics information in the **API Statistics** tab on the detailed screen.
- **Monitoring**: When you select a RAG, you can view the list of monitoring target instances and basic metric charts in the **Monitoring** tab on the detailed screen.

<a id="rag.ingestion.sync"></a>

### Ingestion Synchronization

- When you select a RAG, you can use the ingestion synchronization feature in the **Vector Store** tab on the detailed screen.
- If documents are added, deleted, or modified in the ingestion data path, you can run **Ingestion Synchronization** to reflect the changes.
- File formats, sizes, and quantities available for ingestion may be restricted. For more information, see the table below.

| Item | Limit |
|-----|------|
| Total File Size | 100GB |
| Maximum Number of Files | 1,000,000 |

| Category | Supported Formats | Maximum File Size |
|--------|---------|------------|
| Text Documents | `.txt`, `.text`, `.md` | 3MB |
| Documents | `.doc`, `.docx`, `.pdf` | 50MB |
| Spreadsheets | `.csv`, `.xls`, `.xlsx` | 3MB |
| Presentations | `.ppt`, `.pptx` | 50MB |

<a id="rag.delete"></a>

### Delete RAG

- You cannot delete a RAG while creation or deletion is in progress.
- Requested deletion tasks cannot be canceled.

<a id="rag.query.request.guide"></a>

### RAG Query Request Guide

- When requesting a query, include `model` and `messages` in the request body like the OpenAI Chat Completion API. Enter the RAG name for the `model` field.
- For detailed request examples, see the following content.

<details>
<summary><strong>Call Example (cURL)</strong></summary>

```bash
curl -X POST https://{API endpoint address}/rag/v1/query \
  -H "Content-Type: application/json" \
  -d '{
    "model": "{RAG name}",
    "messages": [
      {
        "role": "user",
        "content": "{query_text}"
      }
    ]
  }'
```

</details>

<details>
<summary><strong>Streaming Call Example (cURL)</strong></summary>

```bash
#!/bin/bash
set -euo pipefail

DEFAULT_URL="https://{API endpoint address}/rag/v1/query"
DEFAULT_MODEL="{RAG name}"
DEFAULT_PROMPT="Please explain the AI EasyMaker service."

usage() {
  cat <<'EOF'
Usage:
  <file name> -k <API_KEY> [-u URL] [-m MODEL] [-p PROMPT]

Options:
  -k   API key (sent as x-nhn-apikey: <API_KEY> header)
  -u   Call URL
  -m   Model name
  -p   User prompt
  -h   Help

Description:
  - Make stream=true calls with OpenAI compatible spec,
    and sequentially write only choices[].delta.content
    of each chunk delivered via streaming to standard output.

Required Tools:
  - curl, jq
EOF
}

API_KEY=""
URL="$DEFAULT_URL"
MODEL="$DEFAULT_MODEL"
PROMPT="$DEFAULT_PROMPT"

while getopts ":k:u:m:p:h" opt; do
  case "$opt" in
    k) API_KEY="$OPTARG" ;;
    u) URL="$OPTARG" ;;
    m) MODEL="$OPTARG" ;;
    p) PROMPT="$OPTARG" ;;
    h) usage; exit 0 ;;
    \?) echo "Unknown option: -$OPTARG" >&2; usage; exit 2 ;;
    :) echo "Option -$OPTARG requires a value." >&2; usage; exit 2 ;;
  esac
done

if ! command -v curl >/dev/null 2>&1; then
  echo "Error: curl is required." >&2
  exit 1
fi
if ! command -v jq >/dev/null 2>&1; then
  echo "Error: jq is required." >&2
  exit 1
fi

# Create JSON Payload (OpenAI Chat Completions compatible format)
payload="$(jq -n \
  --arg model "$MODEL" \
  --arg prompt "$PROMPT" \
  '{
    model: $model,
    messages: [ { role: "user", content: $prompt } ],
    stream: true
  }'
)"

headers=( -H "Content-Type: application/json" )
if [[ -n "$API_KEY" ]]; then
  headers+=( -H "x-nhn-apikey: $API_KEY" )
fi

echo "Request URL: $URL" >&2
echo "Model: $MODEL" >&2
echo "---------------- Streaming Started ----------------" >&2

# Streaming processing: extract only delta.content from data: {json} lines
curl -sS -N -X POST "$URL" "${headers[@]}" --data-raw "$payload" \
| while IFS= read -r line; do
    [[ -z "$line" ]] && continue
    if [[ "$line" == "data: [DONE]"* ]]; then
      break
    fi
    if [[ "$line" == data:* ]]; then
      json="${line#data: }"
      # Output all choices since there may be multiple
      # Handle cases where delta.content may not exist
      while IFS= read -r piece; do
        printf "%s" "$piece"
      done < <(printf '%s\n' "$json" | jq -r '.choices[]?.delta?.content // empty')
    fi
  done

echo
echo "---------------- Streaming Completed ----------------" >&2
```

</details>

<a id="appendix"></a>

## Appendix

<a id="appendix.1.object.storage.account.permission"></a>

### 1. Add AI EasyMaker System Account Permissions to NHN Cloud Object Storage

When some features of AI EasyMaker use your NHN Cloud Object Storage as input/output storage,
you must grant read or write permissions for the AI EasyMaker system account to your NHN Cloud Object Storage container for normal operation.

Granting read/write permissions for the AI EasyMaker system account to your NHN Cloud Object Storage container means that the AI EasyMaker system account can read or write files according to the permissions granted for all files in your NHN Cloud Object Storage container.

You must review this information carefully and configure access policies in your Object Storage only for necessary accounts and permissions.

During the access policy configuration process, you are responsible for any consequences resulting from allowing access to your Object Storage from accounts other than the AI EasyMaker system account. AI EasyMaker assumes no liability for such consequences.

!!! tip "To Know"
    Depending on the feature, the files that AI EasyMaker reads or writes when accessing Object Storage are as follows.

| Feature       | Permission | Access Target                                            |
| ---------- | ---- | ---------------------------------------------------- |
| Training, Hyperparameter Tuning       | Read | Algorithm path and training input data path entered by user |
| Training, Hyperparameter Tuning       | Write | Training output data and checkpoint path entered by user   |
| Model       | Read | Model artifact path entered by user                   |
| Model Evaluation | Read | Input data path entered by user                   |
| Model Evaluation | Write | Output data path entered by user                   |
| Batch Inference | Read | Input data path entered by user                   |
| Batch Inference | Write | Output data path entered by user                   |
| RAG | Read | Collection data path entered by user                   |

To add read/write permissions for the AI EasyMaker system account to NHN Cloud Object Storage, refer to the following:

1. Click **[Training]** or **[Model]** tab > **AI EasyMaker System Account Information**.
2. Save the AI EasyMaker system account information: **AI EasyMaker Tenant ID** and **AI EasyMaker API User ID**.
3. Navigate to the NHN Cloud Object Storage console.
4. Refer to the [Allow read/write access for specific projects or specific users](https://docs.nhncloud.com/ko/Storage/Object%20Storage/ko/acl-guide/#role-based-access-allow-rw-project-or-user) document to add the necessary read and write permissions for the AI EasyMaker system account in the NHN Cloud Object Storage console.

<a id="appendix.2.lncs.service.usage.guide.and.log.inquiry.guide"></a>

### 2. NHN Cloud Log & Crash Search Service Usage Guide and Log Inquiry Method

<a id="appendix.2.lncs.service.usage.guide"></a>

#### NHN Cloud Log & Crash Search Service Usage Guide

Logs and events generated from the AI EasyMaker service can be stored in the NHN Cloud Log & Crash Search service.
To store logs in the Log & Crash Search service, you must enable the Log & Crash service, and separate usage fees will be charged.

- **Log & Crash Search Service Usage and Pricing Information**
    - Detailed information and pricing for the Log & Crash Search service can be found below:
        - [Log & Crash Search Service Guide](https://docs.nhncloud.com/ko/Data%20&%20Analytics/Log%20&%20Crash%20Search/ko/Overview/)
        - [Log & Crash Search Pricing](https://www.nhncloud.com/kr/pricing/by-service?c=Data%20%26%20Analytics&s=Log%20%26%20Crash%20Search)

<a id="appendix.2.lncs.service.log.inquiry.guide"></a>

#### Log Inquiry

1. Navigate to the Log & Crash Search service console page.
2. Enter search conditions in the Log & Crash Search service to retrieve logs.
    - AI EasyMaker training log query: Retrieve logs where the category field is "easymaker.training".
        - Query: category:"easymaker.training"
    - AI EasyMaker endpoint log query: Retrieve logs where the category field is "easymaker.inference".
        - Query: category:"easymaker.inference"
    - AI EasyMaker full log query: Retrieve logs where the logType field is "NHNCloud-AIEasyMaker".
        - Query: logType:"NHNCloud\-AIEasyMaker"
3. For detailed usage instructions for the Log & Crash Search service, refer to [Log & Crash Search Service Console Guide](https://docs.nhncloud.com/ko/Data%20&%20Analytics/Log%20&%20Crash%20Search/ko/console-guide/).

The AI EasyMaker service sends logs to the Log & Crash Search service with fields defined as follows:

- **Common Log Fields**

    | Name            | Description              | Valid Range                             |
    | --------------- | ------------------------- | --------------------------------------- |
    | easymakerAppKey | AI EasyMaker AppKey       | -                                       |
    | category        | Log category             | easymaker.training, easymaker.inference |
    | logLevel        | Log level                | INFO, WARNING, ERROR                    |
    | body            | Log content              | -                                       |
    | logType         | Log provider service name| NHNCloud-AIEasyMaker                    |
    | time            | Log occurrence time (UTC)| -                                       |

- **Training Log Fields**

    | Name       | Description         |
    | ---------- | -------------------- |
    | trainingId | AI EasyMaker Training ID |

- **Hyperparameter Tuning Log Fields**

    | Name                   | Description                            |
    | ---------------------- | ----------------------------------- |
    | hyperparameterTuningId | AI EasyMaker Hyperparameter Tuning ID |

- **Endpoint Log Fields**

    | Name            | Description                     |
    | --------------- | --------------------------- |
    | endpointId      | AI EasyMaker Endpoint ID    |
    | endpointStageId | Endpoint Stage ID           |
    | inferenceId     | Inference Request Unique ID |
    | action          | Action type (Endpoint.Model) |
    | modelName       | Target model name for inference |

- **Batch Inference Log Fields**

    | Name             | Description                  |
    | ---------------- | ------------------------- |
    | batchInferenceId | AI EasyMaker Batch Inference ID |

<a id="appendix.3.hyperparameter"></a>

### 3. Hyperparameters

- Key-Value format values received through the console.
- Passed as execution arguments (--{Key}) when running the entry point.
- Can also be stored and used as environment variable values (EM_HP_{Key converted to uppercase}).

You can use hyperparameter values entered when creating training as shown in the example below.<br>
![Hyperparameter input screen](http://static.toastoven.net/prod_ai_easymaker/console-guide_appendix_hyperparameter_ko.png)

```python
import argparse

model_version = os.environ.get("EM_HP_MODEL_VERSION")

def parse_hyperparameters():
    parser = argparse.ArgumentParser()

    # Parse input hyperparameters
    parser.add_argument("--epochs", type=int, default=500)
    parser.add_argument("--batch_size", type=int, default=32)
    ...

    return parser.parse_known_args()
```

<a id="appendix.4.environment"></a>

### 4. Environment Variables

- Information required for training is passed to the training container as **environment variables**, and the **training script** can utilize the environment variables passed to it.
- Environment variable names created from user input are converted to uppercase.
- In your code, the trained model must be saved to the path specified in EM_MODEL_DIR.
- **Key Environment Variables**

    | Environment Variable Name                      | Description                                                                        |
    |-----------------------------| --------------------------------------------------------------------------- |
    | EM_SOURCE_DIR               | Absolute path to the folder where the algorithm script entered during training creation is downloaded  |
    | EM_ENTRY_POINT              | Algorithm entry point name entered during training creation                             |
    | EM_DATASET_${Dataset Name}     | Absolute path to the folder where each dataset entered during training creation is downloaded |
    | EM_DATASETS                 | List of all datasets (JSON format)                                            |
    | EM_MODEL_DIR                | Model save path                                                              |
    | EM_CHECKPOINT_INPUT_DIR     | Input checkpoint save path                                                  |
    | EM_CHECKPOINT_DIR           | Output checkpoint save path                                                  |
    | EM_HP_${Hyperparameter Key in Uppercase} | Hyperparameter value corresponding to the hyperparameter key                              |
    | EM_HPS                      | List of all hyperparameters (JSON format)                                         |
    | EM_TENSORBOARD_LOG_DIR      | TensorBoard log path for checking training results                                    |
    | EM_REGION                   | Current region information                                                              |
    | EM_APPKEY                   | App key for the currently used AI EasyMaker service                                   |

- **Example Code Using Environment Variables**

```python
import os
import tensorflow

dataset_dir = os.environ.get("EM_DATASET_TRAIN")
train_data = read_data(dataset_dir, "train.csv")

model = ... # Implement model using input data
model.load_weights(os.environ.get('EM_CHECKPOINT_INPUT_DIR', None))
callbacks = [
    tensorflow.keras.callbacks.ModelCheckpoint(filepath=f'{os.environ.get("EM_CHECKPOINT_DIR")}/cp-{{epoch:04d}}.ckpt', save_freq='epoch', period=50),
    tensorflow.keras.callbacks.TensorBoard(log_dir=f'{os.environ.get("EM_TENSORBOARD_LOG_DIR")}'),
]
model.fit(..., callbacks)

model_dir = os.environ.get("EM_MODEL_DIR")
model.save(model_dir)
```

<a id="appendix.5.tensorboard.store.metric.log"></a>

### 5. Saving metric logs for TensorBoard

- To check result metrics on the TensorBoard dashboard after training, you must set the TensorBoard log storage location to the specified path (`EM_TENSORBOARD_LOG_DIR`) when writing your training script.

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

<details>
<summary><strong>Checking TensorBoard logs</strong></summary>

<img src="http://static.toastoven.net/prod_ai_easymaker/console-guide_appendix_tensorboard.png" alt="Checking TensorBoard logs">

</details>

!!! danger "Caution"
    TensorBoard metric logs are retained for 120 days. Metric logs older than 120 days are automatically deleted.

<a id="appendix.6.framework.training.settings"></a>

### 6. Distributed training configuration by framework

- **Tensorflow**
    - The `TF_CONFIG` environment variable required for distributed training is set automatically. For more details, refer to the [Tensorflow official guide documentation](https://www.tensorflow.org/guide/distributed_training#multiworkermirroredstrategy).
- **Pytorch**
    - The `Backends` configuration is required for distributed training. Set it to gloo if conducting distributed training on CPU, or nccl if on GPU. For more details, refer to the [Pytorch official guide documentation](https://pytorch.org/docs/stable/distributed.html).

<a id="appendix.7.cluster.upgrade"></a>

### 7. Cluster Version Upgrade

AI EasyMaker service periodically upgrades cluster versions to provide stable service and new features.
When a new cluster version is deployed, notebooks and endpoints running on the old version cluster must be migrated to the new cluster.
This guide provides the migration method for each resource type.

<a id="appendix.7.cluster.upgrade.notebook"></a>

#### Notebook Cluster Version Upgrade

In the **Notebook** list screen, notebooks that need to be migrated to a new cluster will display a **Restart** button to the left of their name.
When you hover your mouse pointer over the **Restart** button, a restart instruction message and expiration date will be displayed.

- Before expiration, verify the following precautions and click the **Restart** button.
    - When restarted, data stored in data storage (the /root/easymaker directory path) will be preserved.
    - When restart is executed, data stored in boot storage will be reset and may be lost. Move data to data storage before restarting.

The restart takes approximately 25 minutes on the first execution, and approximately 10 minutes thereafter.
If a restart fails, it will be automatically reported to the administrator.

<a id="appendix.7.cluster.upgrade.endpoint"></a>

#### Endpoint Cluster Version Upgrade

In the **Endpoint List** screen, endpoints that need to be migrated to a new cluster will display a **! Notice** message to the left of their name.
When you hover your mouse pointer over the **! Notice** message, a version upgrade instruction message and expiration date will be displayed.
Before expiration, you must migrate stages running on the old version cluster to the new version cluster following the guidance below.

<a id="appendix.7.cluster.upgrade.endpoint.stage"></a>

##### Cluster Version Upgrade for General Stages

1. Delete general stages that are not the default stage. Before deletion, first verify whether the stage is in service.
2. Recreate the stage.
3. When the new stage becomes ACTIVE, verify that API calls and inference responses are functioning normally at the stage endpoint.

!!! danger "Caution"
    If you delete a stage, the endpoint will be terminated and API calls will not be possible. Before deletion, verify that the stage is not in service.

<a id="appendix.7.cluster.upgrade.endpoint.default.stage"></a>

##### Cluster Version Upgrade for Default Stage

The default stage is the stage where actual service is operated.
To migrate the cluster version of the default stage without service downtime, follow the guide below.

1. Create a new stage to replace the default stage of the old version cluster.
2. Verify that API calls and inference responses are functioning normally at the new stage endpoint.
3. Click the **Change Default Stage** button. Select the new stage to change it to the default stage.
4. When the change is complete, the new stage will be set as the default stage, and the existing default stage will be deleted.

<a id="appendix.8.torchrun.usage"></a>

### 8. How to Use torchrun

- The code is written to enable distributed training in PyTorch. When you specify the number of distributed nodes and the number of processes per node, distributed training is performed using torchrun with distributed nodes and multi-process capabilities.
- Training and hyperparameter tuning may fail due to insufficient memory caused by factors such as the total number of processes, model size, input data size, and batch size. If training fails due to insufficient memory, an error message like the one below may appear. However, the presence of the message below does not necessarily indicate that the failure is due to insufficient memory. Set an appropriate instance type based on your memory usage.

```plaintext
exit code : -9 (pid: {pid})
```

- For more detailed information about torchrun, refer to the [PyTorch official guide documentation](https://pytorch.org/docs/stable/elastic/run.html).

<a id="appendix.9.resource.info"></a>

### 9. Resource Information

When creating batch inference or endpoints in AI EasyMaker, resources are allocated from the selected instance type, excluding the default usage. Since the required resources vary depending on the model's request volume and complexity, carefully configure the number of pods and resource allocation along with an appropriate instance type.

For batch inference, actual usage is divided by the number of pods to allocate resources to each pod. For endpoints, the allocated resources you specify cannot exceed the actual usage of the instance, so verify resource usage in advance.
For both batch inference and endpoints, creation may fail if the allocated resources are less than the minimum usage required for inference, so be careful.

<a id="appendix.10.endpoint.api.specification"></a>

### 10. Endpoint API Specification

AI EasyMaker service provides endpoints based on the OIP (open inference protocol) specification.
For detailed information about the OIP specification, refer to [OIP specification](https://github.com/kserve/open-inference-protocol).

| Name                          | Method | API Path                                                                |
| ----------------------------- | ------ | ----------------------------------------------------------------------- |
| Model List                    | GET    | /{model_name}/v1/models                                                 |
| Model Ready                   | GET    | /{model_name}/v1/models/{model_name}                                    |
| Inference                     | POST   | /{model_name}/v1/models/{model_name}/predict                            |
| Explain                       | POST   | /{model_name}/v1/models/{model_name}/explain                            |
| Server Information            | GET    | /{model_name}/v2                                                        |
| Server Live                   | GET    | /{model_name}/v2/health/live                                            |
| Server Ready                  | GET    | /{model_name}/v2/health/ready                                           |
| Model Information             | GET    | /{model_name}/v2/models/{model_name}\[/versions/{model_version}\]       |
| Model Ready                   | GET    | /{model_name}/v2/models/{model_name}\[/versions/{model_version}\]/ready |
| Inference                     | POST   | /{model_name}/v2/models/{model_name}\[/versions/{model_version}\]/infer |
| OpenAI Generative Model Inference | POST   | /{model_name}/openai/v1/completions                                     |
| OpenAI Generative Model Inference | POST   | /{model_name}/openai/v1/chat/completions                                |

!!! tip "Note"
    OpenAI generative model inference is used when using generative models such as OpenAI's GPT-4o.
    Input values required for inference must be provided according to OpenAI's API specification. For more details, refer to [OpenAI API documentation](https://platform.openai.com/docs/api-reference/chat).
    For models supported by Completion and Chat Completion APIs provided by AI EasyMaker, check [Model endpoint compatibility](https://platform.openai.com/docs/models/model-endpoint-compatibility).

<a id="appendix.11.framework.note"></a>

### 11. Framework-specific serving notes

<a id="appendix.11.framework.note.tensorflow.framework"></a>

#### TensorFlow Framework

TensorFlow model serving provided by AI EasyMaker uses SavedModel(.pb) recommended by TensorFlow.
To use checkpoints, save the checkpoint variables directory in SavedModel format together in the model directory, and it will be used for model serving.
Reference: [https://www.tensorflow.org/guide/saved_model](https://www.tensorflow.org/guide/saved_model)

<a id="appendix.11.framework.note.pytorch.framework"></a>

#### PyTorch Framework

AI EasyMaker serves PyTorch models(.mar) using TorchServe.
It is recommended to use MAR files created with model-archiver, and serving with weight files is also possible, but there are required files that must be included with weight files.
For the required files and detailed information, check the table below and the [model-archiver documentation](https://github.com/pytorch/serve/blob/master/model-archiver/README.md).

| File Name                    | Required | Description                                                    |
| ---------------------------- | --------- | -------------------------------------------------------------- |
| model.py                     | Yes       | Model structure file passed as the model-file parameter.       |
| handler.py                   | Yes       | File passed as the handler parameter to handle inference logic. |
| weight file(.pt, .pth, .bin) | Yes       | File storing model weights and structure.                      |
| requirements.txt             | No        | File for installing Python packages required for serving.      |
| extra/                       | No        | Files in the directory are passed as the extra-files parameter.|

!!! danger "Caution"
    There is a difference in request format between using TorchServe directly and using AI EasyMaker serving, so please be careful when writing handler.py.
    Check the values passed in the handler.py example below and write the handler accordingly.

<details>
<summary><strong>Request example (cURL)</strong></summary>

```bash
curl --location --request POST '{API Gateway resource path}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "instances": [
        [1.0, 2.0],
        [3.0, 4.0]
    ]
}'
```

</details>

<details>
<summary><strong>Example (handler.py)</strong></summary>

```python
class TestHandler(BaseHandler):
    # ...
    def preprocess(self, data): # Example: data = [[1.0, 2.0], [3.0, 4.0]]
        features = []
        for row in data:
            content = row # Example: row = [1.0, 2.0]
            features.append(content)
        tensor = torch.tensor(features, dtype=torch.float32).to(self.device)
        return tensor
    # ...
```

</details>

<a id="appendix.11.framework.note.scikitlearn.framework"></a>

#### Scikit-learn Framework

AI EasyMaker serves Scikit-learn models(.joblib) using mlserver.
The `model-settings.json` required when using mlserver directly is not necessary when using AI EasyMaker serving.

<a id="appendix.11.framework.note.hugging.face.framework"></a>

#### Hugging Face Framework

Hugging Face models can be served using the runtime provided by AI EasyMaker or using TensorFlow Serving and TorchServe.

<a id="appendix.11.framework.note.hugging.face.framework.runtime"></a>

##### Hugging Face Runtime

An easy way to serve Hugging Face models.
Hugging Face runtime serving does not support fine-tuning. To serve fine-tuned models, use the TensorFlow/PyTorch Serving method.

1. Check the model you want to serve on Hugging Face.
2. Copy the Hugging Face model ID.
3. On the AI EasyMaker model creation page, select the Hugging Face framework and enter the Hugging Face model ID.
4. Create the model by entering the required input values according to the model.
5. Check the created model and create an endpoint.

!!! tip "Note"
    Currently, the Hugging Face runtime does not support all Hugging Face tasks.
    Supported tasks are `sequence_classification`, `token_classification`, `fill_mask`, `text_generation`, and `text2text_generation`.
    To use unsupported tasks, use the TensorFlow/PyTorch Serving method.

!!! tip "Note"
    To serve a Gated Model, you must enter a token from an account with access permission as a model parameter.
    If you do not enter a token or enter a token from an unauthorized account, model deployment will fail.

<a id="appendix.11.framework.note.hugging.face.framework.tensorflow.pytorch.serving"></a>

##### TensorFlow/PyTorch Serving

How to serve Hugging Face models trained with TensorFlow and PyTorch.

1. Download the Hugging Face model.
    - You can download it using AutoTokenizer, AutoConfig, and AutoModel from the transformers library as shown in the example code below.

            from transformers import AutoTokenizer, AutoConfig, AutoModel

            model_id = "<model_id>"
            revision = "main"

            model_dir = f"./models/{model_id}/{revision}"

            tokenizer = AutoTokenizer.from_pretrained(model_id, revision=revision)
            model_config = AutoConfig.from_pretrained(model_id, revision=revision)
            model = AutoModel.from_config(model_config)

            tokenizer.save_pretrained(model_dir)
            model.save_pretrained(model_dir)

    - If model download fails, try importing the class that matches the model instead of AutoModel and attempt to download again.
    - If fine-tuning is necessary, you can write and train your own code according to the [Hugging Face fine-tuning guide](https://huggingface.co/docs/transformers/main/ko/training).
        - For more details on AI EasyMaker training, check [Training](#training).

2. Check the Hugging Face model information and create the files needed for serving.
    - Save the model in the form required for framework-specific serving.
    - For more details, check the notes on TensorFlow and PyTorch frameworks.
3. Upload the model files to OBS or NAS.
4. For the subsequent steps, check the [Model Creation](#model.create) and [Endpoint Creation](#endpoint.create) guides.