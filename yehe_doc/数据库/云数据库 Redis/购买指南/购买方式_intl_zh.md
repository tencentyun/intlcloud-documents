
腾讯云为您提供了两种方式购买云数据 Redis：控制台购买和 API 购买。

## 控制台购买
1. 登录 [Redis 购买页](https://buy.intl.cloud.tencent.com/redis)，根据您的实际需求选择配置，确认无误后，单击**立即购买**。
  - **计费模式**：支持按量计费。
    - 若业务量有瞬间大幅波动场景，建议选择按量计费。
 - **地域**：选择您业务需要部署 Redis 的地域。建议您选择与云服务器同一个地域，不同地域的云产品内网不通，购买后不能更换。
 - **产品版本**：支持内存版，基于开源 Redis 引擎的高性能版本，兼容 Redis 2.8、4.0、5.0。
 - **兼容版本**：兼容 Redis 2.8、4.0、5.0。其中，2.8版暂停售卖，建议您选择4.0及以上版本，如需购买2.8版本请 [提交工单](https://console.cloud.tencent.com/workorder/category) 申请。
 - **架构版本**：支持标准架构、集群架构。
 - **副本数量**：Redis 2.8 标准版支持0 - 1个副本。Redis 4.0、5.0 标准版支持1 - 5个副本。Redis 4.0、5.0 集群版支持1 - 5个副本。
  - **网络类型**：云数据库 Redis 所属网络，建议您选择与云服务器同一个地域下的同一 [私有网络](https://intl.cloud.tencent.com/document/product/215)，实例购买后支持基础网络转换为 VPC 网络，不支持 VPC 网络转换为基础网络。
 - **可用区**：选择主节点和副本组的可用区，相对单可用区实例，多可用区实例具有更高的可用性和容灾能力，请参见 [多可用区部署](https://intl.cloud.tencent.com/document/product/239/39812)。
 - **端口**：自定义端口号需在1024到65535之间。
 - **参数模板**：通过使用参数模板，您可以实现批量参数设置，请参见 [使用参数模板](https://intl.cloud.tencent.com/document/product/239/41810)。
 - **指定项目/安全组**：指定数据库的项目和 [安全组](https://intl.cloud.tencent.com/document/product/239/31945)。
 - **实例名/设置密码**：实例名和密码支持直接设置和创建完后在实例列表进行设置。
2. 购买完成后，返回实例列表，待实例状态显示为**运行中**，即可正常使用。
3. （可选）修改实例名，在实例列表的**实例 ID / 名称**列，单击以下小图标可修改实例名。
![](https://qcloudimg.tencent-cloud.cn/raw/a73ef77b663048109c3fffc74eb01391.png)

## API 购买
通过 API 购买云数据库 Redis 的用户，可参考 API 文档 [创建实例](https://intl.cloud.tencent.com/document/product/239/32069)。

