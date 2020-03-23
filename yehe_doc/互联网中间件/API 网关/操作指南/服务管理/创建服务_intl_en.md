## Operation Scenarios
Generally, certain specific features are implemented through a group of correlated APIs. The service management module of API Gateway helps you manage such APIs in an efficient and convenient way, and you can create a service for them.

## Directions
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/) and click [API Gateway](https://console.cloud.tencent.com/apigateway/index?rid=1) at the top.
2. On the left sidebar, click **[Service](https://console.cloud.tencent.com/apigateway/service?rid=1)** to enter the service list page.
3. Under the current region, click **Create** at the top-left corner to create a service.
> After the number of services in the current region reaches the maximum of 50, no more services can be created.
4. Enter the service name and remarks and select the frontend type (HTTP, HTTPS, or HTTP/HTTPS).
![](https://main.qcloudimg.com/raw/c639838554162c971ce682416e877b9d.png)
>
>- Supported frontend types include HTTP and HTTPS, indicating the protocol types supported by the service.
>- Public network access, private network VPC access, or both can be selected. API Gateway will generate different domain names to help implement access.
> Access scope of a private network VPC domain name: CVM instances in VPCs in the same region as the service.
Private network VPC access is currently in beta test. If you want to try it out, please contact your Tencent Cloud rep or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
> - The service name can contain up to 50 characters out of `a-z`, `A-Z`, `0-9`, and `_`.
5. Click **Submit** to complete the creation.
You can click the service name to enter the service details page and create APIs. For more information, please see [API Creation Overview](
https://intl.cloud.tencent.com/document/product/628/11795).
![](https://main.qcloudimg.com/raw/fe3a6726c9abfe5095e86c91c1d0382e.png)



