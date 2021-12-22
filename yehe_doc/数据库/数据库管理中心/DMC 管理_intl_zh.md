本文主要为您介绍 DMC 控制台的新建库表、库管理、实例监控、实例会话、表数据可视化编辑等功能。

## 新建库表
1. 登录 [DMC 控制台](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)，在导航栏选择**新建** > **新建库** > **新建数据库**或**新建** > **新建表**。
![](https://qcloudimg.tencent-cloud.cn/raw/21c9ca3e61a0c67054b85ba9035131d4.png)
2. 在弹出的对话框，对新建的库表进行相关配置。
>?字符集、排序规则介绍可参见 [MySQL 官方文档](https://dev.mysql.com/doc/)。
>
 - 新建库对话框：
![](https://qcloudimg.tencent-cloud.cn/raw/c289a718db9b8e5b1ba26e8214b3a2bb.png)
 - 新建表对话框：
![](https://qcloudimg.tencent-cloud.cn/raw/f507d945618902b19f5304a8b08acb63.png)

## 库管理
登录 [DMC 控制台](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)，在导航栏单击**库管理**，进入数据库管理页面，用户可新建、编辑、删除数据库。
![](https://qcloudimg.tencent-cloud.cn/raw/278e378f5cb5f2690d7965017e2ec6f7.png)

## 实例会话
登录 [DMC 控制台](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)，在导航栏单击**实例会话**，进入实例会话页面，用户可查看当前数据库中所有实例的会话详细信息，以及按照会话概览、用户、访问来源和数据库四个不同维度的信息展示。
DMC 提供 kill 会话的功能，方便用户对会话进行管理。
![](https://qcloudimg.tencent-cloud.cn/raw/ab05ae2ce700317eaca2f2854f6b5ac5.png)

## SQL 窗口
登录 [DMC 控制台](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)，单击顶部导航中的**SQL 窗口**，或者左侧栏表格**操作**菜单中的**SQL 操作**进入SQL 窗口页面。SQL 窗口支持如下功能：
- SQL 命令执行及结果查看
- SQL 格式优化
- 查看 SQL 命令执行计划
- 常用 SQL 保存
- 模板 SQL
- SQL 结果导出
![](https://qcloudimg.tencent-cloud.cn/raw/b18a3f9326246eed52c84970ab0eb1ee.png)

## 数据管理
登录 [DMC 控制台](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login)，在导航栏选择**数据管理** > **数据导入**或**数据导出**，可对数据库进行数据导入导出操作。
![](https://qcloudimg.tencent-cloud.cn/raw/bb2049f5fef3864bf21f3847c49bbe57.png)

## 表数据可视化编辑
DMC for MySQL 增加了对数据增删改的支持。用户可在左侧栏单击**数据表**，对表数据进行批量的增、删、改操作，修改完成后，在**快捷操作**栏单击**确定**预览本次修改的 SQL 语句，二次确认后将批量执行修改。
![](https://qcloudimg.tencent-cloud.cn/raw/de8b920772749a6bbbcf5faa5f0c463d.png)