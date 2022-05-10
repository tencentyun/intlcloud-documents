# 上传资源

## 背景说明
在后台接口中，因为稳定性和资源地域隔离的要求，所有传入文件的地方，我们都需要使用腾讯云COS链接代替，腾讯云后台通过这些链接以HTTP GET请求下载到需要的文件。

## 传入要求
  /提示如果您暂无云存储或者COS使用经验并且需要快速接入，可以先看最佳实践部分/ 
 
对于传入的链接需要满足以下几点要求：
- 它必须是腾讯云COS的域名，并且bucket所在地域需要和您要使用的接口中的Region参数一致，例如使用ap-singapore的服务，链接应该是符合这种形式 https://<your-bucket>-<your-appid>.cos.ap-singapore.myqcloud.com   详情见[对象存储](https://intl.cloud.tencent.com/zh/document/product/436/6224) 
- 它必须可以直接被GET请求从公网访问。
	
## 最佳实践
### 使用自建的腾讯云COS传入
	如果您有腾讯云COS或者因为其他原因的需要存储在自己的COS中，可以使用这个方法：
- 使用[接口创建存储桶](https://intl.cloud.tencent.com/zh/document/product/436/7738) 或在[控制台创建桶](https://intl.cloud.tencent.com/zh/document/product/436/13309) ，注意创建桶的地域和您使用的接口地域一致
- 上传对象[PUT Object](https://intl.cloud.tencent.com/zh/document/product/436/7749) 
- 计算对象的32位MD5摘要（腾讯云后台下载完成对象后会以此校验防止文件错乱）
- [预签名授权下载](https://intl.cloud.tencent.com/zh/document/product/436/14116) 保证此链接可以在指定时间范围内获取对象

### 使用CreateUploadUrl中转

如果您不需要使用自己的腾讯云COS，我们提供了一个单独的接口[CreateUploadUrl](https://intl.cloud.tencent.com/zh/document/product/1061/37028?!editLang=en) 来帮助您暂时存储并且生成可访问的链接：
- 使用[CreateUploadUrl](https://intl.cloud.tencent.com/zh/document/product/1061/37028?!editLang=en)传入TargetAction如DetectReflectLivenessAndCompare，传入地域如ap-singapore
- 根据返回的UploadUrl，在指定的时间范围内，使用HTTP PUT方法上传
- 计算对象的32位MD5摘要（腾讯云后台下载完成对象后会以此校验防止文件错乱）
- 在DetectReflectLivenessAndCompare接口中传入ResourceUrl以及计算得到的MD5

## 其他说明

### 数据存储安全性问题
	如果您使用的是我们的CreateUploadUrl接口，这个接口暂时不支持主动删除，只会定期清理，过期时间目前为2小时，如果需要更加严谨安全的做法，建议使用自己的COS，在接口使用完毕之后将上传的对象做一些保护措施。
	
### MD5的作用
内容的MD5是做完整性校验的，防止您原本的对象被覆盖，例如多次比对请求使用了同一个对象或者链接，我们后台返回了比对相似度低，但这种错误不易察觉。因此MD5的计算需要您的后台计算即可（在SDK场景也需要自行计算，因为主要目的是为了防止后台错乱，SDK不做计算。）
	
	
	
## 常见问题解决方法

### 接入阶段常见错误：
- 服务返回 invalid resourceUrl，这种情况可以检查一下传入的url是否符合#传入要求中的COS域名要求
- 服务返回FailedOperation.DownLoadError，检查下传入的url是否可以直接在公网访问
- 服务返回md5错误，检查url下载后的内容是否和您自己计算的一致（如DetectReflectLivenessAndCompare接口需要两个不同的Url）

其他接入阶段不易发现的上传内容错误，如DetectReflectLivenessAndCompare接口中LiveData错误或者FailedOperation.LifePhotoDetectFaces等可能是上传内容错误，如图片需要上传图片的二进制数据而不是Base64。

### 线上常见问题：
	当服务接入成功之后会有一些不可避免的算法问题，需要您记录好我们返回的RequestId以及您请求的参数，然后联系我们的售后[联系我们](https://intl.cloud.tencent.com/zh/contact-us) 

# 下载资源
	
一些接口会返回图片如DetectReflectLivenessAndCompare中会返回BestFrame，我们也会通过一个短效的Url传递，需要您尽快下载转存，否则会被清理。
	