## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add the necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the operation order of nodes through node connections.
    4. Run the flow.
    5. Check the log information to verify that the flow executed normally.

## Management

This is a page to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, flows that include the search term in their name are retrieved.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Display search results in table format.

* Displays simple flow metadata and current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can retrieve flows of a specific status using the filter condition feature.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* A maximum of 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> continues to occur, contact **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> continues to occur, contact **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the status changes to the target notification status.
* Target notification flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is activated

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow's purpose.
* You can easily load flows with desired functionality by specifying a flow template.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description to reflect changes in the flow metadata.
* Flow templates cannot be specified.
* You can modify the flow even while it is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Create new metadata based on an existing flow definition.

* Create new metadata with `_copy` appended to the name of the existing flow.
* Copy the flow logic from the existing flow as-is.
* You can copy a running flow.
* Running flows are copied in a stopped state.
* If the current save status of a flow is temporary save, the last saved version of the existing flow is not copied.
* Even if a flow with a scheduler registered is copied, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can only run one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that are only temporarily saved without ever being saved cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is running by the scheduler, you cannot start the flow in the same way as a flow started by the user.

### More - Stop Flow
* You can stop flows that are preparing to run, running, or draining.
* Stops without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing the remaining events in the flow.
* If the timeout is exceeded, the flow terminates even if draining is not complete.
* If draining completes while timeout remains, the flow terminates immediately.
* A draining flow can be terminated immediately through flow termination.