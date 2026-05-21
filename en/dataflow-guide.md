## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Run Flow
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define the behavior of each node.
    3. Complete the flow by connecting nodes to determine the order of node operations.
    4. Run the flow.
    5. Check the log information to verify that the flow ran successfully.

## Management

This page is used to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* Searching by flow name returns flows that contain the search term in their name.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Search results are displayed in table format.

* Displays simple flow metadata and current flow execution status.
* Sorted by most recent modification date.
* You can select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status using the filter condition feature.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* 12 flows are retrieved per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Resources for flow execution are being secured. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure, etc. If <b>ERROR</b> continues to occur, contact us via **Customer Support > Inquiry**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> continues to occur, contact us via **Customer Support > Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to the notification target status.
* Notification target flow status
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with **DataFlow ADMIN** role in the project where the DataFlow service is activated

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select the execution mode based on the flow purpose.
* You can specify a flow template to easily load a flow with the desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the metadata of a flow.

* Modify the existing flow name and description and apply them to the flow metadata.
* A flow template cannot be specified.
* The flow can be modified even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied starting from the next flow execution.

### Copy Flow

Create new metadata using the definition of an existing flow.

* Create new metadata with `_copy` added to the existing flow name.
* Copy the flow logic of the existing flow as is.
* You can copy even running flows.
* Running flows are copied in a stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can only run one at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that has only been temporarily saved without ever being saved cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is running by a scheduler, you cannot start the flow the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are in preparation, running, or draining state.
* Stops without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow is terminated even if draining is not complete.
* If draining completes before the timeout expires, the flow terminates immediately.
* A draining flow can be terminated immediately through flow termination.