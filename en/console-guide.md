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

Client application deployment settings involve two main steps: setting artifacts and uploading binaries.

<a id="setting-artifacts"></a>
### Setting Artifacts { #setting-artifacts }

![deploy_03_201812](https://static.toastoven.net/prod_tcdeploy/deploy_03_201812.png)

1. In the top left of the **Deploy** page, choose **Create**.
2. Select **Client Application** for the artifact type.
    - Enter name (required), description (optional), and port (required).
3. Choose **Create**.

<a id="setting-binaries"></a>
### Binary Settings { #setting-binaries }

<a id="upload"></a>
#### Upload

* For iOS, upload .ipa and .plist files. For Android, upload .apk files.
* The etc option is used for installation applications on other operating systems, such as Windows.

![deploy_04_201812](https://static.toastoven.net/prod_tcdeploy/deploy_04_201812.png)

1. On the **Deploy** page, choose **Binary Group > Default** in the bottom tabs.
    To create a new binary group, choose **New**.
2. Choose **Upload** on the right.
3. In the **Binary Upload** window, choose **Select Files** and select the binary file.
    * iOS: .ipa file (required), .plist file (required)
        * .plist: Used for installation on the Download Page. The download URL in the file is optional.
    * Android: .apk file (required)
    * Enter version (optional) and description (optional).
4. When finished, choose **Upload**.

<a id="deploy"></a>
#### Deploy

You can send a specific binary download page link via SMS or email.

![deploy_27_202407](https://static.toastoven.net/prod_tcdeploy/deploy_27_202407.png)
![deploy_28_202407](https://static.toastoven.net/prod_tcdeploy/deploy_28_202407.png)
![deploy_29_202407](https://static.toastoven.net/prod_tcdeploy/deploy_29_202407.png)

1. Choose **Send** on the right.
2. In the **Send Download Path** window, set the **Send Type** and **Recipient**, then choose **Send**.
    * For **Send Type**, you can select **SMS**, **E-mail**, or both.
    * In **Individual Selection**, you can select recipients individually. In **Select Group**, you can select a notification receiver group.
    * On the **Select Group** tab, choose **View** in the **Details** column to open the project notification receiver group management window.

The binary download page is sent to recipients via the specified send type.

<a id="server-application"></a>
## Server Application { #server-application }

Server application deployment involves configuration steps (artifact, server group, and scenario), binary upload, and deployment.

<a id="server-application-setting-artifacts"></a>
### Setting Artifacts { #server-application-setting-artifacts }

![deploy_06_201812](https://static.toastoven.net/prod_tcdeploy/deploy_06_201812.png)

1. Choose **Create** above the list.
2. Select **Server Application** for the artifact type.
    - Enter name (required), description (optional), and port (required).
3. In the **Create Artifact** window, choose **Create**.

<a id="setting-server-groups"></a>
### Server Group Settings { #setting-server-groups }

This feature lets you manage servers to deploy to.

![deploy_07_201812](https://static.toastoven.net/prod_tcdeploy/deploy_07_201812.png)

1. On the **Deploy** page, choose **Server Group > New** in the bottom tabs.
2. In the **Create Server Group** window, configure the new server group.
    * Enter name (required) and description (optional).
    * Select an OS and specify the Shell Type. You can select the Shell Type from the **Shell Type** list or enter it manually.
    * Select a Phase to categorize server equipment. Select NONE if you do not want to specify one.
    * Add Server
        * There are two ways to add a server. For more information, see the [Detail Functional Guide server group menu](./reference/#server-group).
            * Bulk Add
            * Individual Add
         * Enter the host name (required), IP address (required), and OS (optional), then choose **Add**.
         * Verify the added entries in the server list below. Only servers with their left checkbox selected will be registered.

3. When finished, choose **Create**.

<a id="setting-binary-groups"></a>
### Binary Group Settings { #setting-binary-groups }

This feature lets you manage binaries to deploy.

![deploy_25_202402](https://static.toastoven.net/prod_tcdeploy/deploy_25_202402.png)
![deploy_26_202402](https://static.toastoven.net/prod_tcdeploy/deploy_26_202402.png)

1. On the **Deploy** page, choose **Binary Group > New** in the bottom tabs.
    * A Default binary group is automatically created when you create an artifact.
2. In the **Create Binary Group** window, configure the new binary group.
    * Enter name, description, and region.
        * If the **Region** differs from the region of the deployment target server, network latency may increase.
    * Configure auto-delete settings.
        * This feature periodically deletes binaries based on conditions such as period, capacity, and count.
        * The maximum count and minimum retention count are required, and you can set up to 10.
3. When finished, choose **Create**.

<a id="create-scenarios"></a>
### Create Scenarios { #create-scenarios }

![deploy_08_201812](https://static.toastoven.net/prod_tcdeploy/deploy_08_201812.png)

1. On the **Deploy** page, choose **Deploy > New** in the bottom tabs.
2. Enter a scenario name (optional) in the scenario area added below.
3. Choose **Create**.

<a id="add-tasks"></a>
### Add Tasks { #add-tasks }

A task is a scenario component that performs individual functions and controls execution order.
There are two types of tasks:

* pre-run Task: Functions run before deployment
* Normal Task: Functions run during deployment

You can select and use the one that you want. This section covers the tasks that are required for basic deployment.
For more tasks, see the [Detail Functional Guide task menu](./reference/#tasks).

Add the following three tasks for deployment testing.

<a id="add-user-commands"></a>
#### 1. Add User Command

* This is a user-defined Command task that runs during deployment.
* You can use Available Variables.
    * Available Variables: Reserved keywords. For more information, see the [Detail Functional Guide task menu](./reference/#tasks).

![deploy_09_201812](https://static.toastoven.net/prod_tcdeploy/deploy_09_201812.png)

1. On the right side of the scenario area in the **Deploy** tab, choose **Add Task**.
2. Choose **User Command** under **Normal Task**.
3. Enter the new task details.
    * Timeout(min)
        * Specifies the wait time for the task to complete. Minimum 1 minute, maximum 30 minutes.
    * Run As
        * Enter the execution account.
    * Command
        * Enter the command to run.

4. When finished entering or making changes, choose **Apply**.

<a id="add-binary-deploy"></a>
#### 2. Add Binary Deploy

This is a task that lets you configure deployment settings for uploaded binary files.

![deploy_10_201812](https://static.toastoven.net/prod_tcdeploy/deploy_10_201812.png)

1. Choose **Add Task** and then choose **Binary Deploy** under **Normal Task**.
2. Enter the new task details.
    * Timeout(min)
        * Specifies the wait time for the task to complete. Minimum 1 minute, maximum 30 minutes.
    * Run As
        * Enter the execution account.
3. To upload a binary file, choose **Upload** on the right.
4. Enter the binary file information.
    * Choose **Select Files** and select the binary file.
    * Enter version (optional) and description (optional).
5. Choose **Upload**.
6. After the upload is complete, choose **Select Binary**.
7. Select the desired binary version.
    * If there are multiple versions, use the search feature.
8. Choose **Select**.
  <br/>
   * Variable As
       * Specify a variable name for the binary to use binary information in User Command. For more information, see the task menu in the [Detail Functional Guide](./reference/).
   * Target Directory
       * Specifies the target directory where the binary will be deployed.

<a id="add-tasks-add-user-commands"></a>
#### 3. Add User Command

![deploy_11_201812](https://static.toastoven.net/prod_tcdeploy/deploy_11_201812.png)

1. Choose **Add Task** and then choose **User Command** under **Normal Task**.
2. Enter the new task details.
    * Timeout(min)
        * Specifies the wait time for the task to complete. Minimum 1 minute, maximum 30 minutes.
    * Run As
        * Enter the execution account.
    * Command
        * Enter the command to run.
3. When finished entering or making changes, choose **Apply**.

<a id="execute"></a>
### Run { #execute }

![deploy_12_201812](https://static.toastoven.net/prod_tcdeploy/deploy_12_201812.png)

1. Choose **Run** on the right to request a deployment.
2. Enter the deployment run details.
    * Specify the deployment note (optional) and authentication method.
    * If you select **Password**, enter the password or select and upload a .pem file.
3. When finished, choose **OK**.

![deploy_13_201812](https://static.toastoven.net/prod_tcdeploy/deploy_13_201812.png)

1. You can check the deployment progress.
2. Verify that deployment is complete.
    * Use exit code to see if each task is normally executed.
3. To view detailed results, choose **See Results**.
4. In the **See Results** window, verify the deployment result.
    * Use exit code to see if each task is normally executed.

- - -

You have deployed files to the server!
NHN Cloud Deploy supports more features. For more information, see the [Detail Functional Guide](./reference/).