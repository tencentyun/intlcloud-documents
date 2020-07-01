

### 并发上限

指通道可以支持的最大并发连接数。



### CNAME 记录

CNAME 记录是指域名解析中的别名记录（Canonical Name）。
例如，有一台服务器名为`host.example.com`，它同时提供 WWW 和 MAIL 服务，为了方便用户访问服务。这台服务器可以在 DNS 解析服务商分别添加`www.example.com`和`mail.example.com`两个 CNAME，所有访问这两个 CNAME 的请求都会被转到`host.example.com`。



### GAAP

参见 [全球应用加速](#GAAP1)



### 监听器

提供请求转发策略配置功能，如协议、端口、多源站之间的调度策略和健康检查配置等。请求会按监听器的策略转发到后端源站服务器上。

### 加速区域

指用户所在的区域，该区域的用户可以通过加速通道访问到处于源站区域的业务服务器。


<span id="GAAP1"></span>
### 全球应用加速

全球应用加速（Global Application Acceleration Platform，GAAP）是一款实现业务全球最佳访问延迟的 PAAS 类产品，依赖全球节点之间的高速通道、转发集群及智能路由技术，实现各地用户的就近接入，并将流量转发至源站，帮助业务解决全球用户访问卡顿或者延迟过高的问题。



### 源站

源站是客户的业务服务器。源站可以是用户自建的服务器，也可以是腾讯云 [对象存储](https://intl.cloud.tencent.com/product/cos) 的存储桶。
