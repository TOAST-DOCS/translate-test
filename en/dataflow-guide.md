## Data & Analytics > DataFlow > Console Guide

You can use DataFlow in the following order:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add the required nodes and define how each node operates by entering configuration values.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Run the flow.
    5. Check the log information to verify that the flow ran successfully.

## Management

This is a page for viewing and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/en/management_main_2025_06.png)

### Search

Search for flows based on the given criteria.

* When you search based on flow name, it searches for flows whose names contain the search term.

### Filter

Search for flows based on the given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the flow search results in table format.

* Displays basic flow metadata and the current flow execution status.
* Sorts based on the most recent modification date.
* You can select a flow to use management functions such as flow modification, flow details view, and flow start.
* You can view only flows with specific statuses through the filter condition function.
* Once flows are retrieved, you must click **Refresh** to update the search results.
* Each page displays 12 flows, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Flow execution request failed. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation completed. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure, authentication failure, or other issues. If <b>ERROR</b> occurs persistently, contact us at **Customer Support > Inquiries**. |
| STOP\_FAILED   | Flow termination request failed. |
| STOPPED        | Flow terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> occurs persistently, contact us at **Customer Support > Inquiries**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to a target notification status.
* Target notification flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is activated


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow purpose.
* By specifying a flow template, you can easily load a flow with the functionality you want.
* You can set the instance type for running the flow.

### Modify Flow

Modifies the flow's metadata.

* Modifies the existing flow name and description and reflects them in the flow metadata.
* Flow templates cannot be specified.
* You can modify the flow even while it's running.
* You can change the instance type for running the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Creates new metadata using an existing flow definition.

* Creates new metadata with `_copy` added to the existing flow name.
* Copies the flow logic from the existing flow as is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the flow's current save state is temporary save, the existing flow's last saved version is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a flow in stopped state.

* Each flow can only run one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is running by a scheduler, you cannot start the flow in the same way as a flow started by a user.

### More - Terminate Flow
* You can terminate flows that are preparing to run, running, or draining.
* Terminates without processing remaining events.

### More - Drain and Terminate Flow
* You can drain and then terminate a running flow.
* Draining means processing the flow's remaining events.
* If the timeout period is exceeded, it terminates even if draining is not finished.
* If draining finishes while timeout time remains, it terminates immediately.
* Flows that are draining can be terminated immediately through flow termination.