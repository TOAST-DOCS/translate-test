## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence.

* Service Activation
    1. Create a project.
    2. Select your desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Run the flow.
    5. Check log information to verify that the flow executed successfully.

## Management

This page allows you to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, flows that include the search term in their name are returned.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the search results as a table.

* Displays basic flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* By selecting a flow, you can use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status through the filter condition feature.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* Displays 12 flows per page, and you can move between pages by clicking **Previous** and **Next**.

#### Flow Execution Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Resources for flow execution are being secured. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is currently running. |
| ERROR              | An error occurred due to communication failure or authentication failure during flow execution. If <b>ERROR</b> persists, please contact us through **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred due to an unknown cause during flow execution. If <b>UNKNOWN</b> persists, please contact us through **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to a notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is activated

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated across different flows.
* Select an execution mode based on the flow purpose.
* You can specify a flow template to easily load a flow with desired functionality.
* You can set the instance type for flow execution.

### Modify Flow

Modify the flow metadata.

* Modify the existing flow name and description and reflect them in the flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is running.
* You can change the instance type for flow execution.
    * However, the changed instance type will be applied from the next flow execution.

### Copy Flow

Create new metadata with an existing flow definition.

* Create new metadata with `_copy` appended to the existing flow name.
* Copy the flow logic of the existing flow as is.
* You can copy a flow that is currently running.
* A running flow is copied in a stopped state.
* If the current save state of the flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a scheduler registered, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete the flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a flow in a stopped state.

* Each flow can only run once at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that has only been temporarily saved without ever being saved cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is running due to a scheduler, it cannot be started by a user in the same way as a user-initiated flow.

### More - Stop Flow
* You can stop a flow that is preparing to run, currently running, or draining.
* Stops without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow stops even if draining is not complete.
* If draining completes while timeout remains, the flow stops immediately.
* A draining flow can be stopped immediately through flow termination.