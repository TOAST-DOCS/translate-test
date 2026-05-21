## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define the operation method of each node.
    3. Complete the flow by determining the operation sequence of nodes through node connections.
    4. Execute the flow.
    5. Check the log information to verify that the flow executed normally.

## Management

A page to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search flows based on the given criteria.

* When searching by flow name, flows that include the search term in the name are displayed.

### Filter

Search flows based on the given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays search results as a table of flows.

* Displays simple flow metadata and the current flow execution status.
* Sorted by last modified date.
* You can select a flow to use management features such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status using the filter condition feature.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* Displays 12 flows per page, and you can move pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is executing. |
| ERROR              | An error occurred due to communication failure or authentication failure during flow execution. If <b>ERROR</b> occurs continuously, contact **Customer Support > Inquiry**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has stopped. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred due to an unknown cause during flow execution. If <b>UNKNOWN</b> occurs continuously, contact **Customer Support > Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to a notification target status.
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
* Select the execution mode according to the flow purpose.
* You can specify a flow template to easily load flows with the desired functionality.
* You can set the instance type to execute the flow.

### Modify Flow

Modify the flow metadata.

* Modify the existing flow name and description to reflect them in the flow metadata.
* Flow templates cannot be specified.
* You can modify the flow even while the flow is running.
* You can change the instance type to execute the flow.
    * However, the changed instance type applies from the next flow execution.

### Copy Flow

Create new metadata using the existing flow definition.

* Create new metadata with `_copy` added to the name of the existing flow.
* Copy the flow logic of the existing flow as is.
* You can copy a flow that is running.
* Running flows are copied in a stopped state.
* If the current save status of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a scheduler registered, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete the flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can run only one at a time.
* A temporarily saved flow starts with the last saved version.
* Flows that have only been temporarily saved without ever saving cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is running by the scheduler, it cannot be started by the user in the same way as a user-initiated flow.

### More - Stop Flow
* You can stop flows that are preparing to run, running, or draining.
* Stop without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow stops even if draining is not complete.
* If draining completes while timeout remains, the flow stops immediately.
* A flow that is draining can be stopped immediately through the stop flow operation.