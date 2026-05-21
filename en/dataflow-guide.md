## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence:

* Enable Service
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Execute Flow
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by connecting nodes to determine the order of node operations.
    4. Execute the flow.
    5. Check the log information to verify that the flow executed successfully.

## Management

A page to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search flows based on given criteria.

* Searching by flow name displays flows that contain the search term in the name.

### Filter

Search flows based on given conditions.

* Provides filtering options based on flow status.

### Flow List

Query results are displayed in table format.

* Shows simple flow metadata and current flow execution status.
* Sorted by most recent modification date.
* You can select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status using the filter condition feature.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* 12 flows are retrieved per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is executing. |
| ERROR              | An error occurred due to communication failure or authentication failure during flow execution. If <b>ERROR</b> persists, contact us through **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred due to unknown causes during flow execution. If <b>UNKNOWN</b> persists, contact us through **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to the notification target status.
* Notification target flow status
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service being used is enabled

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select an execution mode based on the flow purpose.
* By specifying a flow template, users can easily load flows with desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the metadata of a flow.

* Modify the existing flow name and description to reflect the changes in flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while a flow is executing.
* You can change the instance type for executing the flow.
    * However, the changed instance type will be applied from the next flow execution.

### Copy Flow

Create new metadata based on an existing flow definition.

* Create new metadata with `_copy` appended to the existing flow's name.
* Copy the flow logic of the existing flow as is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a scheduler registered, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a flow that is in a stopped state.

* Each flow can only run one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without being saved at least once cannot be started.
* Flows must be saved at least once before they can be started.
* If a flow is running due to a scheduler, the flow cannot be started by the user in the same way as a user-initiated flow.

### More - Stop Flow
* Flows that are in preparation, running, or draining can be terminated.
* Remaining events are not processed and the flow terminates.

### More - Drain and Stop Flow
* Running flows can be terminated after draining.
* Draining means processing the remaining events of a flow.
* If the timeout is exceeded, the flow terminates even if draining is not complete.
* If draining completes while timeout remains, the flow terminates immediately.
* Flows that are draining can be terminated immediately through flow termination.