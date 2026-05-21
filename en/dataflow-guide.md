## Data & Analytics > DataFlow > Console User Guide

DataFlow can be used in the following sequence.

* Activate the service
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Run a flow
    1. Create a flow.
    2. Add the necessary nodes and define how each node operates by entering configuration values.
    3. Complete the flow by determining the order of node operations through node connections.
    4. Run the flow.
    5. Check log information to verify that the flow has executed successfully.

## Management

This is the page where you can view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on the given criteria.

* When you search by flow name, flows whose names contain the search term are returned.

### Filter

Search for flows based on the given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the search results in table format.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow and use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can use the filter condition feature to view only flows with a specific status.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* Displays 12 flows per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute flow due to insufficient resources for flow execution. |
| STARTING       | Resources for flow execution are being secured. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> persists, please contact **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> persists, please contact **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow changes to a notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service being used is activated

### Create Flow

Creates metadata to define a flow.

* Adds a name and description to identify the flow, creating flow metadata.
* The flow name can be duplicated with other flows.
* Selects an execution mode according to the flow's purpose.
* You can specify a flow template to easily load flows with desired functionality.
* You can configure the instance type for running the flow.

### Modify Flow

Modifies the metadata of a flow.

* Modifies the existing flow name and description and reflects them in the flow metadata.
* The flow template cannot be specified.
* You can modify the flow even while the flow is running.
* You can change the instance type for running the flow.
    * However, the changed instance type will be applied from the next flow execution onward.

### Copy Flow

Creates new metadata with the definition of an existing flow.

* Creates new metadata with `_copy` appended to the name of the existing flow.
* Copies the flow logic of the existing flow as-is.
* You can copy a running flow.
* Running flows are copied in a stopped state.
* If the current save state of the flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have a registered scheduler.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a stopped flow.

* Only one flow can run at a time for each flow.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* A flow must be saved at least once before it can be started.
* If a flow is running due to a scheduler, you cannot start the flow the same way as when started by a user.

### More - Stop Flow
* You can stop flows that are preparing to run, running, or draining.
* Stops without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow stops even if draining is not complete.
* If draining completes while timeout remains, the flow stops immediately.
* A draining flow can be stopped immediately through flow termination.