### COS API 是否支持 S3 协议？

COS 提供了 AWS S3 兼容的 API，详情请参见 [使用 AWS S3 SDK 访问 COS](https://intl.cloud.tencent.com/document/product/436/32537) 。

### 调用 API 接口时，出现“Request has expired”等错误信息，该如何处理？

出现该提示，存在两种可能：
- 一是因为您发起请求的时间超过了签名的有效时间。
- 二是您本地系统时间和所在时区的时间不一致。

针对第一种可能，建议重新获取有效的请求签名再进行 API 操作。若是第二种可能，请将您的本地系统时间按照所在时区的时间进行校正。

### 如何调用 API 删除掉未完成上传文件？

首先调用接口 ListMultipartUploads 列出未完成上传文件，然后调用 Abort Multipart upload 接口舍弃一个分块上传并删除已上传的块。

### 调用批量删除接口返回正确，但实际文件删除失败怎么办？

请检查删除的文件路径，文件路径不需要以`/`开头。



### COS 中分块上传 UploadPart 请求时返回 NoSuchUpload？

当传入 **uploadId** 和 **partNumber** 都相同的时候，后传入的块将覆盖之前传入的块。当 **uploadId** 不存在时会返回“404错误，NoSuchUpload”，详情请参见 [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) 文档。

### 如何通过 API 修改对象的存储类型？

用户可通过调用 PUT  Object - Copy 接口，修改 x-cos-storage-class 参数实现修改对象的存储类型，详情请参见 [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)。

### 对象存储怎么设置签名永久有效？

对象存储的签名是使用时间戳来判断请求是否过期，并不能设置永久有效。假设用户使用永久密钥生成签名，希望签名达到长期有效的目的，可以设置一个较为长久的时间戳，例如过期时间为当前时间+50年。若用户使用临时密钥生成签名，由于临时密钥的有效期最多为2小时，那么生成的签名，其有效期也在2小时内。

### 对象存储 COS 支持 API 查询账单吗？

COS 不提供查询账单的 API，请您通过控制台 [账单详情](https://console.cloud.tencent.com/expense/bill/summary) 查看。如需通过 API 查询账单明细数据，请参见 [查询账单明细数据](https://intl.cloud.tencent.com/document/product/555/30756) 计费文档。

### 是否支持使用 API 查询存储对象的大小？

可以通过 [GET Bucket（List Objects）](https://intl.cloud.tencent.com/document/product/436/30614) 接口查询对象的大小。

### 如何通过 API 修改对象名称？

使用 [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) 复制对象并指定对象名称实现重命名。

### 如何通过 API 获取存储桶域名？

通过 [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) 接口获取存储桶域名。响应头中 “x-cos-bucket-region”参数值即表示存储桶所在地域。

### 如何通过 API 获取存储桶大小？

COS 没有直接获取存储桶大小的 API，建议您通过 [云监控接口](https://intl.cloud.tencent.com/document/product/248/37269) 获取存储桶中各存储类型的存储量后累加计算存储桶的存储量。

### 如何通过 API 查询用量明细？

可参见以下方式：

1. 直接使用 [API 请求工具](https://console.cloud.tencent.com/api/explorer?Product=billing&Version=2018-07-09&Action=DescribeDosageCosDetailByDate&SignVersion=) 进行查询。

### COS 是否有目录操作的 API 接口？

对象存储中本身是没有文件夹和目录的概念的，控制台所展示的文件夹其实是以 / 结尾的空对象。

### 如何通过 API 创建目录/文件夹？

通过调用 [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) 接口实现，上传文件名以 “/” 结尾的空文件即可生成目录的形式。

>?对象存储中本身是没有文件夹和目录的概念的，为了满足用户使用习惯，对象存储在控制台、COS browser 等图形化工具中模拟了「文件夹」或「目录」的展示方式。具体实现是通过创建一个文件名以“/”结尾，内容为空的对象，展示方式上模拟了传统文件夹。

### 如何使用 API 删除目录/文件夹？

COS API 仅支持删除单个文件，如需删除整个目录，需要使用 [GET Bucket（List Objects）](https://intl.cloud.tencent.com/document/product/436/30614) 接口获取指定前缀（prefix 参数）的所有文件后，再使用 [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) 进行删除。

### COS 智能分层存储如何区分 Object 所处存储层？

通过 [查询对象元数据](https://intl.cloud.tencent.com/document/product/436/7745) 接口返回的 **x-cos-storage-tier**  获取对象所处的存储层。

### COS 如何使用 API 搜索对象？

可以使用 [HEAD Object 接口](https://intl.cloud.tencent.com/document/product/436/7745) 判断该对象是否存在。如果您需要搜索某个对象，可通过 [Get Bucket 接口](https://intl.cloud.tencent.com/document/product/436/30614) 获取存储桶内所有对象后进行判断。

### COS 使用 GET Object 接口时，动态指定返回的内容是否以附件下载？

使用 GET Object 接口时，在 url 上携带 **response-content-disposition** 参数，需要下载附件时指定值为 **attachment** 即可。此类型的 GET Object 请求必须要携带签名，您可以使用COS 签名工具生成签名。

### 调用 COS 的 putObjectCopy 时提示 NoSuchKey，该如何处理？

请检查源文件是否存在，若源文件存在一般是因为文件夹后面没添加“/”导致的报错，请添加“/”后再尝试操作。

### 是否支持通过 API 获取某个 object 的 request 次数？

 COS 没有 API 支持获取某个 Object 的 request 次数。您可以通过分析日志来进行操作，请您这边先 [开启日志管理功能](https://intl.cloud.tencent.com/document/product/436/17040)，之后可以通过分析日志来进行获取。



