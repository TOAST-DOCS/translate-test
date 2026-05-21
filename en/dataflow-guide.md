## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence.

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define the behavior of each node.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Execute the flow.
    5. Check the log information to verify that the flow executed normally.

## Management

This page allows you to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, flows that contain the search term in the name are returned.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Query results are displayed in table format.

* Displays simple flow metadata and the current flow execution status.
* Sorted by most recent modification date.
* You can select a flow to use management functions such as changing the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status using the filter condition feature.
* Once a flow is queried, you must click **Refresh** to update the query results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                            | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Resources for flow execution are being allocated. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure, etc. If <b>ERROR</b> continues to occur, contact **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred due to unknown causes during flow execution. If <b>UNKNOWN</b> continues to occur, contact **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive a notification email when the flow status changes to the target notification status.
* Target notification flow status
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
* You can specify a flow template to easily retrieve flows with the desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description to reflect the changes in the flow metadata.
* Flow templates cannot be specified.
* Flow can be modified even while the flow is executing.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution onwards.

### Copy Flow

Create new metadata based on an existing flow definition.

* Creates new metadata with `_copy` appended to the existing flow name.
* Copies the flow logic of the existing flow as is.
* You can copy even running flows.
* Running flows are copied in a stopped state.
* If the current save state of the flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete the flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can only be executed one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that are only temporarily saved without being saved once cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is being executed by a scheduler, it cannot be started by a user in the same way as a user-initiated flow.

### More - Stop Flow
* You can stop flows that are in preparation for execution, executing, or draining.
* Stops without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop running flows.
* Draining means processing remaining events in the flow.
* If the timeout is exceeded, the flow terminates even if draining is not complete.
* If draining completes while timeout remains, the flow terminates immediately.
* Draining flows can be terminated immediately through flow stop.