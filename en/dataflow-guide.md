## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence:

* Enable the service
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Run the flow
    1. Create a flow.
    2. Add the necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Run the flow.
    5. Check the log information to verify that the flow executed successfully.

## Management

This page allows you to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When you search by flow name, flows that contain the search term in their name are displayed.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays search results in table format.

* Displays simple flow metadata and the current flow execution status.
* Sorted by most recent modification date.
* You can select a flow to use management features such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status using the filter condition feature.
* For flows that have been retrieved once, you must press **Refresh** to update the search results.
* 12 flows are retrieved per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status | Description |
|---|---|
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute the flow due to insufficient resources for flow execution. |
| STARTING       | Acquiring resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure, etc. If <b>ERROR</b> occurs continuously, please contact us through **Customer Support > Inquiry**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has stopped. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred due to an unknown cause during flow execution. If <b>UNKNOWN</b> occurs continuously, please contact us through **Customer Support > Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to a notification target status.
* Notification target flow status
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service being used is activated

### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select an execution mode based on the flow purpose.
* You can specify a flow template to easily load flows with desired functionality.
* You can set the instance type for running the flow.

### Modify Flow

Modifies the metadata of a flow.

* Modifies the existing flow name and description and reflects them in the flow metadata.
* Flow templates cannot be specified.
* You can modify the flow even while the flow is running.
* You can change the instance type for running the flow.
    * However, the changed instance type is applied from the next flow execution onwards.

### Copy Flow

Creates new metadata with an existing flow definition.

* Creates new metadata with `_copy` added to the existing flow name.
* Copies the flow logic of the existing flow as-is.
* You can copy a running flow.
* Running flows are copied in a stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a scheduler registered, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a stopped flow.

* Only one flow can run simultaneously for each flow.
* Temporarily saved flows start with the last saved version.
* Flows that are only temporarily saved without ever being saved cannot be started.
* Flows must be saved at least once before they can be started.
* Even if a flow is running due to a scheduler, you cannot start the flow in the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing to run, running, or draining.
* Stops without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing remaining events of the flow.
* If the timeout is exceeded, the flow is stopped even if draining is not complete.
* If draining completes before the timeout expires, the flow stops immediately.
* A draining flow can be stopped immediately through flow termination.