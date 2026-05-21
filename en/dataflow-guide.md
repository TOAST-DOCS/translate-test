## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence.

* Service activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Run flow
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define the operation method for each node.
    3. Complete the flow by determining the operation order of nodes through node connections.
    4. Execute the flow.
    5. Check log information to verify that the flow executed successfully.

## Management

This page allows you to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, flows that contain the search term in their name are returned.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the search results in table format.

* Displays simple flow metadata and current flow execution status.
* Sorts by the most recent modification date.
* You can select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status using the filter condition feature.
* Once flows are retrieved, you must click **Refresh** to update the search results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                            | Description |
|---------------------------------------------------| --- |
| START_FAILED  | Failed to request flow execution. |
| QUOTA_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure, authentication failure, etc. If <b>ERROR</b> persists, contact **Customer Support > Inquiries**. |
| STOP_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> persists, contact **Customer Support > Inquiries**. |

#### Flow Status Change Notification Email
* You can receive a notification email when the flow status changes to a monitored status.
* Monitored flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is activated

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow purpose.
* You can easily load a flow with desired functionality by specifying a flow template.
* You can configure the instance type for executing the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description and apply them to the flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type applies from the next flow execution.

### Copy Flow

Create new metadata with an existing flow definition.

* Create new metadata with `_copy` added to the existing flow's name.
* Copy the flow logic of the existing flow as is.
* You can copy a running flow.
* Running flows are copied in a stopped state.
* If the current save state of the flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a flow that is in a stopped state.

* Only one flow can be executed at a time for each flow.
* A temporarily saved flow starts with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* A flow must be saved at least once before it can be started.
* If a flow is running due to a scheduler, it cannot be started by a user in the same way as a user-initiated flow.

### More - Stop Flow
* You can stop flows that are in preparation for execution, running, or draining.
* Stops without processing any remaining events.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing the remaining events of the flow.
* If the timeout period is exceeded, the flow stops even if draining is not complete.
* If draining completes while timeout remains, the flow stops immediately.
* A draining flow can be stopped immediately through flow termination.