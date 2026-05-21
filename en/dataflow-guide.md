## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence.

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add necessary nodes and define how each node operates by entering configuration values.
    3. Complete the flow by determining the order of node operations through node connections.
    4. Execute the flow.
    5. Check the log information to verify that the flow has executed correctly.

## Management

A page for inquiring and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search flows based on given criteria.

* When you search based on flow name, flows that contain the search term in their name are retrieved.

### Filter

Search flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Display the retrieved flows in table format.

* Displays simple flow metadata and the current flow execution status.
* Sorts by the most recent modification date.
* You can select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can retrieve only flows with a specific status through the filter condition function.
* Once a flow is retrieved, you must click **Refresh** to update the retrieval results.
* Displays 12 flows per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                 | Description |
|---------------------------------------------------| --- |
| START_FAILED  | Failed to request flow execution. |
| QUOTA_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Resources for flow execution are being secured. |
| PREPARING      | Preparation for flow execution is complete. |
| RUNNING        | The flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> continues to occur, contact us through **Customer Support > Inquiry**. |
| STOP_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> continues to occur, contact us through **Customer Support > Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to a status designated for notifications.
* Notification target flow status
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is activated

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow purpose.
* You can specify a flow template to easily load flows with the desired functionality.
* You can set the instance type to execute the flow.

### Modify Flow

Modify the metadata of a flow.

* Modify the existing flow name and description to reflect changes in flow metadata.
* Flow templates cannot be specified.
* You can modify the flow even while the flow is executing.
* You can change the instance type to execute the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Create new metadata using an existing flow definition.

* Create new metadata with `_copy` appended to the existing flow name.
* Copy the flow logic of the existing flow as-is.
* You can copy even executing flows.
* Executing flows are copied in stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have the scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Executing flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can only execute one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is executed by the scheduler, the flow cannot be started in the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing to execute, executing, or draining.
* Stops without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop an executing flow.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow is stopped even if draining is not complete.
* If draining completes while timeout remains, the flow is stopped immediately.
* A draining flow can be stopped immediately through flow termination.