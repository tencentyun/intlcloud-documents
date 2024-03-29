
## 简介

本文档提供关于图片持久化处理的 API 概览以及 SDK 示例代码。

| API                                                          | 说明                                 |
| :----------------------------------------------------------- | :----------------------------------- |
| [图片持久化处理](https://intl.cloud.tencent.com/document/product/436/40592) | 用于图片持久化处理 |


## 上传时处理

COS 提供的上传时处理功能可以帮助使用者在上传时实现图片处理。您只需要在请求包头部中加入 Pic-Operations 项并设置好相应参数，即可在图片上传时实现相应的图片处理，并可将原图和处理结果存入到 COS。目前支持20M 以内文件处理。

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
			FileId: "format.jpg",
			Rule:   "imageView2/format/png",
		},
	},
}
opt.XOptionHeader.Add("Pic-Operations", cos.EncodePicOperations(pic))
name := "test.jpg"
local_filename := "./test.jpg"
res, _, err := c.CI.PutFromFile(context.Background(), name, local_filename, opt)
```

#### 参数说明

```go
type PicOperations struct {
    IsPicInfo int                  
    Rules     []PicOperationsRules
}
type PicOperationsRules struct {
    Bucket string
    FileId string
    Rule   string
}
```

| 参数名称  | 参数描述                                                     | 类型   | 是否必填 |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| IsPicInfo | 是否返回原图信息，0不返回原图信息，1返回原图信息，默认为0    | int    | 否   |
| Rules     | 处理规则，一条规则对应一个处理结果（目前支持五条规则），不填则不进行图片处理 | Array  | 否   |
| Bucket    | 存储结果的目标存储桶名称，格式为 BucketName-APPID，如果不指定的话默认保存到当前存储桶 | string | 否   |
| FileId    | 处理结果的文件路径名称，如以`/`开头，则存入指定文件夹中，否则，存入原图文件存储的同目录 | string | 是 |
| Rule      | 处理参数，参见图片持久化处理 API。若按指定样式处理，则以`style/`开头，后加样式名，如样式名为`test`，则 rule 字段为`style/test` | string | 否   |

## 云上数据处理

该接口能够对已存储在 COS 的图片进行相应处理操作，并将结果存入到 COS。

#### 请求示例
```go
opt := &cos.ImageProcessOptions{
	IsPicInfo: 1,
	Rules: []cos.PicOperationsRules{
		{
			FileId: "format.jpg",
			Rule:   "imageView2/format/png",
		},
	},
}
name := "test.jpg"
res, _, err := c.CI.ImageProcess(context.Background(), name, opt)
```



