
根据腾讯云安全防范要求，2022年4月8日起将对数据库智能管家 DBbrain 直连 API 接口增加 CAM 鉴权访问，为保证升级后您可以正常使用对应接口，请在2022年4月8日前登录腾讯云 [访问管理控制台](https://console.cloud.tencent.com/cam/policy) 添加对应接口的授权访问。

## 注意事项
本次授权仅对使用 DBbrain 只读访问权限（QcloudDBBRAINReadOnlyAccess）的用户，使用 DBbrain 全读写访问权限（QcloudDBBRAINFullAccess）的用户不需要进行本次授权。

## 接入 CAM 鉴权的 API 列表（共8个）

| 接口名称                                                     | 接口功能                           | 接口类型 |
| ------------------------------------------------------------ | ---------------------------------- | -------- |
| [DescribeSlowLogUserHostStats](https://intl.cloud.tencent.com/document/product/1035/41182) | 获取慢日志来源地址统计分布图       | 资源级   |
| [DescribeUserSqlAdvice](https://intl.cloud.tencent.com/document/product/1035/41181) | 获取 SQL 优化建议                  | 资源级   |
| [DescribeMySqlProcessList](https://intl.cloud.tencent.com/document/product/1035/41193) | 查询实时线程列表                   | 资源级   |
| [DescribeTopSpaceSchemas](https://intl.cloud.tencent.com/document/product/1035/41189) | 获取 Top 库的空间统计信息          | 资源级   |
| [DescribeDBDiagEvents](https://intl.cloud.tencent.com/document/product/1035/44292) | 获取诊断事件列表                   | 接口级   |
| [DescribeProxySessionKillTasks](https://intl.cloud.tencent.com/document/product/1035/45410) | 查询代理节点 Kill 会话任务执行状态 | 资源级   |
| [DescribeDiagDBInstances](https://intl.cloud.tencent.com/document/product/1035/41195) | 获取实例列表接口                   | 接口级   |
| [CreateProxySessionKillTask](https://intl.cloud.tencent.com/document/product/1035/44869) | 创建中止代理节点会话的任务         | 资源级   |

## 授权操作指导

1. 登录 [访问管理控制台](https://console.cloud.tencent.com/cam/overview)。
2. 在左侧导航栏，单击**策略**。

#### 资源级接口

选择**新建自定义策略** > **按策略生成器创建**，配置对应的策略参数。
- 服务：数据库智能管家 (dbbrain) 。
- 资源：可以选择指定实例，也可选择全部资源。

#### 接口级接口
选择**新建自定义策略** > **按策略生成器创建**，配置对应的策略参数。
- 服务：数据库智能管家 (dbbrain) 。
- 资源：无法指定实例，选择全部资源即可。

