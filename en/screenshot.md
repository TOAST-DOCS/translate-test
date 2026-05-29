<a id='restarting-guide-for-maintenance'></a>
## Load Balancer Restart Guide for Equipment Maintenance

NHN Cloud periodically updates the software of load balancer equipment to improve the security and stability of basic infrastructure services. For load balancer equipment maintenance, load balancers running on equipment scheduled for maintenance must be moved to maintenance-completed load balancer equipment through restart.

Load balancers that require restart display a **! Restart** button next to their name, which can be used to restart them.

Navigate to the project containing load balancers designated for maintenance and perform the restart following these procedures:

1. Check the load balancers scheduled for maintenance. Load balancers with a **! Restart** button next to their name are the ones scheduled for maintenance.
   ![image-001](https://static.toastoven.net/prod_translate/translate-test/en/lb_p_migration_ko_1.png)
   Hover your mouse cursor over the **! Restart** button to see detailed maintenance schedule information. Please perform this during times that won't affect your service.
   ![image-002](https://static.toastoven.net/prod_translate/translate-test/en/lb_p_migration_ko_2.png)
2. Select the load balancer scheduled for maintenance and click the **! Restart** button next to its name.
3. When a dialog asking whether to restart the load balancer appears, click the **OK** button.
4. Wait until the status indicator turns green and the **! Restart** button disappears.
   If the load balancer status indicator doesn't change or the **! Restart** button doesn't disappear, please try 'Refresh'.

During load balancer restart, no operations can be performed on that load balancer.
If the load balancer restart does not complete normally, it is automatically reported to the administrator, and NHN Cloud will contact you separately.