### API的详细说明

接入慧眼SDK主要涉及如下几个类，它们分别是API的接口类HuiYanOSKit， 参数配置类HuiYanOsConfig，结果回调类HuiYanOKitSuccCallback以及HuiYanOKitFailCallback。

#### HuiYanOSKit

| API                                   | 功能描述                |
| ------------------------------------- | ----------------------- |
| [startHuiYaneKYC()](#startHuiYaneKYC) | 进入慧眼SDK活体检测流程 |
| [release()](#release())               | 释放SDK资源的接口       |



##### release()

功能介绍：

慧眼SDK资源释放的接口。

```objective-c
+ (void)release;
```



##### startHuiYaneKYC

功能介绍：

开启活体检测SDK，并配置SDK，回调返回结果或错误

```objective-c
/// 开启慧眼活体检测流程
/// @param faceToken token
/// @param kitConfig SDK配置
/// @param succCallback 活体检测成功回调
/// @param failCallback 活体检测失败回调
- (void)startHuiYaneKYC:(NSString *)faceToken withConfig:(HuiYanOsConfig *)kitConfig
        witSuccCallback:(HuiYanOKitSuccCallback)succCallback
       withFailCallback:(HuiYanOKitFailCallback)failCallback;
```

传入参数：

| 数类型                                               | 参数名称     | 参数含义         |
| ---------------------------------------------------- | ------------ | ---------------- |
| NSSting                                              | faceToken    | 活体流程单号     |
| [HuiYanOsConfig](#HuiYanOsConfig)                    | kitConfig    | SDK配置类        |
| [HuiYanOKitSuccCallback](#HuiYanOKitSuccCallbackens) | succCallback | 活体检测成功回调 |
| [HuiYanOKitFailCallback](#HuiYanOKitFailCallback)    | failCallback | 活体检测失败回调 |



#### HuiYanOsAuthResult

| 数类型  | 参数名称  | 参数含义                                       |
| ------- | --------- | ---------------------------------------------- |
| NSSting | faceToken | 活体流程token                                  |
| NSSting | bestImage | 开启最佳桢返回时，成功后返回的最佳桢base64图片 |

最后需要通过这个token，去腾讯云API的后台接口**GetFaceldResultIntl**拉取最终活体是否成功的数据。



#### HuiYanOsConfig

HuiYanOsConfig是在启动慧眼SDK时的配置实体类，主要包含了以下属性。

| 类型                                    | 名称                   | 含义                                                         | 默认值                    |
| --------------------------------------- | ---------------------- | ------------------------------------------------------------ | ------------------------- |
| NSString                                | authLicense            | 客户申请的用户核审授权的Licens文件名                         | 空                        |
| long                                    | authTimeOutMs          | 设置活体检测的超时时间                                       | 10000毫秒（10秒）         |
| long                                    | prepareTimeoutMs       | 设置准备阶段检测的超时时间                                   | 0                         |
| [HYShowTimeOutMode](#HYShowTimeOutMode) | showTimeOutMode        | 设置显示倒计时阶段                                           | HYShowTimeOutMode_PREPARE |
| BOOL                                    | isDeleteVideoCache     | 是否删除核身视频的本地缓存                                   | YES                       |
| BOOL                                    | iShowTipsPage          | 是否显示引导页                                               | NO                        |
| NSString                                | userUIBundleName       | 自定义的UI的bundle文件名 比如 UserUIBundle.bundle 则设置为"UserUIBundle"; | nil                       |
| NSString                                | userLanguageFileName   | 自定义的languageBundle 名称 比如 UseLanguage.bundle 则设置为"UseLanguage"; | nil                       |
| NSString                                | userLanguageBundleName | 自定义本地国际化文件名 比如 en.lproj 则设置为"en";           | nil                       |
| [LanguageType](#LanguageType)           | languageType           | SDK内部文字语言设置                                          | DEFAULT                   |
| BOOL                                    | isGetBestImg           | 是否获取最佳帧图片                                           | NO                        |
| NSString                                | setLanguageFileName    | 默认HuiYanSDKUI.bundle 内新增的语言文件目录名称 优先级最高   | nil                       |



#### HuiYanOKitSuccCallback

```objective-c
/**
 * 活体检测成功回调
 *
 * @param authResult  活体验证结果
 * @param reserved 预留位
 */
typedef void (^HuiYanOKitSuccCallback)(HuiYanOsAuthResult * _Nonnull authResult, id _Nullable reserved);
```



#### HuiYanOKitFailCallback

```objective-c
/**
 * 活体检测失败回调
 *
 * @param errCode 错误码
 * @param errMsg 错误信息
 * @param reserved 预留位
 */
typedef void (^HuiYanOKitFailCallback)(int errCode, NSString * _Nonnull errMsg ,id _Nullable reserved);
```



#### LanguageType 

SDK内包含的国际化String

```objective-c
typedef enum : NSUInteger {
    DEFAULT = 0,//跟随系统设置
    ZH_HANS,//中文简体
    ZH_HANT,//中文繁体
    ZH_HK,//中文繁体香港
    ZH_TW,//中文繁体台湾
    EN,//英文
    MS,//马来西亚语
    RU,//俄语
    JA,//日语
    CUSTOMIZE_LANGUAGE, //定制语言
} LanguageType;
```



#### HYShowTimeOutMode

```objective-c
typedef NS_OPTIONS(int, HYShowTimeOutMode) {
    HYShowTimeOutMode_TIMEOUT_HIDDEN = 1 << 0,// 隐藏所有倒计时
    HYShowTimeOutMode_PREPARE = 1 << 1,// 准备阶段倒计时
    HYShowTimeOutMode_ACTION = 1 << 3,// 动作阶段倒计时
};
```



### SDK终端错误码(iOS)

| 错误码                                | 错误码值 | 错误码含义               |
| ------------------------------------- | -------- | ------------------------ |
| HY_SUCCESS                            | 0        | 成功                     |
| HY_INITIALIZATION_PARAMETER_EXCEPTION | 210      | 初始化参数异常           |
| HY_BUNDLE_CONFIGURATION_EXCEPTION     | 211      | bundle配置异常           |
| HY_YTSDK_CONFIGURATION_EXCEPTION      | 212      | 优图配置异常             |
| HY_PLEASE_CALL_FIRST_INIT_API         | 213      | 需要先进行初始化接口     |
| HY_SDK_AUTH_FAILED                    | 214      | SDK 授权失败             |
| HY_USER_VOLUNTARILY_CANCELED          | 215      | 用户手动取消             |
| HY_YTSDK_LOCAL_AUTH_FAILED            | 216      | SDK 人脸本地检测失败     |
| HY_CAMERA_OPEN_FAIL                   | 217      | 相机开启失败             |
| HY_DONOT_SWITCH_APPS                  | 218      | 请勿在核身过程中切换应用 |
| HY_CAMEREA_PERMISSION_EXCEPTION       | 219      | 摄像头权限异常           |
| HY_SDK_VEDIO_CUT_EXCEPTION            | 220      | 视频裁剪失败             |
| HY_LIGHT_DATA_FORMAT_EXCEPTION        | 221      | 光线数据格式错误         |