>! 高防资源将提供 CNAME，请将 DNS 解析地址修改为该 CNAME 高防资源。CNAME 解析目的高防 IP 将不定期更换。（不涉及三网资源）。

## 接入规则
1. 登录 [DDoS 高防 IP（新版）管理控制台](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4) ，在左侧目录中，单击**业务接入** > **端口接入**。
2. 在端口接入页面，单击**开始接入**。
![](https://main.qcloudimg.com/raw/fd5e5fff3727183e497db5a0d643a8ce.png)
3. 在端口业务接入页面，选择关联实例 ID，单击**下一步：协议端口**。
>? 支持多选，多实例同时接入。

4. 选择转发协议，填写转发端口和源站端口，单击**下一步：回源方式**。
5. 选择回源方式，填写源站 IP+端口或源站域名。如有备用源站可选中备用源站，添加备用源站及权重，单击**下一步：修改 DNS 解析**。

>?
>- 备用源站：当源站转发异常会自动切换转发至备用源站。
>- 在端口业务接入的第二步**协议端口**。输入**转发端口**后，会判定此高防 IP 资源下此端口是否已被占用。若是被占用，无法进入下一步。

6. 单击**完成**，即可完成接入规则。

## 查询规则
在 [端口接入页面](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4)，单击搜索框通过源站 IP/域名、源站端口、关联高防 IP、转发协议和转发端口关键字对规则进行查询。
![](https://qcloudimg.tencent-cloud.cn/raw/a26bee93c987a36989e19f842c850601.png)

## 配置规则
1. 在 [端口接入页面](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4)，选择所需规则，单击操作列的**配置**。
2. 在配置四层转发规则页面，可修改相关参数，单击**确定**保存。

## 删除规则
1. 在 [端口接入页面](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4)，支持删除单个或批量删除规则。
   - 单个：选择所需规则，单击操作列的**删除**，弹出删除规则弹窗。
   - 批量：选择一个或多个规则，单击**批量删除**，弹出删除规则弹窗。
   
2. 在删除规则弹窗，单击**删除**，即可删除所选规则。

## 导入规则
1. 在 [端口接入页面](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4)，单击**批量导入**。
2. 在批量导入四层转发规则弹窗，填写所需规则，单击**确定**。

## 导出规则
1. 在 [端口接入页面](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4)，单击**导出规则**。
2. 在批量导出四层转发规则弹窗，选择所需规则，单击**复制**。