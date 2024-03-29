## 简介

使用文件存储（Cloud File Storage，CFS）监控功能前，您需要在使用了 CFS 文件存储的云服务器或容器等客户端上安装 CFS 服务监控插件，以便您更好的管理 CFS 服务。

## 安装监控插件

#### 前提条件
CFS 服务监控插件是集成在腾讯云云监控组件上的一个插件，用于监控 CFS 文件系统的性能及客户端连接。

>! 在安装 CFS 服务监控插件前，请确保您的客户端已经安装腾讯云平台的云监控组件，详情请参见 [云监控组件安装操作指引](https://intl.cloud.tencent.com/document/product/248/6211)。
>

#### 操作系统支持

CFS 服务监控插件目前**支持通过 NFS 协议挂载的客户端监控（CIFS/SMB暂不支持）**、支持平台如下，其他 Linux 内核版本系统可能会存在兼容性问题。


<table>
   <tr>
      <th>操作系统</th>
      <th>版本</th>
   </tr>
   <tr>
      <td rowspan=8>CentOS</td>
      <td>CentOS 7.6 64位</td>
   </tr>
	  <tr>
      <td>CentOS 7.5 64位</td>
   </tr>
   <tr>
      <td>CentOS 7.4 64位</td>
   </tr>
   <tr>
      <td>CentOS 7.3 64位</td>
   </tr>
   <tr>
      <td>CentOS 7.2 64位</td>
   </tr>
   <tr>
      <td>CentOS 6.9 64位</td>
   </tr>
   <tr>
      <td>CentOS 6.9 32位</td>
   </tr>
   <tr>
      <td>CentOS 6.8 64位</td>
   </tr>
   <tr>
      <td>Ubuntu</td>
      <td>Ubuntu Server 16.04.1 LTS 64位</td>
   </tr>
</table>



#### 功能说明

插件原理及主要功能如下：

- 原理：插件读取数据来源为`/proc/self/mountstats`以及`/var/log/messages`中 NFS 相关日志，读取数据为性能、状态及挂载参数相关数据，不涉及用户实际业务数据。
- 主要功能：读取使用 CFS 的客户端挂载点状态，对挂载点做可用性探测并收集性能相关数据。

## Linux 安装指引

您在登录 Linux 实例后，可以按照以下步骤 [下载插件](#step1) > [赋予安装程序可执行权限](#step2) > [安装插件](#step3) 来获取并安装 CFS 服务监控插件。

<span id="step1"></span>

#### 下载插件

通过以下命令，下载 CFS 服务监控插件到客户端当前目录下。

```sh
## 下载 CFS 服务监控插件
wget http://mirrors.tencentyun.com/install/cfs/cfs_barad_plugin_installer_release_v11
```

<span id="step2"></span>

#### 赋予安装程序可执行权限

通过以下命令，赋予 CFS 服务监控插件安装程序可执行权限。

```sh
## 赋予安装程序可执行权限
chmod +x cfs_barad_plugin_installer_release_v11
```

<span id="step3"></span>

#### 安装插件

通过以下命令，安装 CFS 服务监控插件，并返回安装成功。

```sh
## 安装插件
./cfs_barad_plugin_installer_release_v11
```

安装成功将显示“cfs barad plugin install success”，如下图所示：
![](https://main.qcloudimg.com/raw/d4138a9caa55d3b2ef030f658b3e86e9.png)

>?Ubuntu 客户端需要 root 权限才可执行上述操作，需在命令前加上 sudo。

## Windows 安装指引

Windows 客户端暂未支持。

## 监控来访客户端

登录 [CFS 控制台](https://console.cloud.tencent.com/cfs) ，单击文件系统名称进入文件系统详情页，单击【已挂载客户端】，可以查看到已挂载该文件系统的客户端信息，若客户端未安装插件则无法获取信息。

>! 客户端信息展示会有1 - 3分钟的延迟。
>

## 性能监控

前往  [CFS 云监控控制台](https://console.cloud.tencent.com/monitor/product/cfs)，单击【云监控】>【云产品监控】>【文件存储】，在文件存储监控页面可查看各个文件系统健康状态、查看告警信息等。

#### 查看文件系统性能监控

单击上图中的任意一个文件系统 ID/名称，进入到详情页面。用户可以自行选择对应时间区间窗口，查看监控文件系统的使用情况。

CFS 支持的监控指标及指标含义如下：

| 指标中文名称 | 指标含义                       | 单位 | 维度       |
| ------------ | ------------------------------ | ---- | ---------- |
| 存储量       | 文件系统当前时刻的存储量       | GB   | 单文件系统 |
| 读取带宽     | 文件系统平均每秒钟读取的数据量 | KB/s | 单文件系统 |
| 写入带宽     | 文件系统平均每秒钟写入的数据量 | KB/s | 单文件系统 |
| 读取IOPS     | 文件系统平均每秒钟读操作次数   | 次/s | 单文件系统 |
| 写入IOPS     | 文件系统平均每秒钟写操作次数   | 次/s | 单文件系统 |

>! 由于客户端本地缓存原因，云监控获取到的文件系统的**读取带宽**及**读取 IOPS** 可能会略小于实际用量。
>

#### 查看文件系统告警策略

进入到告警策略页面，用户可以查看到绑定到该文件系统上的告警策略，单击策略名称可以查看策略详情或进行解绑的操作。

## 设置告警

腾讯云支持基于监控指标，为文件系统配置告警及通知策略。若您希望新建策略或为文件系统绑定策略，可以前往  [云监控告警策略](https://console.cloud.tencent.com/monitor/policylist) 进行配置。
单击【云监控】>【告警管理】>【告警策略】，进入告警策略页面进行操作，详细操作请参考 [云监控告警服务指引](https://intl.cloud.tencent.com/document/product/248/6126) 文档。


