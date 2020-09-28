
MediaLive 支持输出 HLS 文件至腾讯云COS进行归档，这需要您先在 COS 中完成存储桶的创建并授权 MediaLive访问您的存储桶。
### 前提条件
在开始输出至 COS 归档前，请先确保您已经开通腾讯云 [COS服务](https://console.cloud.tencent.com/cos5)
### 步骤1：创建COS存储桶
完成 COS 服务的开通后，您可创建就近地区的 COS 存储桶。
 ![](https://main.qcloudimg.com/raw/e31c7202bb6435015f3093321a938155.jpg)

### 步骤2：选择输出类型
回到 MediaLive 控制台，在配置输出时，选择输出类型为 HLS_ARCHIVE
 ![](https://main.qcloudimg.com/raw/bee1eddef01d63637ac7847ba10b645f.jpg)

### 步骤3：授权 MediaLive 访问 COS 存储桶
由于您暂未授权 MediaLive 访问您的 COS 存储桶，COS 目的地字段将会置灰并不允许填写。点击提示中的 “click here” 跳出授权提示框。
 ![](https://main.qcloudimg.com/raw/e77c846ead0f4bd86dbe3e123f4633d4.jpg)
点击 “Authorize Now” 会前往授权界面。点击 “Grant” 完成授权。
 ![](https://main.qcloudimg.com/raw/f7aea806667ee05ed69210e246efc3db.jpg)
完成授权后回到 MediaLive 界面，选择 “Authorization completed”，则此时 COS Destination 字段可以填写。
 ![](https://main.qcloudimg.com/raw/5bfb748841656922aa56ee9407330d30.jpg)

### 步骤4：填写 COS 归档地址
您可基于您创建的 COS 存储桶填写 COS 归档地址，格式为：http://<BucketName-APPID>.cos.<Region>.myqcloud.com/path
### 步骤5：保存并提交配置
此时您可回到 [MediaLive 频道创建](https://intl.cloud.tencent.com/document/product/1048/38373) 完成其余channel配置，并点击保存之后提交。
