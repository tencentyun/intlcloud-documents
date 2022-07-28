iOS端eKYC SDK主要涉及的类主要包含VerificationKit、VerificationConfig、VerifiCommDef这几个主要类型下面对其支持的API做出详细说明。

### VerificationKit

VerificationKit为eKYC SDK的对外接口类，主要逻辑也都是调用此类完成。

| API                                                 | 功能描述                 |
| --------------------------------------------------- | ------------------------ |
| [initWithViewController:](#initWithViewController:) | 初始化接口               |
| [clearInstance](#clearInstance)                     | 资源释放接口             |
| [startVerifiWithConfig:](#startVerifiWithConfig:)   | 启动eKYC身份证核验的流程 |



#### initWithViewController:

```objective-c
// 初始化方法
- (void)initWithViewController:(UIViewController *)viewController;
```

功能介绍：

​	eKYC SDK的初始化接口。

传入参数:	

| 参数类型         | 参数名称       | 参数含义              |
| ---------------- | -------------- | --------------------- |
| UIViewController | viewController | 当前调用SDK页面VC对象 |



#### clearInstance

```objective-c
/// 清理SDK资源
+ (void)clearInstance;
```

功能介绍：

​	eKYC SDK资源释放的接口。



#### startVerifiWithConfig:

```objective-c
/// 开启eKYC验证
- (void)startVerifiWithConfig:(VerificationConfig *)verifiConfig
            withSuccCallback:(TXYVerifiKitProcessSucceedBlock)succCallback
             withFialCallback:(TXYVerifiKitProcessFailedBlock)failCallback;
```

功能介绍：

​	启动eKYC身份证核验的流程方法。

传入参数：

| 参数类型                                                     | 参数名称     | 参数含义                   |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [VerificationConfig](#VerificationConfig)                    | verifiConfig | eKYC本次流程启动的配置信息 |
| [TXYVerifiKitProcessSucceedBlock](#TXYVerifiKitProcessSucceedBlock) | succCallback | eKYC SDK检测成功回调       |
| [TXYVerifiKitProcessFailedBlock](#TXYVerifiKitProcessFailedBlock) | failCallback | eKYC SDK检测失败回调       |



### VerificationConfig

VerificationConfig是在启动eKYC SDK时的配置实体类，主要包含了以下属性。

| 类型                          | 名称           | 含义                                              | 默认值            |
| ----------------------------- | -------------- | ------------------------------------------------- | ----------------- |
| NSString                      | ekycToken      | 从服务器端获取的Token值，作为此次核身唯一业务凭证 | 空                |
| NSString                      | licPath        | 客户申请的用户授权Licens文件路径                  | 空                |
| long                          | verAutoTimeOut | 鉴伪SDK的超时时间                                 | 20000毫秒（20秒） |
| long                          | hyFaceTimeOut  | 人脸核身单一动作的超时时间                        | 10000毫秒（10秒） |
| BOOL                          | isHiddenAlbum  | 是否隐藏OCR相册按钮                               | NO                |
| BOOL                          | isHiddenFlash  | 是否隐藏OCR手电筒按钮                             | NO                |
| [LanguageType](#LanguageType) | languageType   | 本次流程的语言风格                                | DEFAULT (0)       |

##### OCRRegionType
核验卡证的类型

| 枚举名 | 说明               |
| ---------------- | ---------------- |
|OCR_TYPE_HK|中国香港证件|
|OCR_TYPE_ML|马来西亚证件|
|OCR_TYPE_PV_ID|菲律宾-驾驶执照|
|OCR_TYPE_PDL|菲律宾-VoteID|

### LanguageType

eKYC默认界面的多语言配置信息。

| LanguageType类型 | 含义             |
| ---------------- | ---------------- |
| DEFAULT          | 跟随系统语言版本 |
| EN               | 英语             |
| ZH_HANS          | 简体中文         |
| ZH_HANT          | 繁体中文         |



### TXYVerifiKitProcessSucceedBlock

eKYC SDK检测成功回调。

```objective-c
/// SDKKIt处理成功回调接口
/// @param errorCode 错误码
/// @param resultInfo 回调返回的信息
/// @param reserved 预留位
typedef void (^TXYVerifiKitProcessSucceedBlock)(int errorCode,id _Nonnull resultInfo, id _Nullable reserved);
```



### TXYVerifiKitProcessFailedBlock

eKYC SDK检测失败回调。

```objective-c
/// SDKKIt处理失败回调接口
/// @param errorCode 错误码
/// @param errorMsg 错误信息
/// @param reserved 预留位
typedef void (^TXYVerifiKitProcessFailedBlock)(int errorCode, NSString *_Nonnull errorMsg, id _Nullable reserved);
```



### 错误码与含义

| 错误码                                | 错误码值 | 错误码含义               |
| ------------------------------------- | -------- | ------------------------ |
| HY_SUCCESS                            | 0        | 成功                     |
| HY_VERIFI_FAIL                        | -1       | 检测失败                 |
| HY_VERIFI_OCR_FAIL                    | -2       | 卡证识别失败             |
| HY_SDK_INNER_ERR                      | -4       | 慧眼EKYC内部错误         |
| HY_INITIALIZATION_PARAMETER_EXCEPTION | 310      | 初始化参数异常           |
| HY_BUNDLE_CONFIGURATION_EXCEPTION     | 311      | bundle配置异常           |
| HY_YTSDK_CONFIGURATION_EXCEPTION      | 312      | 优图配置异常             |
| HY_PLEASE_CALL_FIRST_INIT_API         | 313      | 先调用初始化接口         |
| HY_SDK_AUTH_FAILED                    | 314      | SDK 授权失败             |
| HY_USER_VOLUNTARILY_CANCELED          | 315      | 用户手动取消             |
| HY_YTSDK_LOCAL_AUTH_FAILED            | 316      | SDK 人脸本地检测失败     |
| HY_CAMERA_OPEN_FAIL                   | 317      | 相机开启失败             |
| HY_DONOT_SWITCH_APPS                  | 318      | 请勿在核身过程中切换应用 |
| HY_CAMEREA_PERMISSION_EXCEPTION       | 319      | 摄像头权限异常           |
| HY_SDK_VEDIO_CUT_EXCEPTION            | 320      | 视频裁剪失败             |
| HY_LIGHT_DATA_FORMAT_EXCEPTION        | 321      | 光线数据格式错误         |
| HY_GET_REMOTE_DATA_EXCEPTION          | 322      | 光线数据格式错误         |

