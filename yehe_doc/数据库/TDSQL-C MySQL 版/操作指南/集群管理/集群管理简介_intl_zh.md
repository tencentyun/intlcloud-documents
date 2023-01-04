本文为您介绍 TDSQL-C MySQL 集群概念、集群管理操作及如何查看集群列表。

## 集群概述
集群是包含读写实例和只读实例的一组网络资源。TDSQL-C MySQL 版最基本的管理单元为集群，一个集群中最多只能有一个读写实例，最多可以创建15个只读实例。

## 集群管理概览
| 集群管理项 | 说明 | 操作方法 |
|---------|---------|---------|
| 修改集群名 | <li>您可对集群名进行修改<li>集群名需满足的格式要求：长度小于60，由中文、英文字母、“-”、“_”、“.” | [修改集群名](https://intl.cloud.tencent.com/document/product/1098/44621) |
| 修改集群项目 | 您可对集群所属项目进行设置和修改 | [修改集群项目](https://intl.cloud.tencent.com/document/product/1098/44620) |
| 删除集群 | 请确定此集群您不再使用，再执行删除 | [删除集群](https://intl.cloud.tencent.com/document/product/1098/44619) |
| 恢复集群 | <li>您可在误删或其他需要恢复的情况下恢复已隔离状态的集群<li>回收站会显示该集群可恢复的期限</li> | [恢复集群](https://www.tencentcloud.com/document/product/1098/51182) |

## 查看集群列表
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb)。
2. 在上方选择地域，选择引擎版本为 MySQL，即可查询对应地域下的集群列表信息。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5uM8196_11.png)
