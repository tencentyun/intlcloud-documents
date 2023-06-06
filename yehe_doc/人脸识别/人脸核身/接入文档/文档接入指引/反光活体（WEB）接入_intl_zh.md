# 接入说明

## 接入准备
- 注册腾讯云账号并进入慧眼控制台[开通服务](https://console.intl.cloud.tencent.com/faceid) 

## 名词介绍

- Customer H5: 客户自己开发的H5
- Customer Server: 客户自己的业务后台
- Tencent Cloud API: 腾讯云提供的后台接口，用于获取刷脸凭证并获取刷脸结果
- Tencent Cloud H5: 腾讯云的核身页面

## 时序图（简）

![1](https://qcloudimg.tencent-cloud.cn/raw/97952f84b9b010959070ccbeb8551dbe.png)

相关后台接口：[ApplyWebVerificationToken](https://www.tencentcloud.com/document/product/1061/49953)，[GetWebVerificationResult](https://www.tencentcloud.com/document/product/1061/49950)
## 时序图（详）

实际使用时，后台获取token的接口需要传入比对图URL，具体使用和原因可以见[如何传递资源](https://www.tencentcloud.com/document/product/1061/46849) 。
*CreateUploadUrl在图中将作为一个独立的参与角色*

![2](https://qcloudimg.tencent-cloud.cn/raw/872a25f5cbcd02d9b9e9418aed8cae2b.png)

相关后台接口：[ApplyWebVerificationToken](https://www.tencentcloud.com/document/product/1061/49953)，[GetWebVerificationResult](https://www.tencentcloud.com/document/product/1061/49950)，[CreateUploadUrl](https://www.tencentcloud.com/document/product/1061/47648)


### 兼容性说明

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


>!
>1. 由于 H.264 版权限制，华为系统的 Chrome 浏览器和以 Chrome WebView 为内核的浏览器,均不支持实时音视频技术的正常运行
>2. 对于不支持实时音视频技术的情况,Web人脸核身会将光线活体检测切换为视频录制模式,保证用户可正常完成核验流程

### 模式切换说明

在Web人脸核验流程后，优先使用光线活体检测模式，但在不满足实时音视频兼容性要求下，会自动切换为静默(视频录制)模式。两种模式服务流程如下:

光线活体检测模式用户做Web人脸核验流程:

![img](https://qcloudimg.tencent-cloud.cn/raw/5bc060671b612d043a5dbb354f2f513a.png)

静默模式用户做Web人脸核验流程:

![img](https://qcloudimg.tencent-cloud.cn/raw/7ea4ecb0d5815ef727df1b9ee97d1935.png)


### 光线活体摄像机授权说明

调用Web人脸核验流程时，光线活体检测模式需要用户摄像机的使用授权.如果用户拒绝授权,需要重新进入人脸核验流程和允许授权.部分浏览器会存在无法拉起授权界面,可以尝试清理浏览器的缓存

| 返回信息                                                     | 处理措施                             |
| ------------------------------------------------------------ | ------------------------------------ |
| Unable to access your camera/mic. Please make sure that there is no other app requesting access to them and try again. | 建议用户检查所需的摄像机是否被占用   |
| Mic and camera permissions of your device are required during the whole verification. Please clear your browser cache and try again. | 建议用户重新进入并允许摄像机的授权   |
| Please check whether the camera/mic can be accessed normally and try again | 建议用户检查所需的摄像头设备是否正常 |
