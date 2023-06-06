## eKYC SDK for iOS API Overview
The eKYC SDK mainly involves the following classes: `HuiYanOsApi` (API class), `HuiYanOsConfig` (parameter configuration class), and `HuiYanConfigSuccCallback`, `HuiYanConfigFailCallback`, `HuiYanResultSuccCallback`, and `HuiYanResultFailCallback` (result callback classes).

### HuiYanOsApi

| API                                                   | Feature Description                                             |
| ----------------------------------------------------- | ---------------------------------------------------- |
| [release()](#release())                               | Releases resources                                         |
| [startGetAuthConfigData()](#startGetAuthConfigData()) | Gets the local configuration information of the eKYC SDK                        |
| [startAuthByLightData()](#startAuthByLightData())     | Passes in the light sequence obtained by the server to continue the liveness detection for identity verification  |

#### release()

```objective-c
+ (void)release;
```

Feature overview:

	This API is used to release the eKYC SDK resources.

#### startGetAuthConfigData()

```objective-c
+ (void)startGetAuthConfigData:(HuiYanOsConfig *)huiYanOsConfig
              withSuccCallback:(HuiYanConfigSuccCallback)huiYanConfigSuccCallback
              withFailCallback:(HuiYanConfigFailCallback)huiYanConfigFailCallback;
```

Feature overview:

	This API is used to pull the eKYC SDK configuration parameters during local detection as the parameters for subsequent acquisition of the light sequence.

Input parameters:

| Parameter Type | Parameter | Description        |
| ----------------------------------------------------- | ------------------------ | ---------------------- |
| [HuiYanOsConfig](#HuiYanOsConfig)                     | huiYanOsConfig           | Configuration parameter             |
| [HuiYanConfigSuccCallback](#HuiYanConfigSuccCallback) | huiYanConfigSuccCallback | Callback for configuration result pull success |
| [HuiYanConfigFailCallback](#HuiYanConfigFailCallback) | huiYanConfigFailCallback | Callback for configuration result pull failure |

#### startAuthByLightData()

```objective-c
+ (void)startAuthByLightData:(NSString *)reflectSequence
         withSuccCallback:(HuiYanResultSuccCallback)huiYanResultSuccCallback
         withFailCallback:(HuiYanResultFailCallback)huiYanResultFailCallback;
```

Feature overview:

	This API is used to pass in the light sequence data pulled from the server to the eKYC SDK and continue the identity verification process to get the local detection result.

Input parameters:

| Parameter Type | Parameter | Description        |
| ----------------------------------------------------- | ------------------------ | ------------------------------------------ |
| NSString                                              | reflectSequence          | Base64-Encoded light sequence obtained from the server to start identity verification |
| [HuiYanResultSuccCallback](#HuiYanResultSuccCallback) | huiYanResultSuccCallback | Callback for local identity verification success                     |
| [HuiYanResultFailCallback](#HuiYanResultFailCallback) | huiYanResultFailCallback | Callback for local identity verification failure                     |



### HuiYanOsConfig

`HuiYanOsConfig` is the configuration entity class during eKYC SDK start, which mainly contains the following attributes:

| Type           | Name               | Description                                 | Default Value               |
| ----------------------------- | ------------------ | ------------------------------------ | ----------------- |
| NSSString                     | authLicense        | Name of the license file requested for user identity verification | Empty                |
| long                          | authTimeOutMs      | Liveness detection timeout period               | 10000 milliseconds (10 seconds) |
| BOOL                          | isDeleteVideoCache | Specifies whether to delete the local cache of the video for identity verification           | YES               |
| [LanguageType](#LanguageType) | languageType       | Font language                         | Same as the system language (DEFAULT) |



### LanguageType

`LanguageType` enumerates the font language settings inside the SDK.

1. DEFAULT,// Same as the system settings

2. ZH_HANS,// Simplified Chinese

3. ZH_HANT,// Traditional Chinese

4. EN,// English

   

### HuiYanConfigSuccCallback

Callback for initialization and local configuration acquisition success.

```java
/**
 * Callback for initialization success
 *
 * @param result Initialization callback data
 */
typedef void (^HuiYanConfigSuccCallback)(NSString * _Nonnull result);
```

### HuiYanConfigFailCallback

Callback for initialization and local configuration acquisition failure.

```objective-c
/**
 * Callback for initialization failure
 *
 * @param errCode Error code
 * @param errMsg Error message
 */
typedef void (^HuiYanConfigFailCallback)(int errCode, NSString * _Nonnull errMsg);
```

### HuiYanResultSuccCallback

Callback for local identity verification process and local result acquisition success.

```objective-c
/**
 * Callback for liveness detection success
 *
 * @param data Data for comparison after Gzip compression
 * @param videoPath Liveness detection video path
 */
typedef void (^HuiYanResultSuccCallback)(NSData * _Nonnull data, NSString * _Nonnull videoPath);
```

### HuiYanResultFailCallback

Callback for local identity verification process and local result acquisition failure.

```objective-c
/**
 * Callback for liveness detection failure
 *
 * @param errCode Error code
 * @param errMsg Error message
 */
typedef void (^HuiYanResultFailCallback)(int errCode, NSString * _Nonnull errMsg);
```

