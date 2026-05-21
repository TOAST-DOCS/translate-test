## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence:

* Enable Service
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Run Flow
    1. Create a flow.
    2. Add the required nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the order of node operations through node connections.
    4. Run the flow.
    5. Check the log information to verify that the flow executed normally.

## Management

This is a page for viewing and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching based on flow name, flows that include the search term in their name are searched.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays search results as a table with flows.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* Select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can view flows with a specific status only through the filter condition feature.
* Once a flow is queried, you must press **Refresh** to update the query results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure, etc. If <b>ERROR</b> continues to occur, please contact us through **Customer Support > Inquiry**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred due to an unknown cause during flow execution. If <b>UNKNOWN</b> continues to occur, please contact us through **Customer Support > Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to a notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service being used is activated

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select an execution mode according to the flow purpose.
* You can easily load flows with desired functionality by specifying a flow template.
* You can set the instance type for running the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description and reflect them in the flow metadata.
* Flow template cannot be specified.
* You can modify the flow even while it is running.
* You can change the instance type for running the flow.
    * However, the changed instance type will be applied from the next flow execution onwards.

### Copy Flow

Create new metadata using the existing flow definition.

* Creates new metadata with `_copy` added to the name of the existing flow.
* Copies the flow logic that the existing flow has as is.
* You can copy running flows.
* Running flows are copied in a stopped state.
* If the flow's current save state is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a scheduler registered, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a flow in stopped state.

* Each flow can run only one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without being saved once cannot be started.
* Flows must be saved at least once to be started.
* Even if a flow is running by the scheduler, you cannot start the flow in the same way as a flow started by the user.

### More - Stop Flow
* You can stop a flow that is in preparation for execution, running, or draining.
* Remaining events are not processed and the flow is terminated.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing the remaining events in the flow.
* If the timeout is exceeded, the flow is terminated even if draining is not complete.
* If draining completes within the timeout period, the flow is terminated immediately.
* A draining flow can be terminated immediately through flow stop.