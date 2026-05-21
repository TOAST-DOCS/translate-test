## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order.

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define the operation method of each node.
    3. Complete the flow by determining the operation sequence of nodes through node connections.
    4. Execute the flow.
    5. Check log information to verify that the flow has executed normally.

## Management

This page inquires and manages flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on the given criteria.

* When searching by flow name, flows that include the search term in the name are searched.

### Filter

Search for flows based on the given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays searched flows in table format.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can inquire only flows with specific statuses through the filter condition feature.
* Once a flow is inquired, you must press **Refresh** to update the inquiry results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Flow execution request failed. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources for flow execution. |
| STARTING       | Resources are being secured for flow execution. |
| PREPARING      | Flow execution preparation has been completed. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> continues to occur, contact **Customer Support > Contact Us**. |
| STOP\_FAILED   | Flow termination request failed. |
| STOPPED        | The flow has been stopped. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> continues to occur, contact **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the status changes to the notification target flow status.
* Notification target flow status
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is activated

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select an execution mode according to the flow purpose.
* You can specify a flow template to easily retrieve flows of the desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the flow metadata.

* Modify the existing flow name and description and reflect it in the flow metadata.
* Flow templates cannot be specified.
* You can modify the flow even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Create new metadata with the existing flow definition.

* Creates new metadata with `_copy` appended to the name of the existing flow.
* Copies the flow logic that the existing flow has as is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete the flow metadata.

* Completely deletes the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a flow in a stopped state.

* Each flow can only run one at a time.
* A temporarily saved flow starts with the last saved version.
* Flows that have only been temporarily saved without being saved even once cannot be started.
* A flow must be saved at least once to be started.
* Even if the flow is running by a scheduler, the flow cannot be started in the same way as a flow started by the user.

### More - Stop Flow
* You can stop flows that are in preparation for execution, running, or draining.
* Remaining events are not processed and the flow is stopped.

### More - Drain and Stop Flow
* You can drain a running flow and then stop it.
* Draining means processing the remaining events of the flow.
* If the timeout period is exceeded, the flow is stopped even if draining is not complete.
* If draining is completed while there is remaining timeout time, the flow is stopped immediately.
* A draining flow can be stopped immediately through the stop flow function.