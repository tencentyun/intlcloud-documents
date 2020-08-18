Currently, a public network CLB instance supports cross-region binding of CVM. You can select the region of real servers and bind them across VPCs or regions. For cross-region binding in Mainland China, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1) for application. For cross-region binding outside Mainland China, please [contact your Tencent Cloud rep](https://console.cloud.tencent.com/workorder/category).

>Cross-region CVM instance binding is currently not supported for private network CLB and classic CLB.

## Use Cases
1. This feature can meet the needs of P2P and other gaming businesses to access the server from multiple regions. For example, if your real server cluster is deployed in Guangzhou, you can create CLB instances in Shanghai and Beijing and bind them to the same real server cluster in Guangzhou for game acceleration and traffic convergence, effectively ensuring the data transfer quality and reducing the latency.
2. This feature can meet the needs in financial business and payment scenarios by effectively ensuring the transfer quality and consistency of data in key businesses.
![](https://main.qcloudimg.com/raw/b61f652d7100166236b4b7b0e6a26f43.png)

## Operation Examples
After purchasing a public network CLB instance, you can view the region attribute of the real server on the instance details page. At the time of purchase, the region attribute of the real server is the same as that of the CLB instance by default.
If a public network CLB instance has been bound to a CVM instance in the same region, you need to unbind the CVM instance first before switching the region.
![](https://main.qcloudimg.com/raw/b5b03db3b9df5ae38acde5e23449b57c.png)

Click **Edit** to modify the region and network attributes of the real server. Fees for cross-region binding will be charged daily by bandwidth. After the modification is completed, you can select a CVM instance in the corresponding backend region on the CVM instance binding page for cross-region binding. **Currently, only real servers in the same region can be bound.**
![](https://main.qcloudimg.com/raw/93443dfb2eb35da82c50a7032df0ae0a.png)

>
> - Currently, one CLB instance can be bound to CVM instances in only one region. For example, one CLB instance in Beijing can be bound to CVM instances in Beijing but cannot be bound to CVM instances in Beijing and Shanghai at the same time.
> - After you modify the region attribute of the backend CVM instance, if the new region is different from that of the CLB instance, you cannot change back to the original same-region binding.
> - Currently, it is not allowed to bind CLB instances to CVM instances across VPCs in the same region.
> - Classic network-VPC binding is supported.

