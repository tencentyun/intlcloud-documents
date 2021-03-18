## Overview
When you migrate a container cluster created in the IDC to the cloud container service (CCS), you may also choose to migrate the created container image hosting service to the cloud for hosting at the same time. After the created image repository service is migrated to TCR, the O&M costs for setup and maintenance are reduced, and professional and stable cloud hosting services and technical support are provided. In addition, the linkage with CCS is implemented, users can enjoy a consistent CCS experience, the container cluster can be used to pull images from the private network, and the cost of public network bandwidth is reduced.

Harbor is an open source enterprise-class Docker Registry project of VMware. On the basis of the open source Docker distribution capability, Harbor extends capabilities such as RBAC, secure image scanning, and image synchronization. At present, it has become the first choice of self-built container hosting and distribution services. This document describes how to synchronize a container image or Helm Chart in Harbor that is set up in the IDC or on the cloud server to the TCR Enterprise Edition.

## Prerequisites
To synchronize data in the self-built Harbor to a TCR instance, you need to confirm and complete the following preparations first:
- The Harbor service has been set up and only Harbor V1.8.0 and later versions are supported.
- The self-built Harbor can access TCR through a private line, public network, or VPC.
- You have [Purchased Instances](https://intl.cloud.tencent.com/document/product/1051/39088) in the region of the cloud container cluster or in an adjacent region.
- If you are using a sub-account, you must have granted the sub-account the permission to push TCR and Helm Chart to corresponding instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248). We recommend that you grant the full TCR access permissions to the sub-account used for synchronization configuration.

## Directions
<span id="Configuration"></span>

### Configuring a TCR Enterprise Edition instance that can be accessed by the self-built Harbor service

You can choose to [access through Tencent Cloud VPC](#vpc) or [access through a public network](#publicnet) to configure a TRC Enterprise Edition instance based on actual network conditions of the self-built Harbor service.

<span id="vpc"></span>

####  Accessing through Tencent Cloud VPC
If the current self-built Harbor service is deployed in Tencent Cloud VPC environment or is connected to the Tencent Cloud VPC through a private line, you can synchronize data through the private network. Data synchronization through the private network increases the data synchronization speed and reduces public network traffic costs.

1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and choose **Network ACL** > **Private network** in the left sidebar.
2. In the **Instance** drop-down list in the upper part of the page, select an instance for data synchronization.
3. Click **Create**. In the **Create a private network access linkage** window that is displayed, configure a new private access linkage to allow the self-built Harbor service to access the instance through the private network.
	- **Associated Instance**: the currently selected instance, that is, the instance for data synchronization.
	- **Virtual Private Cloud**: the VPC where the self-built Harbor service is located or the VPC connected through Direct Connect.
	- **Subnet**: the created private access linkage occupies a private IP address of the selected VPC. Select a subnet under the VPC to assign the subnet of the private IP address.
4. After the configuration is complete, the target access IP address of the private access linkage is obtained. To resolve the domain name of the instance into the private IP address in the VPC, please manage the automatic resolution of the private network access linkage and enable the automatic resolution of the default domain name. For more information, see [Managing Private Network Resolution](https://intl.cloud.tencent.com/document/product/1051/35492).
![](https://main.qcloudimg.com/raw/3f1992c74f5f97496bb84d806951ea63.png)
You can also configure the host on the CVM where the self-built Harbor service is located. If you choose manual configuration, you can run the following command on CVM to configure the host. If an independent DNS is currently in use, you may also configure the host in the DNS.
```
echo x.x.x.x harbor-sync.tencentcloudcr.com >> /etc/hosts
```
<span id="publicnet"></span>
#### Accessing through a public network
If the current self-built Harbor service is not deployed in a Tencent Cloud VPC environment or cannot be connected to Tencent Cloud VPC through a private line, you can synchronize data through a public network. During synchronization, a public network traffic fee may be generated. For more information, refer to the pricing of the network ISP or cloud service provider.
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and choose **Network ACL** > **Public network** in the left sidebar.
2. In the **Instance** drop-down list in the upper part of the page, select an instance for data synchronization.
3. Select **Open Internet Access Entry** in the upper part of the list to enable the public network access entry.
After the status of the button changes **Close Internet Access Entry** from **Enabling** and **Add a public IP to allowlist** is available, the entry is enabled. In this case, public access requests from all sources are rejected by default.
4. Click **Add a public IP to allowlist**. In the "Create Public Network Access Allowlist" window that is displayed, configure an allowlist policy to allow the self-built Harbor service to access the instance through a public network.
	- **Associated Instance**: the currently selected instance, that is, the instance for data synchronization.
	- **Public IP Range**:  the public IP address of the self-built Harbor service egress. If no specific public IP address can be confirmed, the IP address can be temporarily set to `0.0.0.0/0` to allow access from all public network sources. After synchronization is complete, delete the configuration as soon as possible.
	- **Note**: you can enter remarks of the allowlist configuration, for example, “Allow the self-built Harbor service to access through public network”.




<span id="getCertificate"></span>

### Creating an access credential for the Enterprise Edition instance

The TCR Enterprise Edition supports creating and managing multiple access credentials. It is recommended that you create an independent access credential for data synchronization and delete the credential in time after data synchronization is completed, so as to avoid leakage of the access permission of the instance.
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Instance** in the left sidebar.
2. On the “Instance List” page, select an instance for data synchronization. The instance details page is displayed.
3. Select the **Access Credential** tab and click **Create** in the upper part of the instance list.
4. In the **Create Access Credential** window that is displayed, perform the following steps:
  1. In the “Create Access Credential” step, enter information in **Usage Description** of a credential and click **Next**. You can enter “Synchronize data for self-built Harbor” in **Usage Description**.
  2. In the “Save Access Credential” step, click **Save Access Credential** to download the credential. **Please save the access credential properly. You have only one chance to save the credential.**
After an access credential is created, you can view the credential in the **Access Credential** tab. After data synchronization is completed, please disable and delete the access credential in time.

### Configuring a Harbor synchronization registry and a synchronization rule
Harbor supports adding a third-party registry and configuring a data replication rule. This document takes Harbor V2.1.2 as an example.
1. Log in to the self-built Harbor service by using an administrator account. You can view and perform **System Management**.
2. Choose **System Management** > **Registry Management** in the left sidebar. The **Registry Management** page is displayed.
3. <span id="Step3"></span>On the **Registry Management** page, click **Create Target**. Refer to the following information to add an Enterprise Edition instance.
- **Provider**: select “Tencent TCR”.
	- **Target Name**: custom the name of the synchronization target, for example, tencent-tcr.
	- **Description**: the description of the synchronization target.
	- **Target URL**: the access domain name of the Enterprise Edition instance, for example, `https://harbor-sync.tencentcloudcr.com`.
	- **Access ID**: enter the SecretId obtained from **Access Key** > **Manage API Key**.
	- **Access Password**: enter the SecretKey obtained from **Access Key** > **Manage API Key**.
	- **Verify Remote Certificate**: use the default value.
4. Click **Test Connection**.
 - If “Test connection successful” is displayed, the current self-built Harbor service can access the Enterprise Edition instance.
 - If “Test connection failed” is displayed, make sure that you [configure a TCR Enterprise Edition instance that can be accessed by the self-built Harbor service](#Configuration).
5. Click **OK** to create the target registry.


If the self-built Harbor is an earlier version, there is no "Tencent TCR" option for the **Provider**. Please select "Docker Registry" for **Provider** when creating a new target registry, and respectively fill in the image registry long-term access credential (user name + password) obtained in the instance management for **Access ID** and **Access Password**, instead of Tencent Cloud's SecretId and SecretKey. Under this configuration, the automatic creation of a namespace in the TCR is currently not supported.

6. <span id="createRule"></span>Choose **System Management** > **Replication Management** in the left sidebar and click **Create Rule**. Refer to the following information to create a synchronization rule.
 - **Name**: the name of the synchronization rule. You can enter a name based on the actual usage scenario.
	- **Description**: the description of the replication rule.
	- **Replication Mode**: only “Push-based” is supported.
	- **Resource Source Filter**: you can filter and select resources to be synchronized. If the field is not specified, all container images and Helm Chart resources in the self-built Harbor service are selected by default.
	- **Target Registry**: select the target registry created in [Step 3](#Step3).
	- **Target Namespace**: the namespace of the specified destination. If the field is not specified, the namespace with the same name is used by default. It is recommended that you use the default value.
	- **Trigger Mode**: by default, manual trigger is selected. If automatic synchronization is required when a new container image or Helm Chart is pushed, select “Event-driven”. It is recommended that you not select “Delete remote images at the same time when deleting local images”.
	- **Overwrite**: by default, resources with the same name are overwritten.


### Triggering synchronization and viewing the synchronization log
Push a container image and Helm Chart to the self-built Harbor service. If the trigger mode is set to “Event-driven” in the synchronization rule, the pushed resources are automatically synchronized to the Enterprise Edition instance. You can select the synchronization rule to view the synchronization log and access the Enterprise Edition instance console to check whether synchronization is successful. In this step, assume the `nginx:latest` container image is manually pushed to the self-built Harbor service to trigger synchronization.
1. Push a container image and view the image.
Push the local `nginx:latest` container image by using the docker client, access the self-built Harbor service console, and view the pushed image.
2. View the synchronization record and progress.
Choose **System Management** > **Replication Management** in the left sidebar and select the synchronization rule created in [Step 5](#createRule) to view the replication task of the synchronization rule.
3. View the synchronized image in TCR.
Access the **Image Repository** page of the TCR console and select the instance for synchronizing with the self-built Harbor service to view the container image that is successfully synchronized.

