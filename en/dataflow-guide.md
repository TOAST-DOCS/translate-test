## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence:

* Activate Service
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Run Flow
    1. Create a flow.
    2. Add the necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by connecting nodes to determine the order of node operations.
    4. Run the flow.
    5. Check the log information to verify that the flow ran successfully.

## Management

This is a page where you can view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on the given criteria.

* When you search by flow name, flows that contain the search term in their name are returned.

### Filter

Search for flows based on the given conditions.

* Provides filtering options based on flow status values.

### Flow List

The query results are displayed in table format.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow and use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can use the filter condition feature to view only flows in a specific status.
* Once a flow is queried, you must press **Refresh** to update the query results.
* Up to 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status | Description |
|---------------------------------------------------| --- |
| START_FAILED  | The flow execution request failed. |
| QUOTA_EXCEEDED | The flow execution failed due to insufficient resources. |
| STARTING       | Resources for flow execution are being acquired. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure, etc. If <b>ERROR</b> continues to occur, contact us through **Customer Support > Contact Us**. |
| STOP_FAILED   | The flow termination request failed. |
| STOPPED        | The flow has stopped. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> continues to occur, contact us through **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to the notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is activated

### Create Flow

Creates metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow's purpose.
* You can specify a flow template to easily load flows with the functionality you want.
* You can set the instance type to run the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description to reflect them in the flow metadata.
* Flow templates cannot be specified.
* You can modify the flow even while it is running.
* You can change the instance type to run the flow.
    * However, the changed instance type will be applied from the next flow execution onwards.

### Copy Flow

Creates new metadata using the definition of an existing flow.

* Creates new metadata with `_copy` appended to the existing flow's name.
* Copies the flow logic of the existing flow as-is.
* You can copy a running flow.
* Running flows are copied in a stopped state.
* If the current saved state of the flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow that has a scheduler registered, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete the flow metadata.

* Completely deletes the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can run only one at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that is only temporarily saved without being saved even once cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is running due to a scheduler, it cannot be started the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing to run, running, or draining.
* The flow stops without processing remaining events.

### More - Drain and Stop Flow
* You can drain a running flow and then stop it.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow stops even if draining is not complete.
* If draining completes before the timeout expires, the flow stops immediately.
* A draining flow can be stopped immediately through flow termination.