## Data & Analytics > DataFlow > Console User Guide

DataFlow can be used in the following sequence:

* Service activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the operation order of nodes through node connections.
    4. Execute the flow.
    5. Check the log information to verify that the flow executed normally.

## Management

This is a page for viewing and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, flows that contain the search term in their name are returned.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the query results as a table of flows.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status using the filter condition feature.
* Once a flow is queried, you must click **Refresh** to update the query results.
* Up to 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Acquiring resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure, etc. If <b>ERROR</b> persists, contact us through **Customer Support > Inquiries**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> persists, contact us through **Customer Support > Inquiries**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow changes to a target notification status.
* Target notification flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is currently activated.


### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow purpose.
* Specify a flow template to easily load flows with the desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the metadata of a flow.

* Modify the existing flow name and description and reflect them in the flow metadata.
* Flow templates cannot be specified.
* You can modify a flow even while it is executing.
* You can change the instance type for executing the flow.
    * However, the changed instance type applies from the next flow execution.

### Copy Flow

Create new metadata using an existing flow definition.

* Create new metadata with `_copy` appended to the name of the existing flow.
* Copy the flow logic of the existing flow as-is.
* You can copy flows that are currently executing.
* Executing flows are copied in a stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a registered scheduler.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Executing flows cannot be deleted.

### More - Start Flow
Start a flow that is in a stopped state.

* Each flow can only execute one at a time.
* A temporarily saved flow starts with the last saved version.
* Flows that have only been temporarily saved without saving at least once cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is being executed by a scheduler, you cannot start a flow in the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are in preparation for execution, executing, or draining.
* Termination occurs without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop an executing flow.
* Draining means processing the remaining events of a flow.
* If the timeout is exceeded, termination occurs even if draining is not complete.
* If draining completes before the timeout is reached, termination occurs immediately.
* A flow that is draining can be terminated immediately through flow termination.