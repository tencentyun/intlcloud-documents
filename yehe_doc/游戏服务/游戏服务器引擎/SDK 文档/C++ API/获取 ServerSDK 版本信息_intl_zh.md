### 接口描述
本接口（GetSdkVersion）用于获取 ServerSDK 版本信息。


### 参数描述
无参数。


### 返回值说明
版本号，具体类型为 [StringOutcome](https://intl.cloud.tencent.com/document/product/1055/36700#jtlx)。


### 使用示例
```
TencentCloud::Gse::StringOutcome SdkVersionOutcome = 
   TencentCloud::Gse::Server::GetSdkVersion();
```
