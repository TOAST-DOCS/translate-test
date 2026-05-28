## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add necessary nodes and define each node's behavior by entering configuration values.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Execute the flow.
    5. Check log information to verify that the flow executed normally.

## Management

This is a page for viewing and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/en/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, it searches for flows that contain the search term in their name.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the search result flows in table format.

* Displays simple flow metadata and current flow execution status.
* Sorted by most recent modification date.
* You can select flows to use management features such as flow modification, flow details view, and flow start.
* You can view only flows with specific statuses through the filter condition feature.
* Once flows are retrieved, you must click **Refresh** to update the search results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> occurs continuously, please contact **Customer Support > Inquiries**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> occurs continuously, please contact **Customer Support > Inquiries**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the status changes to a target flow status for notifications.
* Target flow statuses for notifications
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is activated


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Selects execution mode according to the flow purpose.
* You can easily load flows with desired functionality by specifying a flow template.
* You can set the instance type for executing the flow.

### Modify Flow

Modifies the flow's metadata.

* Modifies existing flow name and description and reflects them in the flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is executing.
* You can change the instance type for executing the flow.
    * However, the changed instance type applies from the next flow execution.

### Copy Flow

Creates new metadata using existing flow definition.

* Creates new metadata with `_copy` added to the existing flow's name.
* Copies the flow logic that the existing flow has as-is.
* Running flows can also be copied.
* Running flows are copied in stopped state.
* If the flow's current save state is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a flow in stopped state.

* Only one flow can be executed simultaneously for each flow.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* Flows must be saved at least once to be started.
* Even if a flow is being executed by a scheduler, you cannot start a flow the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing for execution, executing, or draining.
* Terminates without processing remaining events.

### More - Drain and Stop Flow
* You can drain and then stop a running flow.
* Draining means processing the flow's remaining events.
* If the timeout period is exceeded, it terminates even if draining is not finished.
* If draining finishes while there is remaining timeout time, it terminates immediately.
* Flows that are draining can be terminated immediately through flow termination.