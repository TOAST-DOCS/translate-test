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

The components that make up an instance are as follows:

- **Image**: A virtual disk that contains the instance's operating system
- **Flavor**: The virtual hardware performance of an instance
- **Availability zone** (AZ): The physical location where an instance is created
- **Key pair**: A key used to access an instance
- **Security group**: Network security settings for an instance
- **Network**: The virtual network to which an instance is connected

Instance properties and usage change depending on these components. While settings for these components, with the exception of image and availability zone, can be modified after the creation of an instance, some flavors cannot be modified after an instance has been created. For more details on modifying instance flavors, see [Modify Flavor in the Console Guide](./console-guide/#modify-flavor).

<a id="image"></a>
### Image { #image }

An image is a virtual disk that contains the operating system. NHN Cloud currently supports Debian, Ubuntu, Rocky, and Windows.

All images are configured to run optimally on an instance's virtual hardware and are safe to use as they have undergone security inspection by NHN Cloud. For more details on images, see [Image Overview](/Compute/Image/en/overview/).

<a id="flavor"></a>
### Instance flavor { #flavor }

NHN Cloud provides various instance flavors to support a wide range of use cases. Instances can be created with flavors that best match the requirements of your services or applications. Flavors can be easily modified from the web console, even after an instance has been created.

| Flavor  | Description                                                                                                                                                                                                                                                    |
| ------- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| m2 | A flavor with a balanced configuration of CPU and memory. Use this flavor when the performance requirements of your service or application are not clearly defined.                                                                                             |
| c2 | An instance flavor with a high-performance CPU configuration. Use this flavor for web application servers or analysis systems that require high-performance computations.                                                                                       |
| r2 | Use this flavor when memory usage is high relative to other resources. Typically used for in-memory databases or cache servers.                                                                                                                                  |
| t2 | A cost-effective instance flavor. Use this flavor for servers with low workloads.                                                                                                                                                                               |
| u2 | The most cost-effective instance flavor. Use this flavor for servers with low workloads.<br>Because it uses local block storage, it is less stable but a more affordable option than other instance types.<br>I/O performance is not guaranteed for this flavor. |
| x1 | A flavor that supports high-end CPU and memory. Use this flavor for services or applications that require high performance.                                                                                                                                      |

<a id="availability-zone"></a>
### Availability zone { #availability-zone }

NHN Cloud has divided the entire system into multiple availability zones to prepare for potential failures caused by physical hardware issues. Each availability zone has its own storage system, network switch, data center space, and power supply units. A failure that occurs within one availability zone does not affect other zones, thereby increasing the availability of the whole service. You can ensure increased service availability by creating instances across multiple availability zones.

The following characteristics exist between different availability zones:

- Instances created across multiple availability zones can communicate with each other over the network, and no network usage fees are charged for this communication.
- Block storage can be shared between instances in the same availability zone, but cannot be shared between instances in different availability zones.
- Floating IP can be shared across different availability zones. If one availability zone experiences a failure, floating IP can quickly be relocated to another availability zone in order to minimize downtime.

<a id="key-pair"></a>
### Key pair { #key-pair }

A key pair is a pair of [PKI](https://ko.wikipedia.org/wiki/%EA%B3%B5%EA%B0%9C_%ED%82%A4_%EA%B8%B0%EB%B0%98_%EA%B5%AC%EC%A1%B0)-based public and private SSH keys. To access an instance created in NHN Cloud, a key pair is required instead of keyboard-inputted ID/PW authentication, which is vulnerable to security attacks. You can safely access an instance once you have been authenticated after sending the instance your login information, encoded by your key pair's private key. For more details on how to access instances using key pairs, see [How to Access Instances](#how-to-access-instances).

Key pairs can be newly generated from the NHN Cloud Console during instance creation, or you can register your own existing key pairs. For more details on how to register key pairs, see [Import Key Pairs in the Console Guide](./console-guide/#import-key-pairs-windows).

> [Caution]
> When a key pair is newly generated, its private key is downloaded. As private keys are issued only once, be sure to store downloaded private keys in a safe disk or USB drive. If a private key is exposed, anyone can access the instance using the exposed private key, so it must be managed carefully.

> [Note]
> Key pairs are resources assigned to user accounts, so they are not deleted even when a project is deleted.

<a id="security-groups"></a>
### Security groups { #security-groups }

A security group is a virtual firewall that determines the network traffic delivered to an instance. For more details on security groups, see [VPC Overview](/Network/VPC/en/overview$[ vpc_ov ]$/).

> [Note]
> The default security group is configured to ignore all inbound network traffic. Before accessing an instance using SSH, configure the instance's security group to allow access to the SSH port.

<a id="network"></a>
### Network { #network }

For an instance to communicate with the outside, it must be connected to at least one network defined in the VPC. Instances that are not connected to a network cannot be accessed. To create or modify a network, see [VPC Overview](/Network/VPC/en/overview$[ vpc_ov ]$/).

<a id="pricing"></a>
## Pricing { #pricing }

The instance pricing model is as follows:

* Instances are charged from the moment they are created.
* The root block storage of an instance is charged separately from the instance, based on block storage pricing.
* When an instance is stopped, a 90% discount from the website rate is applied for 90 days. If the stopped status exceeds 90 days, the instance remains in stopped status and reverts to normal rates.
* Terminated instances are not charged.

For more details on pricing, see the [Pricing page](https://$[ price_dom[f] ]$/kr/service/compute/instance#price) for each service.

<a id="how-to-access-instances"></a>
## Access instances { #how-to-access-instances }

<a id="how-to-access-linux-instances"></a>
### Access Linux instances { #how-to-access-linux-instances }

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

The PuTTY SSH client is an SSH client program widely used on Windows. Install [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) or [iPuTTY](https://github.com/iPuTTY/iPuTTY/releases/tag/l0.70i), which includes a Korean language patch.

To access a Linux instance using the PuTTY SSH client on Windows, you must complete three steps:

* Convert the key pair's private key to a PuTTY-compatible private key
* Register the PuTTY-compatible private key in PuTTY
* Access an instance using PuTTY

##### 1. Convert the key pair's private key to a PuTTY-compatible private key

In PuTTY, you must convert the key pair's private key to PuTTY's private key format before use. Use puttygen, which is installed along with PuTTY, to convert the key.

![Image1](http://static.toastoven.net/prod_instance/putty001.png)

At the bottom of the **PuTTY Key Generator** window under **Parameters**, select **RSA** for the **Type of key to generate**, and enter the default value '2048' bits for the **Number of bits in a generated key**. Under **Actions**, click **Load** next to **Load an existing private key file** to import your key pair's private key file.

![Image2](http://static.toastoven.net/prod_instance/putty002.png)

Under **Actions**, click **Save private key** next to **Save the generated key** to save the key pair's private key converted for PuTTY. If you save the private key with **Key passphrase** left blank, a message appears asking **Are you sure you want to save this key without a passphrase to protect it?** To store the converted private key more securely, set a passphrase before saving.

> [Caution]
> If you wish to be able to automatically log in to your instance, you should not set a key passphrase. When a passphrase is used, you must manually enter the private key's passphrase during login.

##### 2. Register the PuTTY-compatible private key in PuTTY

The PuTTY-compatible private key that you created can be registered and used in two ways:

* Register and use the authentication private key file in PuTTY
* Register and use the authentication private key file in pageant (PuTTY authentication agent)

**A. Register and use the authentication private key file in PuTTY**


Run PuTTY and select **Connection > SSH > Auth** from the **Category** on the left. Under **Authentication parameters** on the right, register your PuTTY-compatible private key in **Private key file for authentication**.

![Image3](http://static.toastoven.net/prod_instance/putty005.png)

Once you register your private key, you do not have to re-register your private key file each time you access your instance if you save your access information. For details on how to save your access information, see the section below on accessing instances.


**B. Register and use the authentication private key file in pageant (PuTTY authentication agent)**


When you run pageant, which is installed along with PuTTY, the icon shown below appears in the Windows tray. Right-click the pageant icon and select **Add Key** to add your PuTTY-compatible private key.

![Image4](http://static.toastoven.net/prod_instance/putty006.png)

To verify that the private key has been added, select **View Keys**. If the key was added successfully, the added key appears as shown below.

![Image5](http://static.toastoven.net/prod_instance/putty008.png)

Once you run pageant, it remains running in the Windows tray, so there is no need for you to rerun it every time you access an instance. However, you must run pageant again when you restart Windows.

##### 3. Access an instance using PuTTY

Once the PuTTY-compatible private key is registered successfully, run PuTTY.

![Image6](http://static.toastoven.net/prod_instance/putty009.png)

Use the following **Host Name** in the basic access information:

Ubuntu

	ubuntu@<Instance IP>

Debian

	debian@<Instance IP>

Rocky

	rocky@<Instance IP>

Set **Port** to 22, the default SSH port, and set **Connection type** to **SSH**.

If all of the information is correct, save the session. Under **Load, save or delete a stored session**, enter the name of the session to save in **Saved Sessions** and click **Save** to save the session. If you do not save the session, your private key settings registered in 2-A are also not preserved.

Click **Open** to connect to the instance.

<a id="how-to-access-windows-instances"></a>
### Access Windows instances { #how-to-access-windows-instances }

To access your Windows server, select a Windows instance to access from the NHN Cloud console. In the instance details page under the **Access Information** tab, click **Confirm Password** to check the password set in the Windows server.

The key pair's private key that you enter in **Confirm Password** is not sent to the server. It is used only to decrypt the password in your browser.

Click **Connect** next to **Confirm Password** to download and run the .rdp file, which contains the remote desktop connection settings. This connects you to the Windows server. The Windows server's ID is `Administrator`, and the password is the one that you confirmed in the NHN Cloud console.

{% if "public" in build_flags %}
<a id="how-to-connect-serial-console"></a>
### Connect to the serial console { #how-to-connect-serial-console }

In situations where an SSH client cannot be used, such as boot failure or network configuration issues, you can connect to an instance through the serial console.

The serial console feature has the following limitations:

* Only one serial console connection is allowed per instance. Multiple connection attempts may not connect successfully.
* Serial console access is not guaranteed for instances created from user-uploaded images or private images.
* A serial console connection can remain active for up to 10 minutes.
* Windows instances do not support the serial console feature.
* Instances created before the January 27, 2026 deployment require **Stop Instance** followed by **Start Instance**. The **Reboot Instance** feature does not apply.

> [Caution]
> Changing the boot method while connected to the serial console may cause boot failure. You are responsible for any consequences that result from such changes.
> In normal circumstances, we recommend that you use an SSH client to access instances.

<a id="how-to-connect-serial-console-change-grub-bootloader-settings"></a>
#### Change GRUB bootloader settings

Instances created before the November 26, 2024 deployment require GRUB configuration to operate the bootloader.

Modify the GRUB configuration file.

```
$ sudo vi /etc/default/grub.d/50-cloudimg-settings.cfg
GRUB_TIMEOUT=3
GRUB_TERMINAL="console serial"
GRUB_SERIAL_COMMAND="serial --speed=9600 --unit=0 --word=8 --parity=no --stop=1"
```

Apply the changed settings. The command for applying GRUB settings may vary depending on the OS.

```
$ sudo update-grub
```
{% else %}
{% endif %}