## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define how each node behaves.
    3. Complete the flow by determining the order of nodes' actions through node connections.
    4. Execute the flow.
    5. Check log information to verify that the flow executed successfully.

## Management

This is a page for viewing and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](https://static.toastoven.net/prod_translate/translate-test/en/management_main_2025_06.png)

### Search

Search flows based on given criteria.

* When searching by flow name, it searches for flows that contain the search term in their names.

### Filter

Search flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the query result flows in table format.

* Displays simple flow metadata and current flow execution status.
* Sorted by most recent modification date.
* You can select flows to use management features such as change flow, view flow details, and start flow.
* You can view only flows with specific statuses through the filter condition feature.
* Once flows are queried, you must click **Refresh** to update the query results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Flow execution request failed. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication issues. If <b>ERROR</b> occurs continuously, please contact us through **Customer Support > Contact Us**. |
| STOP\_FAILED   | Flow termination request failed. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> occurs continuously, please contact us through **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when changed to target flow status for alerts.
* Target flow statuses for alerts
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with **DataFlow ADMIN** role in the project where the DataFlow service being used is activated


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select execution mode based on flow purpose.
* You can easily load flows with desired functionality by specifying a flow template.
* You can set the instance type to execute the flow.

### Change Flow

Modifies the flow's metadata.

* Modifies existing flow name and description and reflects them in the flow metadata.
* Flow templates cannot be specified.
* Flow changes are possible even while the flow is running.
* You can change the instance type to execute the flow.
    * However, the changed instance type will be applied from the next flow execution.

### Copy Flow

Creates new metadata with an existing flow definition.

* Creates new metadata with `_copy` added to the existing flow's name.
* Copies the flow logic that the existing flow has as-is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the flow's current save state is temporary save, the last saved version of the existing flow is not copied.
* Even if a flow with a registered scheduler is copied, the copied flow will not have the scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a flow in stopped state.

* Each flow can only run one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without being saved at least once cannot be started.
* Flows must be saved at least once to be started.
* Even if a flow is running by the scheduler, you cannot start the flow the same as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing for execution, running, or draining.
* Terminates without processing remaining events.

### More - Stop After Draining
* You can stop running flows after draining.
* Draining means processing remaining events in the flow.
* If the timeout period is exceeded, it terminates even if draining is not finished.
* If draining finishes while timeout time remains, it terminates immediately.
* Flows that are draining can be stopped immediately through flow termination.