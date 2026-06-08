<a id="third-party-user-guide-terraform-user-guide"></a>
## Third Party User Guide > Terraform User Guide
This document describes how to use NHN Cloud with Terraform.

<a id="terraform"></a>
## Terraform
Terraform is an open-source tool that allows you to build infrastructure easily, change it safely, and efficiently manage the infrastructure configuration. The key features of Terraform are as follows:

* **Infrastructure as Code**
    * You can increase productivity and transparency by defining infrastructure as code.
    * You can easily share the defined code for efficient collaboration.
* **Execution Plan**
    * You can reduce mistakes when applying changes by separating change planning and change application.
* **Change Automation**
    * You can automate building and changing infrastructure with the same configuration in multiple locations.
    * You can save time building infrastructure and reduce mistakes.


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
### Note

* **The Terraform version used in the examples below is 1.0.0.**
* **The names and numbers of components including versions may change, so check before use.**


<a id="terraform-installation"></a>

## Install Terraform
Download the file for your local PC's operating system from the [Terraform download page](https://www.terraform.io/downloads.html). Extract the file, place it in your desired path, and add that path to your environment settings to complete the installation.

The following shows a Linux (Ubuntu/Debian) installation example.

```
$ wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
$ sudo apt update && sudo apt install terraform
$ terraform -v
Terraform v1.14.2
```

<a id="terraform-provider-provided"></a>

## Terraform provider

NHN Cloud is an official partner of HashiCorp and provides a Terraform provider through the [Terraform Registry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest).

Terraform runs by starting with the terraform binary file and invoking the desired target in either a local environment or a remote environment such as a deployment server. The 'desired target' has different invocation methods, but interacts by calling APIs provided by the target's supplier, that is, the provider. Here, what enables Terraform to interact with targets is the 'provider'.



<a id="terraform-initialization"></a>

## Terraform Initialization
Before using Terraform, create a provider configuration file as follows.

You can set the provider file name arbitrarily. This example uses `provider.tf`.

Refer to the `VERSION` information in [NHN Cloud Terraform Registry](https://registry.terraform.io/providers/nhn-cloud/nhncloud/latest) to create the provider version.

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
    * In the NHN Cloud console, go to **Compute > Instance > Management** and click the **API Endpoint Settings** button to check the tenant ID.
* **password**
    * Use the **API password** saved in the **API Endpoint Settings** dialog box.
    * For information about setting up an API password, see **User Guide > Compute > Instance > API Preparation**.
* **auth_url**
    * Specify the NHN Cloud identity service address.
    * In the NHN Cloud console, go to **Compute > Instance > Management** and click the **API Endpoint Settings** button to check the identity service URL.
* **region**
    * Enter the region information for managing NHN Cloud resources.
    * **KR1**: Korea (Pangyo) region
    * **KR2**: Korea (Pyeongchon) region
    * **JP1**: Japan (Tokyo) region

Initialize Terraform by using the `init` command in the path where the provider configuration file is located.

```
$ ls
provider.tf
$ terraform init
```



<a id="terraform-usage">

## Basic Terraform Usage

Infrastructure construction using Terraform typically has the following lifecycle:

1. Write tf files
2. Verify the construction plan
3. Create resources
4. Modify resources
5. Delete resources

First, write the infrastructure configuration to be built in tf files. You can verify the construction plan according to the written tf files by using the `plan` command as follows:

```
$ terraform plan
```

If there are no issues with the construction plan, use the `apply` command to create, modify, and delete resources.

```
$ terraform apply
```

The following sections explain these steps in more detail with examples.


<a id="create-tf-files"></a>
### Write tf files

Write tf files in the path where the provider configuration file is located. You can collect multiple resource configurations in one tf file, or write separate tf files for each resource. Terraform reads all the written tf files at once and establishes a construction plan.

The following is an example tf file that defines a resource for creating an instance in the `instance.tf` file:

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

