## Overview
When you migrate a container cluster in the customer IDC to TCR, you can also migrate the external container image hosting service to TCR for hosting. After the external image repositories are migrated to TCR, it can not only reduce the O&M costs of building and maintaining the image repository, but also provide professional and stable cloud hosting services and technical supports. In addition, you can use the container service in Tencent Cloud, enjoying a consistent cloud container experience, and use the container clusters to pull images via the private network, reducing the cost of using public network bandwidth.

Harbor is an open source enterprise-class Docker Registry project of VMware. Based on the open source Docker distribution capability, Harbor extends capabilities such as RBAC, secure image scanning, and image synchronization. At present, it has become the preference of creating container image hosting and distribution services. This document describes how to synchronize a container image or Helm Chart in Harbor that is built on the IDC or the cloud server to the TCR Enterprise Edition.

## Prerequisites
To synchronize data in the external Harbor to a TCR Enterprise Edition instance, you need to confirm and complete the following preparations first:
- You have built the Harbor service with V1.8.0 and later versions.
- The external Harbor can access TCR through a private line, public network, or VPC.
- You have [purchased instances](https://intl.cloud.tencent.com/document/product/1051/39088) in the region of the cloud container cluster or in an adjacent region.
- If you are using a sub-account, you must have granted the sub-account the permission to push TCR and Helm Chart to corresponding instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248). We recommend that you grant the full TCR access permissions to the sub-account used for synchronization configuration.

## Directions
<span id="Configuration"></span>

### Configuring access to the TCR Enterprise Edition instance for Harbor

Based on the actual network of Harbor, you can select [access via Tencent Cloud VPC](#vpc) or [access via public network](#publicnet) to configure access to the TCR Enterprise Edition instance.

<dx-tabs>
::: Accessing via Tencent Cloud VPC
If the current Harbor is deployed in Tencent Cloud VPC or has been connected to the Tencent Cloud VPC through a private line, you can synchronize data through the private network, which can increase the speed of data synchronization and reduce the cost of public network traffic.

1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Network ACL** > **Private network** on the left sidebar.
2. In the **Instance** drop-down list at the top of the page, select an instance for data synchronization.
3. Click **Create**, and in the **Create a private network access linkage** window that is displayed, configure a new private access linkage to allow Harbor to access the instance through the private network.
	- **Associated Instance**: the currently selected instance for data synchronization.
	- **Virtual Private Cloud**: the VPC where the Harbor is located or the VPC connected through Direct Connect.
	- **Subnet**: the created private access linkage occupies a private IP address of the selected VPC. Select a subnet under the VPC to assign the subnet of the private IP address.
4. After completing the above configuration, you can obtain the target access IP address of the private access linkage. To resolve the domain name of the instance into the private IP address in the VPC, please manage the automatic resolution of the private network access linkage and enable the automatic resolution of the default domain name. For more information, see [Managing Private Network Resolution](https://intl.cloud.tencent.com/document/product/1051/35492).
![](https://main.qcloudimg.com/raw/3f1992c74f5f97496bb84d806951ea63.png)
You can also configure the host on the CVM where the Harbor is located. If you choose manual configuration, you can run the following command on CVM to configure the host. If an independent DNS is currently in use, you can also configure the host in the DNS.
```
echo x.x.x.x harbor-sync.tencentcloudcr.com >> /etc/hosts
```
:::
::: Accessing via public network
If the current Harbor is not deployed in a Tencent Cloud VPC or cannot be connected to Tencent Cloud VPC through a private line, you can synchronize data through the public network. The synchronization may incur public network traffic fees. For billing details, please refer to the pricing of the network ISP or cloud service provider.
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Network ACL** > **Public network** on the left sidebar.
2. In the **Instance** drop-down list at the top of the page, select an instance for data synchronization.
3. Click **Open Internet Access Entry** at the top of the list to enable the public network access entry.
When the status of the button changes from **Enabling** to **Close Internet Access Entry**, and **Add a public IP to allowlist** becomes available, the public network access entry is successfully enabled, and then all public accesses are rejected by default.
4. Click **Add a public IP to allowlist**. In the "Create Public Network Access Allowlist" window that is displayed, configure an allowlist policy to allow the external Harbor to access the instance through the public network.
	- **Associated Instance**: the currently selected instance for data synchronization.
	- **Public IP Range**: the egress public IP address of the external Harbor. If there is no specific public IP address, the IP address can be temporarily set to `0.0.0.0/0` to allow all public network accesses. After the synchronization is completed, please delete the temporary IP address as soon as possible.
	- **Note**: the remarks of the allowlist configuration, for example, “Allow the external Harbor to access the instance through public network”.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/YGw7975_487b82faa82a11edbb45525400c56988.png)
:::
</dx-tabs>

### Creating an access credential for the TCR Enterprise Edition instance

You can create and manage multiple access credentials in TCR Enterprise Edition. We recommend that you create an independent access credential for data synchronization and delete it in time after the data synchronization to avoid the leakage of the instance’s access permission.
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Instance** on the left sidebar.
2. On the “Instance List” page, select an instance for data synchronization to go to its details page.
3. Select the **Access Credential** tab and click **Create** at the top of the instance list.
4. In the pop-up **Create Access Credential** window, perform the following steps:
    1. In the “Create Access Credential” section, enter the usage description of the credential and click **Next**. For example, “Dedicated for data synchronization of external Harbor”.
    2. In the “Save Access Credential” section, click **Save Access Credential** to download the credential. **Please save the access credential properly. You will not be able to get it again.**
After the access credential is created, you can view it in the **Access Credential** tab. Please disable and delete the access credential in time after the data synchronization.

### Configuring the synchronization repository and rule of Harbor
You can add a third party Registry and configure the data replication rules in Harbor. This document takes Harbor V2.1.2 as an example.
1. Log in to Harbor console with an admin account. You can view and perform **Administration**.
2. Select **Administration** > **Registries** on the left sidebar to go to the **Registries** page.
3. <span id="Step3"></span>On the **Registries** page, click **NEW ENDPOINT**. Refer to the following information to add a TCR Enterprise Edition instance.
	- **Provider**: select “tencent-tcr”.
	- **Name**: custom the endpoint name for the synchronization such as tencent-tcr.
	- **Description**: the description of the synchronization endpoint.
	- **Endpoint URL**: the access domain name of the TCR Enterprise Edition instance, for example `https://harbor-sync.tencentcloudcr.com`.
	- **Access ID**: enter the `SecretId` obtained from **Access Keys** > **[Manage API Key](https://console.cloud.tencent.com/cam/capi)**.
	- **Access Secret**: enter the `SecretKey` obtained from **Access Key** > **[Manage API Key](https://console.cloud.tencent.com/cam/capi)**.
	- **Verify Remote Cert**: keep the default setting.
4. Click **TEST CONNECTION**.
   - If “Connection tested successfully” is displayed, the current Harbor can access the TCR Enterprise Edition instance normally.
   - If “Failed to ping endpoint” is displayed, make sure that you have [configured access to the TCR Enterprise Edition instance for the external Harbor](#Configuration).
5. Click **OK** to create the registry endpoint.


>! If the Harbor is an earlier version, there is no "tencent-tcr" option for the **Provider**. Please select "Docker Registry" for **Provider** when creating a registry endpoint. For **Access ID** and **Access Password**, respectively enter the **Login Username** and **Login password** of the long-term access credential of the image repository obtained in **Instance** > **Access Credential** page. In this case, the namespace cannot be automatically created in the TCR.

6. <span id="createRule"></span>Select **Administration** > **Replications** on the left sidebar and click **NEW REPLICATION RULE**. Refer to the following information to create the rule.
   - **Name**: the rule name. You can enter a name based on the actual usage scenario.
	- **Description**: the rule description.
    - **Replication mode**: defaults to **Push-based**. Only when “tencent-tcr” is selected for **Provider** and the version of Harbor is V2.1.2 or later, you can select **Pull-based**. **Push-based** means to synchronize the new image in the Harbor to the TCR, while **Pull-based** means to synchronize the new image in the TCR to the Harbor.
	- **Source resource filter**: you can filter resources to synchronize. If you do not set a filter, all container images and Helm Chart resources in the Harbor are selected by default.
	- **Destination registry**: select the repository endpoint created in [Step 3](#Step3).
	- **Destination namespace**: specify the destination namespace. If it is left empty, the resources will be put under the same namespace as the source. The default setting is recommended.
	- **Trigger Mode**: defaults to **Manual**. If you need automatic synchronization for the newly pushed container image or Helm Chart, please select “Event Based”. We recommend that you do not select “Delete remote resources when locally deleted”.
	- **Override**: defaults to override the resources at the destination if a resource with the same name exists.


### Triggering synchronization and viewing the synchronization log
If you select **Event Based** for the **Trigger Mode**, when container images and Helm Chart are pushed to the Harbor, they will be automatically synchronized to the TCR Enterprise Edition instance. You can select the replication rule to view the synchronization log, and access the TCR Enterprise Edition instance console to check whether synchronization is successful. This document takes the example of manually pushing the container image `nginx:latest` to the Harbor and triggering the synchronization.
1. Push the container image and view it in Harbor.
Use the docker client to push the local container image `nginx:latest` to Harbor, and then log in to the Harbor console to view the pushed image.
2. View the synchronization record and progress.
Select **Administration** > **Replications** on the left sidebar and select the replication rule created in [Step 6](#createRule) to view the replication task of the rule.
3. View the synchronized image in TCR console.
Log in to the TCR console and select **Image Repository** on the left sidebar. In the **Image Repository** page, select the instance used for synchronizing with the Harbor to view the successfully synchronized container image.

