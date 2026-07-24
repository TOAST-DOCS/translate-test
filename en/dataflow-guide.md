## Data & Analytics > DataFlow > Console User Guide

You can use DataFlow in the following order:

* Activate the Service
    1. Create a project.
    2. Select the project that you want.
    3. Activate the DataFlow service.
* Run a Flow
    1. Create a flow.
    2. Add the necessary nodes and enter configuration values to define the behavior of each node.
    3. Connect nodes to determine the order of operations and complete the flow.
    4. Run the flow.
    5. Check the log information to verify that the flow ran successfully.

## Management

Page that queries and manages the flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Searches for flows based on the given criteria.

* Searching by flow name retrieves flows that contain the search term in their name.

### Filter

Filters flows based on the given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the query results as a list of flows in a table.

* Displays basic flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management features such as changing flows, viewing flow details, and starting flow.
* You can use the filter conditions to view only flows in a specific status.
* Once a flow is queried, click **Refresh** to update the query results.
* You can query 12 flows per page and navigate using the **Previous** and **Next** buttons.

#### Flow Status Information

| Flow Execution Status                                    | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | The flow start request failed. |
| QUOTA\_EXCEEDED | The flow failed to start due to insufficient resources. |
| STARTING       | Securing resources to run the flow. |
| PREPARING      | Flow preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> continues to occur, contact us at **Customer Support > Contact Us**. |
| STOP\_FAILED   | The flow stop request failed. |
| STOPPED        | The flow has stopped. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred for unknown reasons during the execution of the flow. If <b>UNKNOWN</b> continues to occur, contact us at **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive a notification email when a flow changes to one of the notification target statuses.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is activated


### Create a Flow

Creates metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Duplicate flow names are allowed.
* Select an execution mode based on the flow's purpose.
* You can specify Flow Template to easily load flows of features users wants.
* You can set the instance type for running the flow. 

### Modify a Flow

Modifies the flow's metadata.

* Modify the existing flow name and description to update the flow metadata.
* You cannot specify a flow template.
* You can modify a flow even while it is running.
* You can change the instance type for running the flow.
    * However, the changed instance type takes effect starting from the next flow execution.

### Copy a Flow

Creates new metadata using the definition of an existing flow.

* Create new metadata with the phrase `_copy` added to the name of existing flow.
* Copies the flow logic of the existing flow as-is.
* You can also copy a flow that is currently running.
* A running flow is copied in a stopped state.
* If the current storage state of flows is temporary, it does not copy the last saved version of existing flows.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely independent of the original flow.

### Delete a Flow

Deletes the flow metadata.

* Permanently deletes the flow metadata.
* Deleted flows cannot be recovered.
* You cannot delete a flow that is currently running.

### More - Start a Flow
Starts a stopped flow.

* Only one instance of each flow can run at a time.
* A temporarily saved flow starts from the last saved version.
* A flow that has only been temporarily saved and never fully saved cannot be started.
* A flow must be saved at least once before it can be started.
* A flow cannot be started the same as the flow initiated by the user, even if the flow is already being run by Scheduler.

### More - Stop a Flow
* You can stop a flow that is preparing to run, running, or draining.
* The flow stops without processing remaining events.

### More - Drain and Stop a Flow
* You can drain and then stop a running flow.
* Draining means processing the remaining events in the flow.
* If the timeout period is exceeded, the flow stops even if draining is not complete.
* If draining completes before the timeout expires, the flow stops immediately.
* A draining flow can be stopped immediately by using the Stop Flow option.