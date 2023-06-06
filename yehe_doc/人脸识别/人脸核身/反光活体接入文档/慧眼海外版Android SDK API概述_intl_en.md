## eKYC SDK for Android API Overview

The eKYC SDK mainly involves the following classes: `HuiYanOsApi` (API class), `HuiYanOsConfig` (parameter configuration class), and `HuiYanConfigCallback` and `HuiYanResultCallBack` (result callback classes).

### HuiYanOsApi

| API                                                   | Feature Description                                             |
| ----------------------------------------------------- | ---------------------------------------------------- |
| [init()](#init())                                     | Initializes eKYC SDK                                        |
| [release()](#release())                               | Releases resources                                         |
| [startGetAuthConfigData()](#startGetAuthConfigData()) | Gets the local configuration information of the eKYC SDK                        |
| [startAuthByLightData()](#startAuthByLightData())     | Passes in the light sequence obtained by the server to continue the liveness detection for identity verification  |

#### init()

```java
public static void init(Context context)
```

Feature overview:

	This API is used to initialize the eKYC SDK.

Input parameters:	

| Parameter Type | Parameter | Description        |
| -------- | -------- | --------------- |
| Context  | context  | App context information |



#### release()

```java
public static void release() 
```

Feature overview:

	This API is used to release the eKYC SDK resources.





#### startGetAuthConfigData()

```java
public static void startGetAuthConfigData(HuiYanOsConfig startConfig, HuiYanConfigCallback configCallback) 
```

Feature overview:

	This API is used to pull the eKYC SDK configuration parameters during local detection as the parameters for subsequent acquisition of the light sequence.

Input parameters:

| Parameter Type | Parameter | Description        |
| --------------------------------------------- | -------------- | ------------------ |
| [HuiYanOsConfig](#HuiYanOsConfig)             | startConfig    | Configuration parameter         |
| [HuiYanConfigCallback](#HuiYanConfigCallback) | configCallback | Callback for configuration result pull |



#### startAuthByLightData()

```java
public static void startAuthByLightData(String reflectSequence, HuiYanResultCallBack resultCallBack) 
```

Feature overview:

	This API is used to pass in the light sequence data pulled from the server to the eKYC SDK and continue the identity verification process to get the local detection result.

Input parameters:

| Parameter Type | Parameter | Description        |
| --------------------------------------------- | --------------- | ------------------------------------ |
| String                                        | reflectSequence | Light sequence obtained from the server to start identity verification |
| [HuiYanResultCallBack](#HuiYanResultCallBack) | resultCallBack  | Callback for the local identity verification result                   |



### HuiYanOsConfig

`HuiYanOsConfig` is the configuration entity class during eKYC SDK start, which mainly contains the following attributes:

| Type           | Name               | Description                                 | Default Value               |
| -------------- | ------------------ | ------------------------------------ | -------------------- |
| PageColorStyle | pageColorStyle     | Color pattern of the current face recognition                | PageColorStyle.Light |
| String         | authLicense        | Name of the license file requested for user identity verification | Empty                   |
| long                          | authTimeOutMs      | Liveness detection timeout period               | 10000 milliseconds (10 seconds) |
| boolean        | isDeleteVideoCache | Specifies whether to delete the local cache of the video for identity verification           | true                 |



### PageColorStyle

This is the enumeration class of default color patterns on the default identity verification UI. Currently, two color patterns are supported: light and dark.

| PageColorStyle Type   | Description       |
| -------------------- | ---------- |
| PageColorStyle.Light | Light pattern |
| PageColorStyle.Dark  | Dark pattern |



### HuiYanConfigCallback

Callback class for initialization and local configuration acquisition.

```java
/**
 * Callback for eKYC SDK initialization and local configuration pull
 */
public interface HuiYanConfigCallback {

    /**
     * API for configuration acquisition success
     *
     * @param result Configuration information
     */
    void onSuccess(String result);

    /**
     * API for configuration acquisition failure
     *
     * @param errorCode Error code
     * @param errMsg Error message
     */
    void onFail(int errorCode, String errMsg);
}
```



### HuiYanResultCallBack

Callback class for local identity verification process and local result acquisition.

```java
/**
 * Callback type for identity verification completion
 */
public interface HuiYanResultCallBack {

    /**
     * Callback success data
     *
     * @param data Data for comparison
     * @param videoPath Path of the video for identity verification
     */
    void onSuccess(byte[] data, String videoPath);

    /**
     * Callback failure result
     *
     * @param errorCode Error code
     * @param errMsg Error details
     */
    void onFail(int errorCode, String errMsg);
}
```

