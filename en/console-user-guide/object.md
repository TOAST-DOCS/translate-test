<!-- pre-align:aligned sig=24c6566066ad -->

# Object

**Security > Cloud Access > Console User Guide > Object**

In the **Object** tab, you can manage IPs and ports used when creating ACL policies.

<br>

<a id="manage-ip"></a>
## Manage IP { #manage-ip }

<a id="add"></a>
### Add { #add }

![object_add_1.PNG](../../static/images/2025.06.24/object_add_1.png)

Create an object by entering the required information.

<a id="modify"></a>
### Modify { #modify }

Click **Modify** to modify the object.

<a id="delete"></a>
### Delete { #delete }

Click **Delete** to remove the object.

<a id="additional-features"></a>
### Additional Features { #additional-features }

* Add User Object: Add objects based on registered users.
* Download Template: Download a template file for bulk registration.
* Upload Object in Batch: Use the template to register multiple objects at once.
* Download Object in Batch: Download all IP objects currently registered in the **Object** tab at once.

<br>

!!! tip "Note"
    * When creating a group object, other group objects cannot be added (only single or range objects can be selected).
    * The type cannot be changed when modifying an IP object.
    * IP objects created during Cloud Access setup cannot be modified or deleted.

!!! danger "Caution"
    * If you delete an object currently used in a policy, it will be replaced with the "ALL" object. Proceed with caution.

<br>

<a id="manage-port"></a>
## Manage Port { #manage-port }

<a id="manage-port-add"></a>
### Add { #manage-port-add }

![object_add_2.PNG](../../static/images/2025.06.24/object_add_2.png)

Create an object by entering the required information.

<a id="manage-port-modify"></a>
### Modify { #manage-port-modify }

Click **Modify** to modify the object.

<a id="manage-port-delete"></a>
### Delete { #manage-port-delete }

Click **Delete** to remove the object.

<a id="manage-port-additional-features"></a>
### Additional Features { #manage-port-additional-features }

* Download Template: Download a template file for bulk registration.
* Upload Object in Batch: Use the template to register multiple port objects at once.
* Download Object in Batch: Download all port objects currently registered in the Objects tab at once.

!!! tip "Note"
    * When creating a group object, other group objects cannot be added (only single or range objects can be selected).
    * The type cannot be changed when modifying a port object.
    * Port objects created during Cloud Access setup cannot be modified or deleted.

!!! danger "Caution"
    * If you delete an object currently used in a policy, it will be replaced with the "ALL" object. Proceed with caution.