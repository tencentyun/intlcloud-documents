本教程将详细地指导您如何使用云点播的事件通知，包括“普通回调”和“可靠回调”两种方式。

## 前提条件

- [注册腾讯云](https://intl.cloud.tencent.com/document/product/378/17985) 账号，并完成 [实名认证](https://intl.cloud.tencent.com/document/product/378/3629)。
- 普通回调下，需要 Python 2.7 运行环境。

## 普通回调
### 部署回调接收服务

以 [普通回调](https://intl.cloud.tencent.com/document/product/266/33948#normal-callback) 的方式获取事件通知，需要在有公网 IP 的服务器上，部署回调接收服务。这里以 CVM 为例，介绍如何部署该服务：

1. 进入云服务器 CVM 控制台的 [实例列表](https://console.cloud.tencent.com/cvm/index) 界面，单击【新建】。
2. 选择【快速配置】菜单，【镜像】选择“**Ubuntu Server**”或“**CentOS**”，【公网带宽】选择“**1Mbps**”并勾选“**分配免费公网 IP**”，然后单击【立即购买】。
3. 再次进入 [实例列表](https://console.cloud.tencent.com/cvm/index) 界面，找到您创建成功的 CVM 示例，并拷贝【主IP地址】中的公网 IP（示例中的 IP 是 **134.XXX.XXX.167**）。
![](https://main.qcloudimg.com/raw/d48f654b759159de0935e83bc0e6fdc8.png)
4. 登录您购买的 CVM，下载 [源码压缩包](http://document-1251659802.coscd.myqcloud.com/NotificationTuition.zip) 并解压到您的工作目录，然后执行以下命令：
		python NotificationReceiveServer.py
命令执行后，CVM 的标准输出打印`Started httpserver on port 8080`，表示服务进程已经启动，正在监听8080端口。
5. 在浏览器中输入`http://134.XXX.XXX.167:8080`，CVM 的标准输出将打印如下 HTTP 请求信息。
![](https://main.qcloudimg.com/raw/4e7eaffe641002f9b0307244e4bec8dc.png)

### 配置普通回调
1. 登录 [云点播控制台](https://console.cloud.tencent.com/vod/overview)，单击左侧菜单栏的【回调设置】。
2. 单击【设置】：
	- 回调模式：选择“**普通回调**”。
	- 回调 URL：填入`http://134.XXX.XXX.167:8080`。
	- 回调事件：勾选“**视频上传完成回调**”。
3. 单击【确定】完成设置。

### 发起与接收普通回调

请下载 [演示视频](http://1255566954.vod2.myqcloud.com/ca75586fvodgzp1255566954/484c46995285890788305672872/xUCHV5kOGyIA.wmv) 到您的本地，用于入门教学。
1. 单击左侧菜单栏的【媒资管理】，选择【已上传】，单击【上传视频】。
![](https://main.qcloudimg.com/raw/4724951966b46c801498efed4b6ebec9.png)
2. 弹出“**上传视频**”的对话框后，选择【本地上传】，单击【选择视频】，将**演示视频**上传到云点播平台。
![](https://main.qcloudimg.com/raw/e0eb51db29de59e948b332ad05a069db.png)
 执行上传之后，您将在“**正在上传**”栏看到视频的上传进度。
![](https://main.qcloudimg.com/raw/7f072f0e67b4f3be6907ff1f5a414848.png)
 上传完成之后，在“**已上传**”栏的视频列表中，将看到上传完成的视频，以及视频对应的 ID（即 FileId）。
![](https://main.qcloudimg.com/raw/6c18e73eb8576fc120fe903fc0848927.png)
3. 检查 CVM，标准输出打印 [视频上传完成](https://intl.cloud.tencent.com/document/product/266/33950#817356113) 通知的内容。
 <img src="https://main.qcloudimg.com/raw/f6439edcd8ae59cab1d393987382e136.png" width="818">
4. 在【媒资管理】的“**已上传**”栏，勾选刚上传成功的视频，单击[【视频处理】](https://intl.cloud.tencent.com/document/product/266/33892)。【处理类型】选择“**手动选择转码模板**”选项，并在【转码模板】中勾选“**MP4-流畅-FLU (10)**”，保持【视频封面】勾选，单击【确定】。
5. 等待10分钟后，检查 CVM，标准输出打印 [任务流状态变更](https://intl.cloud.tencent.com/document/product/266/33953#.E6.99.AE.E9.80.9A.E5.9B.9E.E8.B0.83) 通知的内容，其中包括了转码（`Type`为`Transcode`）和时间点截图做封面（`Type`为`CoverBySnapshot`）的结果。
 <img src="https://main.qcloudimg.com/raw/4e577e7feb5524ff82e8a82c8e1cbdd2.png" width="818">

至此，您上传了一个视频并对其执行了转码任务。上传和转码完成后，您的回调接收服务分别接收到了一个“**视频上传完成**”和“**任务流状态变更**”通知。

## 可靠回调

1. 登录 [云点播控制台](https://console.cloud.tencent.com/vod/overview)，单击左侧菜单栏的【回调设置】。
2. 单击【设置】：
	- 回调模式：选择“**可靠回调**”。
	- 回调事件：勾选“**视频上传完成回调**”。
3. 单击【确定】完成设置。

### 发起可靠回调

1. 单击左侧菜单栏的【媒资管理】，选择【已上传】，单击【上传视频】。
![](https://main.qcloudimg.com/raw/4724951966b46c801498efed4b6ebec9.png)

2. 弹出“**上传视频**”的对话框后，选择【本地上传】，单击【选择视频】，将**演示视频**上传到云点播平台。
![](https://main.qcloudimg.com/raw/e0eb51db29de59e948b332ad05a069db.png)
 
 执行上传之后，您将在“**正在上传**”栏看到视频的上传进度。
![](https://main.qcloudimg.com/raw/7f072f0e67b4f3be6907ff1f5a414848.png)
 
 上传完成之后，在“**已上传**”栏的视频列表中，将看到上传完成的视频，以及视频对应的 ID（即 FileId）。
![](https://main.qcloudimg.com/raw/6c18e73eb8576fc120fe903fc0848927.png)

3. 在【媒资管理】的“**已上传**”栏，勾选刚上传成功的视频，单击[【视频处理】](https://intl.cloud.tencent.com/document/product/266/33892)。【处理类型】选择“**手动选择转码模板**”选项，并在【转码模板】中勾选“**MP4-流畅-FLU (10)**”，保持【视频封面】勾选，单击【确定】。

至此，您重新上传了一个视频，并对视频发起了转码任务。这些操作将会触发事件通知。