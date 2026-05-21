## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence.

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Execute the flow.
    5. Check the log information to verify that the flow executed normally.

## Management

This is a page where you can view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on the given criteria.

* When you search by flow name, flows that contain the search term in their name are returned.

### Filter

Search for flows based on the given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays search results as a table of flows.

* Displays simple flow metadata and current flow execution status.
* Sorts by the most recent modification date.
* You can select a flow to use management features such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status using the filter condition feature.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Insufficient resources to execute the flow. |
| STARTING       | Acquiring resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is executing. |
| ERROR              | An error occurred due to communication failure or authentication failure during flow execution. If <b>ERROR</b> continues to occur, contact us through **Customer Support > Inquire**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred due to an unknown cause during flow execution. If <b>UNKNOWN</b> continues to occur, contact us through **Customer Support > Inquire**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to a notification target status.
* Notification target flow status
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service being used is activated

### Create Flow

Create metadata to define a flow.

* Add a name and description to create flow metadata for flow identification.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow's purpose.
* You can specify a flow template to easily load a flow with the desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description to reflect the changes in flow metadata.
* Flow templates cannot be specified.
* You can modify the flow even while the flow is executing.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution onwards.

### Copy Flow

Create new metadata using an existing flow definition.

* Creates new metadata with `_copy` appended to the existing flow's name.
* Copies the flow logic of the existing flow as is.
* You can copy an executing flow.
* An executing flow is copied in a stopped state.
* If the flow's current save state is temporary, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely deletes the flow metadata.
* Deleted flows cannot be recovered.
* You cannot delete an executing flow.

### More - Start Flow
Start a stopped flow.

* Each flow can only execute one at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that has only been temporarily saved without being saved even once cannot be started.
* A flow must be saved at least once before it can be started.
* If a flow is being executed by a scheduler, the flow cannot be started by the user in the same way as a user-initiated flow.

### More - Stop Flow
* You can stop a flow that is preparing for execution, executing, or draining.
* The flow stops without processing remaining events.

### More - Stop Flow After Draining
* You can drain and then stop an executing flow.
* Draining means processing the remaining events in the flow.
* If the timeout is exceeded, the flow is terminated even if draining is not complete.
* If draining completes while timeout remains, the flow is terminated immediately.
* A draining flow can be terminated immediately through flow termination.