## Data & Analytics > DataFlow > Console User Guide

You can use DataFlow in the following order:

* Enable the Service
    1. Create a project.
    2. Select the project that you want.
    3. Enable the DataFlow service.
* Run a Flow
    1. Create a flow.
    2. Add the required nodes and enter the settings to define how each node operates.
    3. Connect the nodes to determine the order of operations and complete the flow.
    4. Run the flow.
    5. Check the log information to verify that the flow ran properly.

## Management

Page that queries and manages the flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows by the given criteria.

* When you search by flow name, flows whose name contains the search term are returned.

### Filter

Filters flows by the given conditions.

* Provides filtering options based on flow status.

### Flow List

Displays the queried flows in a table.

* Displays basic flow metadata and the current flow execution status.
* Sorts flows by the most recent modification date.
* You can select a flow to use management features such as changing flows, viewing flow details, and starting flow.
* You can use the filter condition feature to view only flows with a specific status.
* Once queried, you must click **Refresh** to update the query results.
* You can view 12 flows per page and navigate through the **Previous** and **Next** buttons.

#### Flow Status Information

| Flow Execution Status | Description |
|---| --- |
| START\_FAILED  | Failed to start the flow. |
| QUOTA\_EXCEEDED | The flow failed to start due to insufficient resources. |
| STARTING       | Securing resources to run the flow. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> continues to occur, contact **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to stop the flow. |
| STOPPED        | The flow has stopped. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred for unknown reasons during flow execution. If <b>UNKNOWN</b> continues to occur, contact **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive a notification email when the flow status changes to a monitored status.
* Monitored flow statuses:
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients:
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is enabled


### Create a Flow

Creates metadata to define a flow.

* Add a name and description to identify the flow and create the flow metadata.
* Flow names can be the same as those of other flows.
* Select the execution mode that matches the purpose of the flow.
* You can specify a flow template to easily load a flow with the features that you want.
* You can set the instance type for running the flow.

### Modify a Flow

Modifies the flow metadata.

* Edit the existing flow name and description to reflect the changes in the flow metadata.
* You cannot specify a flow template.
* You can modify the flow while it is running.
* You can change the instance type for running the flow.
    * The changed instance type will be applied from the next flow execution.

### Copy a Flow

Creates new metadata using the definition of an existing flow.

* Creates new metadata with `_copy` appended to the name of the existing flow.
* Copies the flow logic of the existing flow.
* You can also copy a flow that is currently running.
* A running flow is copied in a stopped state.
* If the current storage state of flows is temporary, it does not copy the last saved version of existing flows.
* Even if you copy a flow that has a scheduler registered, the copied flow does not have a scheduler registered.
* The copied flow is completely independent from the original flow.

### Delete a Flow

Deletes the flow metadata.

* Permanently deletes the flow metadata.
* Deleted flows cannot be recovered.
* You cannot delete a flow that is currently running.

### More - Start a Flow
Starts a stopped flow.

* Only one instance of each flow can run at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that has only been temporarily saved and never fully saved cannot be started.
* A flow must be saved at least once before it can be started.
* A flow cannot be started the same as the flow initiated by the user, even if the flow is already being run by Scheduler.

### More - Stop a Flow
* You can stop a flow that is preparing to run, running, or draining.
* Stops without processing remaining events.

### More - Stop a Flow After Draining
* You can drain and then stop a running flow.
* Draining means processing the remaining events in the flow.
* If the timeout period is exceeded, the flow stops even if draining is not complete.
* If draining completes before the timeout period expires, the flow stops immediately.
* A draining flow can be stopped immediately by using the Stop a Flow feature.