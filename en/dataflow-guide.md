## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow execution
    1. Create a flow.
    2. Add necessary nodes and define the operation method of each node by entering configuration values.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Execute the flow.
    5. Check log information to verify that the flow executed normally.

## Management

This is a page for viewing and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](https://static.toastoven.net/prod_translate/en/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* Searching by flow name returns flows that contain the search term in their name.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the query result flows in table format.

* Shows simple flow metadata and current flow execution status.
* Sorted by last modified date.
* You can select a flow to use management functions such as modify flow, view flow details, and start flow.
* You can view only flows with specific statuses using the filter condition feature.
* Once queried, flows require clicking **Refresh** to update the query results.
* Shows 12 flows per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources for execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation completed. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication issues. If <b>ERROR</b> occurs persistently, please contact us through **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> occurs persistently, please contact us through **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the status changes to a target flow status for notification.
* Target flow statuses for notification
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with **DataFlow ADMIN** role in the project where the DataFlow service in use is activated


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select execution mode according to flow purpose.
* You can easily load flows with desired functionality by specifying a flow template.
* You can set the instance type for executing the flow.

### Modify Flow

Modifies the metadata of a flow.

* Modifies existing flow name and description and reflects them in the flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Creates new metadata using existing flow definitions.

* Creates new metadata with `_copy` added to the existing flow name.
* Copies the flow logic of the existing flow as-is.
* Running flows can also be copied.
* Running flows are copied in stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a flow in stopped state.

* Each flow can run only one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* Flows must be saved at least once to be started.
* Even if a flow is running by the scheduler, you cannot start the flow in the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing for execution, running, or draining.
* Terminates without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop running flows.
* Draining means processing remaining events in the flow.
* If the timeout period is exceeded, it terminates even if draining is not finished.
* If draining finishes while timeout time remains, it terminates immediately.
* Draining flows can be terminated immediately through flow stop.