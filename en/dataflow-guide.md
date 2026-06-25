## Data & Analytics > DataFlow > Console User Guide

You can use DataFlow in the following order:

* Enable Service
    1. Create a project.
    2. Select the project you want.
    3. Enable the DataFlow service.
* Run Flow
    1. Create a flow.
    2. Add the required nodes and enter configuration values to define how each node behaves.
    3. Connect nodes to determine the order of nodes' actions and complete the flow.
    4. Run the flow.
    5. Check the log information to verify that the flow ran successfully.

## Management

Page that queries and manages the flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](https://static.toastoven.net/prod2_translate-test/en/management_main_2025_06.png)

### Search

Search for flows based on the given criteria.

* Searching by flow name returns flows whose names contain the search term.

### Filter

Search for flows based on the given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays query results as a list of flows in a table format.

* Displays basic flow metadata and the current flow execution status.
* Sorts by the most recent modification date.
* You can select a flow to use management features such as changing flows, viewing flow details, and starting flow.
* You can use the filter condition feature to view only flows in a specific status.
* Once a flow has been queried, you must click **Refresh** to update the query results.
* You can query 12 flows per page and navigate through the **Previous** and **Next** buttons.

#### Flow Status Information

| Flow Execution Status | Description |
|---|---|
| START\_FAILED | The flow execution request failed. |
| QUOTA\_EXCEEDED | The flow execution failed due to insufficient resources. |
| STARTING | Resources are being secured for flow execution. |
| PREPARING | The flow is ready to run. |
| RUNNING | The flow is running. |
| ERROR | An error occurred during flow execution due to communication failure or authentication failure. If **ERROR** continues to occur, contact us at **Customer Support > Contact Us**. |
| STOP\_FAILED | The flow termination request failed. |
| STOPPED | The flow has been stopped. |
| DRAINING | The flow is draining. |
| UNKNOWN | An error occurred for unknown reasons during the execution of the flow. If **UNKNOWN** continues to occur, contact us at **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive a notification email when a flow changes to the notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is enabled


### Create Flow

Creates metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select an execution mode based on the purpose of the flow.
* You can specify Flow Template to easily load flows of features users want.
* You can set the instance type to use for running the flow.

### Change Flow

Modifies the metadata of a flow.

* Modify the existing flow name and description to reflect changes in the flow metadata.
* A flow template cannot be specified.
* You can change the flow even while the flow is running.
* You can change the instance type used to run the flow.
    * However, the changed instance type is applied starting from the next flow execution.

### Copy Flow

Creates new metadata based on the definition of an existing flow.

* Create new metadata with the phrase `_copy` added to the name of existing flow.
* Copies the flow logic of the existing flow as-is.
* You can copy a flow that is currently running.
* A running flow is copied in a stopped state.
* If the current storage state of flows is temporary, it does not copy the last saved version of existing flows.
* Even if you copy a flow that has a scheduler registered, the copied flow does not have the scheduler registered.
* The copied flow is completely separate from the original flow.

### Delete Flow

Deletes flow metadata.

* Permanently deletes the flow metadata.
* A deleted flow cannot be recovered.
* A flow that is currently running cannot be deleted.

### More - Start Flow
Starts a flow that is in a stopped state.

* Only one instance of each flow can run at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that has only been temporarily saved and never fully saved cannot be started.
* A flow must be saved at least once before it can be started.
* A flow cannot be started the same as the flow initiated by the user, even if the flow is already being run by Scheduler.

### More - Stop Flow
* You can stop a flow that is preparing to run, running, or draining.
* The flow stops without processing remaining events.

### More - Stop Flow After Draining
* You can stop a running flow after draining.
* Draining means processing remaining events in the flow.
* If the timeout period is exceeded, the flow stops even if draining has not finished.
* If draining finishes while there is still time remaining before the timeout, the flow stops immediately.
* A flow that is draining can be stopped immediately by using Stop Flow.