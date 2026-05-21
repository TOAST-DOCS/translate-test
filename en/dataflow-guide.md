## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence.

* Enable Service
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Run Flow
    1. Create a flow.
    2. Add the required nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the order of node operations through node connections.
    4. Run the flow.
    5. Check the log information to verify that the flow executed successfully.

## Management

This page displays and manages flow metadata information.
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

* Shows simple flow metadata and current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management functions such as flow modification, flow details view, and flow start.
* You can view only flows with a specific status using the filter condition feature.
* Once flows are retrieved, you must click **Refresh** to update the results.
* Up to 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Flow execution request failed. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Acquiring resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> continues to occur, contact us via **Customer Support > Contact Us**. |
| STOP\_FAILED   | Flow termination request failed. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> continues to occur, contact us via **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow changes to a target notification status.
* Target notification flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is active

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated across different flows.
* Select the execution mode according to the purpose of the flow.
* Specify a flow template to easily load a flow with the desired functionality.
* You can configure the instance type for executing the flow.

### Modify Flow

Modify the metadata of a flow.

* Modify the existing flow name and description to reflect changes in the flow metadata.
* Flow templates cannot be specified.
* You can modify flows even while they are running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied starting from the next flow execution.

### Copy Flow

Create new metadata based on an existing flow definition.

* Create new metadata with `_copy` appended to the existing flow's name.
* Copy the flow logic from the existing flow.
* You can copy flows that are running.
* Running flows are copied in a stopped state.
* If the current save state of a flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have a registered scheduler.
* A copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can only run one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without being saved at least once cannot be started.
* Flows must be saved at least once before they can be started.
* Even if a flow is running due to a scheduler, it cannot be started in the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing to run, are running, or are draining.
* Remaining events are not processed and the flow is terminated.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing the remaining events in the flow.
* If the timeout is exceeded, the flow is stopped even if draining is not complete.
* If draining completes while timeout remains, the flow stops immediately.
* A draining flow can be stopped immediately via flow stop.