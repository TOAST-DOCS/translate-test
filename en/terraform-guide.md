<a id="third-party-user-guide-terraform-user-guide"></a>
## Third Party User Guide > Terraform User Guide
This document describes how to use NHN Cloud with Terraform.

<a id="terraform"></a>
## Terraform
Terraform is an open source tool that makes it easy to build infrastructure, safely make changes, and efficiently manage infrastructure configuration. The main features of Terraform are as follows:

* **Infrastructure as Code**
    * Define infrastructure as code to increase productivity and transparency.
    * Easily share defined code for efficient collaboration.
* **Execution Plan**
    * Separate change planning from change application to reduce mistakes that can occur when applying changes.
* **Change Automation**
    * Automate building and changing infrastructure with the same configuration in multiple locations.
    * Save time building infrastructure and reduce errors.


#### Resources Support

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

#### Data Sources Support

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
### Important Information

* **The Terraform version used in the examples below is 1.0.0.**
* **Names and numbers of components including versions may change, so please verify before use.**


<a id="terraform-installation"></a>

## Terraform Installation
Download the appropriate file for your local PC's operating system from the [Terraform download page](https://www.terraform.io/downloads.html). Extract the file, place it in your desired path, and add that path to your environment settings to complete the installation.

The following is an installation example for Linux (Ubuntu/Debian).

```
$ wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
$ sudo apt update && sudo apt install terraform
$ terraform -v
Terraform v1.14.2
```

<a id="terraform-provider-provided"></a>

## Terraform Provider

NHN Cloud is an official partner of HashiCorp and provides Terraform providers through the [Terraform Registry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest).

Terraform runs by starting with the terraform binary file and calling desired targets in local environments or remote environments such as deployment servers. While these 'desired targets' have different calling methods, they interact by calling APIs provided by the target's supplier, namely the provider. The 'provider' is what enables terraform to interact with targets.



<a id="terraform-initialization"></a>

## Terraform Initialization
Before using Terraform, create a provider configuration file as follows.

The provider file name can be set arbitrarily. In this example, `provider.tf` is used.

For the provider version, refer to the `VERSION` information in the [NHN Cloud Terraform Registry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest).

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
    * Check the tenant ID by clicking the **API Endpoint Settings** button in the **Compute > Instance > Management** menu of the NHN Cloud console.
* **password**
    * Use the **API password** saved in the **API Endpoint Settings** dialog box.
    * For information on how to set up an API password, refer to **User Guide > Compute > Instance > Preparing to Use APIs**.
* **auth_url**
    * Specify the NHN Cloud identity service address.
    * Check the identity service URL by clicking the **API Endpoint Settings** button in the **Compute > Instance > Management** menu of the NHN Cloud console.
* **region**
    * Enter the region information for managing NHN Cloud resources.
    * **KR1**: Korea (Pangyo) region
    * **KR2**: Korea (Pyeongchon) region
    * **JP1**: Japan (Tokyo) region

Initialize Terraform using the `init` command in the path where the provider configuration file is located.

```
$ ls
provider.tf
$ terraform init
```



<a id="terraform-usage"></a>

## Terraform Basic Usage

Infrastructure construction using Terraform typically follows the lifecycle shown below.

1. Create tf files
2. Review construction plan
3. Create resources
4. Modify resources
5. Delete resources

First, write the infrastructure configuration to be built in tf files. You can review the construction plan based on the written tf files using the `plan` command as follows.

```
$ terraform plan
```

If there are no issues with the construction plan, use the `apply` command to create, modify, and delete resources.

```
$ terraform apply
```

The following sections explain these steps in more detail with examples.


<a id="create-tf-files"></a>
### Creating tf Files

Create tf files in the path where the provider configuration file is located. You can either group multiple resource configurations in a single tf file or create separate tf files for each resource. Terraform reads all written tf files at once to establish a construction plan.

Below is an example of a tf file that defines a resource for creating an instance in the `instance.tf` file.

```
$ ls
instance.tf provider.tf
$ cat instance.tf
resource "nhncloud_compute_instance_v2" "terraform-instance-01" {
  name      = "terraform-instance-01"
  region    = "KR1"
  flavor_id = "da74152c-0167-4ce9-b391-8a88a8ff2754"
  key_pair  = "terraform-keypair"
  network {
    uuid = "00d5b852-cb77-4307-b6be-d81dad24eec1"
  }
  security_groups = ["default"]
  block_device {
    uuid = "6d0993b4-cd6d-4242-b59b-94258f265331"
    source_type = "image"
    destination_type = "volume"
    boot_index = 0
    volume_size = 20
    delete_on_termination = true
  }
}
```

