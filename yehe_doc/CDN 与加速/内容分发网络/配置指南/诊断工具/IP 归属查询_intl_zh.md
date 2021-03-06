## 功能介绍
内容分发网络（CDN）为您提供了 IP 归属查询工具，您可以通过此工具查询指定的 IP 是否为腾讯云 CDN 全球加速节点，以及 IP 所在加速服务区域、省份及运营商信息。
## 适用场景
在排障类场景可使用此工具协助排查，当用户访问出现异常时，将客户端请求实际访问的 IP 在此处进行查询：
- 若不归属于腾讯云 CDN，则域名解析配置可能出现异常，前往域名解析服务商处查看 CNAME 是否配置正常；
- 若归属于腾讯云 CDN，可通过查看节点服务状态，是否出现节点上下线导致请求中断。

## 操作指南
### 查询方式
登录 [CDN 控制台](https://console.cloud.tencent.com/cdn)，选择左侧目录的【诊断工具】>【IP 归属查询】，进入功能页。
![](https://main.qcloudimg.com/raw/7c72a39a1c0f33e633057d02af9c3a6f.png)
### 使用约束
- 在文本框中输入多条需要验证的 IP 地址，一行一个。
- 最多可一次性验证20个 IP。
- 支持 IPv4、IPv6 地址验证。
- 支持全球范围内加速节点验证，中国境内节点会返回所在省份运营商数据，中国境外节点会返回所在国家数据。
- 支持查看节点**近三个小时**服务状态变更，若存在上下线变动，可查看出对应的操作时间。

## 使用案例
### IP 归属于中国境内
![](https://main.qcloudimg.com/raw/92a04bfdc0905c9be0465d3dc4825dd3.png)
### IP 归属于中国境外
![](https://main.qcloudimg.com/raw/6a2e1b6f94362d5508ed98a52bd2d125.png)







