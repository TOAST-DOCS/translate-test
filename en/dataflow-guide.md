## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Enable the Service
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Execute Flow
    1. Create a flow.
    2. Add the necessary nodes, enter configuration values, and define how each node operates.
    3. Complete the flow by connecting nodes to determine their operation order.
    4. Execute the flow.
    5. Check the log information to verify that the flow executed normally.

## Management

This is the page for retrieving and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, flows that include the search term in their name are retrieved.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays retrieved flows in table format.

* Displays basic flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* By selecting a flow, you can use management functions such as modifying the flow, viewing flow details, and starting the flow.
* Using the filter condition feature, you can retrieve only flows in a specific status.
* Once flows are retrieved, you must click **Refresh** to update the search results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status | Description |
|---|---|
| START\_FAILED  | Flow execution request failed. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Allocating resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If ERROR persists, please contact **Customer Support > Contact Us**. |
| STOP\_FAILED   | Flow termination request failed. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If UNKNOWN persists, please contact **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow changes to a notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is enabled and in use


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding name and description for flow identification.
* Flow names can be duplicated across different flows.
* Select the execution mode based on the flow's purpose.
* By specifying a flow template, users can easily load flows with the desired functionality.
* You can configure the instance type for running the flow.

### Modify Flow

Modifies the flow's metadata.

* Modifies the existing flow name and description and reflects them in the flow metadata.
* Flow templates cannot be specified.
* The flow can be modified even while it is running.
* You can change the instance type for running the flow.
    * However, the changed instance type takes effect starting from the next flow execution.

### Copy Flow

Creates new metadata based on the existing flow definition.

* Creates new metadata with `_copy` appended to the name of the existing flow.
* Copies the flow logic of the existing flow as-is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the flow's current save state is a temporary save, the last saved version of the existing flow is not copied.
* Even if a flow with a registered scheduler is copied, the copied flow will not have the scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes the flow's metadata.

* Completely deletes the flow's metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a flow in a stopped state.

* Only one flow can be executed at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without being saved once cannot be started.
* A flow must be saved at least once before it can be started.
* When a flow is already running via the scheduler, you cannot manually start the same flow.

### More - Terminate Flow
* You can terminate flows that are preparing for execution, running, or draining.
* Terminates without processing remaining events.

### More - Drain and Then Terminate Flow
* You can drain and then terminate a running flow.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow terminates even if draining is not complete.
* If draining completes before the timeout is reached, the flow terminates immediately.
* A flow that is draining can be immediately terminated through flow termination.