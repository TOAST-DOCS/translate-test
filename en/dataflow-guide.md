## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence.

* Activate Service
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Run Flow
    1. Create a flow.
    2. Add the necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Run the flow.
    5. Check the log information to verify that the flow executed normally.

## Management

This page allows you to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on the given criteria.

* When searching by flow name, it searches for flows that include the search term in the name.

### Filter

Search for flows based on the given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the query results as a table of flows.

* Displays basic flow metadata and current flow execution status.
* Sorted by the most recent modification date.
* By selecting a flow, you can use management features such as modifying the flow, viewing flow details, and starting the flow.
* Using the filter condition feature, you can view only flows with a specific status.
* For flows that have been queried once, you must click **Refresh** to update the query results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute flow due to insufficient resources for flow execution. |
| STARTING       | Acquiring resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> occurs continuously, contact us through **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> occurs continuously, contact us through **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow changes to the notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service being used is activated


### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated across different flows.
* Select the execution mode according to the flow purpose.
* You can specify a flow template to easily load flows with the desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description to reflect in the flow metadata.
* Flow templates cannot be specified.
* Flow modifications are possible even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Create new metadata with the definition of an existing flow.

* Creates new metadata with `_copy` appended to the existing flow's name.
* Copies the flow logic of the existing flow as-is.
* Flows that are running can also be copied.
* Running flows are copied in a stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* If you copy a flow with a scheduler registered, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete the flow metadata.

* Completely deletes the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can only run one at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that has only been temporarily saved without being saved once cannot be started.
* A flow must be saved at least once before it can be started.
* If a flow is being executed by a scheduler, it cannot be started the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing to run, running, or draining.
* Terminates without processing remaining events.

### More - Drain and Stop Flow
* You can stop a running flow after draining.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow terminates even if draining is not complete.
* If draining completes while timeout remains, the flow terminates immediately.
* A flow that is draining can be terminated immediately through flow stop.