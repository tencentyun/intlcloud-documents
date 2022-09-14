为了能够让最终用户有更好的访问体验，我们还需要继续配置云直播CSS。

1. [StreamPackage](https://www.tencentcloud.com/products/mdp)已经与[云直播CSS](https://www.tencentcloud.com/products/css)产品打通，系统将自动帮您完成CSS 内播放域名的回源配置。进入刚才创建的StreamPackage Channel，切换至**CDN**标签页，点击 **Edit Configuration**进行配置。
![](https://qcloudimg.tencent-cloud.cn/raw/91fdb17fa19c8c2cc98a230017b9e2f8.png)

2. 在弹出的对话框中输入您规划好的直播播放域名并提交。
![](https://qcloudimg.tencent-cloud.cn/raw/3d9b5fc8f4fbffb56fb9a14d17726be5.png)

3. 系统自动配置完成后会显示如下信息，包括加速域名（**Playback Domain Name**）、**CNAME**地址、加速地区（**Acceleration Region**）以及域名服务状态（**Status**），其中播放域名加速地区默认为中国大陆以外及港澳台地区。
![](https://qcloudimg.tencent-cloud.cn/raw/0d0f202a0394c67926da815e460b7ca4.png)

4. 如果对于直播播放域名还有更进一步细化配置需求，如访问鉴权、Referer 黑白名单、HTTPS等，可点击下方按钮**Go to the CSS CDN Console to Perform More Actions**跳转至CSS控制台。

5. 如果默认配置已能够满足您的加速需求，这时可记录下系统分配的 **CNAME**地址，并进入您的DNS域名管理平台完成播放域名CNAME的解析配置。
![](https://qcloudimg.tencent-cloud.cn/raw/2696cd0cda9bb9412c4d799457b9698e.png)

6. 最终该直播链路的播放地址实际为CSS播放域名加上StreamPackage的Endpoint输出路径。
