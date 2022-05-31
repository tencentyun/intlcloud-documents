当您的自定义域名接入云点播后，系统会为您自动分配一个 CNAME 域名（以 .cdn.dnsv1.com 为后缀)，您可在云点播控制台 [域名管理](https://console.cloud.tencent.com/vod/distribute-play/domain) 进行查看。自动分配的CNAME 域名不能直接访问，您需要在域名服务提供商处完成 CNAME 配置，配置生效后，即可正常访问。

![](https://qcloudimg.tencent-cloud.cn/raw/9ddc932f9b5072705d5d155f7ed2c8b5.png)

## 万网设置方法
若您的 DNS 服务商为万网，您可通过如下步骤添加 CNAME 记录。
1. 登录万网会员中心。
2. 单击会员中心左侧导航栏中的【产品管理】> 【我的云解析】进入万维网云解析列表页。
3. 单击要解析的域名，进入解析记录页。
4. 进入解析记录页后，单击新增解析按钮，开始设置解析记录。
![](https://main.qcloudimg.com/raw/b122299f088cee9c9f1a0a044f34a232.png)
5. 若要设置 CNAME 解析记录，将记录类型选择为 CNAME。主机记录即域名前缀，可任意填写（如：`www`）。记录值填写为当前域名指向的另一个域名。解析线路，TTL 默认即可。
![](https://main.qcloudimg.com/raw/bff5be116fd6e0cd73ec26ce91ecfb1e.png)
6. 填写完成后，单击【保存】，完成解析设置。

## 新网设置方法
若您的 DNS 服务商为新网，您可通过如下步骤添加 CNAME 记录。
**设置别名（CNAME 记录）**
即：别名记录。这种记录允许您将多个名字映射到同一台计算机。通常用于同时提供 WWW 和 MAIL 服务的计算机。例如，有一台计算机名为`host.mydomain.com`（A记录）。它同时提供 WWW 和 MAIL 服务，为了便于用户访问服务。可以为该计算机设置两个别名（CNAME）：WWW 和 MAIL 。如下图：
![](https://main.qcloudimg.com/raw/2e93d51c7fe8502670475d71bbfb20cb.png)

## 验证 CNAME 是否生效
不同的 DNS 服务商，CNAME 生效的时间略有不同，一般会在半个小时之内生效。您可以通过以下方式查询 CNAME 是否配置生效。
- 方法一：【开始】→【运行】→输入 cmd 并回车，输入 PING 命令来查询 CNAME 是否生效，如果返回的解析结果与该域名的 CNAME 值一致，则 CNAME 已配置生效。
![](https://main.qcloudimg.com/raw/3ecec823ae0159bc114754a8a3875ff9.png)
- 方法二：【开始】→【运行】→输入 cmd 并回车，输入 nslookup 命令来查询 CNAME 是否生效，如果返回的解析结果与该域名的 CNAME 值一致，则 CNAME 已配置生效。
![](https://main.qcloudimg.com/raw/3b29de73c80e9d651df6bb38aed83d2a.png)
