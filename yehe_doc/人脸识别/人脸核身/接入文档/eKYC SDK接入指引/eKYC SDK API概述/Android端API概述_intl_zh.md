Android端eKYC SDK主要涉及的类主要包含EkycHySdk、EkycHyConfig、EkycHyCallBack这几个主要类型下面对其支持的API做出详细说明。

### EkycHySdk

EkycHySdk为eKYC SDK的对外接口类，主要逻辑也都是调用此类完成。

| API                                   | 功能描述                 |
| ------------------------------------- | ------------------------ |
| [init()](#init())                     | 初始化接口               |
| [release()](#release())               | 资源释放接口             |
| [startEkycCheck()](#startEkycCheck()) | 启动身份认证eKYC检测流程 |

#### init()

```java
public static void init(Context context)
```

功能介绍：

​	eKYC SDK的初始化接口。

传入参数:	

| 参数类型 | 参数名称 | 参数含义        |
| -------- | -------- | --------------- |
| Context  | context  | App的上下文信息 |



#### release()

```java
public static void release() 
```

功能介绍：

​	eKYC SDK资源释放的接口。



#### startEkycCheck()

```java
public static void startEkycCheck(final String ekycToken, EkycHyConfig ekycHyConfig,
            EkycHyCallBack ekycHyCallBack)
```

功能介绍：

​	启动身份认证eKYC检测流程的流程函数。

传入参数：

| 参数类型                          | 参数名称       | 参数含义                                          |
| --------------------------------- | -------------- | ------------------------------------------------- |
| String                            | ekycToken      | 从服务器端获取的Token值，作为此次流程唯一业务凭证 |
| [EkycHyConfig](#EkycHyConfig)     | ekycHyConfig   | eKYC本次流程启动的配置信息                        |
| [EkycHyCallBack](#EkycHyCallBack) | ekycHyCallBack | 用来接收认证结果回调的接口                        |



### EkycHyConfig

EkycHyConfig是在启动eKYC SDK时的配置实体类，主要包含了以下属性。

| 类型                            | 名称           | 含义                           | 默认值             |
| ------------------------------- | -------------- | ------------------------------ | ------------------ |
| [OcrUiConfig](#OcrUiConfig)     | ocrUiConfig    | ocr界面的一些自定义配置        | null               |
| String                          | licenseName    | 客户申请的用户授权Licens文件名 | 空                 |
| int                             | verAutoTimeOut | 卡证鉴伪的超时时间             | 20000毫秒（20秒）  |
| int                             | hyFaceTimeOut  | 人脸核身单一动作的超时时间     | 10000毫秒（10秒）  |
| [LanguageStyle](#LanguageStyle) | languageStyle  | 本次流程的语言风格             | LanguageStyle.AUTO |

### OcrRegionType
检测证件类型
|枚举名|说明|
|---|---|
|HK|中国香港证件|
|ML|马来西亚证件|
|PhilippinesDrivingLicense|菲律宾-驾驶执照|
|PhilippinesVoteID|菲律宾-VoteID|


### LanguageStyle

eKYC默认界面的多语言配置信息。

| LanguageStyle类型                 | 含义             |
| --------------------------------- | ---------------- |
| LanguageStyle.AUTO                | 跟随系统语言版本 |
| LanguageStyle.ENGLISH             | 英语             |
| LanguageStyle.SIMPLIFIED_CHINESE  | 简体中文         |
| LanguageStyle.TRADITIONAL_CHINESE | 繁体中文         |



### OcrUiConfig

| 类型    | 名称          | 含义                            | 默认值 |
| ------- | ------------- | ------------------------------- | ------ |
| boolean | isRemoveAlbum | OCR识别界面中是否隐藏相册按钮   | false  |
| boolean | isRemoveFlash | OCR识别界面中是否隐藏闪光灯按钮 | false  |



### EkycHyCallBack

用于接收eKYC流程结果的监听类。

```java
/**
 * eKYC的结果回调类
 */
public interface EkycHyCallBack {

    /**
     * 识别成功的结果信息
     *
     * @param result 结果信息
     */
    void onSuccess(EkycHyResult result);

    /**
     * eKYC流程失败的内容
     *
     * @param errorCode 错误码
     * @param errorMsg 错误信息
     * @param ekycToken 当次流程的token
     */
    void onFail(int errorCode, String errorMsg, String ekycToken);
}
```

其中[EkycHyResult](#EkycHyResult) 是成功返回的结果对象

### EkycHyResult

EkycHyResult是eKYC SDK流程成功后的结果对象。

| 类型   | 名称      | 含义                                                         | 默认值 |
| ------ | --------- | ------------------------------------------------------------ | ------ |
| String | ekycToken | 当次eKYC流程的token，此token可以在服务器拉取身份认证过程关键数据 | 空     |



### 错误码与含义

| 错误码 | 对应含义                   |
| ------ | -------------------------- |
| 12000  | 用户主动取消               |
| 12001  | 网络请求失败               |
| 12002  | OCR识别异常导致的错误      |
| 12003  | 本地人脸检测失败引起的异常 |
| 12004  | 失效的token                |
| 12005  | 本地卡证鉴伪失败           |
| 12006  | eKYC SDK初始化流程失败     |
| 12007  | 启动参数校验失败           |
| 12008  | 人脸核身结果返回失败       |
| 12009  | 人脸核身过程本地失败       |



