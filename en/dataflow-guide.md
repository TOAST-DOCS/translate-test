## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Run Flow
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the order of node operations through node connections.
    4. Run the flow.
    5. Check log information to verify that the flow has executed normally.

## Management

This is a page where you can view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on the given criteria.

* When searching by flow name, it searches for flows that include the search term in their name.

### Filter

Search for flows based on the given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the search results as a table.

* Displays simple flow metadata and the current flow execution status.
* Sorts by the most recent modification date.
* You can select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status through the filter condition feature.
* Once a flow is queried, you must click **Refresh** to update the query results.
* 12 flows per page are queried, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Resources for flow execution are being secured. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failures, authentication failures, etc. If <b>ERROR</b> continues to occur, contact us through **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has stopped. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> continues to occur, contact us through **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to the notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is active

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow purpose.
* You can easily load a flow with desired functionality by specifying a flow template.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description to reflect them in the flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution onwards.

### Copy Flow

Create new metadata with an existing flow definition.

* Creates new metadata with `_copy` appended to the name of the existing flow.
* Copies the flow logic of the existing flow as-is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the current saved state of the flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete the flow metadata.

* Completely deletes the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can run only one at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that has only been temporarily saved without being saved cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is running by a scheduler, it cannot be started in the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing to run, running, or draining.
* Termination occurs without processing remaining events.

### More - Stop Flow After Draining
* You can drain and stop a running flow.
* Draining refers to processing the remaining events in the flow.
* If the timeout exceeds, the flow terminates even if draining is not complete.
* If draining completes while timeout remains, the flow terminates immediately.
* A draining flow can be terminated immediately through flow termination.