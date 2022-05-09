## Overview

This document describes how to request the COS service by using a non-default domain name.

### Default CDN acceleration domain name

#### Feature description

After enabling a default CDN acceleration domain name for a bucket through the COS console, you can set the domain name in the SDK code for acceleration.
For more information, see [Enabling Default CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31505).

#### Method prototype

```java
void com.qcloud.cos.ClientConfig.setEndPointSuffix(String endPointSuffix)
```

#### Sample request

```java
// 1. Use a CDN acceleration domain. COS verification information does not need to be sent.
COSCredentials cred = new AnonymousCOSCredentials();
// 2. Set the region abbreviation for the bucket. For abbreviations of COS regions, visit https://intl.cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
// HTTPS is recommended.
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3. Set the suffix for the default CDN acceleration domain.
String cdnSuffix = "file.myqcloud.com";
clientConfig.setEndPointSuffix(cdnSuffix);
// 4. Generate a COS client
COSClient cosclient = new COSClient(cred, clientConfig);
```

#### Parameter description

| Parameter | Description | Type |
| -------------- | ----------------------------------- | ------ |
| endPointSuffix     | Set the domain suffix to use the CDN acceleration domain name | String         |

### Custom CDN acceleration domain name

#### Feature description

After setting a custom CDN acceleration domain name for a bucket through the COS console, you can set the domain name in the SDK code for acceleration. For more information, see [Enabling Custom Accelerated Domain Name](https://intl.cloud.tencent.com/document/product/436/31506).

#### Method prototype

```java
void com.qcloud.cos.ClientConfig.setEndpointBuilder(EndpointBuilder endpointBuilder)
```

#### Sample request

```java
// 1. Use a CDN acceleration domain. COS verification information does not need to be sent.
COSCredentials cred = new AnonymousCOSCredentials();
// 2. Set the region abbreviation for the bucket. For abbreviations of COS regions, visit https://intl.cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
// HTTPS is recommended, which requires the custom domain to have the relevant HTTPS certificate.
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3. Set the custom CDN domain name.
// The `get service` request will use this domain, which is fixed.
String serviceApiEndpoint = "service.cos.myqcloud.com";
String cdnEndpoint = "xxx.xxx.com";
UserSpecifiedEndpointBuilder endPointBuilder = new UserSpecifiedEndpointBuilder(cdnEndpoint, serviceApiEndpoint);
clientConfig.setEndpointBuilder(endPointBuilder);
// 4. Generate a COS client
COSClient cosclient = new COSClient(cred, clientConfig);
```

#### Parameter description

| Parameter | Description | Type |
| ----------------- | -------------------------------- | ---------------------------- |
| endPointerBuilder     | Constructs the custom CDN acceleration domain.  | UserSpecifiedEndpointBuilder   |

UserSpecifiedEndpointBuilder description:

| Parameter | Description | Type |
| --------------------- | ----------------------------------- | ------ |
| generalApiEndpoint       | Custom CDN acceleration domain name                  | String                         |
| getServiceApiEndpoint    | Fixed to `service.cos.myqcloud.com`  | String         |


### Custom origin server domain name

#### Feature description

After setting a custom origin server domain for a bucket through the COS console, you can set the domain name in the SDK code to access COS resources. For more information, see [Enabling Custom Origin Server Domains](https://intl.cloud.tencent.com/document/product/436/31507).

#### Method prototype

```java
void com.qcloud.cos.ClientConfig.setEndpointBuilder(EndpointBuilder endpointBuilder)
```

#### Sample request

```java
// 1. Initialize user authentication information (secretId, secretKey).
// You can log in to the CAM console to view and manage `secretId` and `secretKey`.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 2. Set the region abbreviation for the bucket. For abbreviations of COS regions, visit https://intl.cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
// HTTPS is recommended.
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3. Set the custom domain name.
// The get service request will use this domain, which is fixed.
String serviceApiEndpoint = "service.cos.myqcloud.com";
String userEndpoint = "xxx.xxx.com";
UserSpecifiedEndpointBuilder endPointBuilder = new UserSpecifiedEndpointBuilder(userEndpoint, serviceApiEndpoint);
clientConfig.setEndpointBuilder(endPointBuilder);
// 4. Generate a COS client
COSClient cosclient = new COSClient(cred, clientConfig);
```

#### Parameter description

| Parameter | Description | Type |
| ----------------- | -------------------------- | ---------------------------- |
| endPointerBuilder     | Constructs the custom origin server domain.  | UserSpecifiedEndpointBuilder   |

UserSpecifiedEndpointBuilder description:

| Parameter | Description | Type |
| --------------------- | ----------------------------------- | ------ |
| generalApiEndpoint       | Custom origin server domain  | String      |
| getServiceApiEndpoint    | Fixed to `service.cos.myqcloud.com`  | String         |


### Global acceleration domain name

#### Feature description

After enabling a global acceleration domain name for a bucket through the COS console, you can set the domain name in the SDK code for global acceleration. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/33409).

#### Method prototype

```java
void com.qcloud.cos.ClientConfig.setEndPointSuffix(String endPointSuffix)
```

#### Sample request

```java
// 1. Initialize user authentication information (`secretId`, `secretKey`).
// You can log in to the CAM console to view and manage `secretId` and `secretKey`.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 2. Set the region abbreviation for the bucket. For abbreviations of COS regions, visit https://intl.cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
// HTTPS is recommended.
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3. Set the suffix for the global acceleration endpoint.
String cosSuffix = "cos.accelerate.myqcloud.com";
clientConfig.setEndPointSuffix(cosSuffix);
// 4. Generate a COS client
COSClient cosclient = new COSClient(cred, clientConfig);
```

#### Parameter description

| Parameter | Description | Type |
| -------------- | ---------------------------------- | ------ |
| endPointSuffix     | Set the domain suffix to use a global acceleration domain name. | String         |