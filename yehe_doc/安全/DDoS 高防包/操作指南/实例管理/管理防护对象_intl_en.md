Anti-DDoS Pro provides stronger anti-DDoS protection for Tencent Cloud public IPs. It supports Tencent Cloud services including CVM, CLB, NAT, and WAF.

You can add or delete IPs protected by Anti-DDoS Pro instances as needed.

## Prerequisite
You have [purchased an Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/36115).
>? Anti-DDoS Pro (Enterprise) takes effect only after binding with an Anti DDoS EIP. You need to **change the cloud IP to Anti DDoS EIP**. Anti-DDoS Pro (Enterprise) must be located in the same region with the bound cloud resource. For details, see [Creating Anti DDoS EIP](https://www.tencentcloud.com/document/product/1029/54608).

## Directions
1. Log in to the [Anti-DDoS Pro Console](https://console.cloud.tencent.com/ddos/dashboard/overview) and click **Protection Instance** in the left sidebar.
2. Click the **Protected Resource** on the right of the target Anti-DDoS Pro instance.
![](https://qcloudimg.tencent-cloud.cn/raw/9e257668e6b77c35968eb6646bb982ee.png)
3. On the **Protected Resource** page, select a resource type and a resource instance as needed.
  - Resource type: Supports cloud resources with public IPs such as CVM, CLB, and WAF.

 >? Anti-DDoS Pro (Enterprise) takes effect only after binding it with an Anti DDoS EIP.

  - Select resource: To add one or more resource instances for protection, tick the checkbox for the resource ID. The number of selected resource instances cannot exceed the max number of protected IPs.
  - Selected: To delete the selected resource instance, click **Delete** on the right of it.
![](https://qcloudimg.tencent-cloud.cn/raw/043df469670222df533b20d858b64a69.png)

>?
>- Unbinding a blocked IP from Anti-DDoS Pro instances is not allowed.
>- Searching and selecting more than one associated cloud resource at once is supported.
>- CLB and CVM instances which are detected terminated will be unbound.

4. Click **OK**.