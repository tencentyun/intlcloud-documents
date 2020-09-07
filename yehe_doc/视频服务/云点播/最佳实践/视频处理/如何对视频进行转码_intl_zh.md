

## 使用须知

### 内容介绍

本文档向开发者介绍如何对云点播（VOD）中的视频进行转码，以及如何获取转码后的输出结果。

### 费用

本文提供的代码是免费开源的，但在使用的过程中可能会产生以下费用：

- 购买腾讯云云服务器（CVM）用于执行云 API 请求脚本，详见 [CVM 计费](https://intl.cloud.tencent.com/document/product/213/2180)。

## 在控制台发起转码

### 步骤1：开通云点播<span id="p11"></span>

请参考 [快速入门 - 步骤1](https://intl.cloud.tencent.com/document/product/266/8757) 开通云点播服务。

### 步骤2：上传视频<span id="p12"></span>

参考 [快速入门 - 步骤2](https://intl.cloud.tencent.com/document/product/266/8757) 上传一个测试视频。单击 [此处](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4) 查看本 Demo 使用的测试视频，对应的 FileId 为5285890804162014755，如下图所示：
![](https://main.qcloudimg.com/raw/f8aa62bd40ab37b8cdd371798d4ff1e9.png)
>?建议使用较短的视频文件进行测试（例如时长为几十秒的视频），避免转码过程耗时太长。

### 步骤3：发起转码<span id="p13"></span>

在控制台 [视频管理](https://console.cloud.tencent.com/vod/media) 页面勾选新上传的测试视频，然后单击【视频处理】：
![](https://main.qcloudimg.com/raw/cf6d8e0fa032b2a76acfd918cf5c3146.png)
在弹框中，处理类型选择【转码】，然后单击【转码模板】：
![](https://main.qcloudimg.com/raw/fc857eebabee8b5c547774fed0fe2814.png)
选择所需的转码模板，然后单击【确定】。本 Demo 以系统预置模板 MP4-FLU（模板 ID 100010）和 MP4-SD（模板 ID 100020）为例，如果开发者需要使用自定义的转码模板，请参考 [模板设置文档](https://intl.cloud.tencent.com/document/product/266/14059)。
![](https://main.qcloudimg.com/raw/e82be691470090beccf1ea27dbdcb4c3.png)
单击【确定】，发起转码：
![](https://main.qcloudimg.com/raw/f52ec218600e19af3e42359a90d03298.png)
在“视频管理”页面看到测试视频的状态为“处理中”，则表示视频正在转码：
![](https://main.qcloudimg.com/raw/30d3c90f55970568f55ce09be4cdb32b.png)

### 步骤4：查看转码结果<span id="p14"></span>

在控制台 [视频管理](https://console.cloud.tencent.com/vod/media) 页面等待测试视频的状态变为“正常”，此时表示转码已完成。单击测试视频右侧的【管理】，进入视频管理页面：
![](https://main.qcloudimg.com/raw/694f1b000cea813d12397fcb1c3a86a0.png)
在“基本信息”标签页下的【标准转码列表】中，转出了 MP4-FLU 和 MP4-SD 两个规格。开发者可以单击右侧的【预览】直接观看视频，还可以单击【复制地址】复制转码视频的 URL，然后通过其它渠道发布给观众。
![](https://main.qcloudimg.com/raw/38db47dcfbd840bd6d67478ce42fd1cd.png)

## 调用云 API 发起转码

### 步骤1：准备腾讯云 CVM<span id="p21"></span>

云 API 请求脚本需要运行在一台腾讯云 CVM 上，要求如下：

- 地域：任意。
- 机型：官网最低配置（1核1GB）即可。
- 公网：需要拥有公网 IP，带宽1Mbps或以上。
- 操作系统：官网公共镜像`Ubuntu Server 16.04.1 LTS 64位`或`Ubuntu Server 18.04.1 LTS 64位`。

购买 CVM 的方法请参见 [操作指南 - 创建实例](https://intl.cloud.tencent.com/document/product/213/4855)。重装系统的方法请参见 [操作指南 - 重装系统](https://intl.cloud.tencent.com/document/product/213/4933)。

>!如果您没有符合上述条件的腾讯云 CVM，也可以在其它带外网的 Linux（如 CentOS、Debian 等）或 Mac 机器上执行脚本，但需根据操作系统的区别修改脚本中的个别命令，具体修改方式请开发者自行搜索。

### 步骤2：获取 API 密钥<span id="p22"></span>

请求云 API 需要使用到开发者的 API 密钥（即 SecretId 和 SecretKey）。如果还未创建过密钥，请参见 [创建密钥文档](https://intl.cloud.tencent.com/document/product/598/34228) 生成新的 API 密钥；如果已创建过密钥，请参见 [查看密钥文档](https://intl.cloud.tencent.com/document/product/598/34228) 获取 API 密钥。

### 步骤3：开通云点播<span id="p23"></span>

请参考 [快速入门 - 步骤1](https://intl.cloud.tencent.com/document/product/266/8757) 开通云点播服务。

### 步骤4：上传视频<span id="p24"></span>
参考 [快速入门 - 步骤2](https://intl.cloud.tencent.com/document/product/266/8757) 上传一个测试视频。单击 [此处](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4) 查看本 Demo 使用的测试视频，对应的 FileId 为5285890804162014755，如下图所示：
![](https://main.qcloudimg.com/raw/f8aa62bd40ab37b8cdd371798d4ff1e9.png)
>?建议使用较短的视频文件进行测试（例如时长为几十秒的视频），避免转码过程耗时太长。


### 步骤5：发起转码<span id="p25"></span>

登录 [步骤1](#p21) 中准备好的 CVM（登录方法详见 [操作指南 - 登录 Linux](https://intl.cloud.tencent.com/document/product/213/5436)），在远程终端输入以下命令并运行：
```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/transcode_api.sh
```
>?请将命令中的 SECRET_ID 和 SECRET_KEY 赋值为 [步骤2](#p22) 中获取到的内容。

该命令将从 Github 下载 Demo 源码并自动执行安装脚本。安装过程需几分钟（具体取决于 CVM 网络状况），期间远程终端会打印如下示例的信息：
```
  [2020-06-15 20:39:56]开始安装 pip3。
  [2020-06-15 20:40:06]pip3 安装成功。
  [2020-06-15 20:40:06]开始安装云 API Python SDK 。
  [2020-06-15 20:40:07]云 API Python SDK 安装完成。
  [2020-06-15 20:40:07]开始配置 API 参数。
  [2020-06-15 20:40:07]API 参数配置完成。
```
执行`process_media.py`脚本发起转码：
```
ubuntu@VM-69-2-ubuntu:~$ cd ~/vod-server-demo/transcode_api/; python3 process_media.py 5285890804162014755
```
>?请将命令中的5285890804162014755替换为 [步骤4](#p24) 中得到的实际 FileId。

该命令将对5285890804162014755这个视频发起 [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) 请求，按 VOD [预置转码模板](https://intl.cloud.tencent.com/document/product/266/33932) 100010和100020两个规格进行转码，并打印请求的应答内容：
```
{"TaskId": "1400329073-procedurev2-f6bf6f01612369b6db30f2224792a2aft0", "RequestId": "809918fb-791c-4937-b684-5027ba6bc5f0"}
```

### 步骤6：查看转码结果<span id="p14"></span>

在“视频管理”页面看到测试视频的状态为“处理中”，则表示视频正在转码：
![](https://main.qcloudimg.com/raw/30d3c90f55970568f55ce09be4cdb32b.png)
等待测试视频的状态变为“正常”，此时表示转码已完成。单击测试视频右侧的【管理】，进入视频管理页面：
![](https://main.qcloudimg.com/raw/694f1b000cea813d12397fcb1c3a86a0.png)
在“基本信息”标签页下的【标准转码列表】中，转出了 MP4-FLU 和 MP4-SD 两个规格。开发者可以单击右侧的【预览】直接观看视频，还可以单击【复制地址】复制转码视频的 URL，然后通过其它渠道发布给观众。
![](https://main.qcloudimg.com/raw/38db47dcfbd840bd6d67478ce42fd1cd.png)

## 上传视频后自动转码（任务流）

VOD 有多种上传视频的方式，包括控制台上传、服务端上传、客户端上传和 URL 拉取上传等（详见 [媒体上传综述](https://intl.cloud.tencent.com/document/product/266/9760)）。各种上传方式均支持指定一个 [任务流](https://intl.cloud.tencent.com/document/product/266/33931)，在上传完成后自动触发转码。

## 上传视频后自动转码（事件通知）

VOD 后台在视频上传完成和转码任务完成后均会发起 [事件通知](https://intl.cloud.tencent.com/document/product/266/33948) 请求。开发者可以利用事件通知机制来对新上传的视频发起转码，也可以通过事件通知来自动获取转码结果（上文展示的方法是人工在控制台查看转码结果）。