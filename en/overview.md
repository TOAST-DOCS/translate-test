<!-- machine_translated: true -->

<!-- pre-align:aligned sig=f2414300858d -->

{% set f = (build_flags | select("in", ["public","gov","ncgn","ninc","ngsc","ngovc","ngoic"]) | list | first) %}
{% set vpc_ov = '-gov' if 'gov' in build_flags else '' %}
{% set price_dom = {"public":"www.toast.com","gov":"gov.toast.com","ncgn":"www.gncloud.go.kr","ninc":"www.ninc.go.kr","ngsc":"www.ngsc.go.kr","ngovc":"www.ngovc.com","ngoic":"www.ngoic.com"} %}
<a id="compute-instance-overview"></a>

## Compute > Instance > Overview { #compute-instance-overview }

An instance is a virtual server composed of virtual CPUs, memory, and root block storage. You can install your services and applications on this server and use it in combination with the various services provided by NHN Cloud.

<a id="components"></a>

## Instance components { #components }

An instance consists of the following components:

- **Image**: A virtual disk that contains the instance's operating system
- **Flavor**: The virtual hardware performance of an instance
- **Availability zone** (AZ): The physical location where an instance is created
- **Key pair**: The key used to access an instance
- **Security group**: The network security configuration for an instance
- **Network**: The virtual network that the instance connects to

Instance properties and usage change depending on these components. While settings for these components, with the exception of image and availability zone, can be modified after the creation of an instance, some flavors cannot be modified after an instance has been created. For more details on modifying instance flavors, see [Modify Flavor in the Console Guide](./console-guide/#modify-flavor).

<a id="image"></a>
### Image { #image }

An image is a virtual disk that contains the operating system. NHN Cloud currently supports Debian, Ubuntu, Rocky, and Windows.

All images are configured to run optimally on an instance's virtual hardware and are safe to use as they have undergone security inspection by NHN Cloud. For more details on images, see [Image Overview](/Compute/Image/en/overview/).

<a id="flavor"></a>
### Instance flavor { #flavor }

NHN Cloud provides various instance flavors to support a wide range of use cases. Instances can be created with flavors that best match the requirements of your services or applications. Flavors can be easily modified from the web console, even after an instance has been created.

| Flavor    | Description                                                                                                                                               |
| ------- |--------------------------------------------------------------------------------------------------------------------------------------------------|
| m2 | A flavor with a balanced CPU-to-memory ratio. Use it when the performance requirements of your services or applications are unclear. |
| c2 | A flavor with high CPU performance. Use it for web application servers or analytics systems that require high-performance computations. |
| r2 | Use it when memory usage is significantly higher than that of other resources. Typically used for in-memory databases or cache servers. |
| t2 | A cost-effective flavor. Use it for servers with low workloads. |
| u2 | The most affordable flavor. Use it for servers with low workloads.<br>It uses local block storage, making it less stable but a more affordable option compared to other instances.<br>This flavor does not guarantee I/O performance. |
| x1 | A flavor that supports high-end CPUs and memory. Use it for services or applications that require high performance. |

<a id="availability-zone"></a>
### Availability zone { #availability-zone }

NHN Cloud has divided the entire system into multiple availability zones to prepare for potential failures caused by physical hardware issues. Each availability zone has its own storage system, network switch, data center space, and power supply units. A failure that occurs within one availability zone does not affect other zones, thereby increasing the availability of the whole service. You can ensure increased service availability by creating instances across multiple availability zones.

The following characteristics apply across different availability zones:

- Instances created across multiple availability zones can communicate over the network, and no network usage fees are charged for this communication.
- Block storage can be shared between instances in the same availability zone, but cannot be shared between different availability zones.
- Floating IP can be shared across different availability zones. If one availability zone experiences a failure, floating IP can quickly be relocated to another availability zone in order to minimize downtime.

<a id="key-pair"></a>
### Key pair { #key-pair }

A key pair is a pair of [PKI](https://ko.wikipedia.org/wiki/%EA%B3%B5%EA%B0%9C_%ED%82%A4_%EA%B8%B0%EB%B0%98_%EA%B5%AC%EC%A1%B0)-based public and private SSH keys. To access an instance created in NHN Cloud, a key pair is required instead of keyboard-inputted ID/PW authentication, which is vulnerable to security attacks. You can safely access an instance once you have been authenticated after sending the instance your login information, encoded by your key pair's private key. For more details on how to access instances using key pairs, see [How to Access Instances](#how-to-access-instances).

Key pairs can be newly generated from the NHN Cloud console during instance creation, or you can register your own existing key pairs. For more details on how to register key pairs, see [Import Key Pairs in the Console Guide](./console-guide/#import-key-pairs-windows).

> [Caution]
> When a key pair is newly generated, its private key is downloaded. As private keys are issued only once, be sure to store downloaded private keys in a safe disk or USB drive. If a private key is exposed, anyone can access the instance using the exposed private key, so it must be managed carefully.

> [Note]
> Key pairs are resources assigned to user accounts and are retained even when a project is deleted.

<a id="security-groups"></a>
### Security group { #security-groups }

A security group is a virtual firewall that controls the network traffic delivered to an instance. For more details on security groups, see [VPC Overview](/Network/VPC/en/overview$[ vpc_ov ]$/).

> [Note]
> The default security group is configured to ignore all inbound network traffic. Before accessing an instance using SSH, configure the instance's security group to allow access to the SSH port.

<a id="network"></a>
### Network { #network }

To communicate with the outside, an instance must be connected to at least one network defined in the VPC. An instance that is not connected to a network cannot be accessed. To create or modify a network, see [VPC Overview](/Network/VPC/en/overview$[ vpc_ov ]$/).

<a id="pricing"></a>

## Pricing { #pricing }

Instances are billed as follows:

* Billing starts the moment an instance is created.
* The root block storage of an instance is billed separately from the instance, based on block storage rates.
* When an instance is stopped, a 90% discount off the website rate is applied for 90 days. If the stopped status exceeds 90 days, the instance remains in stopped status and rates revert to normal rates.
* Terminated instances are not billed.

For more details on billing, see the [pricing page](https://$[ price_dom[f] ]$/kr/service/compute/instance#price) for each service.

<a id="how-to-access-instances"></a>

## How to access instances { #how-to-access-instances }

<a id="how-to-access-linux-instances"></a>
### How to access Linux instances { #how-to-access-linux-instances }

You can access your Linux instances using an SSH client. An instance cannot be accessed if its security group does not have SSH ports (22 by default) allowed. See [VPC Overview](/Network/VPC/en/overview$[ vpc_ov ]$/) for more details on how to allow SSH access. If a floating IP is not assigned to an instance, the instance cannot be accessed from outside NHN Cloud. See [VPC Overview](/Network/VPC/en/overview$[ vpc_ov ]$/) for more details on how to assign floating IP.

<a id="how-to-access-linux-instances-from-mac-or-linux-using-an-ssh-client"></a>
#### Access Linux instances from Mac or Linux using an SSH client

Generally, Mac and Linux have SSH clients installed by default. Use a key pair's private key to access an instance from an SSH client as shown below.

Ubuntu instance

	$ ssh -i my_private_key.pem ubuntu@<Instance IP>

Debian instance

	$ ssh -i my_private_key.pem debian@<Instance IP>

Rocky instance

	$ ssh -i my_private_key.pem rocky@<Instance IP>

<a id="how-to-access-linux-instances-from-windows-using-putty-ssh-client"></a>
#### Access Linux instances from Windows using the PuTTY SSH client

The PuTTY SSH client is a widely used SSH client program on Windows. Install [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) or the Korean-patched version [iPuTTY](https://github.com/iPuTTY/iPuTTY/releases/tag/l0.70i).

To access a Linux instance from Windows using the PuTTY SSH client, you must complete three steps.

* Convert the key pair's private key to a PuTTY-compatible private key
* Register the PuTTY-compatible private key in PuTTY
* Access the instance using PuTTY

##### 1. Convert the key pair's private key to a PuTTY-compatible private key

In PuTTY, you must convert the key pair's private key to PuTTY's private key format before using it. Use puttygen, which is installed along with PuTTY, to convert the key.

![Image 1](http://static.toastoven.net/prod_instance/putty001.png)

At the bottom of the **PuTTY Key Generator** window under **Parameters**, select **RSA** for the **Type of key to generate**, and enter the default value '2048' bits for the **Number of bits in a generated key**. Under **Actions**, click **Load** next to **Load an existing private key file** to import your key pair's private key file.

![Image 2](http://static.toastoven.net/prod_instance/putty002.png)

Under **Actions**, click **Save private key** next to **Save the generated key** to save the converted PuTTY-compatible key pair private key. If you leave the **Key passphrase** field empty and save the private key, a message appears asking **Are you sure you want to save this key without a passphrase to protect it?** To store the converted private key more securely, set a passphrase before saving.

> [Caution]
If you wish to be able to automatically log in to your instance, you should not set a key passphrase. When a passphrase is used, you must manually enter the private key's passphrase during login.

##### 2. Register the PuTTY-compatible private key in PuTTY

The PuTTY-compatible private key can be registered and used in two ways.

* Register a private key file for authentication in PuTTY
* Register a private key file for authentication in pageant (PuTTY authentication agent)

**A. Register a private key file for authentication in PuTTY**


Run PuTTY and select **Connection > SSH > Auth** from the **Category** on the left. Under **Authentication parameters** on the right, register your PuTTY-compatible private key in **Private key file for authentication**.

![Image 3](http://static.toastoven.net/prod_instance/putty005.png)

Once you register your private key, you do not have to re-register your private key file each time you access your instance if you save your access information. For details on how to save your access information, see the section below on accessing instances.


**B. Register a private key file for authentication in pageant (PuTTY authentication agent)**


When you run pageant, which is installed along with PuTTY, the icon shown below appears in the Windows tray. Right-click the pageant icon and select **Add Key** to add your PuTTY-compatible private key.

![Image 4](http://static.toastoven.net/prod_instance/putty006.png)

To confirm that the private key has been added, select **View Keys**. If the key was added successfully, the added key appears as shown below.

![Image 5](http://static.toastoven.net/prod_instance/putty008.png)

Once you run pageant, it remains running in the Windows tray, so there is no need for you to rerun it every time you access an instance. However, you must run pageant again when you restart Windows.

##### 3. Access the instance using PuTTY

If the converted PuTTY-compatible private key has been registered successfully, run PuTTY.

![Image 6](http://static.toastoven.net/prod_instance/putty009.png)

Use the following as the **Host Name** in the basic connection settings:

Ubuntu

	ubuntu@<Instance IP>

Debian

	debian@<Instance IP>

Rocky

	rocky@<Instance IP>

Set the **Port** to 22 (the default SSH port) and the **Connection type** to **SSH**.

If all of the information is correct, save the session. Under **Load, save or delete a stored session**, enter the name of the session to save in **Saved Sessions** and click **Save** to save the session. If you do not save the session, your private key settings registered in 2-A are also not preserved.

Now click **Open** to connect to the instance.

<a id="how-to-access-windows-instances"></a>
### How to access Windows instances { #how-to-access-windows-instances }

To access your Windows server, select a Windows instance to access from the NHN Cloud console. In the instance details page under the **Access Information** tab, click **Confirm Password** to check the password set in the Windows server.

The key pair's private key that you enter in **Confirm Password** is not transmitted to the server and is used only for decrypting the password in the browser.

Click **Connect** next to **Confirm Password** to download and run the .rdp file that contains the remote desktop connection settings, which will connect you to the Windows server. The ID for the Windows server is `Administrator`, and use the password that you confirmed in the NHN Cloud console.

{% if "public" in build_flags %}
<a id="how-to-connect-serial-console"></a>
### How to connect to the serial console { #how-to-connect-serial-console }

In situations where an SSH client cannot be used, such as boot failures or network configuration issues, you can connect to the serial console to access the instance.

The serial console feature has the following constraints:

* Only one serial console connection is allowed per instance. If multiple connections are attempted, the connection may not be established properly.
* Serial console access is not guaranteed for instances created from images uploaded by individuals or from private images.
* Serial console connections can remain active for up to 10 minutes.
* Windows instances do not support the serial console feature.
* Instances created before the January 27, 2026 deployment require **Stop Instance** followed by **Start Instance**. Applying the **Reboot Instance** feature does not work.

> [Caution]
> Changing the boot method by accessing the instance through the serial console may cause boot failures, and the user is responsible for any consequences.
> In normal circumstances, we recommend using the SSH client to access instances.

<a id="how-to-connect-serial-console-change-grub-bootloader-settings"></a>
#### Change GRUB bootloader settings

To manipulate the bootloader on instances created before the November 26, 2024 deployment, GRUB settings are required.

Modify the GRUB configuration file.

```
$ sudo vi /etc/default/grub.d/50-cloudimg-settings.cfg
GRUB_TIMEOUT=3
GRUB_TERMINAL="console serial"
GRUB_SERIAL_COMMAND="serial --speed=9600 --unit=0 --word=8 --parity=no --stop=1"
```

Apply the changed settings. The command to apply GRUB settings may vary depending on the operating system.

```
$ sudo update-grub
```
{% else %}
{% endif %}