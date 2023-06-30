
## Overview

After private network access is enabled for the current cluster, TKE will access the cluster through the domain name by default. You need to configure `Host` on the access server to perform DNS queries on the private network. If no DNS rules (`Host`) are configured, an error "no such host" will be reported when you access the cluster on the access server (by running `kubectl get nodes`) as shown below:
![](https://main.qcloudimg.com/raw/2d03150adb99805447c57896cf5866d1.png)

In practice, configuring `Host` will increase your management labor costs. Therefore, we recommend you use Tencent Cloud's newly launched [Private DNS](https://intl.cloud.tencent.com/document/product/1097) service, which helps you get things done in just three steps.  




#### Billing description

Private DNS is billed on a pay-as-you-go basis, where the number of private domains and that of DNS requests are billed on a natural day basis. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1097/40555).  

#### Available regions

Currently, Private DNS is not available in all the available regions of TKE. For the list of its available regions, see [Use Limits](https://intl.cloud.tencent.com/document/product/1097/40553).  

To access clusters over the private network in regions not covered by Private DNS, you need to manually configure the `Host`. To use Private DNS in those regions, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.  


## Prerequisites

A container cluster has been created and private network access has been enabled. For details, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).  


## Directions

### Activating Private DNS

See [Activating Private DNS](https://intl.cloud.tencent.com/document/product/1097/40557).  

### Creating private domain

1. Log in to the [Private DNS console](https://console.cloud.tencent.com/privatedns/domains).  
2. Click **Create Private Domain** and configure the following options (just use the default values for other parameters). For more information, see [Creating Private Domain](https://intl.cloud.tencent.com/document/product/1097/40558).  
![](https://qcloudimg.tencent-cloud.cn/raw/52522159398c2472063c3b9d88b82e0e.png)
 - **Domain**: Enter `tencent-cloud.com` (domain name allocated by TKE for accessing the cluster).  
 - **Associated VPC**: Select the node VPC that needs to access the cluster.  
3. Click **OK**.  



### Configuring DNS records

1. Click the private domain name created above to enter the **DNS Records** page.  
2. Click **Add Records** and configure the following options:
   ![](https://qcloudimg.tencent-cloud.cn/raw/1fad9068e0a26441bbc83835ad430ea4.png)
   - **Host Record**: Enter the secondary domain name for accessing the TKE cluster, for example, `cls-{{clsid}}.css`.  
   - **Record Type**: Enter `A`.  
   - **Record Value**: Enter the private IP for accessing the TKE cluster.  
>?**You can get the **Host Record** and **Record Value** from **[Cluster Management](https://console.cloud.tencent.com/tke2/cluster?rid=1)** > **Cluster** > **Basic Info**. Here, **Host Record** is the domain name in **Access Address**, and **Record Value** is the IP address in **Private Network Access**, as shown below:
>![](https://qcloudimg.tencent-cloud.cn/raw/cb08a884fed0089a638cc2b4605cb1c5.png)
>
>3. Click **Save** in the **Operation** column on the right.  



### Verifying effect

1. Run the following command to access the cluster again.  
```sh
kubectl get nodes
```
2. When the following result is displayed, the cluster has been successfully accessed, and the node list has been pulled.  
![](https://main.qcloudimg.com/raw/95130bf7fa52376c21c11464b25a2741.png)
