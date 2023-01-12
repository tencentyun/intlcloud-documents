本文为您介绍如何通过云数据库 MySQL 控制台查看数据库代理节点监控。

## 前提条件
已 [开通数据库代理](https://www.tencentcloud.com/document/product/236/42052)。

## 支持的监控指标

| 指标项中文名 | 单位 | 说明 |
|---------|---------|---------|
| 当前连接数 | 个 | 当前节点访问连接个数 |
| 请求数 | 次/秒 | 访问节点的请求数 |
| 读请求数 | 次/秒 | 读操作请求数 |
| 写请求数 | 次/秒 | 写操作请求数 |
| CPU 利用率 | % | CPU 的使用情况 |
| 内存利用率 | % | 内存利用情况 |
| 内存占用 | MB | 已使用内存情况 |

## 操作步骤
**方法一：**
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，选择已开启代理的主实例，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
2. 在实例管理页面，选择**数据库代理** > **性能监控**页，单击节点名称切换查看各代理节点监控。
>?粒度为5秒的监控，时间跨度4小时内的监控默认切换为粒度5秒。
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/pMhC112_7.png)

**方法二：**

1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，选择已开启代理的主实例，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
2. 在实例管理页面，选择**数据库代理** > **概览**，在**代理节点**列，单击目标节点 ID 后的![](https://qcloudimg.tencent-cloud.cn/raw/f3f75f219f501d9b6836b3f542e49ed4.png)图标，可直接跳转查看该节点的性能监控情况。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QtfL186_9.png)
跳转后界面如下。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/2HR2348_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_1673407877191.png)
