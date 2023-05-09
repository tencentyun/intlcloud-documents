## API的详细说明

慧眼SDK主要涉及如下几个类，它们分别是API的接口类HuiYanOsApi， 参数配置类HuiYanOsConfig，结果回调类HuiYanOsAuthCallBack和HuiYanAuthEventCallBack。

### HuiYanOsApi

| API                                               | 功能描述                                           |
| ------------------------------------------------- | -------------------------------------------------- |
| [init()](#init())                                 | 初始化接口                                         |
| [release()](#release())                           | 资源释放接口                                       |
| [setAuthEventCallBack()](#setAuthEventCallBack()) | 设置核身过程中的核身关键动作的回调                 |
| [startHuiYanAuth()](#startHuiYanAuth())           | 海外核身接口，只需调用此接口即可完成整体核身流程。 |



#### init()

功能介绍：

慧眼SDK的初始化接口。

```java
public static void init(Context context)
```

传入参数:	

| 参数类型 | 参数名称 | 参数含义        |
| -------- | -------- | --------------- |
| Context  | context  | App的上下文信息 |



#### release()

功能介绍：

慧眼SDK资源释放的接口。

```java
public static void release() 
```




#### setAuthEventCallBack()

功能介绍：

用来注册核身过程中的核身关键动作的回调。

```java
public static void setAuthEventCallBack(HuiYanAuthEventCallBack authEventCallBack)
```

传入参数：

| 参数类型                                            | 参数名称                | 参数含义           |
| --------------------------------------------------- | ----------------------- | ------------------ |
| [HuiYanAuthEventCallBack](#HuiYanAuthEventCallBack) | huiYanAuthEventCallBack | 核身关键动作的回调 |



#### startHuiYanAuth()
功能介绍：

海外核身接口，只需调用此接口即可完成整体核身流程。

```java
public static void startHuiYanAuth(final String startToken, final HuiYanOsConfig startConfig, HuiYanOsAuthCallBack authCallBack)
```

传入参数：

| 参数类型                                      | 参数名称     | 参数含义                              |
| --------------------------------------------- | ------------ | ------------------------------------- |
| String                                        | startToken   | 从服务器兑换来启动核身使用的业务Token |
| [HuiYanOsConfig](#HuiYanOsConfig)             | startConfig  | 配置的参数                            |
| [HuiYanOsAuthCallBack](#HuiYanOsAuthCallBack) | authCallBack | 活体结果的回调                        |




### HuiYanOsConfig

HuiYanOsConfig是在启动慧眼SDK时的配置实体类，主要包含了以下属性。

| 类型                              | 名称               | 含义                                        | 默认值               |
| --------------------------------- | ------------------ | ------------------------------------------- | -------------------- |
| [PageColorStyle](#PageColorStyle) | pageColorStyle     | 此次人脸核身检测的配色                      | PageColorStyle.Light |
| String                            | authLicense        | 客户申请的用户核审授权的Licens文件名        | 空                   |
| long                              | authTimeOutMs      | 设置活体检测的超时时间                      | 10000毫秒（10秒）    |
| boolean                           | isDeleteVideoCache | 是否删除核身视频的本地缓存                  | true                 |
| boolean                           | isShowGuidePage    | 是否打开核身的引导页                        | true                 |
| boolean                           | isNeedBestImage    | 是否需要返回最佳帧                          | false                |
| LanguageStyle                     | languageStyle      | 语言类型                                    | 跟随系统语言         |
| String                            | languageCode       | 语言码（见附录），配合languageStyle一起使用 | 空                   |
| String[]                          | backUpIPs          | 备用IP列表                                  | 空                   |
| String                            | backUpHost         | 备用域名                                    | 空                   |
| AuthUiConfig                      | authUiConfig       | UI配置项                                    | 空                   |



### PageColorStyle

默认核身界面默认配色的枚举类，当前主要包括了两种配色，白色系与黑暗色系。

| PageColorStyle 类型  | 含义       |
| -------------------- | ---------- |
| PageColorStyle.Light | 亮色调配色 |
| PageColorStyle.Dark  | 暗色调配色 |



### LanguageStyle

| LanguageStyle 类型                | 含义       |
| --------------------------------- | ---------- |
| LanguageStyle.AUTO                | 跟随系统   |
| LanguageStyle.ENGLISH             | 英语       |
| LanguageStyle.SIMPLIFIED_CHINESE  | 简体中文   |
| LanguageStyle.TRADITIONAL_CHINESE | 繁体中文   |
| LanguageStyle.CUSTOMIZE_LANGUAGE  | 自定义语言 |



### AuthUiConfig

核身页面自定义UI的参数配置

| 类型                    | 名称                   | 含义                                                       | 默认值 |
| ----------------------- | ---------------------- | ---------------------------------------------------------- | ------ |
| [VideoSize](#VideoSize) | videoSize              | 核身过程中的分辨率                                         | 480P   |
| boolean                 | isShowCountdown        | 是否显示倒计时的控件                                       | true   |
| boolean                 | isShowErrorDialog      | 是否显示错误的dialog                                       | true   |
| int                     | authLayoutResId        | 核身导出客户自定义的布局resID，不调整使用-1                | -1     |
| int                     | feedBackErrorColor     | 异常反馈Tips的颜色（0xFFFFFFFF的类型）不调整使用-1         | -1     |
| int                     | feedBackTxtColor       | 正常反馈Tips颜色（0xFFFFFFFF的类型）不调整使用-1           | -1     |
| int                     | authCircleErrorColor   | 动作错背景圆形框的颜色（0xFFFFFFFF的类型）不调整使用-1     | -1     |
| int                     | authCircleCorrectColor | 动作正确时背景圆形框的颜色（0xFFFFFFFF的类型）不调整使用-1 | -1     |
| int                     | authLayoutBgColor      | 核身界面背景的颜色（0xFFFFFFFF的类型）不调整使用-1         | -1     |



### VideoSize

慧眼核身支持的分辨率枚举

| VideoSize类型       | 含义 |
| ------------------- | ---- |
| VideoSize.SIZE_480P | 480P |
| VideoSize.SIZE_720P | 720P |



### HuiYanOsAuthResult

核身流程的成功回调对应的结果类型。

| 类型   | 名称      | 含义                       | 模式值 |
| ------ | --------- | -------------------------- | ------ |
| String | token     | 此次活体流程中使用的token  | 空     |
| String | bestImage | 活体最佳帧图片的Base64数据 | 空     |

最后需要通过这个token，去腾讯云API的后台接口[GetFaceldResultIntl](//TODO:)拉取最终活体是否成功的数据。



### HuiYanOsAuthCallBack

核身流程的回调接口

```java
/**
 * 海外的结果回调
 *
 * @author jerrydong
 * @since 2022/6/10
 */
public interface HuiYanOsAuthCallBack {

    /**
     * 活体成功回调
     *
     * @param authResult 结果
     */
    void onSuccess(HuiYanOsAuthResult authResult);

    /**
     * 活体失败
     *
     * @param errorCode 错误码
     * @param errorMsg 错误信息
     * @param token 本次核身使用的
     */
    void onFail(int errorCode, String errorMsg, String token);
}
```



### HuiYanAuthEventCallBack

用来监听核身过程中的关键事件的回调，以及如果需要使用自定义布局的UI绑定可以[事件绑定(可以参考自定义能力的文档)](https://iwiki.woa.com/pages/viewpage.action?pageId=4007948338)。

```java
/**
 * 慧眼SDK核身的事件回调
 */
public interface HuiYanAuthEventCallBack {

    /**
     * 核身时tips发生改变的事件通知回调
     *
     * @param tipsEvent tips关键事件
     */
    void onAuthTipsEvent(HuiYanAuthTipsEvent tipsEvent);

    /**
     * 核身的Event事件
     *
     * @param authEvent authEvent
     */
    void onAuthEvent(HuiYanAuthEvent authEvent);

    /**
     * 当认证的主View被创建的回调
     *
     * @param authView
     */
    void onMainViewCreate(View authView);

    /**
     * 界面被回收的回调
     */
    void onMainViewDestroy();

}
```



### 错误码

这里是SDK在失败回调中的错误码，目前慧眼海外版SDK包含的错误码与其含义如下：

| 错误码                                | 错误码值 | 错误码含义                                                   |
| ------------------------------------- | -------- | ------------------------------------------------------------ |
| HY_NETWORK_ERROR                      | 210      | 网络请求出现异常                                             |
| HY_LOCAL_REF_FAILED_ERROR             | 211      | 本地初始化SDK时，检测失败，常见异常不存在license文件或者license过期 |
| HY_USER_CANCEL_ERROR                  | 212      | 用户主动取消核身流程                                         |
| HY_INNER_ERROR_CODE                   | 213      | SDK内部产生的异常，终止了核身流程                            |
| HY_DO_NOT_CHANGE_ERROR                | 214      | 在核身过程中切换应用发生终止流程的异常                       |
| HY_CAMERA_PERMISSION_ERROR            | 215      | 获取摄像头过程中发生异常                                     |
| HY_INIT_SDK_ERROR                     | 216      | 未调用init()方法，直接调用了                                 |
| HY_VERIFY_LOCAL_ERROR                 | 217      | 本地人脸检测失败                                             |
| HY_PERMISSION_CHECK_ERROR             | 218      | 本地SDK所需要的权限不足                                      |
| HY_APP_STOP_ERROR                     | 219      | 集成者主动终止核身流程，startAuthByLightData的reflectSequence为null时 |
| HY_CHECK_LIVE_DATA_ERROR              | 220      | 传入的光线序列参数校验失败                                   |
| HY_INITIALIZATION_PARAMETER_EXCEPTION | 221      | 在未获取设备配置的前提下，直接调用了设置光线序列参数的方法时，会出现的异常 |
| HY_VERIFY_LOCAL_TIME_OUT              | 222      | 本地核身动作检测超时                                         |
| HY_PREPARE_TIME_OUT                   | 223      | 准备过程超时（启动摄像头到第一次检测到人脸的时间超时）       |
| HY_CHECK_PERMISSION_ERROR             | 224      | SDK内部申请摄像头权限失败                                    |
