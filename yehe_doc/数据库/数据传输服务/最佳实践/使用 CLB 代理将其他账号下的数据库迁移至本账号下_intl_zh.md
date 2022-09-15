## 操作场景
本场景为您介绍通过负载均衡 CLB 做代理服务，建立源数据库和 DTS 的网络连接，适用于将其他腾讯云账号下关联的 IDC 自建数据库或是其他云厂商数据库，迁移/同步至本账号下，同时执行任务的账号权限受限的场景，举例如下。

- VPC-A 和 VPC-B 为集团公司网络，VPC-C 为子公司网络，账号 C 没有操作 A 和 B 资源的权限。
- 账号 A 下建立专线打通自建 IDC 网络或者第三方云厂商网络，账号 B 下通过云联网连通 VPC-A、VPC-B 和 VPC-C，所以虚线框中的网络都已打通，账号 C 可以访问到源数据库。
- 使用账号 C 进行 DTS 迁移/同步。

针对这种场景，可以通过 CLB 关联源数据库，因为 CLB 有跨账号关联网络能力，将 CLB 作为 DTS 的代理服务进行路由转发。关键配置原则如下：
1. 使用 C 账号创建 CLB 实例。
2. 在 CLB 上配置后端服务，将源数据库 IP 绑定在后端服务中。
3. 创建迁移/同步任务，源数据库的 IP 地址和端口，填写 CLB 的地址和端口。

## 操作步骤
### 使用 C 账号创建 CLB 实例
1. 使用 C 账号登录腾讯云 [负载均衡购买页](https://buy.intl.cloud.tencent.com/lb)。
2. 配置负载均衡相关参数。选择**按量计费**，和**内网**类型。
3. 返回负载均衡**实例管理**页面，查看 VIP，后续 DTS 配置中需要使用。
   ![](https://qcloudimg.tencent-cloud.cn/raw/ba3f69595bf2f21ae8df95e88bad5fdb.png)

### 将源数据库 IP 绑定在 CLB 后端服务中
> ? 如下指导中的 CLB 操作仅提供参考，如果实际控制台界面有差异，请以 [CLB 官网文档](https://intl.cloud.tencent.com/document/product/214/38442) 为准。

1. 在负载均衡**实例管理**页面，找到刚才购买的负载均衡实例，单击实例 ID。
2. 在**基本信息**页面的**后端服务**区域， 启用绑定非本 VPC 内 IP 的功能，单击**点击配置**。
   ![](https://qcloudimg.tencent-cloud.cn/raw/70adcb0459a06a353058098f23b25a5f.png)
3. 在弹出的对话框中，单击**提交**。
   ![](https://qcloudimg.tencent-cloud.cn/raw/c00934610178e8b32719aee58a86c4a5.png) 
4. 开启后，在后端服务模块会显示新增 SNAT IP，单击**新增 SNAT IP**。
   ![](https://qcloudimg.tencent-cloud.cn/raw/84735d9ce8f922c8fd3fd9a73b21dbdb.png)
5. 在弹出的对话框中，选择子网，然后单击**新增**分配 IP，最后单击**保存**。
6. 配置 SNAT IP。
7. 创建 CLB 监听器。在实例详情页面，单击**监听器管理**页签，然后在 TCP/UDP/TCP SSL/QUIC 监听器下，单击**新建**。
   ![](https://qcloudimg.tencent-cloud.cn/raw/7dc7b16f1020912d5c8b57cc030cad26.png)
8. 在弹出的对话框中配置 TCP 监听器。 健康检查和会话保持，可自行选择是否开启。
9. 监控器配置完成后，单击已创建的配置器，在右侧单击**绑定**，绑定源数据库 IP 地址。
   ![](https://qcloudimg.tencent-cloud.cn/raw/91b459e636f74b5df223efa75459a2e8.png)
10. 在弹出的对话框中，选择**其他内网 IP**，输入需绑定的源数据库 IP 地址，并填写端口与权重， 最后单击**确认**。
      ![](https://qcloudimg.tencent-cloud.cn/raw/0b54092cef7ff8884a9c3254eb433ce3.png)
11. 返回**已绑定后端服务**区域可以查看已绑定的源数据库 IP。

### 配置 DTS 任务
使用 CLD 代理的 DTS 配置步骤，与普通的 [DTS 数据迁移任务](https://intl.cloud.tencent.com/document/product/571/42645) 或 [DTS 数据同步任务](https://intl.cloud.tencent.com/document/product/571/47344) 配置步骤基本一致，这里仅对差异点进行详细介绍。

使用 C 账号购买数据迁移/同步任务后，在**设置源和目标数据库**步骤中，接入方式选择**私有网络 VPC**（需要 [提交工单](https://console.cloud.tencent.com/workorder/category) 申请开通），私有网络及子网选择 C 账号的 VPC 和子网，主机地址填入 CLB 实例的 VIP 地址。

![](https://qcloudimg.tencent-cloud.cn/raw/b0a64971c3df79f56f9d851c69e3c802.png)
