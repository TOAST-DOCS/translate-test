<a id='restarting-guide-for-maintenance'></a>
## Load Balancer Restart Guide for Equipment Maintenance

NHN Cloud periodically updates the software on load balancer equipment to improve the security and stability of basic infrastructure services. For load balancer equipment maintenance, load balancers running on equipment designated for maintenance must be restarted to move to load balancer equipment that has completed maintenance.

Load balancers that need to be restarted display a **! Restart** button next to their name, and you can use this button to restart them.

Go to the project with load balancers designated for maintenance and follow these steps to restart them.

1. Check the load balancers designated for maintenance. Load balancers with a **! Restart** button next to their name are the load balancers designated for maintenance.
   ![image-001](http://static.toastoven.net/prod_load_balancer/lb_p_migration_ko_1.png)
   When you hover your mouse cursor over the **! Restart** button, you can check the detailed maintenance schedule. We recommend that you perform this during times that don't affect your service.
   ![image-002](http://static.toastoven.net/prod_load_balancer/lb_p_migration_ko_2.png)
2. Select the load balancer designated for maintenance and click the **! Restart** button next to its name.
3. When a window appears asking whether to restart the load balancer, click **OK**.
4. Wait until the status indicator turns green and the **! Restart** button disappears.
   If the load balancer status indicator doesn't change or the **! Restart** button doesn't disappear, try refreshing the page.


You can't perform any operations on the load balancer while it's being restarted.
If the load balancer restart doesn't complete normally, it's automatically reported to the administrator, and NHN Cloud will contact you separately.