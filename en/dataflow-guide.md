## Data & Analytics > DataFlow > Console User Guide

DataFlow can be used in the following order:

* Service activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow execution
    1. Create a flow.
    2. Add the necessary nodes and enter configuration values to define how each node behaves.
    3. Determine the order of nodes' actions through node connections to complete the flow.
    4. Execute the flow.
    5. Verify that the flow ran successfully by checking log information.

## Management

Page that queries and manages the flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](https://static.toastoven.net/prod2_translate-test/en/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* Searching based on flow name searches for flows that contain the search term in their name.

### Filter

Search for flows based on given conditions.

* Provides filtering options according to flow status values.

### Flow List

Displays query result flows in table format.

* Displays simple flow metadata and current flow execution status.
* Sorted by most recent modification date.
* You can select a flow to use management features such as changing flows, viewing flow details, and starting flow.
* You can query only flows with specific status through filter condition functionality.
* Once queried flows require clicking **Refresh** to update query results.
* You can query 12 flows per page and navigate through the **Previous** and **Next** buttons.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Flow execution request failed. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation completed. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> continues to occur, contact **Customer Support > Inquiries**. |
| STOP\_FAILED   | Flow termination request failed. |
| STOPPED        | Flow has terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred for unknown reasons during the execution of the flow. If <b>UNKNOWN</b> continues to occur, contact **Customer Support > Inquiries**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the status changes to the target flow status for notifications.
* Target flow status for notifications
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with **DataFlow ADMIN** role in the project where the active DataFlow service is enabled


### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select execution mode according to flow purpose.
* You can specify Flow Template to easily load flows of features users wants.
* You can set instance type for executing the flow.

### Change Flow

Modify the metadata of a flow.

* Modify existing flow name and description to reflect in flow metadata.
* Flow template cannot be specified.
* Flow changes are possible even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type will be applied from the next flow execution.

### Copy Flow

Create new metadata with existing flow definition.

* Create new metadata with the phrase `_copy` added to the name of existing flow.
* Copy the flow logic that the existing flow has as is.
* Running flows can also be copied.
* Running flows are copied in stopped state.
* If the current storage state of flows is temporary, it does not copy the last saved version of existing flows.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a flow in stopped state.

* Each flow can only run one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* Flows must be saved at least once to be started.
* A flow cannot be started the same as the flow initiated by the user, even if the flow is already being run by Scheduler.

### More - Stop Flow
* You can stop flows that are preparing for execution, running, or draining.
* Terminates without processing remaining events.

### More - Stop After Draining Flow
* You can stop running flows after draining.
* Draining means processing remaining events of the flow.
* If timeout is exceeded, it terminates even if draining is not finished.
* If draining finishes while timeout time remains, it terminates immediately.
* Draining flows can be terminated immediately through flow termination.