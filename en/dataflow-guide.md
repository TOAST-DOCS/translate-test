## Data & Analytics > DataFlow > Console Guide

You can use DataFlow in the following order:

* Service activation
    1. Create a project.
    2. Select the project you want.
    3. Enable the DataFlow service.
* Flow execution
    1. Create a flow.
    2. Add the required nodes and enter configuration values to define how each node operates.
    3. Complete the flow by connecting nodes to determine the execution order of the nodes.
    4. Execute the flow.
    5. Check the log information to verify that the flow executed normally.

## Management

This is a page where you can view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/en/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When you search based on the flow name, it searches for flows that contain the search term in their name.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the search result flows in table format.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status through the filter condition function.
* Once flows are retrieved, you must click **Refresh** to update the search results.
* Retrieves 12 flows per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure, authentication failure, etc. If <b>ERROR</b> occurs continuously, contact us through **Customer Support > Inquiries**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred due to an unknown cause during flow execution. If <b>UNKNOWN</b> occurs continuously, contact us through **Customer Support > Inquiries**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the status changes to a target flow status for notifications.
* Target flow statuses for notifications
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is enabled


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select an execution mode based on the flow purpose.
* You can specify a flow template to easily load flows with the functionality you want.
* You can set the instance type for executing the flow.

### Modify Flow

Modifies the flow's metadata.

* Modifies the existing flow name and description and reflects them in the flow metadata.
* You cannot specify a flow template.
* You can modify the flow even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied starting from the next flow execution.

### Copy Flow

Creates new metadata using an existing flow definition.

* Creates new metadata with the `_copy` phrase added to the existing flow's name.
* Copies the flow logic that the existing flow has as-is.
* You can copy even running flows.
* Running flows are copied in a stopped state.
* If the current save state of the flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes the flow metadata.
* Deleted flows cannot be recovered.
* You cannot delete running flows.

### More - Start Flow
Starts a flow in stopped state.

* Each flow can only run one at a time.
* A temporarily saved flow starts with the last saved version.
* You cannot start a flow that has only been temporarily saved without ever being saved.
* A flow must be saved at least once before it can be started.
* Even if the flow is running by the scheduler, you cannot start the flow the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing for execution, running, or draining.
* Stops without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop running flows.
* Draining means processing the remaining events of the flow.
* If the timeout period is exceeded, it stops even if draining is not finished.
* If draining finishes while there is remaining timeout time, it stops immediately.
* A draining flow can be stopped immediately through flow termination.