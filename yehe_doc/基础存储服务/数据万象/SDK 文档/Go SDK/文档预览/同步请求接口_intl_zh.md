
## 简介

本文档提供关于文档预览同步请求的 API 概览以及 SDK 示例代码。

| API  |	说明  |
|----|-----|
| [同步请求接口](https://intl.cloud.tencent.com/document/product/1045/47929)  |       用于同步请求文档预览功能  |



## 同步请求接口

#### 功能说明

文档预览功能同步请求。

#### 方法原型

```go
func (s *CIService) DocPreview(ctx context.Context, name string, opt *DocPreviewOptions) (*Response, error)
```

#### 请求示例

```go
opt := &cos.DocPreviewOptions{
	Page: 1,
}
resp, err := c.CI.DocPreview(context.Background(), "form.pdf", opt)
```

#### 参数说明

```go
type DocPreviewOptions struct {
    SrcType             string
    Page                int
    ImageParams         string
    Sheet               int
    DstType             string
    Password            string
    Comment             int
    ExcelPaperDirection int
    Quality             int
    Zoom                int
}
```

| 参数名称            | 描述                                                         | 类型   |
| ------------------- | ------------------------------------------------------------ | ------ |
| name                | 对象文件名，例如 folder/document.pdf                         | String |
| SrcType             | 源数据的后缀类型，当前文档转换根据 COS 对象的后缀名来确定源数据类型。当 COS 对象没有后缀名时，可以设置该值 | String |
| page                | 需转换的文档页码，默认从1开始计数；表格文件中 page 表示转换的第 x 个 sheet 的第 x 张图 | int    |
| ImageParams         | 转换后的图片处理参数，支持 [基础图片处理](https://intl.cloud.tencent.com/document/product/1045/33694) 所有处理参数，多个处理参数可通过 [管道操作符](https://intl.cloud.tencent.com/document/product/436/36380) 分隔，从而实现在一次访问中按顺序对图片进行不同处理 | String |
| Sheet               | 表格文件参数，转换第 x 个表，默认为1                         | int    |
| DstType             | 转换输出目标文件类型，png 表示转换成 png 格式的图片文件；jpg 表示转换成 jpg 格式的图片文件；pdf 表示转换成 pdf 格式的图片文件。如果传入的格式未能识别，默认使用 jpg 格式 | String |
| Password            | Office 文档的打开密码，如果需要转换有密码的文档，请设置该字段 | String |
| Comment             | 是否隐藏批注和应用修订，默认为 0。 0：隐藏批注，应用修订；1：显示批注和修订 | int    |
| ExcelPaperDirection | 表格文件转换纸张方向，0代表垂直方向，非0代表水平方向，默认为0 | int    |
| Quality             | 生成预览图的图片质量，取值范围：[1-100]，默认值100。 例如：值为100，代表生成图片质量为100% | int    |
| Zoom                | 预览图片的缩放参数，取值范围：[10-200]， 默认值100。 例如：值为200，代表图片缩放比例为200%，即放大两倍 | int    |
