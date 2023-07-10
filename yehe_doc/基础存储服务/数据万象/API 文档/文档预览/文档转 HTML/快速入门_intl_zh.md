## 功能描述

文档转 HTML 功能支持对多种文档类型的文件生成 HTML 格式预览，满足 PC、App 等多个用户端的文档在线浏览需求，适用于在线教育、企业 OA、在线知识库、网盘文档预览等业务场景。

>? 
>- 数据万象封装预览 JS SDK，只需要一条 URL 即可接入 HTML 预览服务。
>- 如需在小程序内使用，请参考 [小程序配置业务域名](https://intl.cloud.tencent.com/document/product/1045/33430)。
>- 如需接入 CDN 域名，需要打开 CDN 的**高级缓存过期设置**，详情请参见 [节点缓存过期配置](https://intl.cloud.tencent.com/document/product/228/35317) CDN 文档。
>

## 请求

#### 请求示例

```plaintext
GET /<ObjectKey>?ci-process=doc-preview&dstType=html HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
```

#### 请求头

此接口仅使用公共请求头部，详情请参见 [公共请求头部](https://intl.cloud.tencent.com/document/product/1045/43609) 文档。

#### 请求参数

| 名称        | 描述                                                         | 类型   | 是否必选 |
| ----------- | ------------------------------------------------------------ | ------ | -------- |
| ObjectKey   | 对象文件名，例如 folder/document.pdf                         | String  | 是       |
| ci-process  | 数据万象处理能力，文档 HTML  预览固定为 doc-preview                 | String | 是       |
| dstType   | 转换输出目标文件类型，文档 HTML 预览固定为 html（需为小写字母）  | String  | 是       |
| srcType | 指定目标文件类型，支持的文件类型请见下方  | String | 否 |
| sign          | 对象下载签名，如果预览的对象为私有读时，需要传入签名，详情请参见 [请求签名](https://intl.cloud.tencent.com/document/product/1045/33452) 文档</br>注意：需要进行 urlencode  | String | 否      |
| copyable          | 是否可复制。默认为可复制，填入值为1；不可复制，填入值为0     | String   | 否      |
| htmlParams          | 自定义配置参数，json结构，需要经过 [URL 安全](https://intl.cloud.tencent.com/document/product/1045/33430) 的 Base64 编码，默认配置为：{ commonOptions: { isShowTopArea: true, isShowHeader: true } }，支持的配置参考 [自定义配置项说明](https://intl.cloud.tencent.com/document/product/436/49416)    | String   | 否   |
| htmlwaterword          | 水印文字，需要经过 [URL 安全](https://intl.cloud.tencent.com/document/product/1045/33430) 的 Base64 编码，默认为空     | String  | 否      |
| htmlfillstyle          | 水印 RGBA（颜色和透明度），需要经过 [URL 安全](https://intl.cloud.tencent.com/document/product/1045/33430) 的 Base64 编码，默认为：rgba(192,192,192,0.6)  | String   | 否      |
| htmlfront          | 水印文字样式，需要经过 [URL 安全](https://intl.cloud.tencent.com/document/product/1045/33430) 的 Base64 编码，默认为：bold 20px Serif    | String   | 否      |
| htmlrotate          | 水印文字旋转角度，0 - 360，默认315度  | String   | 否      |
| htmlhorizontal          | 水印文字水平间距，单位 px，默认为50  | String | 否      |
| htmlvertical          | 水印文字垂直间距，单位 px，默认为100  | String | 否      |

>!
> - 目前支持的输入文件类型包含如下格式：
>  - 演示文件：pptx、ppt、pot、potx、pps、ppsx、dps、dpt、pptm、potm、ppsm。
>  - 文字文件：doc、dot、wps、wpt、docx、dotx、docm、dotm。
>  - 表格文件：xls、xlt、et、ett、xlsx、xltx、csv、xlsb、xlsm、xltm、ets。
>  - 其他格式文件： pdf、 lrc、 c、 cpp、 h、 asm、 s、 java、 asp、 bat、 bas、 prg、 cmd、 rtf、 txt、 log、 xml、 htm、 html。
> - 输入文件大小限制在200MB之内。
> - 输入文件页数限制在5000页之内。
> 


#### 请求体

该请求的请求体为空。


## 响应

#### 响应头

此接口仅返回公共响应头部，详情请参见 [公共响应头部](https://intl.cloud.tencent.com/document/product/1045/43610) 文档。


#### 响应体

此接口请求的响应体为html预览内容，展示效果可参见下方实际案例。


#### 错误码

该请求无特有错误信息，常见的错误信息请参见 [错误码](https://intl.cloud.tencent.com/document/product/1045/33700) 文档。


## 实际案例

#### 案例一：简单预览
将存储桶 examples-1258125638 中的 ObjectKey 为 test.pptx 的 PPT 文件进行在线预览，最终 URL 如下：

```plaintext
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/test.pptx?ci-process=doc-preview&dstType=html
```

>?您还可通过 JS-SDK 实现更多功能的定制，详情请参见 [自定义配置概述](https://www.tencentcloud.com/document/product/1045/47939)。

直接在浏览器中打开链接，生成的预览页面如下图所示，对于幻灯片文档，还可进行全屏的幻灯片放映，支持**动画、触发器**等效果，并提供**虚拟激光笔、演讲者模式**等功能。




#### 案例二：水印 + 自定义配置预览

将存储桶 examples-1258125638 中的 ObjectKey 为 test.pptx 的 PPT 文件进行在线预览。
1. 设置**不可复制**（copyable=0）
2. 设置**test** 水印（通过 URL 安全的 Base64编码得到 htmlwaterword=dGVzdAog）
2. 设置**自定义配置参数**（htmlParams为 {"mode":"normal","commonOptions":{"isShowHeader":false,"isShowTopArea":true},"pptOptions":{"isSlidesStatusPlay": true}}，通过 URL 安全的 Base64编码得到 htmlParams=eyJtb2RlIjoibm9ybWFsIiwiY29tbW9uT3B0aW9ucyI6eyJpc1Nob3dIZWFkZXIiOmZhbHNlLCJpc1Nob3dUb3BBcmVhIjp0cnVlfSwicHB0T3B0aW9ucyI6eyJpc1NsaWRlc1N0YXR1c1BsYXkiOiB0cnVlfX0=）。

则最终 URL 如下：

```plaintext
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/test.pptx?ci-process=doc-preview&dstType=html&copyable=0&htmlwaterword=dGVzdAog&htmlParams=eyJtb2RlIjoibm9ybWFsIiwiY29tbW9uT3B0aW9ucyI6eyJpc1Nob3dIZWFkZXIiOmZhbHNlLCJpc1Nob3dUb3BBcmVhIjp0cnVlfSwicHB0T3B0aW9ucyI6eyJpc1NsaWRlc1N0YXR1c1BsYXkiOiB0cnVlfX0=
```

直接在浏览器中打开链接，生成的预览页面如下图所示，对于幻灯片文档，还可进行全屏的幻灯片放映，支持**动画、触发器**等效果，并提供**虚拟激光笔、演讲者模式**等功能。




预览链接也可以作为iframe嵌入到业务页面中，如下所示：

```plaintext
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <meta name="viewport"
        content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0,user-scalable=no">
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests">
    <meta name="keywords" content="对象存储,文档预览">
    <meta name="description" content="">
    <title>腾讯云-对象存储-文档预览</title>
    <style>
        html,
        body {
            padding: 0;
            margin: 0;
            height: 100%;
            touch-action: manipulation;
        }
    </style>
</head>
<body>
    <iframe src="https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/test.pptx?ci-process=doc-preview&dstType=html&copyable=0&htmlwaterword=dGVzdAog&htmlParams=eyJtb2RlIjoibm9ybWFsIiwiY29tbW9uT3B0aW9ucyI6eyJpc1Nob3dIZWFkZXIiOmZhbHNlLCJpc1Nob3dUb3BBcmVhIjp0cnVlfSwicHB0T3B0aW9ucyI6eyJpc1NsaWRlc1N0YXR1c1BsYXkiOiB0cnVlfX0=" width="100%" height="100%" allowFullScreen="true"></iframe>
</body>
</html>
```
