## 功能介绍
该功能可以帮助您管理 EMR 集群中的用户，快速进行集群用户的增加、编辑、删除操作，新增的用户可以用于 Hadoop 集群任务提交，本文将为您介绍用户管理的相关操作。

>!
>- 目前 EMR-V2.6.0 和 EMR-V3.2.1 版本以及之后新版本支持用户管理功能。
>- 需要手动触发 ranger-ugsync-site.xml 的配置下发，并重启 RangerUsersync 服务，用户同步才能生效。
>- 删除用户、重置密码可能导致正在运行的任务失败，需谨慎操作。

## 操作步骤
1. 登录 [弹性 MapReduce 控制台](https://console.cloud.tencent.com/emr)，在集群列表中单击集群 **ID/名称**进入集群详情页。
2. 在集群详情页，单击**用户管理**，在此页面支持批量新增用户、批量删除用户、重置密码、下载 Keytab 等功能。
 ![](https://qcloudimg.tencent-cloud.cn/raw/453da7c1b4d028a425d4f57f4c9204a6.png)
3. 单击**新建用户**，即可开始新建用户。其中，用户名、用户组、密码为必填项，备注为选填项。
 ![](https://qcloudimg.tencent-cloud.cn/raw/8c8235f44b0937bee06b25ace837b745.png)
4. 手动触发 ranger-ugsync-site.xml 的配置下发，并重启服务。
 - 登录 [弹性 MapReduce 控制台](https://console.cloud.tencent.com/emr)，在集群列表中选择对应的集群单击集群服务进入集群服务列表。
 - 在集群服务列表中，选择 Ranger 服务面板右上角**操作 > 配置管理**。
 - 进入配置管理页后，选择 ranger-ugsync-site.xml 配置文件，单击**修改配置**后，无需修改配置；单击下方**保存配置**，然后在弹窗中选择**保存并下发**。
 - 返回**角色管理**页面，选择 RangerUsersync 服务并单击**重启服务**。
5. 重置密码
在用户管理列表页面点击需要修改密码的用户的右侧操作中的**重置密码**，输入和确认新密码后单击**确定**即可完成重置。
 ![](https://qcloudimg.tencent-cloud.cn/raw/2e23f5a5a637bf25073b0fc414c2319c.png)
6. 下载Keytab
在用户管理列表页面选择需要下载 Keytab 的用户，单击**下载 Keytab** 即可。Keytab 可用于登录集群。
 ![](https://qcloudimg.tencent-cloud.cn/raw/833f681ae7ad1c40da6fd8c79084e24f.png)
>!仅支持 Kerberos 集群支持下载 Keytab。
>
7. 删除用户
在用户管理列表页面点击需要删除的用户的右侧操作中的**删除**，单击**确认删除**即可完成删除。
![](C:\Users\v_vwslwu\AppData\Roaming\Typora\typora-user-images\image-20211129151753347.png)
