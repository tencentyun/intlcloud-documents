您的域名接入 CDN 后，系统会为您自动分配一个以 `.cdn.dnsv1.com` 为后缀的 CNAME 域名，可在 CDN 控制台 [域名管理页](https://console.cloud.tencent.com/cdn/domains) 查看。CNAME 域名不能直接访问，您需要在域名服务提供商处完成 CNAME 配置，配置生效后，即可享受 CDN 加速服务。
![img](https://main.qcloudimg.com/raw/6e3efa29d65ec9a35af7c1a762ebfcb8.png)

## 配置步骤

本文提供腾讯云、阿里云以及新网的 CNAME 配置步骤说明：

- [腾讯云设置方法](#m1)
- [阿里云设置方法](#m2)


<span ID ="m1"></span>
### 腾讯云设置方法

> ! 域名解析各种记录类型之间是有优先级差异的，在主机记录相同的情况下，同一条线路有几种不同的记录类型不能共存，否则将会提示冲突。CNAME 记录与除 CNAME 记录以外的任何记录类型都冲突，需要先删除掉其他记录，再进行配置。

1. 可以登录 [域名服务](https://www.dnspod.com/login?s_url=https%3A%2F%2Fwww.dnspod.com%2F&lang=en) 控制台，在列表中，找到需要添加 CNAME 记录的域名所在行，单击操作栏的【解析】。
2. 在跳转到的DNSPOD页面中，单击【添加记录】，通过如下步骤添加 CNAME 记录。
![img](https://main.qcloudimg.com/raw/36f84a0d21b51bc56d79544943f0f752.png)
	- **主机记录**：填写子域名。例如，添加 `www.dnspod.com` 的解析，您在 “主机记录” 处选择 “www” 即可。如果只是想添加 `dnspod.com` 的解析，您在 “主机记录” 处选择 “@” 即可。“@” 的 CNAME 会影响到 MX 记录的正常解析，添加时请您慎重考虑。
	- **记录类型**：选择 “CNAME”。
	- **线路类型**：选择 “默认” 类型。DNSPod 支持按多种方式划分线路，让指定用户访问该记录。
	- **记录值**：CNAME 指向的域名，只可以填写域名，记录生成后会自动在域名后面补一个“.”，这是正常现象。
	- **权重**：同一条主机记录相同的线路,可以针对不同的记录值设置权重,解析时将根据设置的权重比例进行返回。输入范围为0~100的整数。
	- **MX 优先级**：不需要填写。
	- **TTL**：为缓存时间，数值越小，修改记录各地生效时间越快，默认为600秒。

### 腾讯云分线路开启加速

- 您可以将单个主机记录的线路设置为 “默认” 类型，则是为整站开启加速服务。
	 例如，您需要将所有用户都指向1.com，您可以通过添加线路类型为默认、记录值为`1.com`的这一条 CNAME 记录来实现。
![img](https://main.qcloudimg.com/raw/0c146a23008acc3c0e4884aa1c4d3a3c.png)
- 您也可以分线路开启加速服务。
例如，您需要将联通用户指向 `2.com`，移动用户都指向 `1.com`。您可以通过添加线路类型为移动、记录值为`1.com` 和线路类型为联通、记录值为 `2.com` 的两条       CNAME 记录来实现。
![](https://main.qcloudimg.com/raw/ecf4d1ad94eaf897473647459b923209.png)

<span ID ="m2"></span>
### 阿里云设置方法

若您的 DNS 服务商为阿里云，您可通过如下步骤添加 CNAME 记录。

1. 登录阿里云控制台云解析DNS。
2. 单击要解析的域名，进入解析记录页。
3. 进入解析记录页后，单击【添加记录】按钮，开始设置解析记录。
4. 若要设置 CNAME 解析记录，将记录类型选择为 CNAME。主机记录即域名前缀，可任意填写（如：`www`）。记录值填写为当前域名指向的另一个域名。解析线路，TTL 默认即可。
   ![img](https://main.qcloudimg.com/raw/6b8bb9ce4f998b8d17ca27fd10512dc6.png)
5. 填写完成后，单击【确认】，完成解析设置。



<span ID ="m3"></span>



## 验证 CNAME 是否生效

不同的 DNS 服务商，CNAME 生效的时间略有不同，一般在半个小时之内生效。您可以通过 nslookup 或 dig 的方式来查询 CNAME 是否生效。

- `nslookup -qt=cname <加速域名>`
  
- `dig <加速域名>`
  ![img](https://main.qcloudimg.com/raw/2ba5ec76f1671c3b8ee345cef896de10.png)
