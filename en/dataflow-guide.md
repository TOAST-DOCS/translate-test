## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define the behavior of each node.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Execute the flow.
    5. Check log information to verify that the flow executed normally.

## Management

This page allows you to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* Searching by flow name retrieves flows that contain the search term in their name.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Display query results in table format.

* Displays simple flow metadata and the current flow execution status.
* Sorts by the most recent modification date.
* You can select a flow to use management features such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status through the filter condition feature.
* Once a flow is queried, you must click **Refresh** to update the query results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Resources for flow execution are being secured. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> continues to occur, contact **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An unknown error occurred during flow execution. If <b>UNKNOWN</b> continues to occur, contact **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive a notification email when the flow status changes to a target notification status.
* Target notification flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is activated

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated among different flows.
* Select an execution mode based on the flow purpose.
* You can specify a flow template to easily load flows with the desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description to reflect changes in the flow metadata.
* You cannot specify a flow template.
* You can modify the flow even while the flow is executing.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Create new metadata using an existing flow definition.

* Create new metadata with `_copy` added to the existing flow name.
* Copy the flow logic of the existing flow as is.
* You can copy a flow that is currently executing.
* A running flow is copied in a stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a flow that is in a stopped state.

* Each flow can only run one at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that has only been temporarily saved without being saved even once cannot be started.
* A flow must be saved at least once to be started.
* Even if a flow is running by a scheduler, it cannot be started by the user in the same way as a user-initiated flow start.

### More - Stop Flow
* You can stop a flow that is preparing to run, running, or draining.
* Stops without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing the remaining events in the flow.
* If the timeout is exceeded, the flow is stopped even if draining is not complete.
* If draining completes before the timeout, the flow stops immediately.
* A draining flow can be stopped immediately through flow termination.