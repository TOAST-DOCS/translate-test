## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Activating the service
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Running a flow
    1. Create a flow.
    2. Add the necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the node execution order through node connections.
    4. Run the flow.
    5. Check the log information to verify that the flow executed normally.

## Management

This page allows you to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on the given criteria.

* When searching by flow name, flows containing the search term in the name are displayed.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the search results in table format.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* Using the filter condition feature, you can view only flows in a specific state.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute flow due to insufficient resources. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failures or authentication failures. If <b>ERROR</b> persists, contact us through **Customer Support > Inquiries**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> persists, contact us through **Customer Support > Inquiries**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow changes to a notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is active

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select the execution mode based on the flow purpose.
* You can specify a flow template to easily load flows with the desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description to reflect changes in the flow metadata.
* Flow templates cannot be specified.
* You can modify the flow even while it is executing.
* You can change the instance type for executing the flow.
    * However, the changed instance type applies from the next flow execution.

### Copy Flow

Create new metadata using an existing flow definition.

* Create new metadata with `_copy` appended to the existing flow name.
* Copy the flow logic of the existing flow as is.
* You can copy a flow that is currently executing.
* Running flows are copied in a stopped state.
* If the flow's current save state is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a scheduler registered, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete the flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* You cannot delete a flow that is executing.

### More - Start Flow
Start a flow that is in a stopped state.

* Each flow can only execute one at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that has only been temporarily saved without being saved even once cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is being executed by a scheduler, you cannot start the flow in the same way as a flow started by a user.

### More - Stop Flow
* You can stop a flow that is preparing to execute, executing, or draining.
* Remaining events are not processed and the flow is terminated.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing the remaining events in the flow.
* If the timeout is exceeded, the flow is terminated even if draining is not complete.
* If draining completes while timeout remains, the flow terminates immediately.
* A draining flow can be terminated immediately through flow stop.