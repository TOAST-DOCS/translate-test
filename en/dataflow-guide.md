## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add the required nodes and input configuration values to define the operation of each node.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Execute the flow.
    5. Check the log information to verify that the flow executed normally.

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

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* Select a flow to use management features such as modifying the flow, viewing flow details, and starting the flow.
* Use the filter condition feature to view only flows in a specific status.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status | Description |
|---------------------------------------------------| --- |
| START_FAILED  | Failed to request flow execution. |
| QUOTA_EXCEEDED | Execution failed due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure, etc. If <b>ERROR</b> persists, contact **Customer Support > Contact Us**. |
| STOP_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> persists, contact **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to a notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is activated

### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select an execution mode based on the flow's purpose.
* Specify a flow template to easily load a flow with desired features.
* You can set the instance type for executing the flow.

### Modify Flow

Modifies the metadata of a flow.

* Modifies the existing flow name and description to reflect in the flow metadata.
* Flow templates cannot be specified.
* You can modify the flow even while the flow is executing.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution onward.

### Copy Flow

Creates new metadata with an existing flow definition.

* Creates new metadata with `_copy` appended to the existing flow's name.
* Copies the existing flow's logic as is.
* You can copy an executing flow.
* Executing flows are copied in a stopped state.
* If the current save state of the flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes the flow metadata.
* Deleted flows cannot be recovered.
* You cannot delete an executing flow.

### More - Start Flow

Starts a flow in a stopped state.

* Each flow can only execute one at a time.
* Temporarily saved flows start with the last saved version.
* You cannot start a flow that has only been temporarily saved without being saved even once.
* A flow must be saved at least once to be started.
* Even if a flow is executing due to a scheduler, it cannot be started by a user in the same manner.

### More - Stop Flow

* You can stop flows that are preparing for execution, executing, or draining.
* Stops without processing remaining events.

### More - Drain and Stop Flow

* You can drain and stop an executing flow.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow stops even if draining is not complete.
* If draining completes while timeout remains, the flow stops immediately.
* A draining flow can be stopped immediately through flow termination.