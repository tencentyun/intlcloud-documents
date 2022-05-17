

### Web核验接入说明

##### 前提条件

1. 已注册腾讯云账号，并完成实名认证。
2. 已在[控制台](https://console.intl.cloud.tencent.com/faceid)开通人脸核身服务

##### 接入步骤

1. 接入方先调用[生成上传链接](生成上传链接.md)接口获取上传链接UploadUrl和ResourceUrl，然后将比对照片上传至UploadUrl，上传成功后可以使用ResourceUrl访问资源
2. 接入方服务端传入核验结束后重定向的Web回跳地址，调用[申请Web核验令牌](申请Web核验令牌.md)接口获取用于发起Web核验流程的网址及标识本次核验的令牌
3. 接入方前端在浏览器中重定向到该核验网址，用户在核验页面中完成Web核验流程
4. 用户完成核验流程后，会跳转到接入方传入的回跳地址（系统会自动在此地址中添加本次核验的令牌）
5. 在回调链接地址页面中， 接入方前端需要使用本次核验的令牌，经由接入方服务端，调用[获取Web核验结果](获取Web核验结果.md)接口获取结果信息

接入时序图

![img](https://qcloudimg.tencent-cloud.cn/raw/a554aedf1bf02f57165a24eae09acf1b.png)

##### 兼容性说明

因Web实时音视频技术对浏览器和手机系统存在兼容性要求，实时音视频技术的兼容性情况如下:

<table>
	<tr><td>手机平台</td><td>浏览器</td><td>兼容性要求</td></tr>
	<tr ><td rowspan="3" style= "vertical-align: middle;">IOS</td><td>微信内嵌浏览器</td><td>iOS 系统版本14.3+，微信版本6.5+</td></tr>
	<tr><td>Safari 浏览器</td><td>iOS 系统版本11.1.2+，浏览器版本11+</td></tr>
	<tr><td>Chrome 浏览器</td><td>iOS 系统版本14.3+</td></tr>
	<tr><td rowspan="3" style= "vertical-align: middle;">Android</td><td>微信内嵌浏览器</td><td>支持</td></tr>
	<tr><td>自带浏览器</td><td>Android 系统版本7+ 华为、OPPO、VIVO、魅族、荣耀、三星等自带浏览器兼容性较好（支持率80%），小米自带浏览器兼容性一般（支持率30%）</td></tr>
	<tr><td>其他浏览器</td><td>Android 系统版本7+，支持 Chrome 浏览器，不支持QQ 、UC浏览器</td></tr>
</table>

注意:

1. 由于 H.264 版权限制，华为系统的 Chrome 浏览器和以 Chrome WebView 为内核的浏览器,均不支持实时音视频技术的正常运行
2. 对于不支持实时音视频技术的情况,Web人脸核身会将光线活体检测切换为视频录制模式,保证用户可正常完成核验流程

##### 模式切换说明

在Web人脸核验流程后，优先使用光线活体检测模式，但在不满足实时音视频兼容性要求下，会自动切换为静默(视频录制)模式。两种模式服务流程如下:

光线活体检测模式用户做Web人脸核验流程:

![img](https://qcloudimg.tencent-cloud.cn/raw/5bc060671b612d043a5dbb354f2f513a.png)

静默模式用户做Web人脸核验流程:

![img](https://qcloudimg.tencent-cloud.cn/raw/f15bd944c395b48bdbf3e0f9df3c873c.png)

##### 光线活体摄像机授权说明

调用Web人脸核验流程时，光线活体检测模式需要用户摄像机的使用授权.如果用户拒绝授权,需要重新进入人脸核验流程和允许授权.部分浏览器会存在无法拉起授权界面,可以尝试清理浏览器的缓存

| 返回信息                                                     | 处理措施                             |
| ------------------------------------------------------------ | ------------------------------------ |
| Unable to access your camera/mic. Please make sure that there is no other app requesting access to them and try again. | 建议用户检查所需的摄像机是否被占用   |
| Mic and camera permissions of your device are required during the whole verification. Please clear your browser cache and try again. | 建议用户重新进入并允许摄像机的授权   |
| Please check whether the camera/mic can be accessed normally and try again | 建议用户检查所需的摄像头设备是否正常 |
