## 操作场景

通过任务详情信息，用户可查看同步任务、同步配置、结构初始化、数据初始化、监控数据等信息。

## 前提条件
已成功创建数据同步任务，并已登录 [数据同步控制台](https://console.cloud.tencent.com/dts/replication)。

## 操作步骤
- 方式1：在 [数据同步](https://console.cloud.tencent.com/dts/replication) 列表，选择指定的同步任务，单击任务名称。
- 方式2：在 [数据同步](https://console.cloud.tencent.com/dts/replication) 列表，选择指定的同步任务，在**操作**列单击**查看**。

### 同步任务页面
展示任务基本信息、源库信息以及目标库信息。
![](https://qcloudimg.tencent-cloud.cn/raw/1b9c5f80502aafacfb6abf214e248b29.png)

### 同步配置页面
展示同步任务相关配置。
![](https://qcloudimg.tencent-cloud.cn/raw/37044c19f87ec1aaedc183de3398f36f.png)

### 结构初始化页面
在同步配置中选择了**结构初始化**后，在该页面展示相关信息。

| 参数   | 描述                                             |
| ------ | ------------------------------------------------ |
| 对象名 | 目标实例中表的名称                               |
| 源库   | 源库对象的名称，包括数据库和数据表               |
| 目标库 | 目标库中对象的名称，包括数据库和数据表           |
| 状态   | 展示当前状态，若失败会展示出失败原因             |
| 操作   | 单击【查看创建语法】查看在目标库中执行的创建语法 |

![](https://qcloudimg.tencent-cloud.cn/raw/c6771f7eb82a16a24da4ef3d2b6055ad.png)

### 数据初始化页面
在同步配置中选择了**数据初始化**后，在该页面展示相关信息。
>?若处理失败，可单击**查看失败原因**排查失败原因。
>
![](https://qcloudimg.tencent-cloud.cn/raw/253e5bb2692158df8b5ce7f84c823e89.png)

### 监控数据信息展示
在还未监控到数据的情况下，默认展示 -。
![](https://qcloudimg.tencent-cloud.cn/raw/1ed0cb1972cf91aa07b9c64a3c73f45c.png)

