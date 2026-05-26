## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order.

* Enable the Service
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Execute Flow
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define the behavior of each node.
    3. Complete the flow by determining the execution order of the nodes through node connections.
    4. Run the flow.
    5. Check the log information to verify that the flow is executing properly.

## Management

This is a page to retrieve and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search flows based on given criteria.

* When searching by flow name, it searches for flows that contain the search term in the name.

### Filter

Search flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Display the search results in table format.

* Displays simple flow metadata and the current flow execution status.
* Sorts by the most recent modification date.
* Select a flow to use management functions such as flow modification, flow details view, and flow start.
* You can retrieve only flows in a specific status through the filter condition function.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow execution status | Description |
|---------------------------------------------------| --- |
| START_FAILED  | The flow execution request has failed. |
| QUOTA_EXCEEDED | The flow execution has failed due to insufficient resources. |
| STARTING       | Resources for flow execution are being allocated. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error has occurred due to communication failure or authentication failure during flow execution. If the <b>ERROR</b> continues to occur, please contact **Customer Support > Inquiry**. |
| STOP_FAILED   | The flow termination request has failed. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error has occurred due to unknown causes during flow execution. If the <b>UNKNOWN</b> error continues to occur, please contact **Customer Support > Inquiry**. |

#### Flow Status Change Notification Email
* You can receive a notification email when the flow status changes to a target notification status.
* Target notification flow status
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with **DataFlow ADMIN** role in projects where the DataFlow service is enabled


### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select the execution mode based on the flow purpose.
* Specify a flow template to easily load flows with the desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description and reflect the changes in the flow metadata.
* Flow templates cannot be specified.
* You can modify a flow while it is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type applies from the next flow execution.

### Copy Flow

Create new metadata using the existing flow definition.

* Create new metadata with `_copy` appended to the existing flow name.
* Copy the flow logic from the existing flow as-is.
* You can also copy running flows.
* Running flows are copied in a stopped state.
* If the current save state of a flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a scheduler registered, the copied flow will not have the scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete the flow's metadata.

* Completely delete the flow's metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a flow that is in stopped state.

* Only one flow can be executed at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that has only been temporarily saved without ever being saved cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is running via a scheduler, you cannot start a flow in the same way as a user-initiated flow.

### More - Stop Flow
* You can stop a flow that is preparing to run, running, or draining.
* Remaining events are not processed and the flow is terminated.

### More - Stop Flow After Draining
* You can stop a running flow after draining.
* Draining means processing remaining events in the flow.
* If the timeout is exceeded, the flow terminates even if draining is not complete.
* If draining is complete while timeout time remains, the flow is immediately terminated.
* A draining flow can be immediately terminated through flow termination.