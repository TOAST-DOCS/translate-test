## Data & Analytics > DataFlow > Console User Guide

You can use DataFlow with the following sequence:

* Service activation
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Flow execution
    1. Create a flow.
    2. Add required nodes and input settings to define the operation of each node.
    3. Connect nodes to determine the order of operations and complete the flow.
    4. Execute the flow.
    5. Check the log information to verify that the flow executed successfully.

## Management

Page that queries and manages the flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search flows based on given criteria.

* If you search by flow name, the search returns flows that contain the search term in their name.

### Filter

Search flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow list

Display search results in table format.

* Display simple flow metadata and the current flow execution status.
* Sort by the most recent modification date.
* You can select a flow to use management features such as changing flows, viewing flow details, and starting flow.
* You can query flows with a specific status only through the filter condition function.
* Once a flow is queried, you must click **Refresh** to update the search results.
* You can query 12 flows per page and navigate through the pages by clicking **Previous** and **Next**.

#### Flow status information

| Flow Execution Status  | Description |
|---| --- |
| START_FAILED  | The flow execution request failed. |
| QUOTA_EXCEEDED | The flow execution failed due to insufficient resources. |
| STARTING       | The system is securing resources for flow execution. |
| PREPARING      | The flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> continues to occur, contact **Customer Support > Contact**. |
| STOP_FAILED   | The flow stop request failed. |
| STOPPED        | The flow has stopped. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution for unknown reasons. If <b>UNKNOWN</b> continues to occur, contact **Customer Support > Contact**. |

#### Flow status change notification email
* You can receive notification emails when the flow status changes to a notification target status.
* Notification target flow status
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is activated

### Create a flow

Create metadata to define the flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated across different flows.
* Select an execution mode based on the flow's purpose.
* You can specify Flow Template to easily load flows of features users want.
* You can set the instance type for flow execution.

### Modify a flow

Modify the flow metadata.

* Modify the existing flow name and description to update the flow metadata.
* You cannot specify a flow template.
* You can modify the flow even while it is running.
* You can change the instance type for flow execution.
    * However, the changed instance type takes effect from the next flow execution.

### Copy a flow

Create new metadata using the existing flow definition.

* Create new metadata with the phrase `_copy` added to the name of existing flow.
* Copy the flow logic from the existing flow as-is.
* You can copy a running flow.
* Running flows are copied in a stopped state.
* If the current storage state of flows is temporary, it does not copy the last saved version of existing flows.
* Even if you copy a flow with a registered scheduler, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the original flow.

### Delete a flow

Delete the flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* You cannot delete a running flow.

### More - Start a flow

Start a stopped flow.

* You can run only one instance of each flow at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that has only been temporarily saved and not saved once cannot be started.
* A flow must be saved at least once before it can be started.
* A flow cannot be started the same as the flow initiated by the user, even if the flow is already being run by Scheduler.

### More - Stop a flow

* You can stop a flow that is preparing for execution, running, or draining.
* The flow stops without processing remaining events.

### More - Stop a flow after draining

* You can drain and stop a running flow.
* Draining means processing remaining events in the flow.
* If the timeout is exceeded, the flow stops even if draining is not complete.
* If draining completes before the timeout expires, the flow stops immediately.
* A draining flow can be stopped immediately through the stop flow option.