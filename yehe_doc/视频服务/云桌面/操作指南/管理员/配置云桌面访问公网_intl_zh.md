## 操作步骤
### 步骤1: 新建 NAT 网关
1. 打开 [NAT 网关控制台](https://console.cloud.tencent.com/vpc/nat?rid=1)，单击 **新建**。（确保所选区域与云桌面所在区域相同）
![](https://qcloudimg.tencent-cloud.cn/raw/0456c7b59e97c030d5b66d09395beee7.png)
2. 输入网关名称，所属网络选择云桌面所在 VPC，网关类型及出带宽上限根据企业实际需求进行选择（创建完成后可更改），弹性 IP 选择 **新建弹性 IP** ，确认无误后单击下方 **立即开通**。
<img style="width:700px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/5d31698fc1e8c434793e433e1580bd65.png" />
3. 确认信息无误后，单击 **确认订单**。
<img style="width:700px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/8bf2b471cf1d82997244c998abcd0a05.png" />
4. 完成 NAT 网关创建。
![](https://qcloudimg.tencent-cloud.cn/raw/64b300d8f0e3785fa9ffec80f828e569.png)

### 步骤2: 配置路由表
1. 打开 [路由表控制台](https://console.cloud.tencent.com/vpc/route?rid=1)，单击对应的路由表，编辑路由表。
![](https://qcloudimg.tencent-cloud.cn/raw/04eab214cf8d02d4aad0001028445c34.png)
2. 单击 **新增路由策略**。
![](https://qcloudimg.tencent-cloud.cn/raw/04b975c22996f51349ff7739db168f04.png)
3. 新增路由目的端填写“0.0.0.0/0”、下一跳类型选择 **NAT 网关**，下一跳选择刚才创建的 NAT 网关。
![](https://qcloudimg.tencent-cloud.cn/raw/35001bab62e50f401631c7d4c1bfedb0.png)
>! 目的端填写“0.0.0.0/0”代表将所有出网流量都指向 NAT 网关。

4. 检查确认新建的路由策略处于**启用状态**，此时可在云桌面内实现访问互联网。
![](https://qcloudimg.tencent-cloud.cn/raw/614be31065f8f1cda5633f39d2339244.png)
