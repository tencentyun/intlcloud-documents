## 简介
本文档将介绍如何配置客户端和运行示例 Demo。

## 相关资源

本文涉及的所有工具和 Demo 都存放在 [Github 仓库](https://github.com/tencentyun/qcloud-sdk-ios-samples)，用户可前往获取。

## 搭建用户客户端
### 配置客户端

修改 QCloudCOSXMLDemo/QCloudCOSXMLDemo/key.json 文件，填入 APPID，secretID，secretKey 等参数值，然后执行以下命令：

```plaintext
pod install
```
>? APPID，secretID，secretKey 可前往 [API 密钥管理](https://console.cloud.tencent.com/cam/capi) 页面获取。
>

执行命令完成后，打开 QCloudCOSXMLDemo.xcworkspace 即可进入 Demo 体验。

### 运行示例 Demo

#### 查询存储桶列表

启动示例 App 后，将展示当前用户已创建的存储桶。

#### 创建存储桶

点击右上角**新建桶**，在配置页面输入桶名称并选择存储桶的所属 [地域](https://intl.cloud.tencent.com/document/product/436/6224)。

#### 查询对象列表

选择某个存储桶，进入存储桶详情，将看到该存储桶内所有文件以及文件夹。

#### 上传文件

在文件列表页面点击右上角的**上传**，然后选择照片进行上传，支持设置文件的访问权限和传输状态控制。

#### 下载或删除文件
选择并点击文件，然后点击文件的下载或删除按钮，对文件进行下载或删除操作。
