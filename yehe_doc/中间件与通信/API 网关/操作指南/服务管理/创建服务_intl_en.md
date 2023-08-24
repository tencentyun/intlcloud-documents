## Scenarios
To implement a feature, we usually need to use a group of APIs. In API Gateway, you can add related APIs to a service for easy and efficient management.

## Directions
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1).
2. Click **Service** on the left sidebar.
3. Under the current region, click **Create** at the top-left corner to create a service.
> ?
>- Up to 50 services per region.
>- ‍If the current region is not the one you need, switch the region first. Note that the following regions do not support public IP access: East China (Shanghai Finance
4. Enter the service name and description, and select a frontend type.
![](https://main.qcloudimg.com/raw/c639838554162c971ce682416e877b9d.png)
>?
>- ‍**Fontend type**: The supported protocol. It supports HTTP and HTTPS.
>- **Access type**: Public network access, private network VPC access, or both can be selected. API Gateway will generate different domain names accordingly. It's only available to beta users. 
> Access scope of a private network VPC domain name: CVM instances in VPCs in the same region as the service.
Private network VPC access is in now. To try it out, contact your sales rep or [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>- The service name can contain up to 50 characters ([a-z], [A-Z], [0-9], and [_]).
5. Click **Submit** to complete the creation.
You can click the service name to enter the service details page and create APIs. For more information, please see [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795).
![](https://main.qcloudimg.com/raw/fe3a6726c9abfe5095e86c91c1d0382e.png)



