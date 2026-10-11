## Game > Launching > Console Guide 

## Launching Data Management 

Launching data for a mobile app can be configured as follows:  

## Configuration Information

Current launching information can be queried on the **Configuration Information** tab on a console. 

![console_configuration_00](https://static.toastoven.net/prod_launching/en/console_configuration_00.png)

> [Note]
> With the Launching Service, default template data are provided like the above.   
> (Actual template data may be different.)

### Select/Change Folders and Keys 

Select a folder or key in the search menu on the left to find information on the right. Change name or description of the selected folder or key, and click **Confirm**, then the information is changed.   
![console_configuration_01](https://static.toastoven.net/prod_launching/en/console_configuration_01.png)

> [Note]
> The **Confirm** button applies changes in the console only; to apply such changes in the server, it is required to deploy on the **Deploy** tab.  

> [Note]
> Same key names may exist in different folders, but no two same key names exist under a single folder. For example, there is only one key named 'ip' in the server folder, but the same 'ip' key may exist in another folder.     

### Change Key Formats 

Key formats can be changed, on the key information that shows at the click of the key. By changing it into the drop-down format, values of the character string format of choice may be added or deleted.  

![console_configuration_02](https://static.toastoven.net/prod_launching/en/console_configuration_02.png)

### Folders and Keys 

#### Adding

You may add folders or keys, by selecting a folder from the search menu on the left and clicking on the right; or, at the click of **Add Folders/Keys** on top-left of the search menu.  

![console_configuration_03](https://static.toastoven.net/prod_launching/en/console_configuration_03.png)

#### Copying, Pasting, and Deleting 

Select a folder or key from the search menu on the left, and click **Copy/Delete/Paste** to suit your needs. 

![console_configuration_04](https://static.toastoven.net/prod_launching/en/console_configuration_04.png)

> [Note]
> If a folder is deleted, all its lower-level folders and keys are deleted altogether.

## Logic

Server logic information is available at the click of the **Logic** tab, so as to change registered launching information. Logic refer to a business logic to dynamically change fixed launching information, and as it operates in the server, changed launching information becomes available without app updates.  

![console_logic_00](https://static.toastoven.net/prod_launching/en/console_logic_00.png)

### Adding 

To add a server logic, the start and closing time of a logic operation, as well as conditions and results of logic application must be included. 

You may use the conditional sentence of JavaScript, for which the final result is Boolean. 
Launching information registered at the server, as well as GET parameters of Query Launching API can be applied as general parameters. The launching information is available in the [launching.{folder}.{key}] format, while all the others are considered as general parameters. 

Results, if logic conditions are met, regard to changing launching information, and are available in the [launching.{folder}.{key}] format.  

Period of logic application can be configured in **Period of Application**, and you can even make it applied continuously to logic, without configuring the closing time. 

![console_logic_01](https://static.toastoven.net/prod_launching/en/console_logic_01.png)

> [Note]
> If there is no key specified as result in the launching information, add one; otherwise, existing information is overwritten.

> [Warning]
> A logic cannot exceed 1KB. In addition, at least one logic result must be registered, with the key and value no larger than 255 bytes. 

### Modifying 

Click a registered logic and modify. 

![console_logic_02](https://static.toastoven.net/prod_launching/en/console_logic_02.png)

#### Execute/Suspend  

Check a logic to suspend or execute from the list, and click **Execute/Suspend** to change its status. Logics under suspension are not available to change launching information. 

#### Delete 

Check a logic to delete from the list, and click **Delete** to delete it. 

> [Warning]
> To apply all changes, including execution/suspension, deploy from the **Deploy** tab. 

### Testing 

You may test a logic before its launching information is deployed to server. Configure application period for GET parameters, delivered to call launching information, as well as for the logic, and click **Test Logic** and confirm launching information in which the logic is applied.  

To test delivery of many parameters, click + on the far right of Parameters, and register new parameters. 

![console_logic_03](https://static.toastoven.net/prod_launching/en/console_logic_03.png)

For instance, register your logic like the above and test, then Logic Result shows test results. 

As you can see, if the parameter 'launching.server.cds', as part of a logic condition, is 'TEST', it is configured to put '127.0.0.1 for [lauching.server.ip]; as a result, TEST is configured for 'launching.server.cds', as GET parameter, resulting in '127.0.0.1' for [lauching.server.ip]. 

> [Note]
> The yellow highlights refer to keys that are added or changed, with the logic and GET parameters applied on the origin launching information. 

### Subkeys 

Subkeys start with "launching" and are combined with ".", and they can import partial data only from launching information. 

With [launching.server] specified as subkey, the [launching.server] data only can be imported. 

![console_logic_04](https://static.toastoven.net/prod_launching/en/console_logic_04.png)

> [Warning]
> Subkeys are specified as GET parameters, like the above. Get parameters that have "subkey" as key are considered as subkeys. 

### Key Patterns 

Key patterns refer to special keys which start with "$" and can be applied in logic conditions and results. 
On the route of launching information, which is the final delivery result by using the entire keys or subkeys, relative location can be specified. 

Let's assume the logic is registered like below: 

![console_logic_05](https://static.toastoven.net/prod_launching/en/console_logic_05.png)

In this case, unless a subkey is specified, logic application is not available. 

However, with [launching.server] specified as subkey to import partial data only, the logic condition ".$cds === 'TEST'" is satisfied, and value is changed due to ".ip = '127.0.0.1'". 

![console_logic_06](https://static.toastoven.net/prod_launching/en/console_logic_06.png)

As such, you can use subkeys and key patterns to flexibly change launching information. 

## Import 

You can import launching information and logic registered in Launching Service of another project, from the **Import** tab, or from JSON-format data which is copied with **Copy in JSON Format**.  

Or, select another project, and click **Execute Import** to import launching information and logic. 

You may also import them from JSON-format data, from the **Load from JSON Format** menu.  

> [Note]
> You can test, after **Import** and check launching information and logic in the **Configuration Information/Logic** tab. Import must be deployed on the **Deploy** tab so as to apply to server.  

## Export 

You can export launching information and logic to Launching Service of another project on the **Export** tab, or copy in the JSON-format data. 

Select another project, and click **Execute Export** to export launching information and logic. 

Or, copy JSON-format data from the **Copy in JSON-Format** menu. 

## Deploy 

To apply modification made on the **Configuration Information** and **Logic** tab to server, it must be deployed in the **Deploy** tab. 
Before deployment, you can find, on the **Deploy** tab, launching information and logic, as well as modified description like below. 

![console_deploy_00](https://static.toastoven.net/prod_launching/en/console_deploy_00.png)

Click **Deploy**, and it is applied to server, with changed launching information from the mobile app. You may click **Initialize** to revert what is modified on console.   

With deployment, launching information and logic are backed up, in such states they are immediately before modified on console. Click **Deploy** and specify name to back up.   

### Check Backup History 

![console_deploy_01](https://static.toastoven.net/prod_launching/en/console_deploy_01.png)

Backup history is available at the bottom. 

Click **Configuration Information/Check Logic** to find launching information and logic that are backed up, and they may be restored or deleted.  