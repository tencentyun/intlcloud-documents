
MediaLive支持直接联合Tencent Cloud MediaPackage一起使用，将HLS/DASH格式直播流直接输出至同账号下的MediaPackage中，以便于用户形成自己的源站，从而进行下一步的视频分发与播放。
### 步骤1：开通MediaPackage
在输出至MediaPackage前请先开通MediaPackage服务（控制台链接：https://console.cloud.tencent.com/mdp/channel）并创建Channel。
### 步骤2：完成MediaPackage的Channel创建
点击左上方Create Channel创建一个频道，填写频道的名称以及与MediaLive输出类型一致的协议。例如：当MediaLive选择输出类型为HLS_MediaPackage时，则此处选择HLS。
![](https://main.qcloudimg.com/raw/024c629fe57a6c3fd4761aadaf45a32e.jpg)
>!
>MediaLive与MediaPackage需要处于同一region下。

### 步骤3：创建endpoint
创建channel完毕后会进入到channel的详情页中，此时我们创建一个endpoint节点，您也可以根据业务实际需要选择是否开启IP黑白名单或者鉴权功能。
 ![](https://main.qcloudimg.com/raw/c3bce6fe0f437599c6acb5de6752c21f.jpg)
### 步骤4：获得endpoint地址及Channel ID
创建完毕后的endpoint的URL即为播放/源站地址。
![](https://main.qcloudimg.com/raw/5b98c4ebc014ebaeb9acb56cf436f876.jpg)
>?
>Channel ID将用于MediaLive输出的填写。

### 步骤5：选择输出类型为HLS_MEDIAPACKAGE或DASH_MEDIAPACKAGE
回到MediaLive控制台，在配置输出时，选择输出类型为HLS_MEDIAPACKAGE或者DASH_MEDIAPACKAGE（这取决于您的业务实际需求及您刚刚创建的MediaPackage的channel类型）。再填入您MediaPackage中的channel ID即可。
![](https://main.qcloudimg.com/raw/a6716afaa492de5d744ca1ef03b4c1d5.jpg)

### 步骤6：保存并提交配置
此时您可接着完成其余channel配置，并提交保存。