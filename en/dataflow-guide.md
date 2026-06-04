## Data & Analytics > DataFlow > Console Guide

You can use DataFlow in the following order:

* Service activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define the behavior of each node.
    3. Complete the flow by connecting nodes to determine the execution order of nodes.
    4. Run the flow.
    5. Check log information to verify that the flow ran normally.

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
* You can select a flow to use management functions such as changing the flow, viewing flow details, and starting the flow.
* You can view only flows with specific statuses through the filter condition function.
* Once flows are retrieved, you must click **Refresh** to update the search results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> occurs continuously, contact us through **Customer Support > Inquiries**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> occurs continuously, contact us through **Customer Support > Inquiries**. |

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
* Select the execution mode based on the flow purpose.
* You can easily load a flow with the desired functionality by specifying a flow template.
* You can configure the instance type for running the flow.

### Change Flow

Modifies the metadata of a flow.

* Modifies existing flow names and descriptions and reflects them in the flow metadata.
* Flow templates cannot be specified.
* You can change flows even while the flow is running.
* You can change the instance type for running the flow.
    * However, the changed instance type is applied starting from the next flow execution.

### Copy Flow

Creates new metadata using an existing flow definition.

* Creates new metadata by adding the `_copy` text to the name of the existing flow.
* Copies the flow logic that the existing flow has as-is.
* You can copy flows that are currently running.
* Running flows are copied in a stopped state.
* If the current save state of the flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a flow that is in a stopped state.

* Each flow can run only one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without being saved even once cannot be started.
* Flows must be saved at least once before they can be started.
* Even if a flow is running by the scheduler, you cannot start the flow in the same way as a flow started by a user.

### More - Terminate Flow
* You can terminate flows that are preparing for execution, running, or draining.
* Terminates without processing remaining events.

### More - Terminate Flow After Draining
* You can terminate running flows after draining.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, it terminates even if draining is not finished.
* If draining is finished while timeout time remains, it terminates immediately.
* Flows that are draining can be terminated immediately through flow termination.