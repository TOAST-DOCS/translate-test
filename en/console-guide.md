<!-- machine_translated: true -->

<!-- pre-align:aligned sig=40aa83d794a8 -->

<a id="dev-tools-deploy-console-user-guide"></a>
## Dev Tools > Deploy > Console User Guide { #dev-tools-deploy-console-user-guide }

This document covers the following:

* [Deploy Console Page](#deploy-console-page)
* [Client Application](#client-application)
* [Server Application](#server-application)

(For features not covered here, see the [Detail Functional Guide](./reference/).)

<a id="deploy-console-page"></a>
## Deploy Console Page { #deploy-console-page }

The following is the Deploy service Console page.

![deploy_02_201812](https://static.toastoven.net/prod_tcdeploy/deploy_02_201812.png)

<a id="client-application"></a>
## Client Application { #client-application }

Client application deployment configuration involves two main steps: Setting Artifacts and binary upload.

<a id="setting-artifacts"></a>
### Setting Artifacts { #setting-artifacts }

![deploy_03_201812](https://static.toastoven.net/prod_tcdeploy/deploy_03_201812.png)

1. In the upper left of the **Deploy** page, click **Create**.
2. Select **Client Application** as the artifact type.
    - Enter a name (required), description (optional), and port (required).
3. Click **Create**.

<a id="setting-binaries"></a>
### Binary Settings { #setting-binaries }

<a id="upload"></a>
#### Upload

* For iOS, upload .ipa and .plist files. For Android, upload an .apk file.
* The etc option is used for installation applications on other operating systems, such as Windows.

![deploy_04_201812](https://static.toastoven.net/prod_tcdeploy/deploy_04_201812.png)

1. On the bottom tab of the **Deploy** page, click **Binary Group > Default**.
    To create a new Binary Group, click **New**.
2. Click **Upload** on the right.
3. In the **Binary Upload** dialog, click **Select Files** and select a binary file.
    * iOS: .ipa file (required), .plist file (required)
        * .plist: Used for installation on the Download Page. The download URL inside the file is optional.
    * Android: .apk file (required)
    * Enter version (optional) and description (optional).
4. When finished, click **Upload**.

<a id="deploy"></a>
#### Deploy

You can send a specific binary Download Page via SMS or email.

![deploy_27_202407](https://static.toastoven.net/prod_tcdeploy/deploy_27_202407.png)
![deploy_28_202407](https://static.toastoven.net/prod_tcdeploy/deploy_28_202407.png)
![deploy_29_202407](https://static.toastoven.net/prod_tcdeploy/deploy_29_202407.png)

1. Click **Send** on the right.
2. In the **Send Download Path** dialog, set **Send Type** and **Recipient**, then click **Send**.
    * For **Send Type**, select **SMS**, **E-mail**, or both.
    * In **Individual Selection**, you can select recipients individually. In **Select Group**, you can select a notification recipient group.
    * Choose the **Select Group** tab and click **View** in the **Details** column to open the project notification recipient group management dialog.

The binary Download Page is sent to recipients via the specified Send Type.

<a id="server-application"></a>
## Server Application { #server-application }

Server application deployment goes through configuration (artifact, Server Group, Scenario), binary upload, and the deployment step.

<a id="server-application-setting-artifacts"></a>
### Setting Artifacts { #server-application-setting-artifacts }

![deploy_06_201812](https://static.toastoven.net/prod_tcdeploy/deploy_06_201812.png)

1. Click **Create** above the list.
2. Select **Server Application** as the artifact type.
    - Enter a name (required), description (optional), and port (required).
3. In the **Create Artifacts** dialog, click **Create**.

<a id="setting-server-groups"></a>
### Server Group Settings { #setting-server-groups }

This feature lets you manage servers for deployment.

![deploy_07_201812](https://static.toastoven.net/prod_tcdeploy/deploy_07_201812.png)

1. On the bottom tab of the **Deploy** page, click **Server Group > New**.
2. In the **Create Server Group** dialog, configure the new Server Group.
    * Enter a name (required) and description (optional).
    * Select an OS and specify the Shell Type. You can select the Shell Type from the **Shell Type** list or enter it manually.
    * Select a Phase. This distinguishes server equipment. Select NONE if you do not want to specify one.
    * Add a server.
        * There are two ways to add a server. For more information, see the [Detail Functional Guide Server Group Menu](./reference/#server-group).
            * Bulk add
            * Individual add
         * Enter the host name (required), IP address (required), and OS (optional), then click **Add**.
         * Check the server list below to confirm what was added. Only servers with the left checkbox selected are registered.

3. When finished, click **Create**.

<a id="setting-binary-groups"></a>
### Binary Group Settings { #setting-binary-groups }

This feature lets you manage binaries for deployment.

![deploy_25_202402](https://static.toastoven.net/prod_tcdeploy/deploy_25_202402.png)
![deploy_26_202402](https://static.toastoven.net/prod_tcdeploy/deploy_26_202402.png)

1. On the bottom tab of the **Deploy** page, click **Binary Group > New**.
    * A default Binary Group is automatically created when you create an artifact.
2. In the **Create Binary Group** dialog, configure the new Binary Group.
    * Enter a name, description, and region.
        * If the **region** differs from the region of the deployment target server, network latency may increase.
    * Configure Auto-delete Settings.
        * This feature periodically deletes binaries based on conditions such as period, capacity, and count. 
        * The maximum count and minimum retained count are required values, and up to 10 can be configured.
3. When finished, click **Create**.

<a id="create-scenarios"></a>
### Create Scenarios { #create-scenarios }

![deploy_08_201812](https://static.toastoven.net/prod_tcdeploy/deploy_08_201812.png)

1. On the bottom tab of the **Deploy** page, click **Deploy > New**.
2. Enter a scenario name (optional) in the scenario area added below.
3. Click **Create**.

<a id="add-tasks"></a>
### Add Tasks { #add-tasks }

A task is a scenario component that performs individual functions and controls execution order.
There are two types of tasks:

* pre-run Task: Runs before deployment.
* Normal Task: Runs during deployment.

You can select the type you want. This section covers the tasks required for a basic deployment.
For more tasks, see the [Task Menu in the Detail Functional Guide](./reference/#tasks).

Add the following three tasks for a deployment test.

<a id="add-user-commands"></a>
#### 1. Add User Command

* This is a user-defined Command task that runs during deployment.
* You can use Available Variables.
    * Available Variables: Reserved words. For more information, see the [Task Menu in the Detail Functional Guide](./reference/#tasks).

![deploy_09_201812](https://static.toastoven.net/prod_tcdeploy/deploy_09_201812.png)

1. In the scenario area of the **Deploy** tab, click **Add Tasks** on the right.
2. Click **User Command** under **Normal Task**.
3. Enter the details for the new task.
    * Timeout(min)
        * Specifies how long to wait for the task to finish. Minimum: 1 minute, maximum: 30 minutes.
    * Run As
        * Enter the execution account.
    * Command
        * Enter the command to run.

4. When done entering or modifying, click **Apply**. 

<a id="add-binary-deploy"></a>
#### 2. Add Binary Deploy

This task lets you configure the deployment of an uploaded Binary File.

![deploy_10_201812](https://static.toastoven.net/prod_tcdeploy/deploy_10_201812.png)

1. Click **Add Tasks** and click **Binary Deploy** under **Normal Task**.
2. Enter the details for the new task.
    * Timeout(min)
        * Specifies how long to wait for the task to finish. Minimum: 1 minute, maximum: 30 minutes.
    * Run As
        * Enter the execution account.
3. To upload a Binary File, click **Upload** on the right.
4. Enter the Binary File information.
    * Click **Select Files** to select a Binary File.
    * Enter version (optional) and description (optional).
5. Click **Upload**. 
6. After the upload is complete, click **Select Binary**.
7. Select the binary version you want.
    * When multiple versions exist, use the search feature.
8. Click **Select**.
  <br/>
   * Variable As
       * Specify a variable name for this binary to use binary information in User Command. For more information, see the Task Menu section at the bottom of the [Detail Functional Guide](./reference/).
   * Target Directory
       * Specify the target directory to deploy the binary to.

<a id="add-tasks-add-user-commands"></a>
#### 3. Add User Command

![deploy_11_201812](https://static.toastoven.net/prod_tcdeploy/deploy_11_201812.png)

1. Click **Add Tasks** and click **User Command** under **Normal Task**.
2. Enter the details for the new task.
    * Timeout(min)
        * Specifies how long to wait for the task to finish. Minimum: 1 minute, maximum: 30 minutes.
    * Run As
        * Enter the execution account.
    * Command
        * Enter the command to run.
3. When done entering or modifying, click **Apply**. 

<a id="execute"></a>
### Execute { #execute }

![deploy_12_201812](https://static.toastoven.net/prod_tcdeploy/deploy_12_201812.png)

1. Click **Execute** on the right to request the deployment.
2. Enter the deployment execution information.
    * Specify a Deployment Note (optional) and an authentication method.
    * If **Password** is selected, enter a password or select and upload a .pem file.
3. When finished, click **Confirm**.

![deploy_13_201812](https://static.toastoven.net/prod_tcdeploy/deploy_13_201812.png)

1. You can check the deployment progress.
2. Verify that the deployment is complete.
    * Use the exit code to check whether each task ran successfully.
3. To check detailed results, click **See Results**.
4. Check the deployment result in the **See Results** dialog.
    * You can check details for each task execution (return values, exit codes, errors, and more).

- - -

You have deployed files to the server!
NHN Cloud Deploy supports many more features. For more information, see the [Detail Functional Guide](./reference/).