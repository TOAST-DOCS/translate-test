## Data & Analytics > DataFlow > Console User Guide

DataFlow can be used in the following sequence.

* Enable service
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Run flow
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the operation order of nodes through node connections.
    4. Run the flow.
    5. Check log information to verify that the flow has executed normally.

## Management

A page to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on the given criteria.

* When searching based on flow name, flows that contain the search term in the name are retrieved.

### Filter

Search for flows based on the given conditions.

* Provides filtering options based on flow status values.

### Flow List

Display search results as a table.

* Displays simple flow metadata and the current flow execution status.
* Sorts by the most recent modification date.
* You can select a flow to use management features such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status through the filter condition feature.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* 12 flows are retrieved per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                            | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Acquiring resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> continues to occur, contact us through **Customer Support > Inquire**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> continues to occur, contact us through **Customer Support > Inquire**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to a notification target status.
* Notification target flow status
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is enabled

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select the execution mode based on the flow purpose.
* You can specify a flow template to easily load flows with the desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description to reflect them in the flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Create new metadata using the existing flow definition.

* Create new metadata with `_copy` appended to the existing flow name.
* Copy the flow logic of the existing flow as-is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the flow's current save state is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a scheduler registered, the copied flow does not have a scheduler registered.
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
* Flows that are only temporarily saved without being saved once cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is running due to a scheduler, it cannot be started the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are in execution preparation, running, or draining state.
* Terminates without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow is terminated even if draining is not complete.
* If draining is complete before the timeout is exceeded, the flow is terminated immediately.
* A draining flow can be terminated immediately through flow stop.