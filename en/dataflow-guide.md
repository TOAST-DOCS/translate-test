## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence.

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define the behavior of each node.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Execute the flow.
    5. Check the log information to verify that the flow executed normally.

## Management

This is a page where you can view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/TOAST-DOCS/translate-test/en/management_main_2025_06.png)

### Search

Search for flows based on the given criteria.

* When searching by flow name, flows that include the search term in their name are searched.

### Filter

Search for flows based on the given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays search results as a table of flows.

* Displays simple flow metadata and current flow execution status.
* Sorts by the most recent modification date.
* You can select a flow and use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status using the filter condition feature.
* Once a flow is retrieved, you must press **Refresh** to update the search results.
* 12 flows are retrieved per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure, etc. If <b>ERROR</b> continues to occur, contact us via **Customer Support > Inquiry**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> continues to occur, contact us via **Customer Support > Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to the notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is activated

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow purpose.
* You can specify a flow template to easily load flows with the desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the flow metadata.

* Modify the existing flow name and description and reflect them in the flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution onwards.

### Copy Flow

Create new metadata using the existing flow definition.

* Create new metadata with `_copy` added to the name of the existing flow.
* Copy the flow logic that the existing flow has as-is.
* You can copy flows that are running.
* Running flows are copied in a stopped state.
* If the flow's current save state is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a scheduler registered, the copied flow will not have the scheduler registered.
* A copied flow is completely separate from the existing flow.

### Delete Flow

Delete the flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can only run one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without being saved at least once cannot be started.
* Flows must be saved at least once before they can be started.
* Even if a flow is running by a scheduler, a flow started by a user cannot be started in the same way.

### More - Stop Flow
* You can stop flows that are preparing to run, running, or draining.
* Remaining events are not processed and the flow is terminated.

### More - Stop Flow After Draining
* You can stop a running flow after draining it.
* Draining means processing remaining events in the flow.
* If the timeout is exceeded, the flow terminates even if draining is not complete.
* If draining completes before the timeout expires, the flow terminates immediately.
* Flows in the draining state can be terminated immediately through flow stop.