## 功能概述
腾讯云数据万象通过 **imageMogr2** 接口调节图片亮度。

## 接口形式

```shell
download_url?imageMogr2/bright/<value>
```

## 参数说明

操作名称：bright

| 参数             | 含义                                                         |
| ---------------- | ------------------------------------------------------------ |
| download_url | 文件的访问链接，具体构成为`<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`，<br>例如`examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`。 |
| /bright/&lt;value> | 图片亮度调节功能，value 为亮度参数值，取值范围为[-100, 100]的整数。<br><li>取值＜0：降低图片亮度。</li><li>取值 = 0：不调整图片亮度。</li><li>取值＞0：提高图片亮度。</li> |
| /ignore-error/1            | 当处理参数中携带此参数时，针对文件过大导致处理失败的场景，会直接返回原图而不报错。         |

## 示例

#### 亮度调节

将图片亮度提高70，示例如下：

```PLAINTEXT 
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/bright/70
```

最终效果如下：

![](https://main.qcloudimg.com/raw/f0fac36084c6d6709ad832c91752ee28.jpg)	
  
#### 亮度调节并携带私有文件签名

处理方式同上，仅增加签名部分，并与图片处理参数以“&”连接，示例如下：

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/bright/70
```

>? `<signature>` 为签名部分，获取方式请参考 [请求签名](https://intl.cloud.tencent.com/document/product/436/7778)。
>
