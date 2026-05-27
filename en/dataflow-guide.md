## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow execution
    1. Create a flow.
    2. Add necessary nodes and define the behavior of each node by entering configuration values.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Execute the flow.
    5. Check log information to verify that the flow executed normally.

## Management

This is a page for viewing and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/TOAST-DOCS/translate-test/en/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching based on flow name, it searches for flows that contain the search term in their name.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the search result flows in table format.

* Displays simple flow metadata and current flow execution status.
* Sorted by last modified date.
* You can select a flow to use management functions such as flow modification, flow details view, and flow start.
* You can view only flows with specific status through the filter condition function.
* Once flows are retrieved, you must click **Refresh** to update the search results.
* 12 flows are displayed per page, and you can navigate between pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> occurs continuously, please contact us through **Customer Support > Inquiries**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> occurs continuously, please contact us through **Customer Support > Inquiries**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the status changes to target flow status for notification.
* Target flow status for notification
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with **DataFlow ADMIN** role in the project where the DataFlow service in use is activated


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow purpose.
* You can easily load a flow with the desired functionality by specifying a flow template.
* You can set the instance type for executing the flow.

### Modify Flow

Modifies the metadata of a flow.

* Modifies existing flow name and description and reflects them in the flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type will be applied from the next flow execution.

### Copy Flow

Creates new metadata with the existing flow definition.

* Creates new metadata with `_copy` added to the existing flow's name.
* Copies the flow logic that the existing flow has as-is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a flow in stopped state.

* Each flow can only run one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* Flows must be saved at least once before they can be started.
* Even if a flow is running by the scheduler, you cannot start a flow the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing for execution, running, or draining.
* Terminates without processing remaining events.

### More - Stop Flow After Draining
* You can stop a running flow after draining.
* Draining means processing the remaining events of the flow.
* If the timeout period is exceeded, it terminates even if draining is not finished.
* If draining is completed while there is still timeout time remaining, it terminates immediately.
* Flows that are draining can be terminated immediately through flow termination.