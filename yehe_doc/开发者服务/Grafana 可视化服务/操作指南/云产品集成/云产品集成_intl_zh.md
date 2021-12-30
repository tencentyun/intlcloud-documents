您可以在云产品集成页面中，进行如下操作：
- 查看可用的集成
- 管理已安装集成
- 设置服务角色

## 前提条件
1. 登录 [Grafana 可视化服务控制台](https://console.cloud.tencent.com/monitor/grafana)。
2. 在列表中找到对应的 Grafana 实例。单击对应的实例 ID，进入 Grafana 实例管理页。
3. 在左侧子窗口菜单栏中单击**云产品集成**。

## 查看可用的集成
在“云产品集成”页面，您可以查看并搜索当前实例可用的集成，可对可用的集成进行安装、接入。成功接入后将会在 Grafana 面板展示集成的监控数据。
![](https://qcloudimg.tencent-cloud.cn/raw/97c03d65b8a1d30429c5c3336bbaaf6a.png)


### Prometheus
1. 单击“Prometheus”下方的**安装**，进入安装页面。
2. 数据源配置：
 - 数据源名称：输入 prometheus 实例 ID。
 - 数据源地址：填写 prometheus 内网地址，例如：`http://x.x.x.x:9090`。
 - UID: 此值为数据源的唯一 ID，建议输入 Prometheus 实例 ID。
 - 账号：您的腾讯云账号的 Appid，即 Prometheus 实例详情页中的账号。
 - 密码：Prometheus 实例详情页中的 Token。
 - 面板配置：选填，Prometheus 集成中心中的面板会通过此参数自动安装面板，无需自行填写。

2. 配置完后，单击**保存**。等待系统重建完成后即可在 Grafana 数据源页面查看已安装的 Prometheus 数据源。

### 云监控
1.单击“云监控”下方的**安装**，进入安装页面。
2. 配置数据源：
 - 数据源名称：定义数据源名称。
 - 鉴权：选择鉴权类型。
    - 使用密钥：
      - SecretID：请输入您的 SecretID。
      - SecretKey：请输入您的 SecretKey。
      ![](https://qcloudimg.tencent-cloud.cn/raw/8524cf27df323ca942dee24be0ace15d.png)
    - 使用服务角色：此选项要求您给实例设置对应权限的服务角色，详情请参考 [服务角色](https://intl.cloud.tencent.com/document/product/1124/43961)。
    ![](https://qcloudimg.tencent-cloud.cn/raw/cf3611a9478563ef509a3ef7b9a729f9.png)
3. 配置完后，单击**保存**。等待系统重建完成后即可在 Grafana 数据源页面查看已安装的 Prometheus 数据源。

### 日志服务
1. 单击“日志服务”下方的**安装**，进入安装页面。
   ![](https://qcloudimg.tencent-cloud.cn/raw/d9bf38b5b8ed5d6695c587bf7ee1cd5f.png)
2. 配置数据源：
 - 数据源名称：定义数据源名称。
 - SecretID：请输入您的 SecretID。
 - SecretKey：请输入您的 SecretKey。
3. 配置日志服务。
 - Region：地区例如：ap-guangzhou，完整列表请参考 [可用地域](https://intl.cloud.tencent.com/document/product/614/18940)。
 - TopicId：日志主题，详情请参考 [日志主题](https://intl.cloud.tencent.com/document/product/614/32849)。
4. 配置完后，单击**保存**。等待系统重建完成后即可在 Grafana 数据源页面查看已安装的 Prometheus 数据源。


## 管理已安装集成

选择**集成列表**，查看当前已安装的集成。已安装集成可能是用户自行安装，也可能是云服务通过绑定关系自动安装。在操作列中您可以对已云产品集成进行删除。
![](https://qcloudimg.tencent-cloud.cn/raw/1afadce4f33c829bbf6720f90f1bc854.png)
