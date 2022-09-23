## Installing an Add-on
You can install add-ons with the following methods.
- [Installing on the cluster creation page](#Cluster)
- [Installing on the add-on management page](#Component)


[](id:Cluster)
### Installing on the cluster creation page
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the "Cluster management" page, click **Create** above the cluster list.
3 On the "Create a cluster" page, configure the parameters in the **Basic information**, **Select a model**, **CVM configuration**, and **Add-on configuration** steps in sequence.
![](https://main.qcloudimg.com/raw/b1853e81cf57014951dd88d07a431306.png)
 You can select the add-ons to install based on your business deployment and click **View details** to view the add-on description. Some add-ons require you to complete **Parameter configuration** first.
>? 
>- Add-on installation is not a critical path in cluster creation. An add-on installation failure does not affect the cluster creation.
>- Add-on installation consumes some cluster resources. The specific amount of resources consumed varies depending on the add-ons. For more information, click **View details** for a specific add-on.
4. Click **Next**. Check and confirm the cluster configuration information.
5. Click **OK** to complete the process.


[](id:Component)
### Installing on the add-on management page 
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the **Cluster management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on management** to go to the “Add-on list” page.
4. On the "Add-on list" page, click **Create** to go to the add-on installation page.
![](https://main.qcloudimg.com/raw/80a0da34b1caf87226775d3eeb7343c8.png)
5. Select the add-ons to install and click **OK**.


## Uninstalling an Add-on
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the **Cluster management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on management** to go to the “Add-on list” page.
4. On the "Add-on list" page, click **Delete** to the right of the target add-on.
![](https://main.qcloudimg.com/raw/bb0fea46685de1a11cddfab294dab9b0.png)
5. In the displayed "Delete resource" window, click **Confirm** to uninstall the add-on.


## Upgrading an Add-on
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the **Cluster management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on management** to go to the “Add-on list” page.
4. On the "Add-on list" page, click **Upgrade** to the right of the target add-on.
![](https://qcloudimg.tencent-cloud.cn/raw/e48d1b1ae84f1bc50bc471f3969e4577.png)
5. In the displayed "Upgrade add-on" window, click **Confirm** to upgrade the add-on.

