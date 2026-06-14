## Dev Tools > Pipeline > Console User Guide > Pipeline Management

A pipeline defines an application deployment flow consisting of one or more stages.

### Pipeline Configuration

#### Create Pipeline

You can create a pipeline by clicking **+ Create Pipeline**, or you can create a pipeline by uploading a pipeline template file.
![pipeline-management-guide-01](https://static.toastoven.net/prod2_translate-test/en/management-guide-01.png)


In **Pipeline Management**, click **+ Create Pipeline**.

![pipeline-management-guide-02](https://static.toastoven.net/prod2_translate-test/en/management-guide-02.png)

In the **Create Pipeline** modal window, enter **Pipeline Name** and **Pipeline Description**, and then click **OK**.

You can also create a pipeline with a pipeline template file (pipeline templates use JSON files).

![pipeline-management-guide-03](https://static.toastoven.net/prod2_translate-test/en/management-guide-03.png)

Upload the pipeline template file and click **OK**.

#### Pipeline Studio

Pipeline Studio is a page where users can manage basic information about pipelines or add, change, and delete stages that make up the pipeline.

![pipeline-studio-guide-01](https://static.toastoven.net/prod2_translate-test/en/guide-1.png)

At the top of Pipeline Studio, basic information about the pipeline's name, description, last modified date, and creator is displayed.

In the Pipeline Studio panel, you can check the stages that make up the pipeline.

#### Edit Mode
![pipeline-studio-guide-08](https://static.toastoven.net/prod2_translate-test/en/guide-2.png)

You can enter edit mode by clicking the **Edit Mode** toggle in the upper right. In edit mode, you can add, change, delete, and reposition stages.

#### Add Stage
![pipeline-studio-guide-09](https://static.toastoven.net/prod2_translate-test/en/guide-3.png)

When you enable **Edit Mode**, the left side exposes the **Source**, **Build**, **Deploy**, and **Feature** groups, which are organized into different stages that you can use to organize your application deployment flow.

You can select the stage to add from the four groups and drag and drop it onto the screen.

![pipeline-studio-guide-10](https://static.toastoven.net/prod2_translate-test/en/guide-4.png)

When a stage is added, select the stage to enter required information.

![pipeline-studio-guide-11](https://static.toastoven.net/prod2_translate-test/en/guide-5.png)

Connect the previously executed stage with the stage to add to set the execution order.

![pipeline-studio-guide-12](https://static.toastoven.net/prod2_translate-test/en/guide-6.png)

Click **Save Pipeline** in the upper right to complete adding the stage.

#### Edit Stage
![pipeline-studio-guide-13](https://static.toastoven.net/prod2_translate-test/en/guide-7.png)

After enabling **Edit Mode**, you can edit a stage by clicking the stage to edit.

![pipeline-studio-guide-14](https://static.toastoven.net/prod2_translate-test/en/guide-9.png)

After completing the edit, click **Save Pipeline** in the upper right to complete stage editing.

#### Delete Stage
![pipeline-studio-guide-15](https://static.toastoven.net/prod2_translate-test/en/guide-10.png)

![pipeline-studio-guide-16](https://static.toastoven.net/prod2_translate-test/en/guide-11.png)

After enabling **Edit Mode**, you can delete a stage by clicking the **X** in the upper right of the stage to delete.

![pipeline-studio-guide-17](https://static.toastoven.net/prod2_translate-test/en/guide-12.png)

After deletion, click **Save Pipeline** in the upper right to complete stage deletion.

### Run Pipeline

Pipelines can be run manually or automatically.

#### Manual Run

Using manual run, users can run the pipeline whenever they want.

![pipeline-management-guide-12](https://static.toastoven.net/prod2_translate-test/en/management-guide-12.png)

In **Pipeline Management**, click **▶︎ Run**, then when the **Run Pipeline** modal window appears, check the content and click **OK**.

#### Autorun

Using autorun, you can set the pipeline to run automatically when an event occurs in a GitHub or GitLab repository or when a container image in an image registry is updated.

![management-guide-04](https://static.toastoven.net/prod2_translate-test/en/management-guide-04.png)
![management-guide-05](https://static.toastoven.net/prod2_translate-test/en/management-guide-05.png)

Click **Autorun Settings**, then in the **Autorun Settings** modal window, click **Add**.


* GitHub autorun settings
![management-guide-06](https://static.toastoven.net/prod2_translate-test/en/management-guide-06.png)



You can use the GitHub webhook to set up a pipeline to run automatically when an event occurs in a repository on GitHub or GitHub Enterprise. Set the **autorun type** to **GitHub**, enter the repository's **organization name or username**, **project name**, **branch or tag**, and **secret**, and click **OK**.

To set autorun by tag, enter the tag name in the **Branch or Tag** item, such as `refs/tags/tagname`. You can use a JAVA regular expression for the `tagname` part.

After setting up autorun with tags, builds are performed with the tags set when using the NHN Cloud build tool. To perform builds with tags in the Build - Jenkins stage, you need to set the following settings.

Set parameters as follows in Jenkins:
![pipeline-guide-39.png](https://static.toastoven.net/prod2_translate-test/en/pipeline-guide-39.png)
![pipeline-guide-40.png](https://static.toastoven.net/prod2_translate-test/en/pipeline-guide-40.png)


Enter as follows in **Build Job Parameter** from Set Build Tool:

![management-guide-10](https://static.toastoven.net/prod2_translate-test/en/management-guide-10.png)

* GitHub webhook settings

![pipeline-guide-16](https://static.toastoven.net/prod2_translate-test/en/pipeline-guide-16.png)


| Item | Setting |
|---|---|
| Payload URL | https://kr1-pipeline.api.nhncloudservice.com/webhooks/git/github |
| Content type | application/json |
| Secret | The value entered in the secret of the pipeline autorun settings |
| event | push event, create event (when using tags) |

You can set autorun to occur only when specific files are pushed (up to 5 files).

![management-guide-13](https://static.toastoven.net/prod2_translate-test/en/management-guide-13.png)

For **Source Repository Name**, select the source repository registered in environment settings.
For **GitHub File Path**, enter the path containing the file in the selected source repository.

* GitLab autorun settings

![management-guide-07](https://static.toastoven.net/prod2_translate-test/en/management-guide-07.png)

You can use the GitLab webhook to set up a pipeline to run automatically when an event occurs in your GitLab repository. Set the **autorun type** to **GitLab**, enter the repository's **organization or username**, **project name**, **branch, or tag**, and click **Confirm**. Support for setting GitLab secrets is coming in the future.

* GitLab webhook settings

![pipeline-guide-18](https://static.toastoven.net/prod2_translate-test/en/pipeline-guide-18.png)


| Item | Setting |
|---|---|
| URL | https://kr1-pipeline.api.nhncloudservice.com/webhooks/git/gitlab |
| Trigger | Check Push events |
| Secret | Do not set |
| SSL verification | Check Enable SSL verification |

* Precautions when setting GitLab webhook

When setting autorun with a GitLab username, you must set the username the same as the GitLab username. If you set the username differently, autorun may not work.

![pipeline-guide-19](https://static.toastoven.net/prod2_translate-test/en/pipeline-guide-19.png)

* Image registry autorun settings

![management-guide-08](https://static.toastoven.net/prod2_translate-test/en/management-guide-08.png)

If you want the pipeline to run automatically when the container image is updated, set **Image Registry** for **Autorun Type**.
After selecting **the image registry** registered in **the environment settings**, enter **Image Name**. Enter the image name in the form of `registry name/image name` for NHN Cloud container registry.
For Docker Hub, enter in the form of `docker hub account/image name`. **Tag** can use JAVA regular expression and is automatically executed when a tag matching the entered tag is pushed.
If you do not enter a tag, it will be automatically executed when a new tag except latest is pushed.
When finished, click **Confirm**.

![management-guide-09](https://static.toastoven.net/prod2_translate-test/en/management-guide-09.png)

When you create a new pipeline, the **Autorun** toggle switch is applied in the off state. To run the pipeline automatically, you must click the **Autorun** toggle switch to enable it.

### Pipeline Management

Users can modify basic information about the pipeline.
![pipeline-studio-guide-02](https://static.toastoven.net/prod2_translate-test/en/guide-13.png)

You can modify the pipeline's name and description by clicking the edit icon next to the pipeline name.

After modifying the information, click **OK** to complete the modification.

![pipeline-studio-guide-03](https://static.toastoven.net/prod2_translate-test/en/guide-14.png)

You can run the pipeline by clicking **▶ Manual Run**, and stop a running pipeline by clicking **■ Stop Execution**.


#### Check Recent Execution Information

To check basic information and execution status for each stage of the pipeline's recent execution, click **Recent Execution Information**.

![pipeline-studio-guide-05](https://static.toastoven.net/prod2_translate-test/en/guide-16.png)

#### Download Pipeline JSON

![pipeline-studio-guide-05](https://static.toastoven.net/prod2_translate-test/en/guide-17.png)

You can check the pipeline in JSON format by clicking **Pipeline Version**.

Click the dropdown button showing the pipeline modification date in the upper left to check by modification date.

Click **Download Pipeline Template** in the upper right to save as a JSON file.

#### Pipeline Notification
This is a feature that manages Email and SMS notifications for pipeline start, completion, and failure.

![pipeline-management-guide-13](https://static.toastoven.net/prod2_translate-test/en/pipeline-management-guide-13.png)

You can set notifications by clicking **Pipeline Notification**.

Notification recipient management is available in **Project Settings** > **Notification Management**.

For setting up for notification recipients and how to notify (Email, SMS), refer to [Notification Management Guide](https://docs.nhncloud.com/ko/nhncloud/ko/console-guide/#_33).

#### Pipeline Execution History
Click **Execution History** in Pipeline Studio to check the recent 10 histories.
![pipeline-management-guide-14](https://static.toastoven.net/prod2_translate-test/en/pipeline-management-guide-14.png)

![pipeline-management-guide-15](https://static.toastoven.net/prod2_translate-test/en/pipeline-management-guide-15.png)

When you select an execution history to check in the left area of the execution history modal window, detailed information for each stage is displayed in the right area.

You can check the pipeline's execution status in the **Status** column, and cancel pipeline execution by clicking **Cancel**.

For stages such as **Feature - Approval Management** and **Feature - Judgement (Execution Management)**, you can manage pipeline execution by clicking **Manage**.