## Data & Analytics > DataFlow > Console User Guide

DataFlow can be used in the following sequence.

* Enable service
    1. Create a project.
    2. Select the desired project.
    3. Enable DataFlow service.
* Run flow
    1. Create a flow.
    2. Add the required nodes and define the behavior of each node by entering configuration values.
    3. Complete the flow by determining the order of node operations through node connections.
    4. Run the flow.
    5. Check the log information to confirm that the flow has been executed normally.

## Management

Page that queries and manages the flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search flows by the given criteria.

* Search by flow name to find flows that contain the search term in the name.

### Filter

Search flows by the given conditions.

* Provides filtering options based on flow status values.

### Flow List

Display search results in table format.

* Display simple flow metadata and current flow execution status.
* Sort by last modified date.
* You can select a flow to use management features such as changing flows, viewing flow details, and starting flow.
* You can query only flows of a specific status through filter condition functionality.
* Refresh the query results by clicking **Refresh** once flows are queried.
* Query 12 flows per page and navigate through the **Previous** and **Next** buttons.

#### Flow Execution Status Information

| Flow Execution Status | Description |
|---|---|
| START\_FAILED | The flow execution request failed. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources for flow execution. |
| STARTING | Resources for flow execution are being secured. |
| PREPARING | Flow execution preparation is complete. |
| RUNNING | The flow is running. |
| ERROR | An error occurred during flow execution due to communication failure or authentication failure. If **ERROR** continues to occur, contact **Customer Support > Inquire**. |
| STOP\_FAILED | The flow stop request failed. |
| STOPPED | The flow has stopped. |
| DRAINING | The flow is draining. |
| UNKNOWN | An error occurred for unknown reasons during the execution of the flow. If **UNKNOWN** continues to occur, contact **Customer Support > Inquire**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the status changes to a target flow status.
* Target flow status for notification
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is activated

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow purpose.
* You can specify a Flow Template to easily load flows of features users want.
* You can set the instance type for flow execution.

### Modify Flow

Modify the metadata of a flow.

* Modify the existing flow name and description and apply them to the flow metadata.
* You cannot specify a flow template.
* You can modify a flow even while it is running.
* You can change the instance type for flow execution.
    * The changed instance type applies from the next flow execution.

### Copy Flow

Create new metadata with an existing flow definition.

* Create new metadata with the phrase `_copy` added to the name of existing flow.
* Copy the flow logic of the existing flow as is.
* You can copy even a running flow.
* A running flow is copied in stopped state.
* If the current storage state of flows is temporary, it does not copy the last saved version of existing flows.
* Even if you copy a flow with a scheduler registered, the copied flow does not have a scheduler registered.
* The copied flow is a completely separate flow from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* You cannot delete a running flow.

### More - Start Flow
Start a stopped flow.

* Each flow can run only one at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that is only temporarily saved without ever being saved cannot be started.
* A flow must be saved at least once to be started.
* A flow cannot be started the same as the flow initiated by the user, even if the flow is already being run by Scheduler.

### More - Stop Flow
* You can stop a flow that is preparing to run, running, or draining.
* Stop without processing remaining events.

### More - Stop Flow After Draining
* You can stop a running flow after draining.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow is stopped even if draining is not complete.
* If draining is complete while time remains on the timeout, the flow is stopped immediately.
* A flow that is draining can be stopped immediately through flow stop.