<!-- machine_translated: true -->

<!-- pre-align:aligned sig=40aa83d794a8 -->

<a id="dev-tools-deploy-console-user-guide"></a>
## Dev Tools > Deploy > Console User Guide { #dev-tools-deploy-console-user-guide }

This document covers the following topics:

* [Deploy Console](#deploy-console-page)
* [Client Application](#client-application)
* [Server Application](#server-application)

(Features not covered here can be found in the [Detail Functional Guide](./reference/).)

<a id="deploy-console-page"></a>
## Deploy Console { #deploy-console-page }

The following is the Deploy service console.

![deploy_02_201812](https://static.toastoven.net/prod_tcdeploy/deploy_02_201812.png)

<a id="client-application"></a>
## Client Application { #client-application }

Configuring a client application deployment involves two main steps: Setting Artifacts and uploading binaries.

<a id="setting-artifacts"></a>
### Setting Artifacts { #setting-artifacts }

![deploy_03_201812](https://static.toastoven.net/prod_tcdeploy/deploy_03_201812.png)

1. On the **Deploy** page, click the **Create** button in the upper left.
2. Select **Client Application** as the artifact type.
    - Enter a name (required), description (optional), and port (required).
3. Click the **Create** button.

<a id="setting-binaries"></a>
### Binary Settings { #setting-binaries }

<a id="upload"></a>
#### Upload

* For iOS, upload .ipa and .plist files. For Android, upload .apk files.
* The etc option is used for installation applications on other operating systems such as Windows.

![deploy_04_201812](https://static.toastoven.net/prod_tcdeploy/deploy_04_201812.png)

1. On the **Deploy** page, click **Binary Group > Default** in the tab at the bottom.
    To create a new binary group, click the **new** button.
2. Click the **Upload** button on the right.
3. In the **Binary Upload** window, click the **Select Files** button and select a binary file.
    * iOS: .ipa file (required), .plist file (required)
        * .plist: Used for installation on the Download Page. The download URL within the file is optional.
    * Android: .apk file (required)
    * Enter version (optional) and description (optional) information.
4. When finished, click the **Upload** button.

<a id="deploy"></a>
#### Deploy

You can send a specific binary Download Page via SMS or email.

![deploy_27_202407](https://static.toastoven.net/prod_tcdeploy/deploy_27_202407.png)
![deploy_28_202407](https://static.toastoven.net/prod_tcdeploy/deploy_28_202407.png)
![deploy_29_202407](https://static.toastoven.net/prod_tcdeploy/deploy_29_202407.png)

1. Click the **Send** button on the right.
2. In the **Send Download Path** window, configure the **Send Type** and **recipient**, then click the **Send** button.
    * For **Send Type**, select either **SMS** or **E-mail**, or both.
    * In **Individual Selection**, you can select recipients individually. In **Select Group**, you can select a notification recipient group.
    * On the **Select Group** tab, click the **View** button in the **Details** column to open the project notification recipient group management window.

The binary Download Page is sent to the recipient using the specified Send Type.

<a id="server-application"></a>
## Server Application { #server-application }

Server application deployment involves configuration steps (artifact, server group, and scenario), binary upload, and deployment steps.

<a id="server-application-setting-artifacts"></a>
### Setting Artifacts { #server-application-setting-artifacts }

![deploy_06_201812](https://static.toastoven.net/prod_tcdeploy/deploy_06_201812.png)

1. Click the **Create** button above the list.
2. Select **Server Application** as the artifact type.
    - Enter a name (required), description (optional), and port (required).
3. In the **Create Artifact** window, click the **Create** button.

<a id="setting-server-groups"></a>
### Server Group Settings { #setting-server-groups }

This feature allows you to manage servers for deployment.

![deploy_07_201812](https://static.toastoven.net/prod_tcdeploy/deploy_07_201812.png)

1. On the **Deploy** page, click **Server Group > new** in the tab at the bottom.
2. In the **Create Server Group** window, configure the new server group.
    * Enter a name (required) and description (optional).
    * Select an OS and specify the Shell Type. You can select a Shell Type from the **Shell Type** list or enter one manually.
    * Select a Phase to categorize server equipment. Select NONE if you do not want to specify one.
    * Add servers
        * There are two ways to add servers. For more information, see the [Detail Functional Guide Server Group Menu](./reference/#server-group).
            * Bulk addition
            * Individual addition
         * Enter a host name (required), IP address (required), and OS (optional), then click the **Add** button.
         * Check the server list below for the added entries. Only servers with the checkbox on the left selected are registered.

3. When finished, click the **Create** button.

<a id="setting-binary-groups"></a>
### Binary Group Settings { #setting-binary-groups }

This feature allows you to manage binaries for deployment.

![deploy_25_202402](https://static.toastoven.net/prod_tcdeploy/deploy_25_202402.png)
![deploy_26_202402](https://static.toastoven.net/prod_tcdeploy/deploy_26_202402.png)

1. On the **Deploy** page, click **Binary Group > new** in the tab at the bottom.
    * A Default Binary Group is automatically created when an artifact is created.
2. In the **Create Binary Group** window, configure the new binary group.
    * Enter a name, description, and region.
        * If the **region** differs from the region of the deployment target server, network latency may increase.
    * Configure Auto-delete Settings.
        * This feature periodically deletes binaries based on conditions such as duration, capacity, and count. 
        * Maximum count and minimum retention count are required values, and you can set up to a maximum of 10.
3. When finished, click the **Create** button.

<a id="create-scenarios"></a>
### Create Scenarios { #create-scenarios }

![deploy_08_201812](https://static.toastoven.net/prod_tcdeploy/deploy_08_201812.png)

1. On the **Deploy** page, click the **Deploy > new** button in the tab at the bottom.
2. Enter a scenario name (optional) in the scenario area added below.
3. Click the **Create** button.

<a id="add-tasks"></a>
### Add Tasks { #add-tasks }

A task is a scenario component that performs individual functions and controls the execution order.
There are two types of tasks:

* pre-run Task: Functions executed before deployment
* Normal Task: Functions executed during deployment

You can select and use whichever type you need. This section covers the basic tasks required for deployment.
For more tasks, see the [Task Menu in the Detail Functional Guide](./reference/#tasks).

Add the following three tasks for deployment testing.

<a id="add-user-commands"></a>
#### 1. Add User Command

* This is a user-defined command task that runs during deployment.
* You can use Available Variables.
    * Available Variables: Reserved keywords. For more information, see the [Task Menu in the Detail Functional Guide](./reference/#tasks).

![deploy_09_201812](https://static.toastoven.net/prod_tcdeploy/deploy_09_201812.png)

1. In the **Deploy** tab, click the **Add Task** button on the right side of the scenario area.
2. Click **User Command** under **Normal Task**.
3. Enter the new task details.
    * Timeout(min)
        * Specifies the wait time for the task to complete. Minimum 1 minute, maximum 30 minutes.
    * Run As
        * Enter the execution account.
    * Command
        * Enter the command to execute.

4. When finished entering or making changes, click the **Apply** button. 

<a id="add-binary-deploy"></a>
#### 2. Add Binary Deploy

This task allows you to configure the deployment of uploaded binary files.

![deploy_10_201812](https://static.toastoven.net/prod_tcdeploy/deploy_10_201812.png)

1. Click the **Add Task** button and click **Binary Deploy** under **Normal Task**.
2. Enter the new task details.
    * Timeout(min)
        * Specifies the wait time for the task to complete. Minimum 1 minute, maximum 30 minutes.
    * Run As
        * Enter the execution account.
3. To upload a binary file, click the **Upload** button on the right.
4. Enter the binary file information.
    * Click the **Select Files** button to select a binary file.
    * Enter a version (optional) and description (optional).
5. Click the **Upload** button. 
6. After the upload is complete, click the **Select Binary** button.
7. Select the binary version you want.
    * Use the search feature when multiple versions are available.
8. Click the **Select** button.
  <br/>
   * Variable As
       * You can specify the Variable name for the binary to use binary information in User Command. For more information, see the bottom of the Task Menu in the [Detail Functional Guide](./reference/).
   * Target directory
       * Specifies the target directory to deploy the binary to.

<a id="add-tasks-add-user-commands"></a>
#### 3. Add User Command

![deploy_11_201812](https://static.toastoven.net/prod_tcdeploy/deploy_11_201812.png)

1. Click the **Add Task** button and click **User Command** under **Normal Task**.
2. Enter the new task details.
    * Timeout(min)
        * Specifies the wait time for the task to complete. Minimum 1 minute, maximum 30 minutes.
    * Run As
        * Enter the execution account.
    * Command
        * Enter the command to execute.
3. When finished entering or making changes, click the **Apply** button. 

<a id="execute"></a>
### Execute { #execute }

![deploy_12_201812](https://static.toastoven.net/prod_tcdeploy/deploy_12_201812.png)

1. Click the **Execute** button on the right to request deployment.
2. Enter the deployment execution information.
    * Specify a Deployment Note (optional) and an authentication method.
    * When **Password** is selected, enter a password or select a .pem file and upload it.
3. When finished, click the **Confirm** button.

![deploy_13_201812](https://static.toastoven.net/prod_tcdeploy/deploy_13_201812.png)

1. You can check the deployment progress.
2. Confirm that the deployment is complete.
    * Use exit code to see if each task is normally executed.
3. To check the detailed results, click the **See Results** button.
4. In the **See Results** window, check the deployment results.
    * Use exit code to see if each task is normally executed.

- - -

You have deployed files to the server!
NHN Cloud Deploy supports more features. For more information, see the [Detail Functional Guide](./reference/).