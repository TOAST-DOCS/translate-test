## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence:

* Activate Service
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Run Flow
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Run the flow.
    5. Check log information to verify that the flow executed normally.

## Management

This page allows you to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* Searching by flow name returns flows that contain the search term in their name.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays query results as a table of flows.

* Displays simple flow metadata and the current flow execution status.
* Sorted by most recent modification date.
* You can manage flows by selecting a flow to change it, view flow details, start the flow, and more.
* You can view only flows with a specific status using the filter condition feature.
* Once a flow is queried, you must press **Refresh** to update the query results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Resources for flow execution are being secured. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> continues to occur, contact us through **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> continues to occur, contact us through **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to a notification target status.
* Notification target flow status
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the active DataFlow service is enabled

### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select an execution mode based on the flow's purpose.
* You can specify a flow template to easily load flows with desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modifies the metadata of a flow.

* Modifies the existing flow name and description and reflects them in the flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Creates new metadata with an existing flow definition.

* Creates new metadata with `_copy` added to the existing flow's name.
* Copies the flow logic of the existing flow as is.
* Even executing flows can be copied.
* Executing flows are copied in a stopped state.
* If the flow's current save state is temporary save, the last saved version of the existing flow is not copied.
* Even if a flow with a registered scheduler is copied, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* Executing flows cannot be deleted.

### More - Start Flow
Starts a stopped flow.

* Each flow can only run one at a time.
* A temporarily saved flow starts with the last saved version.
* Flows that are only temporarily saved without ever being saved cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is being executed by a scheduler, it cannot be started in the same way as a flow started by the user.

### More - Stop Flow
* You can stop flows that are in execution preparation, executing, or draining.
* Stops without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow is stopped even if draining is not complete.
* If draining completes while timeout remains, the flow stops immediately.
* Flows that are draining can be stopped immediately through flow termination.