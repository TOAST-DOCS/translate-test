<!-- pre-align:aligned sig=f045bb32393b -->

## Container > NHN Container Service(NCS) > Release Notes
<a id="october-28-2025"></a>

### October 28, 2025
<a id="added-features"></a>

#### Added Features
* Added the feature to perform malware scans for container images used on workloads.

<a id="march-4-2025"></a>

### March 4, 2025
<a id="added-features-2"></a>

#### Added Features
* Added an internal request response latency item when creating workloads. The Internal Request Response Latency setting allows you to enforce a timeout on communication requests to the internal load balancer VIP from other workloads.

<a id="november-26-2024"></a>

### November 26, 2024
<a id="added-features-3"></a>

#### Added Features
* Added web terminal feature to access containers.
* Added workload autoscaling feature.
* Added the feature to restart per workload task.
* The Public API for NCS has been released.
    * For information about the Public API, see the [API Guide](/Container/NCS/en/public-api/).
  
<a id="august-27-2024"></a>

### August 27, 2024
<a id="added-features-4"></a>

#### Added Features
* You can check the events occurred in the NCS from Resource Watcher.

<a id="may-28-2024"></a>

### May 28, 2024
<a id="added-features-5"></a>

#### Added Features
* You can set a scheduled termination time for your workloads.
* Added a feature to manage template versions.
* Added initialization container feature.
* Increased the event lookup period to 30 days.
* You can set HostAliases.

<a id="february-27-2024"></a>

### February 27, 2024
<a id="added-features-6"></a>

#### Added Features
* Added the feature to set container arguments (Args).
* Added the feature to select a workload deployment controller.
* Added the internal load balancer feature.
* Added the feature to integrate with Private DNS for workloads.

<a id="feature-updates"></a>

#### Feature Updates
* Temporary shared storage is provided between containers.

<a id="november-28-2023"></a>

### November 28, 2023
<a id="added-features-7"></a>

#### Added Features
* Added container settings features.
    * DNS server address settings
    * Health check settings (LivenessProbe, StartupProbe)
    * Lifecycle hook settings (Lifecycle Hook)
    * File settings (ConfigMap)
    * Confidential data settings (Secret)
    * NAS container connection path settings
* Added the feature to monitor GPUs and ephemeral storage.
* You can select a security group when creating a workload.
* Events occurred in a user cluster can be checked in NCS.

<a id="feature-updates-2"></a>

#### Feature Updates
* Load Balancer is provided.
    * Load Balancer Instance is no longer supported.
* Added HTTPS, TERMINATED_HTTPS protocols to container ports.
* Improved the Log tab.
* Improved the Events tab to show detailed reasons for the current and last status of containers.

<a id="august-29-2023"></a>

### August 29, 2023
<a id="added-features-8"></a>

#### Added Features
* Added a feature to schedule workloads.
* Added a feature to stop/restart workloads.

<a id="feature-updates-3"></a>

#### Feature Updates
* Improved to identify the cause of NAS storage connection failures on the Event tab.

<a id="july-25-2023"></a>

### July 25, 2023
<a id="feature-updates-4"></a>

#### Feature Updates
* Raised the maximum resource size for containers.

<a id="may-30-2023"></a>

### May 30, 2023
<a id="feature-updates-5"></a>

#### Feature Updates
* Added a feature to select the GPU type.
* Added HTTP protocols for container ports.
* Added the Quota feature.

<a id="march-28-2023"></a>

### March 28, 2023

<a id="feature-updates-6"></a>

#### Feature Updates
* Enhanced service reliability by improving the internal structure.

<a id="february-28-2023"></a>

### February 28, 2023

<a id="added-features-9"></a>

#### Added Features
* Added a feature to subdivide permissions
* Added a feature to change workloads

<a id="january-31-2023"></a>

### January 31, 2023

<a id="added-features-10"></a>

#### Added Features
* Added monitoring feature.

<a id="december-27-2022"></a>

### December 27, 2022

<a id="release-of-a-new-service"></a>

#### Release of a New Service
* You can create and manage containers in the console.
