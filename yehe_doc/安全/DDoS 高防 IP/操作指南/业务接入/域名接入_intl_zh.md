>! 高防资源将提供 CNAME，请将 DNS 解析地址修改为该 CNAME 高防资源。CNAME 解析目的高防 IP 将不定期更换。（不涉及三网资源）。

## 接入规则
1. 登录 [DDoS 高防 IP（新版）管理控制台](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4) ，在左侧目录中，单击**业务接入** > **域名接入**。
2. 在域名接入页面，单击**开始接入**。
![](https://qcloudimg.tencent-cloud.cn/raw/c566b02296505e1ae286529ccf81988c.png)
3. 在域名业务接入页面，选择关联实例 ID，单击**下一步：协议端口**。
>? 支持多选，多实例同时接入。

![](https://qcloudimg.tencent-cloud.cn/raw/9a7e5418069c1ae134490457e8832ad1.png)
3. 选择转发协议，填写业务域名，单击**下一步：回源方式**。
![](https://qcloudimg.tencent-cloud.cn/raw/3a3fd3db21e47b9b149a478879de9ada.png)
4. 选择回源方式，填写源站 IP+端口或源站域名。如有备用源站可选中备用源站，添加备用源站及权重，单击**下一步：修改 DNS 解析**。
![](https://qcloudimg.tencent-cloud.cn/raw/e8c3114f7fbecb574180da803551f1be.png)
>? 备用源站：当源站转发异常会自动切换转发至备用源站。

5. 单击**完成**，接入的规则会出现在域名接入列表中，在接入状态查看是否接入成功。
>?
>- 当因证书问题配置失败时，接入状态右侧会冒泡提醒“因所选证书获取失败，请到 [SSL 证书管理](https://console.cloud.tencent.com/ssl) 查看详情”。
>- 当已经接入成功的域名更新证书时，会产生秒级闪断，如需更新证书，建议低峰期更新。

![](https://qcloudimg.tencent-cloud.cn/raw/21a3776933d55e8f70cab930046edacf.png)

## 配置规则
1. 在 [域名接入页面](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4)，选择所需规则，单击操作列的**配置**。
![](https://qcloudimg.tencent-cloud.cn/raw/95377ab8f1e82d357ed33f551644d1cf.png)
2. 在配置七层转发规则页面，可修改相关参数，单击**确定**保存。
![](https://qcloudimg.tencent-cloud.cn/raw/81b03bf961f2e764dac0c16dafbf38bc.png)

## 删除规则
1. 在域名接入页面，支持删除单个或批量删除规则。
 - 单个：选择所需规则，单击操作列的**删除**，弹出删除规则弹窗。
![](https://qcloudimg.tencent-cloud.cn/raw/195062b3cdaf25e6fe773c9c4e4d11cf.png)
 - 批量：选择一个或多个规则，单击**批量删除**，弹出删除规则弹窗。
![](https://qcloudimg.tencent-cloud.cn/raw/39df53e034fc0105b4585fddbc1015f8.png)
2. 在删除规则弹窗，单击**删除**，即可删除所选规则。

## 导入规则
1. 在域名接入页面，单击**批量导入**。
2. 在批量导入七层转发规则弹窗，填写所需规则，单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/d14e1161d9c788182ce88e78e2042932.png)

## 导出规则
1. 在域名接入页面，单击**导出规则**。
2. 在批量导入七层转发规则弹窗，选择所需规则，单击**复制**。
![](https://qcloudimg.tencent-cloud.cn/raw/550d61d8cd074d4634c314947d962b79.png)