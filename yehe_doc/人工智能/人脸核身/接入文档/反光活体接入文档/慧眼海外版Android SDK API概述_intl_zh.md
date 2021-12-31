## 慧眼SDK Android API概述

慧眼SDK主要涉及如下几个类，它们分别是API的接口类HuiYanOsApi， 参数配置类HuiYanOsConfig，结果回调类HuiYanConfigCallback以及HuiYanResultCallBack。

### HuiYanOsApi

| API                                                   | 功能描述                                             |
| ----------------------------------------------------- | ---------------------------------------------------- |
| [init()](#init())                                     | 初始化接口                                           |
| [release()](#release())                               | 资源释放接口                                         |
| [startGetAuthConfigData()](#startGetAuthConfigData()) | 获取慧眼SDK本地配置信息的接口                        |
| [startAuthByLightData()](#startAuthByLightData())     | 传入服务器获取的光线序列，继续完成活体核身检测的接口 |

#### init()

```java
public static void init(Context context)
```

功能介绍：

​	慧眼SDK的初始化接口。

传入参数:	

| 参数类型 | 参数名称 | 参数含义        |
| -------- | -------- | --------------- |
| Context  | context  | App的上下文信息 |



#### release()

```java
public static void release() 
```

功能介绍：

​	慧眼SDK资源释放的接口。





#### startGetAuthConfigData()

```java
public static void startGetAuthConfigData(HuiYanOsConfig startConfig, HuiYanConfigCallback configCallback) 
```

功能介绍：

​	本地检测慧眼SDK同时拉取配置参数，用来作为后续兑换光线序列的参数。

传入参数：

| 参数类型                                      | 参数名称       | 参数含义           |
| --------------------------------------------- | -------------- | ------------------ |
| [HuiYanOsConfig](#HuiYanOsConfig)             | startConfig    | 配置的参数         |
| [HuiYanConfigCallback](#HuiYanConfigCallback) | configCallback | 拉取配置结果的回调 |



#### startAuthByLightData()

```java
public static void startAuthByLightData(String reflectSequence, HuiYanResultCallBack resultCallBack) 
```

功能介绍：

​	将从服务器拉取到的光线序列数据，传入慧眼SDK同时继续核身流程，并获取本地检测的结果。

传入参数：

| 参数类型                                      | 参数名称        | 参数含义                             |
| --------------------------------------------- | --------------- | ------------------------------------ |
| String                                        | reflectSequence | 从服务器兑换来启动核身使用的光线序列 |
| [HuiYanResultCallBack](#HuiYanResultCallBack) | resultCallBack  | 本地核身的结果回调                   |



### HuiYanOsConfig

HuiYanOsConfig是在启动慧眼SDK时的配置实体类，主要包含了以下属性。

| 类型           | 名称               | 含义                                 | 默认值               |
| -------------- | ------------------ | ------------------------------------ | -------------------- |
| PageColorStyle | pageColorStyle     | 此次人脸核身检测的配色               | PageColorStyle.Light |
| String         | authLicense        | 客户申请的用户核审授权的Licens文件名 | 空                   |
| long           | authTimeOutMs      | 设置活体检测的超时时间               | 10000毫秒（10秒）    |
| boolean        | isDeleteVideoCache | 是否删除核身视频的本地缓存           | true                 |



### PageColorStyle

默认核身界面默认配色的枚举类，当前主要包括了两种配色，白色系与黑暗色系。

| PageColorStyle类型   | 含义       |
| -------------------- | ---------- |
| PageColorStyle.Light | 亮色调配色 |
| PageColorStyle.Dark  | 暗色调配色 |



### HuiYanConfigCallback

初始化并且获取本地配置的回调类

```java
/**
 * 新慧眼SDK初始化与拉取本地配置的回调
 */
public interface HuiYanConfigCallback {

    /**
     * 获取配置成功的接口
     *
     * @param result 配置信息
     */
    void onSuccess(String result);

    /**
     * 获取配置失败的接口
     *
     * @param errorCode 错误码
     * @param errMsg 错误信息
     */
    void onFail(int errorCode, String errMsg);
}
```



### HuiYanResultCallBack

本地核身流程与本地结果获取的回调类

```java
/**
 * 核身完成的回调类型
 */
public interface HuiYanResultCallBack {

    /**
     * 回调成功的数据
     *
     * @param data 比对数据
     * @param videoPath 核身视频路径
     */
    void onSuccess(byte[] data, String videoPath);

    /**
     * 回调失败的结果
     *
     * @param errorCode 错误码
     * @param errMsg 错误详细信息
     */
    void onFail(int errorCode, String errMsg);
}
```

