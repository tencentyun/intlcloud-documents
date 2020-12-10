
本文为您介绍金蝶K/3 WISE 15.0/15.1 如何接入云数据库 SQL Server，实现在 SQL Server 实例和 Windows 云服务器之间执行分布式事务。

解决方案主要分为如下三个步骤：
1. 迁移数据至云数据库 SQL Server，即将本地金蝶K/3 WISE 的账套数据库的全量数据备份恢复至云数据库 SQL Server 中。
2. 设置允许执行分布式事务，即调整云数据库 SQL Server、云服务器 CVM（Windows 系统）的访问设置，确保端口畅通，可以执行分布式事务。
3. 替换账套管理工具，以便兼容云数据库 SQL Server。

>?
>- 由于支持分布式事务配置需要额外资源，故仅支持实例规格在“1核8GB”以上的高可用版实例进行配置，在接入前请完成规格升级。
>- 调整云数据库 SQL Server 访问设置，确保可以执行分布式事务的操作，通过 [提交工单](https://console.cloud.tencent.com/workorder/category) 由腾讯工程师协助处理。提交工单前，请确保完整浏览完本文档，并已完成“迁移数据至云数据库 SQL Server”操作，可提高处理效率。


## 步骤一：迁移数据至云数据库 SQL Server
前提条件：已备份本地金蝶K/3 WISE 账套数据库文件的全量数据备份。

1. [登录 Windows 系统的云服务器](https://intl.cloud.tencent.com/document/product/213/10516#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8) ，安装金蝶K/3 WISE。
>?安装金蝶的云服务器须和云数据库 SQL Server 实例在同一个地域，且同一私有网络。
2. [创建云数据库 SQL Server 实例](https://intl.cloud.tencent.com/document/product/238/31571)。
3. 上传全量备份文件并完成数据恢复，详细步骤可参见 [上传备份至 COS](https://intl.cloud.tencent.com/document/product/238/32558) 和 [通过 COS 源文件迁移数据](https://intl.cloud.tencent.com/document/product/238/32558)。
4. 创建云数据库 SQL Server 帐号并授权，可参见 [创建帐号](https://intl.cloud.tencent.com/document/product/238/7521)。

## 步骤二：设置允许执行分布式事务
### 设置云数据库 SQL Server
调整云数据库 SQL Server 的访问设置，确保可以执行分布式事务的操作，通过 [提交工单](https://console.cloud.tencent.com/workorder/category) 由腾讯工程师协助处理。

### 设置云服务器
#### 设置安全组
1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/instance)，选择实例所在地域，单击实例 ID，进入管理页面。
2. 选择【安全组】页，编辑规则，设置如下规则：
 - “来源”的 IP 信息，可通过 [提交工单](https://console.cloud.tencent.com/workorder/category) 获取。
 - 入站规则和出站规则的“协议端口”，须开通1433、135、1024-65535端口。


#### 设置 Windows 系统
1. [登录 Windows 系统的云服务器](https://intl.cloud.tencent.com/document/product/213/10516#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8)。
2. 打开 hosts 文件，路径为`C:\Windows\System32\drivers\etc\hosts`。
3. 将云数据库 SQL Server 提供的 VIP 和 host 信息（该信息可通过 [提交工单](https://console.cloud.tencent.com/workorder/category) 获取），填写至 hosts 文件的结尾处，并保存 hosts 文件。

4. 在控制面板 > 系统和安全 > 管理工具页面打开组件服务。
5. 选择组件服务 > 计算机 > 我的电脑 > Distributed Transaction Coordinator。
6. 在右侧本地 DTC 上单击鼠标右键，选择属性。

7. 选择安全页签，参照下图进行设置，单击【确定】。

8. 在弹出的 MSDTC 服务对话框中，单击【是】，等待 MSDTC 服务重新启动完成。
 

## 步骤三：初始化账套管理
1. 下载对应的账套管理工具：金蝶K/3 WISE 15.1、金蝶K/3 WISE 15.0。
>?不同金蝶K/3 WISE 版本需要的账套管理工具不同。
2. 解压替换到金蝶的安装目录`K3ERP\KDSYSTEM\KDCOM`。
3. 打开金蝶K/3 WISE 软件。
4. 在弹出的账套管理数据库设置页面，设置相关身份验证信息和数据服务器。
>?数据服务器填写云数据库 SQL Server 实例的内网地址，内网地址可至 [控制台](https://console.cloud.tencent.com/sqlserver) 查看。
>

5. 在“系统”的下拉菜单里单击【预设连接】，设置预设连接，方便使用。

6. 在数据库的下拉菜单里单击【注册账套】。

7. 选择对应的数据库，并单击【所有】。

 
## 步骤四：登录使用金蝶K/3 WISE
全部设置完成后，云服务器 CVM 和云数据库 SQL Server 之间就能够支持分布式事务，您也可以正常登录并使用金蝶K/3 WISE。

若在登入时遇到如下报错信息：
`中间层创建事务失败，请联系系统管理员，高级显示：错误代码:5(5H)`
请参考 [金蝶官方文档](https://club.kingdee.com/club/newclub/helpDetail?product_id=3&id=366259) 进行处理。 


