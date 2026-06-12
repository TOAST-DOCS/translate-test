## Data & Analytics > DataFlow > Release Notes

<a id="may-27-2026"></a>

## May 27, 2026

<a id="feature-updates"></a>

### Feature Updates
* Added new nodes
    * Source
        * (NHN Cloud) EasyQueue
        * (NHN Cloud) Data Lake Storage
    * Sink
        * (NHN Cloud) EasyQueue
        * (NHN Cloud) Data Lake Storage

<a id="april-28-2026"></a>

## April 28, 2026
<a id="added-features"></a>

### Added Features
* Added a feature to define and use the schema of Source nodes in flow information.

<a id="feature-updates-2"></a>

### Feature Updates
* Added new nodes
    * Filter
        * Tokenizer
        * Sampling
        * Stop Words Remover
        * Pattern Extractor (Grok)
    * Branch
        * Dataset Split
* Added the **Schema** property to the JSON node.


<a id="march-24-2026"></a>

## March 24, 2026
<a id="feature-updates-3"></a>

### Feature Updates
* End of support for V1 engine type
    * Support for the V1 engine type has ended, and existing V1 engine type flows can no longer be executed.
    * All flows are created with the V2 engine type.
* Improved the recent log feature for the V2 engine type.
* Improved the monitoring feature for the V2 engine type.
* Added nodes supported by the V2 engine type.
    * Source
        * Kafka
    * Filter
        * Cipher
        * Remove Fields
    * Sink
        * Kafka
* Added the Parquet codec to the (Amazon) S3 and (NHN Cloud) Object Storage Sink nodes.

<a id="bug-fixes"></a>

### Bug Fixes
* Fixed an issue where the collapse button in the left tree structure of the monitoring screen did not work.

<a id="february-10-2026"></a>

## February 10, 2026
<a id="feature-updates-4"></a>

### Feature Updates
* End of support for Cipher node in V1 engine
    * Support for the Cipher node feature in the V1 engine type will be discontinued as of February 10, 2026.
    * If a Cipher node is included in an existing V1 engine type flow, the flow cannot be executed.
    * The Cipher node cannot be selected in flows newly created with the V1 engine type.

<a id="december-23-2025"></a>

## December 23, 2025

<a id="added-features-2"></a>

### Added Features
* Added engine type
    * V1: it is a legacy engine and is fully compatible with all standard nodes and existing templates.
    * V2: it provides faster performance than V1 with the latest architecture-based engine.

<a id="october-28-2025"></a>

## October 28, 2025

<a id="bug-fixes-2"></a>

### Bug Fixes
* Fixed an issue where CPU, Memory, and Network metrics in the Monitoring tab were only displayed for the most recently executed flow.
* Fixed an issue where saving a flow or template configured using a template containing sensitive information would fail.

<a id="september-23-2025"></a>

## September 23, 2025

<a id="feature-updates-5"></a>

### Feature Updates
* Made modification so that sensitive information is marked with asterisks when setting up nodes.
    * (NHN Cloud) Object Storage > Secret Key
    * (NHN Cloud) CloudTrail > Appkey
    * (NHN Cloud) Log & Crash Search > SecretKey
    * JDBC > Password
    * (Amazon) S3 > Secret Key
* (NHN Cloud) Added **Search Query** attribute to the Log & Crash Search node.

<a id="bug-fixes-3"></a>

### Bug Fixes
* Fixed an issue where charts would not be displayed when selecting a flow that had never been run in the Monitoring tab.

<a id="august-26-2025"></a>

## August 26, 2025

<a id="feature-updates-6"></a>

### Feature Updates
* Added a new **Schedule List** tab on the Details screen where you can check the reservation schedule.
* Moved the **Go to Cloud Scheduler Console** button for scheduling flows from the Basic Info tab to the **Schedule List** tab.

<a id="july-29-2025"></a>

## July 29, 2025

<a id="feature-updates-7"></a>

### Feature Updates
* Updated the execution mode to be configured at the flow.
* Renamed CloudTrail event names to match the terminology used in the DataFlow console.

<a id="bug-fixes-4"></a>

### Bug Fixes
* Fixed an issue where the flow did not terminate properly after draining.
* Fixed an issue where log retrieval requests were still made when the View Recent Logs window was open and the flow had ended.

<a id="june-24-2025"></a>

## June 24, 2025

<a id="feature-updates-8"></a>

### Feature Updates
* Replaced the scheduling functionality to integrate with the Cloud Scheduler service.
* Added an execution mode setting to the source node.
    * STREAMING: Processes data in real time without exiting the flow.
    * BATCH: Processes a set amount of data and then terminates the flow.

<a id="may-27-2025"></a>

## May 27, 2025

<a id="feature-updates-9"></a>

### Feature Updates
* Added new nodes
    * Filter
        * Mutate: A node that can rename fields or transform field values.
    * Sink
        * Stdout: A node that outputs flow events to the log. It can be used for debugging purposes.

<a id="bug-fixes-5"></a>

### Bug Fixes
* Fixed an issue where View Logs feature did not function properly when logs accumulated too quickly.

<a id="march-4-2025"></a>

## March 4, 2025

<a id="bug-fixes-6"></a>

### Bug Fixes
* Fixed an issue where flow event in/out graphs are not displayed correctly.

<a id="december-24-2024"></a>

## December 24, 2024

<a id="feature-updates-10"></a>

### Feature Updates
* Integrated (Amazon) S3 Sink node and (Amazon) S3 - Parquet Sink node.
* Integrated (NHN Cloud) Object Storage Sink node and (NHN Cloud) Object Storage - Parquet Sink node.

<a id="september-25-2024"></a>

## September 25, 2024

<a id="feature-updates-11"></a>

### Feature Updates
* Stabilized the flow startup process.
  
<a id="august-27-2024"></a>

## August 27, 2024

<a id="feature-updates-12"></a>

### Feature Updates
* Improved how the Last Executed Time is calculated. 
* Made modifications so that, when displaying the node settings, required items are displayed first.

<a id="july-23-2024"></a>

## July 23, 2024

<a id="feature-updates-13"></a>

### Feature Updates
* Improved to use the enter key to input data when entering data in the `array of strings` type in the node settings screen.
* Separated the **Match** setting for the Date node into a **Source Field** setting and a **Formats** setting.
* Made notifications so that, when starting or ending a flow that has already started or ended, `FLOW_ALREADY_STARTED`/`FLOW_ALREADY_STOPPED` instead of `ERROR` appears.
* Made notifications so that, when saving or deleting Log & Crash Search log save settings, "Save Log & Crash Search save settings" or "Delete Log & Crash Search save settings" are left in CloudTrail logs.

<a id="july-1-2024"></a>

## July 1, 2024

<a id="feature-updates-14"></a>

### Feature Updates
* Added the feature to set the instance type when running flows 
* (Amazon) Changed the endpoint, region settings for the (Amazon) S3 Source, Sink, and (Amazon) S3 - Parquet Sink nodes from required to optional 
    * The nodes will work correctly if only one of the endpoint, region settings is entered.

<a id="bug-fixes-7"></a>

### Bug Fixes
* Fixed an issue where no CloudTrail logs were left when exiting after flow draining, Log & Crash Search logs save settings, enabling and disabling validation.
* Fixed an issue where the scheduling feature was not working intermittently. 
* Fixed an issue where the Cipher node was not working intermittently. 
* Fixed an issue where the (Amazon) S3 Source, Sink, and (Amazon) S3 - Parquet Sink nodes were not able to access the public bucket.
* Fixed an issue where using an unsupported JDBC driver when saving a flow containing a JDBC node with validation disabled would expose `JDBC_UNSUPPORTED_DRIVER` instead of `ERROR`. 
* Fixed an issue where saving a flow containing a Cipher node with validation enabled would expose the appropriate error code instead of `ERROR` if the Cipher node information was entered incorrectly. 
* Fixed an issue where status channge notifications were not sent for flows run by a user who had canceled membership.

<a id="may-28-2024"></a>

## May 28, 2024

<a id="feature-updates-15"></a>

### Feature Updates
* Deleted some settings.
    * Common > Enable Metrics
    * Filter Node Common > Periodic Flush
    * (NHN Cloud) Object Storage > ACL
    * (NHN Cloud) Object Storage > Storage Class
    * (NHN Cloud) Object Storage - Parquet > ACL
    * (NHN Cloud) Object Storage - Parquet > Storage Class
* Made modifications so that, when monitoring for periods longer than 7 days, data would be more precise.

<a id="bug-fixes-8"></a>

### Bug Fixes
* Fixed the revision history of unsubscribed users to appear as "UNKNOWN USER" instead of blank.
* Fixed validation of Object Storage, S3 nodes to expose "S3_NO_SUCH_BUCKET" instead of "ERROR" if an invalid bucket name is entered.
* Fixed an issue where node names were different on the flow setup screen and the monitoring screen.
* Fixed an issue where state change notifications were not being sent for flows run via scheduling.

<a id="april-23-2024"></a>

## April 23, 2024

<a id="added-features-3"></a>

### Added Features
* Added the flow status change notifications feature.

<a id="bug-fixes-9"></a>

### Bug Fixes
* Fixed an issue where, when querying flow monitoring with many nodes, the query fails.

<a id="march-26-2024"></a>

## March 26, 2024

<a id="added-features-4"></a>

### Added Features
* Added the feature to end after flow draining
    * Added the feature to end a flow after draining that processes all remaining events in the flow.
    * A flow that is draining can be ended directly via End Flow.
    * If the draining ends within the timeout, or if the timeout is exceeded during draining, the flow will end at that point.

<a id="february-27-2024"></a>

## February 27, 2024

<a id="feature-updates-16"></a>

### Feature Updates
* Changed the words "file" and "object" in the descriptions of S3 and Object Storage nodes to "object".
* Fixed loading UI to appear on flow save, start, stop, and validation requests.
* Made the order of node setup more natural.

<a id="bug-fixes-10"></a>

### Bug Fixes
* Fixed an issue where saving flows with S3, Object Storage Sink nodes would intermittently leave temporary objects for testing during validation.
* Fixed an issue where deleting a flow would not delete the scheduling stored in that flow.
* Fixed an issue where, when creating a flow immediately after activating a project, the flow would fail to run.
* Fixed an issue where, when looking up monitoring for a long period of time, the lookup would fail.
* Fixed an issue where the execution state of a validation feature would go from `Activating` to `Active` faster than it should.

<a id="january-23-2024"></a>

## January 23, 2024

<a id="feature-updates-17"></a>

### Feature Updates
* Fixed a bug where validation would not turn on unless creating the first flow.

<a id="december-19-2023"></a>

## December 19, 2023

<a id="added-features-5"></a>

### Added Features
* Added a new node
    * Source
        * Added the feature to run queries against the DB to get data.
    * Sink
        * Added the feature to store data in Object Storage with the Parquet type.
        * Added the feature to store data in S3 with the Parquet type.

<a id="bug-fixes-11"></a>

### Bug Fixes
* Fixed a bug where validation would not turn on properly after creating a flow.

<a id="november-28-2023"></a>

## November 28, 2023

<a id="feature-updates-18"></a>

### Feature Updates
* Added error codes when saving or validating flows.
* Changed to allow you to choose whether or not to use the validation feature.

<a id="october-31-2023"></a>

## October 31, 2023

<a id="feature-updates-19"></a>

### Feature Updates
* Improved the error messages that occur while initializing the DataFlow service environment to be more user-friendly.

<a id="october-17-2023"></a>

## October 17, 2023

<a id="feature-updates-20"></a>

### Feature Updates
* Added the SecretKey property to Log & Crash Search Source nodes.

<a id="september-26-2023"></a>

## September 26, 2023

<a id="feature-updates-21"></a>

### Feature Updates
* Modified to support At Least Once when processing data.
* Added new options for time format in Prefix Settings for S3 and Object Storage Sink nodes.

<a id="bug-fixes-12"></a>

### Bug Fixes
* Fixed a bug where the flow would not terminate if an error occurred during the shutdown of the Log & Crash Search node.
* Fixed a bug where, when copying and running a flow containing a Cipher Filter node, the flow would not work correctly.
* Fixed a bug where, when an error occurred while terminating a flow, a request to terminate again would fail.

<a id="july-25-2023"></a>

## July 25, 2023

<a id="bug-fixes-13"></a>

### Bug Fixes

* Modified so that, when a flow fails abnormally during execution, it can resume execution from the last execution point.

<a id="june-27-2023"></a>

## June 27, 2023

<a id="feature-updates-22"></a>

### Feature Updates
* Added a feature to enable Log & Crash Search
    * Added a feature to save flow logs in Log & Crash Search.

<a id="bug-fixes-14"></a>

### Bug Fixes
* Modified the activation timing of the View Log button
    * Modified the activation timing of the View Log button to the PREPARING stage.

<a id="march-28-2023"></a>

## March 28, 2023

<a id="feature-updates-23"></a>

### Feature Updates

* Added new nodes
    * Filter
        * Added various data processing methods such as Alter, Date, UUID, Split, and Truncate.
* Added a flow usage exposure feature
    * Added a feature to check flow usage from the console in real time.

<a id="bug-fixes-15"></a>

### Bug Fixes

* Fixed a bug where flow usage begins to appear before entering the PREPARING stage.

<a id="february-28-2023"></a>

## February 28, 2023

<a id="feature-updates-24"></a>

### Feature Updates

* Added new nodes
    * Source
        * Added a feature to import data from NHN Cloud Object Storage node.
        * Added a feature to import data through Amazon S3 interface.
        * Added a feature to import data through Apache Kafka.
    * Filter
        * Added a feature to preprocess data in various ways by adding Grok, JSON, and CSV nodes.

<a id="january-6-2023"></a>

## January 6, 2023

<a id="bug-fixes-16"></a>

### Bug Fixes

* Fixed an issue where the first button click after adding a node in the flow edit screen does not work.
* Fixed an issue where a field is not added when the cipher node is configured to add fields.

<a id="december-27-2022"></a>

## December 27, 2022

<a id="release-of-a-new-service"></a>

### Release of a New Service

* DataFlow is a service that creates and run ETL flows.
* Supports sources listed below.
    * NHN Cloud Log & Crash Search
    * NHN Cloud CloudTrail
* Supports a filter below.
    * Cipher (Required to connect with NHN Cloud Secure Key Manager)
* Supports sinks below.
    * NHN Cloud Object Storage
    * Amazon S3 (Compatible)
    * Apache Kafka
