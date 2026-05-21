## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order.

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Run Flow
    1. Create a flow.
    2. Add the necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the order of node operations through node connections.
    4. Execute the flow.
    5. Check the log information to verify that the flow has executed normally.

## Management

A page to query and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on the given criteria.

* When searching by flow name, flows that include the search term in the name are returned.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Display query results in table format.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows in a specific state using the filter condition feature.
* Once a flow is queried, you must click **Refresh** to update the query results.
* Up to 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Acquiring resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> occurs continuously, contact **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> occurs continuously, contact **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to the notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is activated

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select an execution mode according to the flow purpose.
* You can specify a flow template to easily load flows with desired functionality.
* You can set the instance type to execute the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description to reflect them in the flow metadata.
* You cannot specify a flow template.
* You can modify the flow even while the flow is executing.
* You can change the instance type to execute the flow.
    * However, the changed instance type is applied starting from the next flow execution.

### Copy Flow

Create new metadata with an existing flow definition.

* Create new metadata with `_copy` added to the name of the existing flow.
* Copy the flow logic of the existing flow as is.
* You can also copy a running flow.
* Running flows are copied in a stopped state.
* If the current save state of the flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a registered scheduler.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete the flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Only one flow can be executed at a time for each flow.
* A temporarily saved flow starts with the last saved version.
* A flow that is temporarily saved without being saved even once cannot be started.
* A flow must be saved at least once before it can be started.
* Even if the flow is executed by the scheduler, the flow cannot be started in the same way as when started by the user.

### More - Stop Flow
* You can stop a flow that is preparing to run, running, or draining.
* Stops without processing remaining events.

### More - Stop Flow After Draining
* You can stop a running flow after draining.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow is terminated even if draining is not complete.
* If draining completes before the timeout is exceeded, the flow is terminated immediately.
* A draining flow can be terminated immediately through flow termination.