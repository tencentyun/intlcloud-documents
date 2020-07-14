
## Feature Overview
EMR provides a software WebUI entry for you to access the native UIs of components. By using the public IP of the master node (you are recommended to configure a security policy timely), you can conveniently access the native component UIs. If your cluster's private network and your organization network are connected, you can disable the public IP and directly access the UIs over the private network.

## Directions
1. 	Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select the target cluster in **Cluster List**, and click **Details** to enter the cluster details page.
2. 	On the cluster details page, select **Cluster Service** and click the **WebUI address** of the target component for access.
The access address requires authentication. The username is "root", and the default password is the one you entered when creating the cluster. To change the password, click **Reset Native UI Password** on the page.
>Access incurs fees that are billed by traffic.
>
![](https://main.qcloudimg.com/raw/3df957fe84cbc905fdefcd8d29ee8d8f.png)
