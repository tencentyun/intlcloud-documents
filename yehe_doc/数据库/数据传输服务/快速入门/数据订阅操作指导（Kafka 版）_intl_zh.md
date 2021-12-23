## 相关知识

- [数据订阅功能描述](https://intl.cloud.tencent.com/document/product/571/13713)。
- [数据订阅支持的数据库](https://intl.cloud.tencent.com/document/product/571/42663)。

## 整理流程
| **操作流程**        | **说明**                                                     |
| ------------------- | ------------------------------------------------------------ |
| 1. 准备工作         | 订阅任务前，需要对网络环境做 [准备工作](https://intl.cloud.tencent.com/document/product/571/42652)。                       |
| 2. 创建数据订阅任务 | 本章节仅提供了基础的订阅任务示例，更多场景请参考 [数据订阅](https://intl.cloud.tencent.com/document/product/571/42664)。 |
| 3. 管理订阅任务     | 修改订阅对象等操作，请参考 [任务管理](https://intl.cloud.tencent.com/document/product/571/42660)。                    |
| 4. 消费订阅数据     | 管理消费组，使用 Kafka 客户端消息订阅数据，请参考 [消费订阅数据](https://intl.cloud.tencent.com/document/product/571/39538)。 |
| 5. 结束任务         | 任务完成后，需要手动结束订阅任务。                           |

## 数据订阅任务示例

1. 登录 [DTS 控制台](https://console.cloud.tencent.com/dts/dss)，在左侧导航选择**数据订阅**页，单击**新建数据订阅**。
2. 在新建数据订阅页，选择相应配置，单击**立即购买**。
3. 购买成功后，返回数据订阅列表，单击**操作**列的**配置订阅**对刚购买的订阅进行配置，配置完成后才可以进行使用。
![](https://qcloudimg.tencent-cloud.cn/raw/e3d28df3f5199d18abcb0d789994bb4c.png)
4. 在配置数据库订阅页面，选择相应配置，单击**下一步**。
![](https://qcloudimg.tencent-cloud.cn/raw/8fdd91f5a9071bbcb0e8471738113c07.png)
5. 在订阅类型和对象选择页面，选择订阅类型，单击**保存配置**。
>?订阅对象会过滤掉系统库表和命名为“test”的数据库。因为 DTS 不支持系统库表的订阅，而命名为“test”的数据库被 DTS 认为是测试数据，所以都会被过滤掉。
>
![](https://qcloudimg.tencent-cloud.cn/raw/e3bd14c693fa91096ef47f254de7200a.png)
6. 在预校验页面，预校验任务预计会运行2分钟 - 3分钟，预校验通过后，单击**启动**完成数据订阅任务配置。
>?如果校验失败，请根据失败提示在待订阅实例中进行修正，并重新进行校验。
>
![](https://qcloudimg.tencent-cloud.cn/raw/458f6897c7b200a59c5c7fa58ecd6f81.png)
7. 单击启动后，订阅任务会进行初始化，预计会运行3分钟 - 4分钟，初始化成功后进入**运行中**状态。
