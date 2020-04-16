- Currently, a public network CLB instance can be bound to CVM instances in another region. This feature allows you to select the region for real servers and bind CLB instances to them across VPCs or regions. To try it out, please submit a [ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1) for application for cross-region binding in Mainland China or [contact your Tencent Cloud rep](https://intl.cloud.tencent.com/contact-sales) for cross-region binding outside Mainland China.

> CVM cross-region binding is not supported for private network CLB or classic CLB instances for the time being.

## Use Cases
1. The cross-region binding feature can well meet the needs in P2P gaming scenarios where the same server is shared by global players. For example, if your real server cluster is deployed in Guangzhou, and you want to create CLB instances in Shanghai and Beijing and bind them to the same real server cluster in Guangzhou, so that gaming access can be accelerated and traffic can be converged. To this end, you can use this feature to effectively guarantee the quality of data transfer and reduce access latency.
2. In financial transaction and order payment scenarios, the transfer quality and consistency of key business data can be effectively guaranteed.
 ![](https://main.qcloudimg.com/raw/b61f652d7100166236b4b7b0e6a26f43.png)

## Operation Examples
After purchasing a public network CLB instance, you can view the region of its real server on its details page, which is the same as its region by default.
If a public network CLB instance has been bound to a CVM instance in the same region, you need to unbind the CVM instance first before switching regions.
![](https://main.qcloudimg.com/raw/a08b2e4d081128fea933ca8c1c82f793.png)

Click **Edit** to modify the region and network attributes of the real server. Bandwidth fees incurred by cross-region binding will be charged daily by bandwidth. After the modification is completed, you can select a CVM in the corresponding region on the CVM instance binding page for cross-region binding. **Currently, only real servers in one region can be bound.**
![](https://main.qcloudimg.com/raw/c722452b95399eea662844c78f32e823.png)

>
> - Currently, one CLB instance can be bound to CVM instances only in one region. For example, a CLB instance in Beijing can be bound to CVM instances in Shanghai, but it cannot be bound to CVM instances in both Beijing and Shanghai at the same time.
> - After you change the region of a real server to one different from that of the CLB instance, it cannot be changed back to the original region for binding.
> - Currently, cross-VPC binding is not allowed for CLB instances and CVM instances in the same region.
> - Cross-basic network/VPC binding is supported.

## Billing Description
Cross-region binding is implemented based on cross-region peering connection. For more information on billing, please see [Billing Description](https://intl.cloud.tencent.com/document/product/214/8848).
