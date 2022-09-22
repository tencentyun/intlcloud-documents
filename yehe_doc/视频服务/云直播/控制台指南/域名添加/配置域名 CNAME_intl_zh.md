域名接入云直播后，系统会为您自动分配一个 CNAME 域名（以`.tlivecdn.com`为后缀)，可在 **[域名管理](https://console.cloud.tencent.com/live/domainmanage)** 列表中查看。CNAME 域名不能直接访问，您需要在域名服务提供商处完成 CNAME 配置，配置生效后，即可享受云直播服务。


## 注意事项
- 推流域名和播放域名均需完成 CNAME 解析。
- 请前往您的域名解析服务商处配置 CNAME 记录，具体操作请咨询您的域名解析服务提供商。
- CNAME 设置完成后约15分钟生效。若您设置多层 CNAME，云直播无法有效监测解析结果，请以实际的访问情况为参考。
- 若 CNAME 设置完成后长时间未显示成功，请参见 [域名配置相关](https://intl.cloud.tencent.com/document/product/267/32478)。

## 前提条件
- 已准备域名。
- 已在云直播控制台的 **[域名管理](https://console.cloud.tencent.com/live/domainmanage)** 中成功 [添加自有域名](https://intl.cloud.tencent.com/document/product/267/35970)，并验证域名归属权且域名 CNAME 地址状态为![](https://main.qcloudimg.com/raw/ed1ac2f8541f629814a3f2420b1eb79c.png)（CNAME 未配置）。



## 配置步骤
本文以在腾讯云、阿里云、百度云、DNSPod、万网、新网配置 CNAME 域名解析为例。操作步骤仅供参考，如与实际配置不符，请以各自 DNS 服务商的信息为准。域名 CNAME 设置完成后，您可根据 [验证 CNAME 是否生效](#check) 所述方法验证域名是否已 CNAME 成功。

[](id:tencent)
### 一键配置 CNAME
域名若是已托管至腾讯云 DNSPod，可一键配置 CNAME。
1. 登录直播控制台 [域名管理](https://console.cloud.tencent.com/live/domainmanage)，可在以下三种方式中进入一键配置 CNAME 流程。
  - 在域名管理页中，查询域名 CNAME 状态为![](https://main.qcloudimg.com/raw/ed1ac2f8541f629814a3f2420b1eb79c.png)，在提示中单击 **一键配置** 进入。
  - 在域名管理页中选择需要配置 CNAME 的域名，单击域名地址或管理，进入域名基本信息页，可在基本信息中单击 **一键配置** 进入。
  - 在域名管理页中添加域名，填写完基本配置后可进入 CANME 配置流程。
2. 域名生效状态为未生效时，可单击一键配置，配置约**15分钟**后生效。

3. 域名解析记录若是添加失败，可前往腾讯云 [DNSPod](https://console.cloud.tencent.com/cns) 控制台处理。

   

[](id:dnspod)
### DNSPod 设置方法
若您的 DNS 服务商为 DNSPod，您可通过如下步骤添加 CNAME 记录。
1. 登录 [DNSPod 域名服务控制台](https://console.dnspod.cn/dns/list)。
2. 在列表中，找到需要添加 CNAME 记录的域名所在行，单击对应域名名称，跳转至“添加记录”界面。
3. 通过如下步骤添加 CNAME 记录：
  1. 主机记录处填子域名（例如需要添加`www.123.com`的解析，只需要在主机记录处填写`www`即可。如果只是想添加`123.com`的解析，主机记录直接留空，系统会自动填一个“@”到输入框内，@的 CNAME 会影响到 MX 记录的正常解析，添加时慎重考虑）。
  2. 记录类型为 CNAME。
  3. 线路类型：选择"默认"类型，否则会导致部分用户无法解析。
例如，您需要将百度用户指向 2.com，所有非百度用户都指向 1.com。您可以通过添加线路类型为默认、记录值为1.com 和线路类型为百度、记录值为 2.com 的两条 CNAME 记录来实现。
  4. 记录值为 CNAME 指向的域名，只可以填写域名，记录生成后会自动在域名后面补一个“.”，这是正常现象。
  5. MX 优先级不需要填写。
  9. TTL 不需要填写，添加时系统会自动生成，默认为600秒（TTL 为缓存时间，数值越小，修改记录各地生效时间越快）。



[](id:ali)
### 阿里云设置方法
若您的 DNS 服务商为阿里云，且已完成域名备案，可参考下述步骤进行 CNAME 设置。

1.  登录阿里云控制台，进入 **云解析DNS** > [**域名解析**](https://dns.console.aliyun.com/#/dns/domainList)。
2. 选择您需添加 CNAME 的域名，单击 **解析设置**。
3. 选择 **添加记录**，在添加记录页进行如下设置：
  -  记录类型：选择 `CNAME`。
  -  主机记录：填写子域名的前缀。若播放域名为`play.myqcloud.com`，则添加`play`；若需要直接解析主域名`myqloud.com`，则输入`@`；若需要解析泛域名，则输入`\*`。
  -  解析路线：建议选择`默认`。
  -  记录值：填写腾讯云控制台域名管理页域名对应的 CNAME 值，格式为`domain.tlivecdn.com`。
  -  TTL：建议填写`10分钟`。
4. 单击 **确定** 即可。


[](id:baidu)
### 百度云设置方法
若您的域名服务商为百度云，您可通过如下步骤添加 CNAME 记录。
1. 登录百度云控制台，选择 [**域名管理**](https://console.bce.baidu.com/bcd/?_=1550137564099#/bcd/manage/list)，进入域名管理列表页。
2. 选择云直播添加的域名，在操作列单击 **解析** 进入 DNS 解析页面。
3. 添加解析记录，在该页面进行如下配置：
 - 主机记录：填写二级域名，即域名前缀。若播放域名为`play.myqcloud.com`，则添加`play`；若需要直接解析主域名`myqloud.com`，则输入`@`；若需要解析泛域名，则输入`\*`。
 - 记录类型：选择 `CNAME 记录`。
 - 解析路线：建议选择`默认`。
 - 记录值：云直播控制台域名管理页域名对应的 CNAME 值，格式为`domain.tlivecdn.com`。
 - TTL：建议填写`10分钟`。
4. 单击 **确定** 提交即可。


[](id:wwwnet)
### 万网设置方法
若您的 DNS 服务商为万网，您可通过如下步骤添加 CNAME 记录。

1. 登录万网会员中心。
2. 单击会员中心左侧导航栏中的 **产品管理** > **我的云解析** 进入万维网云解析列表页。
3. 单击要解析的域名，进入解析记录页。
4. 进入解析记录页后，单击 **新增解析**，开始设置解析记录。
5. 若要设置 CNAME 解析记录，将记录类型选择为 CNAME。主机记录即域名前缀，可任意填写（如：`www`）。记录值填写为当前域名指向的另一个域名。解析线路，TTL 默认即可。
6. 填写完成后，单击 **保存**，完成解析设置。


[](id:xinnet)
### 新网设置方法
若您的 DNS 服务商为新网，您可通过**设置别名（CNAME 记录）**添加 CNAME 记录。
别名记录允许将多个名字映射到同一台计算机。通常用于同时提供 WWW 和 MAIL 服务的计算机。例如，有一台计算机名为`host.mydomain.com`（A记录）。它同时提供 WWW 和 MAIL 服务，为了便于用户访问服务。可以为该计算机设置两个别名（CNAME）：WWW 和 MAIL 。

[](id:check)
## 验证 CNAME 是否生效
不同的 DNS 服务商，CNAME 生效的时间略有不同，一般会在半个小时之内生效。您可通过以下方式查询 CNAME 是否配置生效。
- **方法1：**进入云直播控制台的 **[域名管理](https://console.cloud.tencent.com/live/domainmanage)** 查询后缀为`.myqcloud.com`的域名状态符号是否变成![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png)表明 CNAME 已成功。
![](https://main.qcloudimg.com/raw/7930331f6eb7f4271014083cab27fb26.png)
- **方法2：**进入云直播控制台的 [域名管理](https://console.cloud.tencent.com/live/domainmanage) 添加域名，配置基本配置后，可在CNAME配置中查询CNAME状态。
- **方法3：**Linux/Mac 系统下，通过 dig 命令查看，命令格式为：`dig 自有域名`。若第一行显示解析到云直播提供的目标域名，表明 CNAME 已成功。 
![](https://main.qcloudimg.com/raw/2cbe7fdc1c9d7dbed7851aa86dd64ff1.png)
- **方法4：**Windows 系统，可通过 **开始** > **运行** > 输入 cmd 并回车，在命令行模式下输入：`nslookup 自有域名`。若已解析至云直播提供的目标域名，表明 CNAME 已成功。
![](https://main.qcloudimg.com/raw/765ac099e7c79a70496563f00cdab9a7.png)


>!若 CNAME 设置完成后长时间未显示成功，请参见 [域名配置相关](https://intl.cloud.tencent.com/document/product/267/32478)。