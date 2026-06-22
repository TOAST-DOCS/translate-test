# Parameter Group

**Database > EasyCache > Console User Guide > Parameter Group**

EasyCache provides a parameter group feature to apply Valkey (formerly Redis) settings installed on caches. A parameter group is a collection of parameters that can be used to configure Valkey. When the service is activated, a default parameter group is provided for each version of all engines. The default parameter group is provided as `{engine version name} Default` and consists of the recommended default parameter values for each version. The default parameter group can be modified or deleted in the same way as a regular parameter group.

### Create a Parameter Group

You can create a parameter group in the parameter console as needed. Parameter groups are created for each engine version and can be assigned a name. The following constraints apply:

* Parameter group names can only contain between 1 and 100 uppercase and lowercase English letters, numbers, and certain symbols (-, \_, .). The first character must be an English letter.
* When a parameter group is created, parameters are always set to their default values. To create a parameter group based on an existing one, use the copy parameter group feature.

### Copy a Parameter Group

Creates a new parameter group based on an existing parameter group. The copied parameter group consists of the parameter values of the source parameter group. There is no association between the source parameter group and the copied parameter group, and any changes or deletions made to the source parameter group do not affect the copied parameter group.

### Reset a Parameter Group

Resetting a parameter group changes the values of all parameters to the default values of the engine version.

### Apply a Parameter Group

You can select a parameter group to apply to a cache when creating or modifying the cache. One parameter group is applied to one cache, and one parameter group can be applied to multiple caches. When a parameter in a parameter group is changed, the change is not applied to the cache immediately. If there are associated caches, the parameter group status changes to Apply Required, and **Parameter** button is activated for the associated caches on the Cache List screen. Click **Parameter** button on the Cache List screen to apply the parameter changes to the cache. When the parameter group changes are applied to all associated caches, the parameter group status changes to Apply Completed

!!! tip "Note"
    If a parameter that requires a restart is changed, the cache is restarted during the application process.

### Compare Parameter Groups

Select two different parameter groups in the console and click **Compare** to check which parameters differ. You can compare parameter groups not only for the same engine but also for different engine versions

### Delete a Parameter Group

You can freely delete any parameter group except those currently applied to a cache. To delete a parameter group that is currently applied to a cache, you must first change the parameter group of all associated caches before deleting it.

## Parameter

### Modify Parameters

Select a parameter group in the console and click **Edit Parameters** to modify parameters. Parameters that cannot be changed are displayed as plain text, and parameters that can be changed display an input field for editing. On the edit screen, click **Preview Changes** to display a separate pop-up screen where you can review the changed parameters. Click **Reset** to revert to the values before the changes. All values changed in edit mode are reflected in the parameter group only after clicking **Save** Changes

### Modify the `acl-save-enabled` Parameter
`acl-save-enabled` is a parameter applicable from Redis 6.0 and later, and determines whether to enable the feature that permanently saves the engine's user account and permission information to a file. The default value is `no`. In this case, even if user and permission information is specified for a node, the information is lost and reset to the default settings if the node is restarted. Therefore, to permanently save user information, change this option to `yes`. If user information has been edited, it is strongly recommended to click **Save** to Configuration File to ensure it is fully saved

!!! danger "Caution"
    Modifying the value of the acl-save-enabled parameter requires a restart of the associated caches and nodes. Exercise caution when making changes.