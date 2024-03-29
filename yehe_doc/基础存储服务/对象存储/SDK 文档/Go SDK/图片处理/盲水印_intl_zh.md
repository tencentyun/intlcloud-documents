## 简介

本文档提供关于盲水印的相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作描述                         |
| ------------------------------------------ | -------------------------- |
| [盲水印](https://intl.cloud.tencent.com/document/product/1045/43029) | 对本地图片添加或提取盲水印并上传至存储桶 |


## 添加盲水印

#### 功能说明

盲水印支持在上传时添加以及下载时添加。

#### 请求示例1: 上传时添加盲水印

```go
opt := &cos.ObjectPutOptions{
	nil,
	&cos.ObjectPutHeaderOptions{
		XOptionHeader: &http.Header{},
	},
}
pic := &cos.PicOperations{
	IsPicInfo: 1,
	Rules: []cos.PicOperationsRules{
		{
			FileId: ".jpg",
			Rule:   "watermark/3/type/3/text/" + base64.StdEncoding.EncodeToString([]byte("testwatermark")),
		},
	},
}
opt.XOptionHeader.Add("Pic-Operations", cos.EncodePicOperations(pic))
name := "test.jpg"
filepath := "./test.jpg"
res, _, err := c.CI.PutFromFile(context.Background(), name, filepath, opt)
```

#### 请求示例2：下载时添加盲水印

```go
name = "test.jpg"
filepath := "watermark.jpg"
_, err = c.CI.GetToFile(context.Background(), name, filepath, "watermark/3/type/3/text/"+base64.StdEncoding.EncodeToString([]byte("testwatermark")), nil)
```

## 提取盲水印

提取盲水印的请求包与 COS 简单上传文件接口一致，只需在请求包头部增加图片处理参数 Pic-Operations 并使用提取盲水印参数（watermark/4）即可。

#### 请求示例

```go
opt := &cos.ObjectPutOptions{
	nil,
	&cos.ObjectPutHeaderOptions{
		XOptionHeader: &http.Header{},
	},
}
pic := &cos.PicOperations{
	IsPicInfo: 1,
	Rules: []cos.PicOperationsRules{
		{
			FileId: "format2.jpg",
			Rule:   "watermark/4/type/3/text/" + base64.StdEncoding.EncodeToString([]byte("testwatermark")),
		},
	},
}
opt.XOptionHeader.Add("Pic-Operations", cos.EncodePicOperations(pic))
name := "test2.jpg"
_, err := c.Object.PutFromFile(context.Background(), name, filepath, opt)
```