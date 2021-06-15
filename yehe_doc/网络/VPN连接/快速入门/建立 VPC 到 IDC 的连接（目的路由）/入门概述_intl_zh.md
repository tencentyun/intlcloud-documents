本章节介绍如何快速创建 VPN 连接，并使用路由功能配置路由转发策略，实现 VPC 与对端 IDC 间的安全通信。
> ?VPN 的路由功能当前处于灰度测试中，如需使用，请提交 [工单申请](https://console.cloud.tencent.com/workorder/category)。

## 步骤说明
VPN 连接激活流程图如下所示：
![](https://main.qcloudimg.com/raw/1aa819dbe82889063db1afc22ec7097e.png)

## 示例
通过 IPsec VPN 连接，打通您在**东京**的私有网络 VPC 中的子网 1：`192.168.1.0/24`与您本地 IDC 中的子网：`10.0.1.0/24`。
![](https://main.qcloudimg.com/raw/1fdd3834a5e7e59f785e2b3112889d64.png)

