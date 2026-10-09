<!-- machine_translated: true -->

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

### Additional Features

* Add Instance Object: Add objects by leveraging the instances that exist within the project where Network Firewall was created.
* Download Template: Downloads the template file required for batch registration.
* Batch Register Objects: You can register objects in bulk using the downloaded template.
* Batch Download Objects: You can download all IP or port objects created on the **Objects** tab at once, each in a single batch.

!!! tip "Note"
    * Group objects cannot be added when creating a group object (only single or range objects can be added by selecting them).
    * The Type cannot be modified when modifying an object.
    * The Add Instance Object feature creates an instance-agnostic object by simply referencing the instance's name and private IP address. The objects you create are managed on the **Objects** tab.

!!! danger "Caution"
    If you delete an object that is in use by a policy, it will be changed to an ALL object after deletion. Exercise caution when deleting.