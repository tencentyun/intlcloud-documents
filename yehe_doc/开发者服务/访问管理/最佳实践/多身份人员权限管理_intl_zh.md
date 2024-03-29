## 操作背景

当您的企业涉及不同身份管理人员时，通过 CAM 进行权限划分，对不同身份的人员授予不同的权限，方便管理和控制。本文档以一个典型案例让您轻松了解如何实现子账号不同身份的管理权限。

假设存在以下条件：
- 企业帐号 CompanyExample 下有两个运维人员 DevA、DevB。 
- 运维人员 DevA 为公司服务器运维人员，企业帐号 CompanyExample 该运维人员拥有云服务器（CVM）的全部操作权限。
- 运维人员 DevB 为公司云数据库 MySQL 运维人员，企业帐号 CompanyExample 该运维人员拥有云数据库 MySQL 的全部操作权限。


## 操作步骤

1. 使用企业账号  CompanyExample 登录 [访问管理控制台](https://console.cloud.tencent.com/cam)。
2. 通过 [自定义创建子用户](https://intl.cloud.tencent.com/document/product/598/13674) 创建用户名分别为 DevA、DevB 的两个子账号。
3. 在 [用户列表](https://console.cloud.tencent.com/cam) 页面搜索找到刚才已创建的子账号 DevA，单击右侧操作列下的【授权】，如下图：
![](https://main.qcloudimg.com/raw/68e813264316ad2ef97249077068634c.png)
4. 在弹出的关联策略窗口，搜索勾选  QcloudCVMFullAccess，单击【确定】，如下图：
![](https://main.qcloudimg.com/raw/445d5cf9dccc8c4c822faf71610f435b.png)
5. 参考步骤2和3，为子账号 DevB 关联 QcloudCDBFullAccess 权限。
6. 授权成功后，子账号 DevA 则拥有云服务器（CVM）的全部操作权限，子账号 DevB 则拥有云数据库 MySQL 的全部操作权限。
>?如需将 CAM 用户配置为其他角色，可按照以上流程操作，只需参考步骤2和3搜索并勾选相应的权限策略名。具体权限可参考 [系统权限](#系统权限)。

[](id:系统权限)

## 系统权限

<table>
<tr><th width="20%">负责人</th><th width="40%">策略名称</th><th width="40%">策略说明</th></tr><tr>
<td>管理员</td>
<td>AdministratorAccess</td><td>该策略允许您管理账户内所有用户及其权限、财务相关的信息、云服务资产。</td>
</tr><tr>
<td>财务管理员</td>
<td>QCloudFinanceFullAccess</td><td>该策略允许您管理账户内财务相关的内容，例如：付款、开票。</td>
</tr><tr>
<td rowspan="4">数据库管理员</td>
		<td>QcloudCynosDBFullAccess</td>
		<td>云原生数据库 TDSQL-C 全读写访问权限</td>
	</tr>
  <tr>
		<td>QcloudMariaDBFullAccess</td>
		<td>云数据库 MariaDB 全读写访问权限
</td>
	</tr>
    <tr>
		<td>QcloudSQLServerFullAccess
</td>
		<td>云数据库 SQL Server 全读写访问权限
</td>
	</tr>
      <tr>
		<td>QcloudCDWPGFullAccess
</td>
		<td>云数据仓库 PostgreSQL（CDWPG）全读写访问权限
</td>
	</tr>
  <td rowspan="3">网络管理员</td>
<td>QcloudCLBFullAccess</td><td>负载均衡（CLB）全读写访问权限
</td>
</tr>
<tr>
		<td>QcloudVPCFullAccess</td>
		<td>私有网络（VPC）全读写访问权限</td>
	</tr>
  <tr>
		<td>QcloudDCFullAccess</td>
		<td>专线接入（DC）全读写访问权限
</td>
	</tr>
<td rowspan="2">监控管理员</td>
<td>QcloudMonitorFullAccess</td><td>云监控（MONITOR）全读写访问权限，包括查看用户组的权限
</td>
</tr>
<tr>
		<td>QcloudCATFullAccess</td>
		<td>云拨测（CAT）全读写访问权限</td>
	</tr>
</table>



