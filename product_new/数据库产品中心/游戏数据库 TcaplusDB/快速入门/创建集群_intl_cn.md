## 操作场景
本文为您介绍如何通过控制台创建 TcaplusDB 集群。

##  前提条件
已 [注册腾讯云账号](https://intl.cloud.tencent.com/document/product/378/17985)，并  [实名认证成功](https://intl.cloud.tencent.com/document/product/378/3629)。

## 操作步骤
1. 登录 [TcaplusDB 控制台](https://console.cloud.tencent.com/tcaplusdb/app)，在左侧导航选择【集群列表】页，单击【创建集群】。
2. 在弹出的新建集群对话框，配置集群信息。
 - **网络类型**：选择私有网络 VPC 及子网 Subnet，每个集群只能在创建时选定私有网络和子网，创建完成后不能修改。
 - **连接协议**：选择 TcaplusDB 集群连接协议（数据描述协议）。
 - **集群名称、访问密码**：同账号下集群名称不能重复，访问密码必须是 a - z、A - Z、0 - 9 的字符，且必须包含数字和大小写字母。
![](https://main.qcloudimg.com/raw/403156d42bf01dec755e6b169c77b160.png)
3. 单击【创建集群】，系统将会提示创建成功。
返回集群列表可查看创建完的集群，系统会为每个集群分配一个唯一的集群 ID。
![](https://main.qcloudimg.com/raw/7612056a6d9420ffb5697c0243c0e7d4.png)
