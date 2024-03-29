
## 简介

本文档提供关于基础图片处理的 API 概览以及 SDK 示例代码。

| API                                                          | 操作描述                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [缩放](https://intl.cloud.tencent.com/document/product/436/36366) | 对图片进行缩小或放大                                         |
| [裁剪](https://intl.cloud.tencent.com/document/product/436/36367) | 对图片进行裁剪，包括普通裁剪、缩放裁剪、内切圆裁剪、圆角裁剪和人脸智能裁剪 |
| [旋转](https://intl.cloud.tencent.com/document/product/436/36368) | 对图片进行旋转，包括普通旋转和自适应旋转                     |
| [格式转换](https://intl.cloud.tencent.com/document/product/436/36369) | 对图片进行格式转换、gif 格式优化、渐进显示                   |
| [质量变换](https://intl.cloud.tencent.com/document/product/436/36370) | 对图片质量进行调节                                           |
| [高斯模糊](https://intl.cloud.tencent.com/document/product/436/36371) | 对图片进行模糊处理                                           |
| [锐化](https://intl.cloud.tencent.com/document/product/436/36372) | 对图片进行锐化                                               |
| [图片水印](https://intl.cloud.tencent.com/document/product/436/36373) | 对图片进行水印处理                                           |
| [文字水印](https://intl.cloud.tencent.com/document/product/436/36374) | 对图片进行实时文字水印处理                                   |
| [获取图片基本信息](https://intl.cloud.tencent.com/document/product/436/36375) | 查询图片基本信息，包括格式、长、宽等                         |
| [获取图片 EXIF](https://intl.cloud.tencent.com/document/product/436/36376) | 查询 EXIF 信息                                               |
| [获取图片主色调](https://intl.cloud.tencent.com/document/product/436/36377) | 查询图片主色调信息                                           |
| [去除元信息](https://intl.cloud.tencent.com/document/product/436/36378) | 去除图片元信息，包括 exif 信息                               |
| [快速缩略模板](https://intl.cloud.tencent.com/document/product/436/36379) | 通过图片处理模板，生成相应的缩略图                           |
| [管道操作符](https://intl.cloud.tencent.com/document/product/436/36380) | 实现对图片按顺序进行多种处理                                 |

## 缩放

#### 功能说明

腾讯云数据万象通过 **imageMogr2** 接口提供图片缩放功能。

#### 方法原型
```go
func (s *CIService) Get(ctx context.Context, key string, operation string, opt *ObjectGetOptions, id ...string) (*Response, error)

func (s *CIService) GetToFile(ctx context.Context, key, localpath, operation string, opt *ObjectGetOptions, id ...string) (*Response, error)
```

#### 请求示例
```go
name := "test.jpg"
// Case 1 从响应体中获取对象
resp, err := c.CI.Get(context.Background(), name, "imageMogr2/thumbnail/!50px", nil)
if err != nil {
	//ERROR
}
defer resp.Body.Close()
ioutil.ReadAll(resp.Body)

// Case 2 下载对象到文件
filepath := "test.jpg"
_, err = c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/thumbnail/!50px", nil)
```

#### 参数说明

| 参数名称         | 参数描述                                                     | 类型   | 是否必填 |
| :--------------- | :----------------------------------------------------------- | :----- | :------- |
| key              | 对象键（Key）是对象在存储桶中的唯一标识。例如，在对象的访问域名`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`中，对象键为 doc/pic.jpg | string | 是       |
| operation        | 基础图片处理，可以通过该参数实现缩放、裁剪、旋转、格式转换、质量变换等基础图片处理功能。 | string | 是       |
| ObjectGetOptions | 对象下载参数，详见 [下载对象](https://intl.cloud.tencent.com/document/product/436/43549) | string | 否       |
| id               | 对象 VersionId                                                | string | 否       |

## 裁剪

#### 功能说明

腾讯云数据万象通过 **imageMogr2** 接口提供裁剪功能，包括普通裁剪、缩放裁剪、内切圆裁剪、圆角裁剪和人脸智能裁剪。

#### 请求示例

```go
name := "test.jpg"
filepath := "test.jpg"
_, err = c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/cut/600x600x100x10", nil)
```

## 其他基础图片处理

#### 功能说明

基础图片处理统一使用上述方法完成，其他基础图片处理只需要修改 operation 参数的值即可，例如将图片顺时针旋转90度的样例如下。
```go
name := "test.jpg"
filepath := "test.jpg"
_, err = c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/rotate/90", nil)
```

