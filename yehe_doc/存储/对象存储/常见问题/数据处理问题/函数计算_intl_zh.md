### COS 是否支持文件解压缩？

文件解压缩功能是腾讯云对象存储（Cloud Object Storage，COS）基于 [云函数（Serverless Cloud Function，SCF）](https://intl.cloud.tencent.com/document/product/583) 为用户提供的数据处理解决方案。详情请参见 [设置文件解压缩](https://intl.cloud.tencent.com/document/product/436/35663)。

### COS 文件解压缩功能是否会解压二级目录下的压缩文件？

目前文件解压缩功能不会解压二级目录下的压缩包。您可以自行调整函数逻辑以实现该场景。

### COS 是否支持在上传时自动压缩文件？

不支持。

### COS 是否支持设置 CDN 自动刷新？

可以通过 [云函数（Serverless Cloud Function，SCF）](https://intl.cloud.tencent.com/document/product/583) 设置自动刷新，详情请参见 [设置 CDN 缓存刷新](https://intl.cloud.tencent.com/document/product/436/37273)。

### 可以把云数据库的数据备份到 COS 吗？

可以通过 [云函数（Serverless Cloud Function，SCF）](https://intl.cloud.tencent.com/document/product/583) 设置数据库备份功能。当用户在指定存储桶中配置了备份函数规则后，云函数会定期扫描您的数据库备份文件并将文件转存至存储桶中。详情请参见 [设置云数据库备份](https://intl.cloud.tencent.com/document/product/436/39629)。

