## 操作场景

云数据库 Redis 支持在控制台一键清空实例所有数据。清空实例将对实例进行 **FLUSHALL** 操作，实例数据将被全部清理，且清空之后无法恢复，请谨慎操作。

## 注意事项

- 清空实例后数据将无法恢复，请务必确认完成数据备份后再提交清空。
- 清除数据过程将导致数据库访问受阻，大量数据请求时，连接数据库将断开，无法服务。
- 对全球复制组内的主实例进行清空操作，将清空复制组内所有实例数据。
- 全球复制组内的只读实例，不支持清空操作（清空操作属于写操作），您可以先将只读实例从复制组移除，再进行清空操作。

## 操作步骤

1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)。
2. 在右侧实例列表页面上方，选择地域。
3. 在实例列表中，找到目标实例。
4. 单击目标实例 ID，进入**实例详情**页面。
5. 在**实例详情**页面右上角，单击的**清空实例**。
![](https://qcloudimg.tencent-cloud.cn/raw/b2d3d24e3449235b2c826728d55c6cee.png)
6. 在**清空实例**对话框，了解清空实例的影响，在**密码**后面的输入框输入实例访问密码，单击**确定**。
>?此处需输入的密码为用户设置的实例密码，并非访问实例时所用的“实例ID:实例密码”连接密码。
7. 在左侧导航栏，单击**任务管理**，等待清空实例任务执行完成即可。

## 相关 API

| 接口名称                                                     | 接口功能      |
| :----------------------------------------------------------- | :------------ |
| [ClearInstance](https://intl.cloud.tencent.com/document/product/239/32070) | 清空 Redis 实例 |

