## 慧眼SDK iOS API概述
慧眼SDK主要涉及如下几个类，它们分别是API的接口类HuiYanOsApi， 参数配置类HuiYanOsConfig，结果回调类HuiYanConfigSuccCallback、HuiYanConfigFailCallback、HuiYanResultSuccCallback以及HuiYanResultFailCallback。

### HuiYanOsApi

| API                                                   | 功能描述                                             |
| ----------------------------------------------------- | ---------------------------------------------------- |
| [release()](#release())                               | 资源释放接口                                         |
| [startGetAuthConfigData()](#startGetAuthConfigData()) | 获取慧眼SDK本地配置信息的接口                        |
| [startAuthByLightData()](#startAuthByLightData())     | 传入服务器获取的光线序列，继续完成活体核身检测的接口 |

#### release()

```objective-c
+ (void)release;
```

功能介绍：

​	慧眼SDK资源释放的接口。

#### startGetAuthConfigData()

```objective-c
+ (void)startGetAuthConfigData:(HuiYanOsConfig *)huiYanOsConfig
              withSuccCallback:(HuiYanConfigSuccCallback)huiYanConfigSuccCallback
              withFailCallback:(HuiYanConfigFailCallback)huiYanConfigFailCallback;
```

功能介绍：

​	本地检测慧眼SDK同时拉取配置参数，用来作为后续兑换光线序列的参数。

传入参数：

| 参数类型                                              | 参数名称                 | 参数含义               |
| ----------------------------------------------------- | ------------------------ | ---------------------- |
| [HuiYanOsConfig](#HuiYanOsConfig)                     | huiYanOsConfig           | 配置的参数             |
| [HuiYanConfigSuccCallback](#HuiYanConfigSuccCallback) | huiYanConfigSuccCallback | 拉取配置结果成功的回调 |
| [HuiYanConfigFailCallback](#HuiYanConfigFailCallback) | huiYanConfigFailCallback | 拉取配置结果失败的回调 |

#### startAuthByLightData()

```objective-c
+ (void)startAuthByLightData:(NSString *)reflectSequence
         withSuccCallback:(HuiYanResultSuccCallback)huiYanResultSuccCallback
         withFailCallback:(HuiYanResultFailCallback)huiYanResultFailCallback;
```

功能介绍：

​	将从服务器拉取到的光线序列数据，传入慧眼SDK同时继续核身流程，并获取本地检测的结果。

传入参数：

| 参数类型                                              | 参数名称                 | 参数含义                                   |
| ----------------------------------------------------- | ------------------------ | ------------------------------------------ |
| NSString                                              | reflectSequence          | 从服务器兑换来启动核身使用的光线序列Base64 |
| [HuiYanResultSuccCallback](#HuiYanResultSuccCallback) | huiYanResultSuccCallback | 本地核身的结果成功回调                     |
| [HuiYanResultFailCallback](#HuiYanResultFailCallback) | huiYanResultFailCallback | 本地核身的结果失败回调                     |



### HuiYanOsConfig

HuiYanOsConfig是在启动慧眼SDK时的配置实体类，主要包含了以下属性。

| 类型                          | 名称               | 含义                                 | 默认值            |
| ----------------------------- | ------------------ | ------------------------------------ | ----------------- |
| NSSString                     | authLicense        | 客户申请的用户核审授权的Licens文件名 | 空                |
| long                          | authTimeOutMs      | 设置活体检测的超时时间               | 10000毫秒（10秒） |
| BOOL                          | isDeleteVideoCache | 是否删除核身视频的本地缓存           | YES               |
| [LanguageType](#LanguageType) | languageType       | 设置字体语言                         | 跟随系统(DEFAULT) |



### LanguageType

LanguageType SDK内部字体语言设置枚举。

1. DEFAULT,//跟随系统设置

2. ZH_HANS,//中文简体

3. ZH_HANT,//中文繁体

4. EN,//英文

   

### HuiYanConfigSuccCallback

初始化并且获取本地配置成功的回调

```java
/**
 * 初始化成功回调
 *
 * @param result 初始化回调数据
 */
typedef void (^HuiYanConfigSuccCallback)(NSString * _Nonnull result);
```

### HuiYanConfigFailCallback

初始化并且获取本地配置失败的回调

```objective-c
/**
 * 初始化失败回调
 *
 * @param errCode 错误码
 * @param errMsg 错误信息
 */
typedef void (^HuiYanConfigFailCallback)(int errCode, NSString * _Nonnull errMsg);
```

### HuiYanResultSuccCallback

本地核身流程与本地结果获取成功的回调

```objective-c
/**
 * 活体核身成功回调
 *
 * @param data 活体比对数据，GZip压缩后的数据
 * @param videoPath 活体视频路径
 */
typedef void (^HuiYanResultSuccCallback)(NSData * _Nonnull data, NSString * _Nonnull videoPath);
```

### HuiYanResultFailCallback

本地核身流程与本地结果获取失败的回调

```objective-c
/**
 * 活体核身失败回调
 *
 * @param errCode 错误码
 * @param errMsg 错误信息
 */
typedef void (^HuiYanResultFailCallback)(int errCode, NSString * _Nonnull errMsg);
```

