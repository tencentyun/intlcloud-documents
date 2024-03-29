
## 简介

本文档提供关于文档预览同步请求的 API 概览以及 SDK 示例代码。

| API  |	说明  |
|----|-----|
| [同步请求接口](https://intl.cloud.tencent.com/document/product/436/49404)  |       用于同步请求文档预览功能  |



## 同步请求接口

#### 功能说明

文档预览功能同步请求。

#### 方法原型

```py
    def ci_doc_preview_process(self, Bucket, Key, SrcType=None, Page=None, DstType=None, PassWord=None, Comment=0, Sheet=1,
                               ExcelPaperDirection=0, ExcelRow=0, ExcelCol=0, ExcelPaperSize=None, TxtPagination=False,
                               ImageParams=None, Quality=100, Scale=100, ImageDpi=96, **kwargs)
```

#### 请求示例

```py
    def ci_doc_preview_process():
        # 文档预览同步接口
        response = client.ci_doc_preview_process(
            Bucket=bucket_name,
            Key='1.txt',
        )
        print(response)
        response['Body'].get_stream_to_file('result.png')
```

#### 参数说明


| 参数名称            | 描述                                                         | 类型   |
| ------------------- | ------------------------------------------------------------ | ------ |
| Bucket              | 对象所在存储桶                                               | String |
| Key                 | 对象文件名，例如 folder/document.pdf                         | String |
| SrcType             | 源数据的后缀类型，当前文档转换根据 COS 对象的后缀名来确定源数据类型。当 COS 对象没有后缀名时，可以设置该值 | String |
| Page                | 需转换的文档页码，默认从1开始计数；表格文件中 page 表示转换的第 x 个 sheet 的第 x 张图 | int    |
| DstType             | 转换输出目标文件类型，png 表示转换成 png 格式的图片文件；jpg 表示转换成 jpg 格式的图片文件；pdf 表示转换成 pdf 格式的图片文件。如果传入的格式未能识别，默认使用 jpg 格式 | String |
| Password            | Office 文档的打开密码，如果需要转换有密码的文档，请设置该字段 | String |
| Comment             | 是否隐藏批注和应用修订，默认为 0。 0：隐藏批注，应用修订；1：显示批注和修订 | int    |
| Sheet               | 表格文件参数，转换第 x 个表，默认为1                         | int    |
| ExcelPaperDirection | 表格文件转换纸张方向，0代表垂直方向，非0代表水平方向，默认为0 | int    |
| ExcelRow            | 值为1表示将所有列放到 1 页进行排版，默认值为 0 | int    |
| ExcelCol            | 值为1表示将所有行放到 1 页进行排版，默认值为 0 | int    |
| ExcelPaperSize      | 设置纸张（画布）大小，对应信息为： 0 → A4 、 1 → A2 、 2 → A0 ，默认 A4 纸张 （需配合 excelRow 或 excelCol 一起使用） | int    |
| TxtPagination       | 是否转换成长文本，设置为 true 时，可以将需要导出的页中的文字合并导出，分页范围可以通过 Ranges 控制。默认值为 false ，按页导出 txt。（ ExportType="txt" 时生效) | bool    |
| ImageParams         | 转换后的图片处理参数，支持 [基础图片处理](https://www.tencentcloud.com/document/product/436/36365) 所有处理参数，多个处理参数可通过 [管道操作符](https://intl.cloud.tencent.com/document/product/436/36380) 分隔，从而实现在一次访问中按顺序对图片进行不同处理 | String |
| Quality             | 生成预览图的图片质量，取值范围：[1-100]，默认值100。 例如：值为100，代表生成图片质量为100% | int    |
| Scale               | 预览图片的缩放参数，取值范围为 [10, 200]， 默认值100。 例如取值为200，代表图片缩放比例为200% 即放大两倍 | int    |
| ImageDpi            | 按指定 dpi 渲染图片，该参数与 scale 共同作用，取值范围 96-600 ，默认值为 96 。转码后的图片单边宽度需小于65500像素 | int    |
