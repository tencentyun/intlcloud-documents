您的域名接入 CDN 后，系统会为您自动分配一个以 `.cdn.dnsv1.com` 为后缀的 CNAME 域名，可在 CDN 控制台 [域名管理页](https://console.cloud.tencent.com/cdn/access) 查看。CNAME 域名不能直接访问，您需要在域名服务提供商处完成 CNAME 配置，配置生效后，即可享受 CDN 加速服务。
![img](https://main.qcloudimg.com/raw/073b948565743f7947aae8503eef995d.png)

## 配置步骤

本文提供DNSPod的 CNAME 配置步骤说明：

### 腾讯云设置方法

>? 域名解析各种记录类型之间是有优先级差异的，在主机记录相同的情况下，同一条线路有几种不同的记录类型不能共存，否则将会提示冲突。CNAME 记录与除 CNAME 记录以外的任何记录类型都冲突，需要先删除掉其他记录，再进行配置。详情请参见 [为什么添加解析记录的时候提示 "记录有冲突" ](https://cloud.tencent.com/document/product/302/3468#.E4.B8.BA.E4.BB.80.E4.B9.88.E6.B7.BB.E5.8A.A0.E8.A7.A3.E6.9E.90.E8.AE.B0.E5.BD.95.E7.9A.84.E6.97.B6.E5.80.99.E6.8F.90.E7.A4.BA-.26quot.3B.E8.AE.B0.E5.BD.95.E6.9C.89.E5.86.B2.E7.AA.81.26quot.3B-.EF.BC.9F)。

若您的 DNS 服务商为 DNSPod，登录 [DNSPod 域名服务控制台](https://console.dnspod.cn/dns/list)，在列表中，找到需要添加 CNAME 记录的域名所在行，单击对应域名名称，跳转至“添加记录”界面，通过如下步骤添加 CNAME 记录。

![img](https://main.qcloudimg.com/raw/36f84a0d21b51bc56d79544943f0f752.png)

1. 主机记录处填子域名（例如需要添加`www.123.com`的解析，只需要在主机记录处填写`www`即可。如果只是想添加`123.com`的解析，主机记录直接留空，系统会自动填一个“@”到输入框内，@的 CNAME 会影响到 MX 记录的正常解析，添加时慎重考虑）。
2. 记录类型为 CNAME。
3. 线路类型（默认为必填项，否则会导致部分用户无法解析。在上图中，默认的作用为：除了联通用户之外的所有用户，都会指向 1.com）。
4. 记录值为 CNAME 指向的域名，只可以填写域名，记录生成后会自动在域名后面补一个“.”，这是正常现象。
5. 设置该条记录的权重。
6. TTL 不需要填写，添加时系统会自动生成，默认为600秒（TTL 为缓存时间，数值越小，修改记录各地生效时间越快）。

## 验证 CNAME 是否生效

不同的 DNS 服务商，CNAME 生效的时间略有不同，一般在半个小时之内生效。您可以通过 nslookup 或 dig 的方式来查询 CNAME 是否生效。

如：nslookup -qt=cname <加速域名>或者dig <加速域名>