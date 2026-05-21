## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Execute the flow.
    5. Check the log information to verify that the flow has executed normally.

## Management

This page allows you to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on the given criteria.

* When searching by flow name, flows that contain the search term in the name are displayed.

### Filter

Search for flows based on the given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays search results as a table.

* Displays simple flow metadata and the current flow execution status.
* Sorts by the most recent modification date.
* You can select a flow to use management features such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status using the filter condition feature.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                            | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Resources for flow execution are being secured. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> occurs continuously, contact **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> occurs continuously, contact **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to a notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is activated

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description for flow identification.
* The flow name can be duplicated with other flows.
* Select the execution mode according to the flow purpose.
* You can specify a flow template to easily retrieve the flow of the desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the metadata of a flow.

* Modify the existing flow name and description to reflect them in the flow metadata.
* Flow templates cannot be specified.
* The flow can be modified even while it is executing.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Create new metadata using the existing flow definition.

* Create new metadata with `_copy` appended to the existing flow name.
* Copy the flow logic of the existing flow as is.
* Flows that are executing can also be copied.
* Executing flows are copied in a stopped state.
* If the current save state of the flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a registered scheduler.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete the flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Executing flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can execute only one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without being saved at least once cannot be started.
* Flows must be saved at least once to be started.
* Even if a flow is being executed by a scheduler, it cannot be started in the same way as a flow started by a user.

### More - Stop Flow
* You can terminate flows that are preparing to execute, executing, or draining.
* Terminates without processing remaining events.

### More - Drain and Stop Flow
* You can drain and terminate an executing flow.
* Draining means processing the remaining events of the flow.
* If the timeout time is exceeded, termination occurs even if draining is not complete.
* If draining completes while the timeout time remains, it terminates immediately.
* A draining flow can be terminated immediately through flow termination.