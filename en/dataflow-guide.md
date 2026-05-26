## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Run Flow
    1. Create a flow.
    2. Add necessary nodes and define how each node operates by entering configuration values.
    3. Complete the flow by determining the operation order of nodes through node connections.
    4. Run the flow.
    5. Check the log information to verify that the flow executed successfully.

## Management

This page allows you to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search flows based on given criteria.

* Searching by flow name displays flows that contain the search term in their name.

### Filter

Search flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Display search results as a table of flows.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* Use the filter condition feature to view only flows with a specific status.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* 12 flows are retrieved per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Resources for flow execution are being allocated. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failures or authentication failures, etc. If <b>ERROR</b> occurs continuously, contact **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> occurs continuously, contact **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow changes to the notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is activated


### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select an execution mode according to the flow purpose.
* Specify a flow template to easily load flows with desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the metadata of a flow.

* Modify the existing flow name and description to reflect them in the flow metadata.
* Flow templates cannot be specified.
* You can modify the flow even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Create new metadata with the existing flow definition.

* Create new metadata with `_copy` appended to the existing flow name.
* Copy the flow logic of the existing flow as is.
* You can copy a running flow.
* A running flow is copied in stopped state.
* If the flow's current save state is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a scheduler registered, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can only run one at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that has only been temporarily saved without ever being saved cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is running by the scheduler, it cannot be started the same way as a flow started by the user.

### More - Stop Flow
* You can stop flows that are preparing to run, running, or draining.
* Stops without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow is terminated even if draining is not complete.
* If draining completes while there is remaining timeout, the flow is terminated immediately.
* A draining flow can be terminated immediately through flow termination.