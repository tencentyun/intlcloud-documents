## 简介

本文档提供关于如何使用非默认域名请求 COS 服务。

## 自定义源站域名

关于如何设置自定义源站域名请参见 [自定义源站域名](https://intl.cloud.tencent.com/document/product/436/31507)。

以下代码展示了如何使用自定义源站域名访问 COS 服务。

#### 示例代码

```dart
// 存储桶 region 可以在 COS 控制台指定存储桶的概览页查看 https://console.cloud.tencent.com/cos5/bucket/ ，关于地域的详情见 https://cloud.tencent.com/document/product/436/6224
String region = "ap-beijing"; // 您的存储桶地域
String customDomain = "exampledomain.com"; // 自定义域名

// 创建 CosXmlServiceConfig 对象，根据需要修改默认的配置参数
CosXmlServiceConfig serviceConfig = CosXmlServiceConfig(
    region: region,
    isDebuggable: false,
    isHttps: true,
    hostFormat: customDomain // 修改请求的域名
);
// 注册默认 COS Service
Cos().registerDefaultService(serviceConfig);
```

## 全球加速域名

关于全球加速功能请参考 [全球加速功能概述](https://intl.cloud.tencent.com/document/product/436/33409)。

以下代码展示了如何使用全球加速域名访问 COS 服务。

#### 示例代码

```dart
// 存储桶 region 可以在 COS 控制台指定存储桶的概览页查看 https://console.cloud.tencent.com/cos5/bucket/ ，关于地域的详情见 https://cloud.tencent.com/document/product/436/6224
String region = "ap-beijing"; // 您的存储桶地域
// 是否开启全球加速
bool accelerate = true;
// 创建 CosXmlServiceConfig 对象，根据需要修改默认的配置参数
CosXmlServiceConfig serviceConfig = CosXmlServiceConfig(
    region: region,
    isDebuggable: false,
    isHttps: true,
    accelerate: accelerate // 使用全球加速域名
);
// 注册默认 COS Service
Cos().registerDefaultService(serviceConfig);
```
