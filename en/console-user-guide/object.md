<!-- pre-align:aligned sig=61dff5f1b687 -->

<a id="object"></a>
## Object { #object }

**Security > Network Firewall > Console User Guide > Object**

In the **Object** tab, you can create and manage the IPs and ports to be used when creating policies.

<br>

<a id="configure-objects"></a>
## Configure Objects { #configure-objects }

<a id="add"></a>
### Add { #add }

* Create an object by entering the required fields.
    * Objects can be added in two forms: IP and port.
![(object2)](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/4.object/object2.png)

<a id="modify"></a>
### Modify { #modify }

* Click **Modify** to modify an object.
    * Types cannot be modified.

<a id="delete"></a>
### Delete { #delete }

* Click **Delete** to delete an object.
    * Objects automatically created by Network Firewall cannot be modified or deleted.

<a id="add-instance-object"></a>
### Add Instance Object { #add-instance-object }
* Add objects by leveraging the instances that exist within the project where Network Firewall was created.
![(object3)](https://static.toastoven.net/prod_nfw/26.07.28/2.console-user-guide/4.object/object3.png)

<a id="batch-download-of-objects"></a>
### Batch Download of Objects { #batch-download-of-objects }

* You can download all IP and port objects created in the **Object** tab at once.

!!! tip "Note"

    * Group objects cannot be added when creating a group object (only individual or range objects can be selected and added).
    * Objects are created by simply referencing the instance name and private IP address, regardless of the instance itself. Created objects are managed in the **Object** tab.

!!! danger "Caution"

    Objects in use by a policy will be changed to ALL objects after deletion.