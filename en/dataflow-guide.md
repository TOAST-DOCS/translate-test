## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence.

* Enable the Service
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Run Flow
    1. Create a flow.
    2. Add the necessary nodes and define how each node operates by entering configuration values.
    3. Determine the order of node operations by connecting nodes to complete the flow.
    4. Run the flow.
    5. Check the log information to verify that the flow executed successfully.

## Management

This is a page for retrieving and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on the given criteria.

* Searching by flow name displays flows that contain the search term in their name.

### Filter

Search for flows based on the given conditions.

* Filter options are provided based on flow status values.

### Flow List

Query results are displayed in table format.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* You can manage flows by selecting a flow and using management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can retrieve only flows in a specific status through the filter condition feature.
* Once a flow is retrieved, you must click **Refresh** to update the query results.
* 12 flows are retrieved per page, and you can move between pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                             | Description |
|---------------------------------------------------| --- |
| START_FAILED  | Failed to request flow execution. |
| QUOTA_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Resource allocation for flow execution is in progress. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure, etc. If <b>ERROR</b> continues to occur, contact us at **Customer Support > Inquiry**. |
| STOP_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> continues to occur, contact us at **Customer Support > Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to the notification target status.
* Notification target flow status
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the active DataFlow service is enabled

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be the same as other flows.
* Select the execution mode based on the flow's purpose.
* Specify a flow template to easily retrieve a flow with the desired functionality.
* You can configure the instance type for running the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description to reflect in the flow metadata.
* Flow templates cannot be specified.
* You can modify the flow even while it is running.
* You can change the instance type for running the flow.
    * However, the changed instance type is applied starting from the next flow execution.

### Copy Flow

Create new metadata based on the existing flow definition.

* Create new metadata with `_copy` added to the name of the existing flow.
* The flow logic of the existing flow is copied as-is.
* You can copy a running flow.
* Running flows are copied in a stopped state.
* If the flow's current save state is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have the scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a flow in stopped state.

* Each flow can only run one at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that has only been temporarily saved without being saved cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is running due to a scheduler, you cannot start the flow the same way as a flow started by the user.

### More - Stop Flow
* You can stop flows that are in preparation, running, or draining.
* Remaining events are not processed before stopping.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow is stopped even if draining is not complete.
* If draining completes while timeout remains, it stops immediately.
* A draining flow can be stopped immediately through flow termination.