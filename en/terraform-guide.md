<a id="third-party-user-guide-terraform-user-guide"></a>
## Third-party User Guide > Terraform User Guide
This document describes how to use NHN Cloud with Terraform.

<a id="terraform"></a>
## Terraform
Terraform is an open source tool that makes it easy to build infrastructure, change it safely, and manage infrastructure configuration efficiently. The main features of Terraform are as follows.

* **Infrastructure as Code**
    * You can increase productivity and transparency by defining infrastructure as code.
    * You can easily share the defined code for efficient collaboration.
* **Execution Plan**
    * You can reduce mistakes that may occur when applying changes by separating change planning from change application.
* **Resource Graph**
    * You can preview how minor changes will impact the entire infrastructure.
    * You can create a dependency graph, make plans based on this graph, and verify the changed infrastructure state when the plan is applied.
* **Change Automation**
    * You can automate building and changing infrastructure with the same configuration in multiple locations.
    * You can save time spent building infrastructure and reduce mistakes.


#### Supported Resources

* Compute
    * nhncloud_compute_instance_v2
    * nhncloud_compute_volume_attach_v2
    * nhncloud_compute_keypair_v2
* Network
    * nhncloud_lb_loadbalancer_v2
    * nhncloud_lb_listener_v2
    * nhncloud_lb_pool_v2
    * nhncloud_lb_member_v2
    * nhncloud_lb_monitor_v2
    * nhncloud_networking_floatingip_v2
    * nhncloud_networking_floatingip_associate_v2
    * nhncloud_networking_port_v2
    * nhncloud_networking_vpc_v2
    * nhncloud_networking_vpcsubnet_v2
    * nhncloud_networking_routingtable_v2
    * nhncloud_networking_routingtable_attach_gateway_v2
    * nhncloud_networking_secgroup_v2
    * nhncloud_networking_secgroup_rule_v2
    * nhncloud_keymanager_secret_v1
    * nhncloud_keymanager_container_v1
* Block Storage
    * nhncloud_blockstorage_volume_v2
* Object Storage
    * nhncloud_objectstorage_container_v1
    * nhncloud_objectstorage_object_v1
* Container
    * nhncloud_kubernetes_cluster_v1
    * nhncloud_kubernetes_nodegroup_v1
    * nhncloud_kubernetes_cluster_resize_v1
    * nhncloud_kubernetes_nodegroup_upgrade_v1

#### Supported Data Sources

* nhncloud_images_image_v2
* nhncloud_blockstorage_volume_v2
* nhncloud_compute_flavor_v2
* nhncloud_compute_keypair_v2
* nhncloud_blockstorage_snapshot_v2
* nhncloud_networking_vpc_v2
* nhncloud_networking_vpcsubnet_v2
* nhncloud_networking_routingtable_v2
* nhncloud_networking_secgroup_v2
* nhncloud_keymanager_secret_v1
* nhncloud_keymanager_container_v1
* nhncloud_kubernetes_cluster_v1
* nhncloud_kubernetes_nodegroup_v1


<a id="note"></a>
### Notes

* **The Terraform version used in the examples below is 1.0.0.**
* **Component names and numbers, including versions, may change. Please verify before using.**


<a id="terraform-installation"></a>
## Terraform Installation
Download the file that matches your local PC's operating system from the [Terraform Download page](https://www.terraform.io/downloads.html). Extract the file, place it in your desired path, and add that path to your environment settings to complete the installation.

The following is an installation example for Linux (Ubuntu/Debian).

```
$ wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
$ sudo apt update && sudo apt install terraform
$ terraform -v
Terraform v1.14.2
```


<a id="terraform-initialization"></a>
## Terraform Initialization
Before using Terraform, create a provider configuration file as follows.

The provider file name can be set arbitrarily. In this example, we use `provider.tf`.

The provider version should be written by referring to the `VERSION` information in the [NHN Cloud Terraform Registry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest).

```
# Define required providers
terraform {
  required_providers {
    nhncloud = {
      source = "nhn-cloud/nhncloud"
      version = "{VERSION}"
    }
  }
}

# Configure the nhncloud Provider
provider "nhncloud" {
  user_name   = "terraform-guide@nhncloud.com"
  tenant_id   = "aaa4c0a12fd84edeb68965d320d17129"
  password    = "difficultpassword"
  auth_url    = "https://api-identity-infrastructure.nhncloudservice.com/v2.0"
  region      = "KR1"
}
```

* **user_name**
    * Use your NHN Cloud ID.
* **tenant_id**
    * Click the **API Endpoint Settings** button in the **Compute > Instance > Manage** menu of the NHN Cloud console to check the tenant ID.
* **password**
    * Use the **API Password** saved in the **API Endpoint Settings** dialog.
    * Refer to **User Guide > Compute > Instance > Preparing for API Usage** for how to set the API password.
* **auth_url**
    * Specify the NHN Cloud identity service address.
    * Click the **API Endpoint Settings** button in the **Compute > Instance > Manage** menu of the NHN Cloud console to check the identity service URL.
* **region**
    * Enter the region information to manage NHN Cloud resources.
    * **KR1**: Korea (Pangyo) region
    * **KR2**: Korea (Pyeongchon) region
    * **JP1**: Japan (Tokyo) region

Initialize Terraform by using the `init` command in the path where the provider configuration file is located.

```
$ ls
provider.tf
$ terraform init
```