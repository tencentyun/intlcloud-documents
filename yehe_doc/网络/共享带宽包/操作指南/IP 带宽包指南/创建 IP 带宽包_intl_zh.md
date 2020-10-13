本文将为标准账户类型的用户介绍，如何创建 IP 带宽包。
>? 
>- 目前共享带宽包处于内测阶段，如需使用，请提交 [内测申请](https://intl.cloud.tencent.com/apply/p/86ulv50u1e8)。
>- 标准账户类型仅能创建 IP 带宽包，账户类型判断方式，请参见 [区分账户类型](https://intl.cloud.tencent.com/document/product/684/15246)。
>- 传统账户类型可以 [提交工单](https://console.cloud.tencent.com/workorder/category) 申请修改账户类型为标准账户类型，以使用 IP 带宽包。

1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1)。
2. 单击左侧导航的【共享带宽包】。
3. 选择地域，单击左上角的【+新建】。
4. 在弹窗中，输入名称、选择计费类型，单击【确定】完成创建。
![](https://main.qcloudimg.com/raw/6aac805bcb27daeb1a6ac01fd07c6078.png)
5. 创建完成后，为了防止产生高额费用，建议您为带宽包内的资源设置带宽上限。可参考如下操作：
 - EIP 设置带宽上限：
    1. 登录 [EIP 控制台](https://console.cloud.tencent.com/cvm/eip)。
    2. 在操作栏下，选择【调整网络】进行带宽上限的设置。
    
 - 负载均衡设置带宽上限：
    1. 登录 [负载均衡控制台](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3)。
    2. 在操作栏下，选择【更多】>【调整带宽】进行带宽上限的设置。
		
		
