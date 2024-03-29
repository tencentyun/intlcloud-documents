## 概述
在线迁移是指在系统不停机的情况下，将服务器或虚拟机上的系统、服务程序等从自建机房（IDC）或云平台等源环境迁移同步至腾讯云。
腾讯云提供 [go2tencentcloud 迁移工具](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)，在待迁移的源端主机上执行迁移工具后，源端主机即可整机迁移至腾讯云的目标云服务器。该迁移工具可免除制作镜像、上传并导入镜像的繁琐，从源端直接迁移上云，方便实现企业上云、跨云平台迁移、跨账号/区域迁移或部署混合云等业务需求。

## 迁移工具说明

### 支持的迁移模式

<dx-tabs>
::: 默认模式[](id:DefaultMode)
如果您的源端主机和目标云服务器都具有公网访问能力，则可以使用默认模式进行迁移。
在目前的默认模式中，源端主机通过互联网访问腾讯云 API 发起迁移请求，并向目标云服务器传输数据，将源端主机迁移至腾讯云的目标云服务器。
![](https://main.qcloudimg.com/raw/5203e535f5ba947bb67c1f91dee52f1f.jpg)
:::
::: 内网迁移模式[](id:intranetMigration)
如果您的源端主机或目标云服务器处于某个内网或 VPC 中，源端主机不能通过互联网直接与目标云服务器建立连接，则可以使用工具的内网迁移模式进行迁移。内网迁移模式需要通过使用如 [VPC 对等连接](https://intl.cloud.tencent.com/document/product/553)、[VPN 连接](https://intl.cloud.tencent.com/document/product/1037)、[云联网](https://intl.cloud.tencent.com/document/product/1003) 或者 [专线接入](https://intl.cloud.tencent.com/document/product/216) 等方式建立源端主机与目标云服务器的连接通道。

- [](id:Scenario1)场景1：如果您的源端主机或目标云服务器不能访问公网，则可以先通过一台拥有公网访问能力的主机（如网关）以互联网方式访问腾讯云 API 发起迁移请求，再通过连接通道向目标云服务器传输数据进行迁移。此场景不要求对源端主机和目标云服务器具有公网访问能力。
![](https://main.qcloudimg.com/raw/19300ddf557d4534b1cd77fcbf64ef6a.jpg)
- [](id:Scenario2)场景2：如果您的源端主机可以访问公网，则可以先在源端主机上通过互联网访问腾讯云 API 发起迁移请求，再通过连接通道向目标云服务器传输数据进行迁移。此场景要求对源端主机具有公网访问能力，而目标云服务器则不要求。
![](https://main.qcloudimg.com/raw/90bf988ba7cddb9b80307efb30eaad29.jpg)
- [](id:Scenario3)场景3：如果您的源端主机可以通过代理访问公网，则可以先在源端主机上通过网络代理访问腾讯云 API 发起迁移请求，再通过连接通道向目标云服务器传输数据进行迁移。此场景不要求对源端主机和目标云服务器具有公网访问能力。
![](https://main.qcloudimg.com/raw/14f81f2c4e6cfff80d912841451c5b69.jpg)
:::
</dx-tabs>


### 支持的操作系统
目前在线迁移工具支持的源端主机操作系统包括但不限于以下操作系统（32位或64位均可）：
<table>
	<tr><th>Linux 操作系统</th><th>Windows 操作系统</th></tr>
	<tr><td>CentOS 5/6/7/8</td><td rowspan=7>暂不支持</td></tr>
	<tr><td>Ubuntu 10/12/14/16/18	</td></tr>
	<tr><td>Debian 7/8/9	</td></tr>
	<tr><td>SUSE 11/12/15</td></tr>
	<tr><td>openSUSE 42</td></tr>
	<tr><td>Amazon Linux AMI</td></tr>
	<tr><td>Red Hat 7/8</td></tr>
</table>

### 压缩包文件说明

<table>
	<tr><th>文件名</th><th>说明</th></tr>
	<tr><td>go2tencentcloud_x64</td><td>64位 Linux 系统的迁移工具可执行程序。</td></tr>
	<tr><td>go2tencentcloud_x32</td><td>32位 Linux 系统的迁移工具可执行程序。</td></tr>
	<tr><td>user.json</td><td>迁移时源端主机和目标云服务器的配置文件，请根据 <a href="#userJsonState">user.json 文件参数说明</a> 修改配置。</td></tr>
	<tr><td>client.json</td><td>迁移工具的配置文件，请根据 <a href="#clientJsonState">client.json 文件参数说明</a> 修改配置。</td></tr>
	<tr><td>rsync_excludes_linux.txt</td><td>rsync 配置文件，排除 Linux 系统下不需要迁移的文件目录。</td></tr>
</table>

>?  不能删除配置文件，并请将配置文件存放在和 go2tencentcloud 可执行程序同级目录下。 
>

- <span id="userJsonState">user.json 文件参数说明：</span>
<table>
	<tr><th>参数名称</th><th>类型</th><th>是否必填</th><th>说明</th></tr>
	<tr><td>SecretId</td><td>String</td><td>是</td><td>账户 API 访问密钥 SecretId，详细信息请参考 <a href="https://intl.cloud.tencent.com/document/product/598/32675">访问密钥</a>。</td></tr>
	<tr><td>SecretKey</td><td>String</td><td>是</td><td>账户 API 访问密钥 SecretKey，详细信息请参考 <a href="https://intl.cloud.tencent.com/document/product/598/32675">访问密钥</a>。</td></tr>
	<tr><td>Region</td><td>String</td><td>是</td><td>目标云服务器的地域，只需填写地域，无需填写可用区，取值请参考 <a href="https://intl.cloud.tencent.com/document/product/213/6091">地域</a> 列表。</td></tr>
	<tr><td>InstanceId</td><td>String</td><td>是</td><td>目标云服务器的实例 ID，形如<code>ins-xxxxxxxx</code>。</td></tr>
	<tr><td>DataDisks</td><td>Array</td><td>否</td><td>源端主机待迁移数据盘列表，每一个元素代表一块数据盘，最多支持20块数据盘。</td></tr>
	<tr><td>DataDisks.Index</td><td>Integer</td><td>否</td><td>数据盘序号，取值范围[1,20]，值为<code>1</code>代表该块数据盘将迁移至目标云服务器挂载的第一块数据盘，值为<code>2</code>代表迁移至目标云服务器挂载的第二块数据盘，以此类推。</td></tr>
	<tr><td>DataDisks.Size</td><td>Integer</td><td>否</td><td>源端数据盘大小，单位GB，取值范围[10,16000]。</td></tr>
	<tr><td>DataDisks.MountPoint	</td><td>String</td><td>否</td><td>源端数据盘挂载点，如<code>"/mnt/disk1"</code>。</td></tr>
</table>
例如，将一台 Linux 源端主机迁移至腾讯云广州地域的一台云服务器中，user.json 文件配置为以下内容：
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id"
}  
```
<dx-alert infotype="explain" title="">
请将对应参数值替换为您实际的配置参数。
</dx-alert>
例如，将一台 Linux 源端主机（包含一块数据盘，挂载点为 <code>/mnt/disk1</code>，大小为<code>10</code>GB）迁移至腾讯云广州地域的一台目标云服务器（至少挂载一块数据盘），user.json 文件配置为以下内容：
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id",
	"DataDisks": [
		{
			"Index": 1,
			"Size": 10,
			"MountPoint": "/mnt/disk1"
		}
	]
}  
```
例如，将一台 Linux 源端主机（包含两块数据盘，盘1挂载点为 <code>/mnt/disk1</code>，大小为<code>10</code>GB，欲迁移至目标云服务器的第一块数据盘，盘2挂载点为<code>/mnt/disk2</code>，大小为<code>20</code>GB，欲迁移至目标云服务器的第二块数据盘）迁移至腾讯云广州地域的一台目标云服务器（至少挂载两块数据盘），user.json 文件配置为以下内容：
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id",
	"DataDisks": [
		{
			"Index": 1,
			"Size": 10,
			"MountPoint": "/mnt/disk1"
		},
		{
			"Index": 2,
			"Size": 20,
			"MountPoint": "/mnt/disk2"
		}
	]
}  
```
<dx-alert infotype="explain" title="">
请将对应参数值替换为您实际的配置参数。
</dx-alert>
- <span id="clientJsonState">client.json 文件参数说明：</span>
<table>
	<tr><th>参数名称</th><th>类型</th><th>是否必填</th><th>说明</th></tr>
	<tr><td>Client.Net.Mode</td><td>Integer</td><td>是</td><td>默认值为<code>0</code>，取值范围：<code>0</code>（<a href="#DefaultMode">默认模式</a>）、<code>1</code>（<a href="#Scenario1">内网迁移模式：场景1</a>）、<code>2</code>（<a href="#Scenario2">内网迁移模式：场景2</a>）、<code>3</code>（<a href="#Scenario3">内网迁移模式：场景3</a>），请根据您实际需要进行不同模式/场景的迁移，填写相应的参数值。</td></tr>
	<tr><td>Client.Net.Proxy.Ip</td><td>String</td><td>否</td><td>网络代理 IP 地址，如果您需要进行 <a href="#Scenario3">内网迁移模式：场景3</a> 的迁移，此项为必填参数。</td></tr>
	<tr><td>Client.Net.Proxy.Port</td><td>Integer</td><td>否</td><td>网络代理端口，如果您需要进行 <a href="#Scenario3">内网迁移模式：场景3</a> 的迁移，此项为必填参数。</td></tr>
	<tr><td>Client.Net.Proxy.User</td><td>String</td><td>否</td><td>网络代理用户名，如果您需要进行 <a href="#Scenario3">内网迁移模式：场景3</a> 的迁移并且网络代理需要认证，请填写网络代理用户名。</td></tr>
	<tr><td>Client.Net.Proxy.Password</td><td>String</td><td>否</td><td>网络代理密码，如果您需要进行 <a href="#Scenario3">内网迁移模式：场景3</a> 的迁移并且网络代理需要认证，请填写网络代理密码。</td></tr>
	<tr><td>Client.Extra.IgnoreCheck</td><td>Bool</td><td>否</td><td>默认值为<code>false</code>，迁移工具默认在工具开始运行时自动检查源端主机环境，如果需要略过检查，请设置为<code>true</code>。</td></tr>
	<tr><td>Client.Rsync.BandwidthLimit</td><td>String</td><td>否</td><td>限速配置项，单位为KBytes/s，默认值为空，即默认传输时不限速。</td></tr>
	<tr><td>Client.Rsync.Checksum</td><td>Bool</td><td>否</td><td>传输校验项，设为<code>true</code>后可加强传输一致性校验，但会提高源端主机 CPU 负载和减慢传输速度。默认值为<code>false</code>，即默认不校验。</td></tr>
</table>
<blockquote class="doc-tip"><p class="doc-tip-tit"><i class="doc-icon-tip"></i>说明：</p><p>除了以上参数，client.json 文件剩余配置项通常无需填写。</p>
</blockquote>
- <span id="_linuxTxtState">rsync\_excludes\_linux.txt 文件说明：</span>
排除 Linux 源端主机中不需要迁移传输的文件，或指定目录下的配置文件。该文件中已经默认排除以下目录和文件，**请勿删改**。
```sh
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
```
如果您需要排除其他目录和文件，请在该文件尾部追加内容。例如，排除挂载在 `/mnt/disk1` 的数据盘的所有内容。
```sh
/dev/*
/sys/*
/proc/*
/var/cache/yum/*
/lost+found/*
/var/lib/lxcfs/*
/var/lib/docker-storage.btrfs/root/.local/share/gvfs-metadata/*
/mnt/disk1/*
```

### 工具运行参数说明
<table>
<thead>
<tr>
<th width="15%">参数选项</th>
<th>说明</th>
</tr>
</thead>
<tbody><tr>
<td><code>--help</code></td>
<td>打印帮助信息。</td>
</tr>
<tr>
<td><code>--check</code></td>
<td>对源端主机进行检查，不进行迁移。</td>
</tr>
<tr>
<td><code>--log-file</code></td>
<td>设置日志文件名称，默认为<code>log</code>。</td>
</tr>
<tr>
<td><code>--log-level</code></td>
<td>日志输出级别，取值范围为<code>1</code>（ERROR 级别），<code>2</code>（INFO 级别）和<code>3</code>（DEBUG 级别），默认值为<code>2</code>。</td>
</tr>
<tr>
<td><code>--clean</code></td>
<td>目标云服务器强制退出迁移模式，清理现场。例如，如果控制台提示<code>Please execute '--clean' option manually.</code>，则需要使用此选项执行工具使目标云服务器退出迁移模式。</td>
</tr>
<tr>
<td><code>--version</code></td>
<td>打印版本号。</td>
</tr>
</tbody></table>

## 迁移前的检查
迁移前，需要分别检查源端主机和目标云服务器。源端主机和目标云服务器需要检查的内容如下：
<table>
	<tr><th style="width: 15%;">目标云服务器</th><td><ol  style="margin: 0;"><li>存储空间：目标云服务器的云硬盘（包括系统盘和数据盘）必须具备足够的存储空间用来装载源端的数据。</li><li>安全组：安全组中不能限制443端口和80端口。</li><li>带宽设置：建议尽可能调大两端的带宽，以便更快迁移。迁移过程中，会产生约等于数据量的流量消耗，如有必要请提前调整网络计费模式。</li><li>目标云服务器和源端主机的操作系统类型是否一致：操作系统不一致会造成后续制作的镜像的信息与实际操作系统不符，建议目标云服务器的操作系统尽量和源端主机的操作系统类型一致。例如，CentOS 7 系统的对源端主机迁移时，选择一台 CentOS 7 系统的云服务器作为迁移目标。</li></ol></td></tr>
	<tr><th>Linux 源端主机</th><td><ol  style="margin: 0;"><li>检查和安装 Virtio，操作详情可参考 <a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux 系统检查 Virtio 驱动</a>。</li><li>检查是否安装了 rsync，可执行 <code>which rsync</code> 命令进行验证。</li><li>检查 SELinux 是否已打开。如果 SELinux 已打开，请关闭 SELinux。</li><li>向腾讯云 API 发起迁移请求后，云 API 会使用当前 UNIX 时间检查生成的 Token，请确保当前系统时间无误。</li></ol></td></tr>
</table>

>? 
> - 源端主机检查可以使用工具命令自动检查，如 `sudo ./go2tencentcloud_x64 --check`。
> - go2tencentcloud 迁移工具在开始运行时，默认自动检查。如果需要略过检查强制迁移，请将 client.json 文件中的`Client.Extra.IgnoreCheck`字段配置为`true`。
> 

## 迁移步骤
腾讯云提供的 go2tencentcloud 迁移工具将整个迁移过程主要划分为以下三个阶段，用户可以在工具运行过程中直观的了解迁移的进度。
- **阶段1**：目标云服务器进入迁移模式，准备迁移
- **阶段2**：目标云服务器处于迁移模式，迁移数据中
- **阶段3**：目标云服务器退出迁移模式，迁移完成

每个阶段均会产生一些子任务去执行相关操作，部分耗时的子任务还将具有默认的最大超时时间。由于传输数据耗时受源端数据大小，网络带宽等因素影响，请耐心等待迁移流程的完成。迁移工具支持数据传输的断点续传。

>! 开始迁移后目标云服务器将进入迁移模式，请不要对目标云服务器进行重装系统、关机、销毁、重置密码等操作，直至迁移完成退出迁移模式。 
>

<dx-tabs>
::: 默认模式的迁移步骤
1. 在 user.json 文件配置目标云服务器。
请按照 [user.json 文件参数说明](#userJsonState) 配置必填项和所需项的值。
2. 在 client.json 文件配置迁移模式和其他项。
将 client.json 文件里的`Client.Net.Mode`项设置为`0`，即进行 [默认模式](#DefaultMode) 迁移。此外，如果还需要进行其他项设置，请按照 [client.json 文件参数说明](#clientJsonState) 进行配置。
3. 排除源端主机上不需迁移的文件或目录。（可选）
在 Linux 源端主机迁移时，如果需要排除一些不需迁移的文件或目录，可以将这些不需要迁移的文件或目录追加至 [rsync\_excludes\_linux.txt 文件](#_linuxTxtState) 中。
4. 运行工具。
例如，在64位 Linux 源端主机下，以 root 权限执行以下命令运行工具。
```
sudo ./go2tencentcloud_x64
```
如果运行工具时需要设置日志文件名和日志输出级别，可执行以下命令。
```
sudo ./go2tencentcloud --log-file=my.log --log-level=3
```
工具运行后，请耐心等待迁移流程的完成。 
一般默认模式下，迁移成功的控制台输出如下：
![](https://main.qcloudimg.com/raw/b056d6b1d5ac457ff43e48883848af01.png)
:::
::: 内网迁移模式的迁移步骤
#### 场景1的迁移步骤
1. 建立源端主机和目标云服务器的连接通道。
通过 [VPC 对等连接](https://intl.cloud.tencent.com/document/product/553) / [VPN 连接](https://intl.cloud.tencent.com/document/product/1037) / [云联网](https://intl.cloud.tencent.com/document/product/1003) 等方式，建立源端主机和目标云服务器的连接通道。
2. 在 user.json 文件配置目标云服务器。
 请按照 [user.json 文件参数说明](#userJsonState) 配置必填项和所需项的值。
3. 在 client.json 文件配置迁移模式和其他项。
将 client.json 文件里的 `Client.Net.Mode` 项设置为`1`，即进行 [内网迁移模式：场景1](#Scenario1) 的迁移。此外，如果还需要进行其他项设置，请按照 [client.json 文件参数说明](#clientJsonState) 进行配置。
4. 排除源端主机上不需迁移的文件或目录。（可选）
在 Linux 源端主机迁移时，如果需要排除一些不需迁移的文件或目录，可以将这些不需要迁移的文件或目录追加至 [rsync_excludes_linux.txt 文件](#_linuxTxtState) 中。
5. <span id="Scenario1_step05">在一台可以访问公网的主机（如网关）上运行工具。</span>
例如，在一台可以访问公网的主机上执行以下命令运行工具，进行阶段1的迁移。
```
sudo ./go2tencentcloud_x64
```
若提示`Stage 1 is finished and please run next stage at source machine.`，则说明阶段1已完成。
![](https://main.qcloudimg.com/raw/f861b47c464f58ea184e5cc5a6a30e1c.png)

6. <span id="Scenario1_step06">在待迁移的源端主机上运行工具。</span>
待 [步骤5](#Scenario1_step05)（即阶段1）完成后，需先将阶段1的整个工具目录拷贝至待迁移的源端主机，再运行工具进行阶段2的迁移。
例如，执行以下命令运行工具，进行阶段2的迁移。

```
sudo ./go2tencentcloud_x64
```
若提示`Stage 2 is finished and please run next stage at gateway 
machine.`，则说明阶段2已完成。
![](https://main.qcloudimg.com/raw/5684fc8aee6ebf8ba01e42deff3b4fc2.png)
7. 在一台可以访问公网的主机（如网关）上运行工具。
待 [步骤6](#Scenario1_step06)（即阶段2）完成后，需先将阶段2的整个工具目录拷贝至刚才阶段1的主机，再运行工具进行阶段3的迁移。
例如，执行以下命令运行工具，进行阶段3的迁移。
```
sudo ./go2tencentcloud_x64
```
若提示`Migrate successfully.`，则说明整个迁移任务已完成。
![](https://main.qcloudimg.com/raw/851e90fdc07fb601d3d158386d524985.png)

#### 场景2的迁移步骤

1. 建立源端主机和目标云服务器的连接通道。
通过 [VPC 对等连接](https://intl.cloud.tencent.com/document/product/553) / [VPN 连接](https://intl.cloud.tencent.com/document/product/1037) / [云联网](https://intl.cloud.tencent.com/document/product/1003) 等方式，建立源端主机和目标云服务器的连接通道。
2. 在 user.json 文件配置目标云服务器。
 请按照 [user.json 文件参数说明](#userJsonState) 配置必填项和所需项的值。
3. 在 client.json 文件配置迁移模式和其他项。
 将 client.json 文件里的 `Client.Net.Mode` 项设置为`2`，即进行 [内网迁移模式：场景2](#Scenario2) 的迁移。此外，如果还需要进行其他项设置，请按照 [client.json 文件参数说明](#clientJsonState) 进行配置。
4. 排除源端主机上不需迁移的文件或目录。（可选）
在 Linux 源端主机迁移时，如果需要排除一些不需迁移的文件或目录，可以将这些不需要迁移的文件或目录追加至 [rsync_excludes_linux.txt 文件](#_linuxTxtState) 中。
5. 运行工具。
例如，在64位 Linux 源端主机下，以 root 权限执行以下命令运行工具。

```
sudo ./go2tencentcloud_x64
```
工具运行后，请耐心等待迁移流程的完成。

一般迁移成功的控制台输出如下：
![](https://main.qcloudimg.com/raw/d32b4be8287d4b06697f0cb03cc6cff8.png)

#### 场景3的迁移步骤

1. 建立源端主机和目标云服务器的连接通道。
 通过 [VPC 对等连接](https://intl.cloud.tencent.com/document/product/553) / [VPN 连接](https://intl.cloud.tencent.com/document/product/1037) / [云联网](https://intl.cloud.tencent.com/document/product/1003)  等方式，建立源端主机和目标云服务器的连接通道。
2. 在 user.json 文件配置目标云服务器。
请按照 [user.json 文件参数说明](#userJsonState) 配置必填项和所需项的值。
3. 在 client.json 文件配置迁移模式和其他项。
 1. 将 client.json 文件里的 `Client.Net.Mode` 项设置为`3`，即进行 [内网迁移模式：场景3](#Scenario3) 的迁移。
 2. 将 client.json 文件里的 `Client.Net.Proxy.Ip` 和 `Client.Net.Proxy.Port` 项设置为网络代理的 IP 地址和端口。
如果您的网络代理还需要认证，请在 `Client.Net.Proxy.User` 和 `Client.Net.Proxy.Password` 项填写网络代理的用户名和密码；如果不需要认证，则不填。此外，如果您还需要进行其他项设置，请按照 [client.json 文件参数说明](#clientJsonState) 进行配置。
4. 排除源端主机上不需迁移的文件或目录。（可选）
在 Linux 源端主机迁移时，如果需要排除一些不需迁移的文件或目录，可以将这些不需要迁移的文件或目录追加至 [rsync_excludes_linux.txt 文件](#_linuxTxtState) 中。
5. 运行工具。
例如，在64位 Linux 源端主机下，以 root 权限执行以下命令运行工具。

```
sudo ./go2tencentcloud_x64
```
工具运行后，请耐心等待迁移流程的完成。
一般迁移成功的控制台输出如下：
![](https://main.qcloudimg.com/raw/2195589176d3669f08fbb5745901040b.png)
:::
</dx-tabs>


## 迁移后的检查
1. 如果迁移结果失败，请检查日志文件（默认为迁移工具目录下的 log 文件）的错误信息输出、指引文档或者 [服务迁移类 FAQ](https://intl.cloud.tencent.com/document/product/213/32395) 进行排查和修复问题。
2. 如果迁移结果成功，请检查目标云服务器能否正常启动、目标云服务器数据与源端主机是否一致、网络是否正常或者其他系统服务是否正常等等。
3. 如有任何疑问、迁移异常等问题请查看 [服务迁移类 FAQ](https://intl.cloud.tencent.com/document/product/213/32395) 或者 [联系我们](https://intl.cloud.tencent.com/document/product/213/34837) 解决。

