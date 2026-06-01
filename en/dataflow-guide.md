## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add the necessary nodes and enter configuration values to define how each node behaves.
    3. Complete the flow by determining the order of nodes' actions through node connections.
    4. Execute the flow.
    5. Check the log information to verify that the flow ran successfully.

## Management

This is the page for querying and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](https://static.toastoven.net/translate-test/en/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, it searches for flows that contain the search term in their name.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the query result flows in table format.

* Shows simple flow metadata and current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management features such as flow modification, flow details view, and flow start.
* You can query only flows with specific status through filter condition functionality.
* Once flows are queried, you must click **Refresh** to update the query results.
* Displays 12 flows per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> persists, please contact us through **Customer Support > Inquiries**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> persists, please contact us through **Customer Support > Inquiries**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the status changes to a target flow status for notification.
* Target flow statuses for notification
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is activated


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow purpose.
* You can easily load a flow with the desired functionality by specifying a flow template.
* You can configure the instance type for executing the flow.

### Change Flow

Modifies the metadata of a flow.

* Modifies the existing flow name and description and reflects them in the flow metadata.
* Flow templates cannot be specified.
* Flow changes are possible even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type will be applied from the next flow execution.

### Copy Flow

Creates new metadata with the existing flow definition.

* Creates new metadata with `_copy` added to the existing flow's name.
* Copies the flow logic that the existing flow has exactly as it is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a stopped flow.

* Each flow can only run one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* Flows must be saved at least once to be started.
* Even if a flow is running by the scheduler, you cannot start the flow in the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing to run, running, or draining.
* Terminates without processing remaining events.

### More - Stop After Draining
* You can stop running flows after draining.
* Draining means processing remaining events in the flow.
* If the timeout period is exceeded, it terminates even if draining is not finished.
* If draining finishes while there is still timeout time remaining, it terminates immediately.
* Flows that are draining can be terminated immediately through flow termination.