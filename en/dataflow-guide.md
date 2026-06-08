## Data & Analytics > DataFlow > Console Guide

You can use DataFlow in the following order:

* Service activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define the behavior of each node.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Execute the flow.
    5. Check log information to verify that the flow executed normally.

## Management

This is a page for viewing and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/en/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When you search based on flow name, it searches for flows that contain the search term in their name.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the search results as flows in a table format.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management features such as changing the flow, viewing flow details, and starting the flow.
* You can view only flows with specific statuses through the filter condition feature.
* Once flows are retrieved, you must click **Refresh** to update the search results.
* Retrieves 12 flows per page, and you can move between pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation completed. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failures or authentication issues. If <b>ERROR</b> continues to occur, please contact us through **Customer Support > Inquiries**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> continues to occur, please contact us through **Customer Support > Inquiries**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the status changes to a target flow status.
* Target flow statuses for notifications
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is activated


### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select an execution mode based on the flow purpose.
* You can easily load flows with desired features by specifying a flow template.
* You can set the instance type for executing the flow.

### Change Flow

Modify the metadata of a flow.

* Modify existing flow name and description to reflect them in the flow metadata.
* You cannot specify a flow template.
* You can change the flow even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Create new metadata with an existing flow definition.

* Creates new metadata with `_copy` added to the existing flow name.
* Copies the flow logic that the existing flow has as is.
* You can copy flows that are running.
* Running flows are copied in a stopped state.
* If the current save state of the flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* You cannot delete flows that are running.

### More - Start Flow
Start a flow in stopped state.

* Each flow can only run one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* Flows must be saved at least once to be started.
* Even if a flow is running by a scheduler, you cannot start a flow in the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing for execution, running, or draining.
* Stops without processing remaining events.

### More - Stop Flow After Draining
* You can stop running flows after draining.
* Draining means processing remaining events in the flow.
* If the timeout period is exceeded, it stops even if draining is not finished.
* If draining finishes while there is remaining timeout time, it stops immediately.
* Flows that are draining can be stopped immediately through flow termination.