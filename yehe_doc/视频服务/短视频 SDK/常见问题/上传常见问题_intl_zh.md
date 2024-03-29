[](id:que1)
### 什么是客户端视频上传？
客户端视频上传，是指 App 用户将本地视频直接上传到云点播。

[](id:que2)
### 视频上传功能 TXUGCPublish 找不到？
视频上传模块已经从 SDK 中独立出来，并开源到 Demo 中，需要用户自己集成短视频上传，步骤如下：   
1. 下载 [Demo](https://intl.cloud.tencent.com/document/product/1069/37914)。
2. 将`app\libs\upload`目录下上传的 jar 包拷贝到您的项目`..\app\libs\upload`目录下。
3. 将短视频上传源码目录`Demo\app\src\main\java\com\tencent\liteav\demo\videoupload`拷贝到您自己的工程目录下，并修改源码里的 package 名称。
4. 在工程 App 目录下的 build.gradle 中，添加引用 jar 包的代码。
```
dependencies {
  compile fileTree(include: ['*.jar'], dir: 'libs/upload')
}
```
5. 在`AndroidManifest.xml`中配置 App 的权限。
```
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

[](id:que3)
### 上传失败，报1000的内部错误？ 
请检查是否开启云点播服务。

[](id:que4)
### 短视频上传参数类错误？
请检查视频文件地址和图片地址是否正确，该路径下是否能找到相应文件。

[](id:que5)
### 短视频上传签名错误？
客户端在发起上传前，需要向 App 服务器请求上传签名，如果 App 服务器允许客户端上传，则会按照 [签名规则](https://intl.cloud.tencent.com/document/product/266/33922) 为客户端生成一个上传签名，客户端必须携带该签名，让云点播验证客户端上传是否被授权。

客户端上传签名的步骤如下：
1. 获取 API 密钥。
2. 拼接明文串。
3. 将明文串转为最终签名。
4. 服务搭建完毕之后，开发者可以通过云点播提供的工具来校验签名的正确性：
	- [签名生成工具](https://video.qcloud.com/signature/ugcgenerate.html?_ga=1.100430424.799380133.1510203220)：根据参数和密钥，快速生成签名。
	- [签名校验工具](https://video.qcloud.com/signature/ugcdecode.html?_ga=1.100430424.799380133.1510203220)：对签名进行解析，得到生成签名时所使用的各项参数。

更多请参见 [客户端上传签名](https://intl.cloud.tencent.com/document/product/266/33922)。

[](id:que6)
### 视频上传时，最大允许上传的时长和大小有限制吗？
短视频 SDK 对上传视频的时长和大小没有限制。

[](id:que7)
### 是否可以上传图片？
 **暂不支持单独上传图片功能**，但上传视频时可附带封面图，相关说明请参见 [视频上传](https://intl.cloud.tencent.com/document/product/1069/38016)。 

