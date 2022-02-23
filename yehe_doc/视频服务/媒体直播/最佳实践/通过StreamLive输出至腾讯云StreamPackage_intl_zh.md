StreamLive支持直接联合腾讯云StreamPackage一起使用，将HLS/DASH格式直播流直接输出至同账号下的StreamPackage中，以便于用户形成自己的源站，从而进行下一步的视频分发与播放。

### 开通StreamPackage

在输出至StreamPackage前请先[开通StreamPackage服务](https://console.cloud.tencent.com/mdp/channel)并创建Channel。

### 完成StreamPackage的Channel创建

点击左上方【Create Channel】创建一个频道，填写频道的名称以及与StreamLive输出类型一致的协议。例如：当StreamLive选择输出类型为HLS_StreamPackage时，则此处选择HLS。

>! StreamLive与StreamPackage需要处于同一Region下。

![img](https://main.qcloudimg.com/raw/ca0ae9e483499e4489a8db47b7bb290b.png)

### 创建Endpoint

创建Channel完毕后会进入到Channel的详情页中，此时我们创建一个Endpoint节点，您也可以根据业务实际需要选择是否开启IP黑白名单或者鉴权功能。

![img](https://main.qcloudimg.com/raw/da2c4f2cefcbb73aa5ba68f75579937c.png)

### 获得Endpoint地址及Channel ID

创建完毕后的Endpoint的URL即为播放/源站地址。

![img](https://main.qcloudimg.com/raw/30594049a37593a5d8827990bd9a13a1.png)

>? Channel ID将用于StreamLive输出的填写。

![img](https://main.qcloudimg.com/raw/c66b1bb5f1c9f570225310e66f8e0a66.png)

### 选择输出类型

回到StreamLive控制台，在配置输出时，选择输出类型为HLS_STREAMPACKAGE或者DASH_STREAMPACKAGE（这取决于您的业务实际需求及您刚刚创建的StreamPackage的Channel类型）。再填入您StreamPackage中的Channel ID即可。

![img](https://main.qcloudimg.com/raw/486e54380f8bbecd2430c01ad8265c86.png)

### 保存并提交配置

保存并提交配置。此时您可接着完成 [StreamLive频道管理](https://intl.cloud.tencent.com/document/product/1048/45214)节中的其余Channel配置，并提交保存。
