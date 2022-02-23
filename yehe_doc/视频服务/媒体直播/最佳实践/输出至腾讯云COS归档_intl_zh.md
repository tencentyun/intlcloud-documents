StreamLive支持输出HLS文件至腾讯云COS进行归档，需要您先在COS中完成存储桶的创建并授权StreamLive访问您的存储桶。

1. 开通COS服务并创建COS存储桶

在开始输出至COS归档前，请先确定您已经[开通腾讯云COS服务](https://console.cloud.tencent.com/cos5)。完成COS服务的开通后，在[COS存储桶控制台](https://console.cloud.tencent.com/cos5)选择【存储桶列表】，单击【创建存储通】创建就近地区的COS存储桶。

![img](https://main.qcloudimg.com/raw/258a128f8e010886f7bea5b6dac83c72.png)

2. 选择输出类型为HLS_ARCHIVE。回到StreamLive控制台，在配置输出时，选择输出类型为HLS_ARCHIVE。

![img](https://main.qcloudimg.com/raw/5e782e85e27d4f860d9921cc86f1165f.png)

3. 授权StreamLive访问COS存储桶。由于您暂未授权StreamLive访问您的COS存储桶，COS 目的地字段将会置灰并不允许填写。点击提示中的【click here】跳出授权提示框。点击【Authorize Now】前往授权界面。点击【Grant】完成授权。

![img](https://main.qcloudimg.com/raw/5327f143f1fc7482c68225e8abad3c82.png))![img](https://main.qcloudimg.com/raw/3b3a91b1e9053f9ac0b6c9bc2955e12c.png)

完成授权后回到StreamLive界面，选择【Authorization completed】，则此时COS Destination字段可以填写。

![img](https://main.qcloudimg.com/raw/ee8f5a51ec6fb2642e570a9c67f91865.png))![img](https://main.qcloudimg.com/raw/41fc5c9c4a18d04b54f6585241231688.png)

4. 填写COS归档地址。您可基于您创建的COS存储桶填写COS归档地址，格式为：http://.cos..myqcloud.com/path。

5. 保存并提交配置。此时您可接着完成 [StreamLive频道管理](https://intl.cloud.tencent.com/document/product/1048/45214)中的其余channel配置，并提交保存。




