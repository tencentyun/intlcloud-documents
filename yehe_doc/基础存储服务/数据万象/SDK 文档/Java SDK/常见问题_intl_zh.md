### 客户端网络正常，但是通过 HTTP 访问 COS 非常慢，或者报错 Connection reset，该如何处理？

部分区域的运营商可能会对 COS 的域名进行劫持，因此建议通过 HTTPS 来访问 COS。

### 引入 SDK 运行后，出现 java.lang.NoSuchMethodError 的异常，该如何处理？

**原因**：一般是发生了 JAR 包冲突，例如，用户的工程中的 httpclient 库中 的 JAR 包版本没有 A 方法，但是  SDK 依赖的 JAR 包使用了 A 方法。此时，由于运行时加载顺序的问题，加载了用户工程中的 httpclient  库，运行时便会抛出 NoSuchMethodError 的异常。
**解决方法**：
- 方式一：将工程中引起 NoSuchMethodError 包的版本，改成和 SDK 中 pom.xml 里的对应库的版本一致。
- 方式二：将 cos-java-sdk 换成 cos_api-bundle。此方案会将 cos-java-sdk 的所有依赖都独立安装，所以会占用更多的空间。
```
<groupId>com.qcloud</groupId>
       <artifactId>cos_api-bundle</artifactId>
<version>5.6.35</version>
```

### Java SDK 的默认超时时间是多少？

Java SDK 默认连接超时时间为30000ms，默认读写超时时间为30000ms，可以使用 SDK 中的 SetConnectionTimeoutMs 方法和 setSocketTimeout 来进行调整。

### Java SDK 上传速度慢，日志频繁打印 IOException，该如何处理？

原因与解决办法如下：
1. 确认是否是通过公网访问 COS 或 CI。
目前同地域 CVM 访问 COS 一般通过内网访问（内网域名解析出的 IP 是10、100、169网段，有关 COS 域名请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224)）。如果是通过公网访问，需确认出口带宽是否较小，或者是否有其他程序占用带宽资源。
2. 确保在生产环境中的日志级别不是 DEBUG，推荐使用 INFO 日志。
3. 如果 WARN 日志打印 IOException 可以忽略，SDK 会进行重试。IOException 的原因可能是网速过慢，解决办法可参考步骤1和步骤2。

### 上传文件请求路径中带有“+”，报错 Code: 403  SignatureDoesNotMatch，如何处理？

**可能原因**：用户 Java 环境的 httpclient 版本引起的 urlencode 编码错误。
**解决方法**：
- 方式一：使用 httpclient 4.5.3 版本
```
<groupId>org.apache.httpcomponents</groupId>
       <artifactId>httpclient</artifactId>
 <version>4.5.3</version> 
```
- 方式二：将 cos-java-sdk 换成 cos_api-bundle。此方案会将 cos-java-sdk 的所有依赖都独立安装，所以会占用更多的空间。
```
<groupId>com.qcloud</groupId>
       <artifactId>cos_api-bundle</artifactId>
<version>5.6.35</version>
```

### 使用 Java SDK 报错提示某个依赖版本太低，如何处理？

**原因**：用户 Java 环境的依赖版本和 Java SDK 需要的依赖版本有冲突。
**解决方法**：
- 方式一：按照提示，升级对应依赖到要求的版本。
- 方式二：将 cos-java-sdk 换成 cos_api-bundle。此方案会将 cos-java-sdk 的所有依赖都独立安装，所以会占用更多的空间。
```
<groupId>com.qcloud</groupId>
       <artifactId>cos_api-bundle</artifactId>
<version>5.6.35</version>
```

### SDK 如何创建COS的文件目录？

对象存储中文件和目录都是对象，目录只是以`/`结尾的对象。创建文件时，不需要创建目录。如创建一个对象键为 `xxx/yyy/zzz.txt`的文件，只用把 key 设置为`xxx/yyy/zzz.txt`即可，不用建立`xxx/yyy/`这个对象。在控制台上展示时，也会以`/`作为分隔，展示出目录的层级效果。但这些目录对象是不存在的。如果想创建一个目录对象，可使用以下的示例代码：

```java
String bucketName = "examplebucket-1250000000";
String key = "folder/images/";
// 目录对象即是一个/结尾的空文件，上传一个长度为 0 的 byte 流
InputStream input = new ByteArrayInputStream(new byte[0]);
ObjectMetadata objectMetadata = new ObjectMetadata();
objectMetadata.setContentLength(0);

PutObjectRequest putObjectRequest =
new PutObjectRequest(bucketName, key, input, objectMetadata);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
```

### SDK 如何使用 HTTPS?

SDK 中相关的配置都统一放在 ClientConfig 类中，示例代码如下：

```java
// 初始化用户身份信息(secretId, secretKey)
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 设置 bucket 的区域, COS 地域的简称请参照 https://intl.cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 配置使用 https
clientConfig.setHttpProtocol(HttpProtocol.https);
// 生成 cos 客户端
COSClient cosClient = new COSClient(cred, clientConfig);
```

### SDK 如何使用代理？

对于需要使用代理访问 COS 或 CI 的用户，可在 ClientConfig 类中，配置使用代理 IP （或域名）以及端口，示例代码如下：

```java
// 初始化用户身份信息(secretId, secretKey)
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 设置 bucket 的区域, COS 地域的简称请参照 https://intl.cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 配置使用代理(IP 和端口需要同时设置)
// 设置代理 IP (也可传入域名)
clientConfig.setHttpProxyIp("192.168.2.3");
// 设置代理端口
clientConfig.setHttpProxyPort(8080);
// 生成 cos 客户端
COSClient cosClient = new COSClient(cred, clientConfig);
```

### 如何设置自定义 EndpointBuilder？

您的场景也许需要指定 API 请求的 Endpoint。此时，您需要实现 EndpointBuilder 接口中的 buildGeneralApiEndpoint 和 buildGetServiceApiEndpoint 中的两个函数，分别为普通 API 请求和 GETService 请求指定远端的 Endpoint。使用示例如下：
```
// 步骤1：实现 EndpointBuilder 接口中的两个函数
class SelfDefinedEndpointBuilder implements EndpointBuilder {
    @Override
    public String buildGeneralApiEndpoint(String bucketName) {
        return String.format("%s.%s", bucketName, "mytest.com");
    }

    @Override
    public String buildGetServiceApiEndpoint() {
        return "service.mytest.com";
    }
}

// 步骤2：初始化客户端
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
SelfDefinedEndpointBuilder selfDefinedEndpointBuilder = new SelfDefinedEndpointBuilder();
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
clientConfig .setEndpointBuilder(selfDefinedEndpointBuilder);
COSClient cosClient = new COSClient(cred, clientConfig);
```

### SDK 的上传、下载、批量删除等操作中，使用的 key 值是否需要添加 `/` 前缀？

对象存储的 key 值无需携带 `/` 前缀。例如，您将对象 key 值设置为 exampleobject 上传的对象，可以通过 URL： `http://cos.ap-guangzhou.myqcloud.com/exampleobject`进行访问。
>! 在批删请求中，请勿传入 `/` 前缀的 key，这将导致对象删除失败。
>


### 使用 Java SDK 上传报错 please make sure bucket name must contain legal appid when appid is missing. example: bucektname-1250000000，该如何处理？

COS Java SDK 旧版本仅支持例如125开头的 APPID，如果您使用的是130开头的 APPID，建议您将 SDK 更新至最新版本。Java SDK 下载安装请参见 [Java SDK 文档](https://intl.cloud.tencent.com/document/product/436/10199)。

### 使用 Java SDK 上传大文件报错，该如何处理？

使用 Java SDK 上传大于5G的文件时，建议使用 [高级上传接口](https://www.tencentcloud.com/document/product/436/44015)。高级上传接口根据用户文件的长度和数据类型，自动选择以简单上传或分块上传方式。

### Java SDK 如何获取文件上传进度？

需获取上传进度，建议使用 [高级上传](https://www.tencentcloud.com/document/product/436/44015) 接口，通过调用 Upload 的方法 getProgress() 获取上传的进度 TransferProgress 类。

### Java SDK 能否使用长连接?

Java SDK 默认使用长连接。

### 如何使用 Java SDK 获取指定目录所有路径的同时，判断路径是文件还是文件夹？

可以使用 Java SDK 中的 [查询对象列表](https://intl.cloud.tencent.com/document/product/436/10199#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8) 功能来列出存储桶内的对象，**使用 prefix 参数可以指定目录前缀**。

### Java SDK 报错连接池已关闭，抛出异常： java.lang.IllegalStateException: Connection pool shut down，该如何处理？

1. COSClient 是线程安全的类，允许多线程访问同一实例。
因为实例内部维持了一个连接池，创建多个实例可能导致程序资源耗尽。请确保程序生命周期内实例只有一个，且在不再需要使用时，调用 COSClient.shutdown() 方法将其关闭。
如果需要新建实例，请先将之前的实例关闭。**推荐一个进程里只使用一个 COSClient，在程序全部结束退出时才调用 COSClient.shutdown()**。
2. 高级接口封装类的 TransferManager 中也使用了 COSClient，建议在程序全部结束退出时再调用 TransferManager.shutdownNow(false)。
此外，如果在创建 TransferManager 实例时复用了其他 COSClient，请在关闭时加入参数 false（即 TransferManager.shutdownNow(false)），避免关闭复用的 COSClient，导致其他使用 COSClient 的地方报错。



