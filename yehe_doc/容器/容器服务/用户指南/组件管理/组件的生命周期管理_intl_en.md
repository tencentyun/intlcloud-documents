


## Installing an Add-on
You can install an add-on using either of the following methods:
- [Installing an add-on on the cluster creation page](#Cluster)
- [Installing an add-on on the add-on management page](#Component)


<span id="Cluster"></span>
### Installing an add-on on the cluster creation page
1. Log in to the [TKE Console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click **Create** above the cluster list.
3. On the "Create Cluster" page, set the "Cluster Information", "Select Model", "CVM Configuration", "Component Configurations" and "Confirm Info" in order as shown below:
![](https://main.qcloudimg.com/raw/b1853e81cf57014951dd88d07a431306.png)
 You can select the add-ons to install based on your business deployment and click **View Details** for an add-on card to view the description of the add-on. Some add-ons require you to complete **Parameter Configuration** first.
>? 
>- Add-on installation is not a critical path in cluster creation. An add-on installation failure does not affect cluster creation.
>- Add-on installation consumes some cluster resources. The specific amount of resources consumed varies with different add-ons. For more information, click **View Details** for a specific add-on.
4. Click **Next** to check and confirm the cluster configuration information.
5. Click **Finish**.



<span id="Component"></span>

### Installing an add-on on the add-on management page 
1. Log in to the [TKE Console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the "Add-on List" page.
4. On the "Add-on List" page, click **Create** to go to the add-on installation page, as shown in the figure below:
![](https://main.qcloudimg.com/raw/80a0da34b1caf87226775d3eeb7343c8.png)
5. Select the add-ons to install and click **Finish**.

## Uninstalling an Add-on
1. Log in to the [TKE Console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the "Add-on List" page.
4. On the "Add-on List" page, click **Delete** to the right of the row of the add-on that you want to delete, as shown in the figure below:
![](https://main.qcloudimg.com/raw/bb0fea46685de1a11cddfab294dab9b0.png)
5. In the displayed "Delete Resources" window, click **Confirm** to uninstall the add-on.

