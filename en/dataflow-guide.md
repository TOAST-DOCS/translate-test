## Data & Analytics > DataFlow > Console User Guide

DataFlow can be used in the following sequence.

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add the required nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the order of node operations through node connections.
    4. Execute the flow.
    5. Check the log information to verify that the flow executed normally.

## Management

This page allows you to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on the given criteria.

* When you search by flow name, flows with the search term included in the name are returned.

### Filter

Search for flows based on the given conditions.

* Provides filtering options based on flow status values.

### Flow List

Display the search results as a table of flows.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management functions such as modifying the flow, viewing flow details, and starting a flow.
* You can view only flows in a specific status using the filter condition feature.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* 12 flows are retrieved per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Acquiring resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> persists, please contact **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> persists, please contact **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to the notification target status.
* Notification target flow status
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is currently active

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow purpose.
* You can specify a flow template to easily load flows with the desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the metadata of a flow.

* Modify the existing flow name and description to reflect the changes in the flow metadata.
* You cannot specify a flow template.
* You can modify the flow even while it is executing.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Create new metadata with the definition of an existing flow.

* Create new metadata with `_copy` appended to the name of the existing flow.
* Copy the flow logic of the existing flow as-is.
* You can copy even an executing flow.
* A running flow is copied in a stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* If a flow with a registered scheduler is copied, the copied flow will not have the scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete the flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* You cannot delete an executing flow.

### More - Start Flow
Start a flow that is in a stopped state.

* Only one flow can execute simultaneously for each flow.
* A temporarily saved flow starts with the last saved version.
* You cannot start a flow that has only been temporarily saved without being saved even once.
* A flow must be saved at least once before it can be started.
* Even if a flow is being executed by a scheduler, you cannot start the flow in the same manner as a flow started by the user.

### More - Stop Flow
* You can stop a flow that is preparing to execute, executing, or draining.
* Remaining events are not processed and the flow is terminated.

### More - Drain and Stop Flow
* You can drain and stop an executing flow.
* Draining means processing the remaining events in the flow.
* If the timeout is exceeded, the flow is terminated even if draining is not complete.
* If draining completes before the timeout is exceeded, the flow is terminated immediately.
* A draining flow can be terminated immediately through flow termination.