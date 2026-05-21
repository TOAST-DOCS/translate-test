## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define the operation method for each node.
    3. Complete the flow by determining the operation order of nodes through node connections.
    4. Execute the flow.
    5. Check the log information to verify that the flow executed normally.

## Management

This is a page for inquiring and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, flows that include the search term in the name are returned.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the search results as a table of flows.

* Displays simple flow metadata and current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management features such as flow modification, flow detail view, and flow start.
* You can view flows with a specific status only through the filter condition feature.
* Once a flow is retrieved, you must press **Refresh** to update the search results.
* 12 flows are retrieved per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure, etc. If <b>ERROR</b> persists, contact **Customer Support > Inquiry**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred due to an unknown cause during flow execution. If <b>UNKNOWN</b> persists, contact **Customer Support > Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow changes to a notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service being used is activated

### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select an execution mode according to the flow purpose.
* By specifying a flow template, users can easily load flows with the desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modifies the metadata of a flow.

* Modifies the existing flow name and description to reflect changes in flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution onwards.

### Copy Flow

Creates new metadata using the existing flow definition.

* Creates new metadata with `_copy` appended to the existing flow name.
* Copies the flow logic that the existing flow has.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if a flow with a registered scheduler is copied, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow

Starts a flow that is in a stopped state.

* Each flow can only run one at a time.
* Temporarily saved flows are started with the last saved version.
* Flows that have only been temporarily saved without being saved even once cannot be started.
* Flows must be saved at least once before they can be started.
* Even if a flow is running due to a scheduler, the flow cannot be started in the same way as a flow started by a user.

### More - Stop Flow

* You can stop a flow that is preparing for execution, running, or draining.
* Stops without processing remaining events.

### More - Drain and Stop Flow

* You can drain and stop a running flow.
* Draining means processing remaining events in the flow.
* If the timeout time is exceeded, the flow is stopped even if draining is not complete.
* If draining is complete while timeout time remains, the flow is stopped immediately.
* A draining flow can be stopped immediately through flow stop.