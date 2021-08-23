IoT Hub device SDK for Android relies on a secure and powerful data channel to enable IoT developers to quickly connect devices to the cloud for two-way communication. You only need to complete the corresponding project configuration to connect devices.

## Prerequisites
Products and devices have been created as instructed in [Device Connection Preparations](https://intl.cloud.tencent.com/document/product/1105/41476).

## How to Import
#### SDK integration
If you don't need to run the IoT Hub SDK in the service component, only dependency on [iot_core](https://github.com/tencentyun/iot-device-java/tree/master/hub/hub-device-android/iot_core) is required.
 - Depend on Maven for remote build. Below is the sample code:
```gr
dependencies {
			implementation 'com.tencent.iot.hub:hub-device-android-core:x.x.x'
			implementation 'com.tencent.iot.hub:hub-device-android-service:x.x.x'
}
```
>?
>
>- You can set the above x.x.x to the latest version according to [SDK for Android Release Notes](https://intl.cloud.tencent.com/document/product/1105/41855).
>- If you don't need to run the IoT Hub SDK in the service component, only dependency on `iot_core` is required.
>- If you need to run the IoT Hub SDK in the service component, only dependency on `iot_service` is required.
>

 - Depend on the local SDK source code for build:
   Modify the [build.gradle](https://github.com/tencentyun/iot-device-java/blob/master/hub/hub-android-demo/build.gradle) of the application module to make it dependent on the [iot_core](https://github.com/tencentyun/iot-device-java/tree/master/hub/hub-device-android/iot_service) and [iot_service](https://github.com/tencentyun/iot-device-java/tree/master/hub/hub-device-android/iot_service) source code. Below is the sample code:
```gr
dependencies {
			implementation project(':hub:hub-device-android:iot_core')
			implementation project(':hub:hub-device-android:iot_service')
}
```

## Connection Authentication

Edit the configuration information in the [app-config.json](https://github.com/tencentyun/iot-device-java/blob/master/hub/hub-android-demo/app-config.json) file so that the following data in [IoTMqttFragment.java](https://github.com/tencentyun/iot-device-java/blob/master/hub/hub-android-demo/src/main/java/com/tencent/iot/hub/device/android/app/IoTMqttFragment.java) can be read:

``` gr
{
			"PRODUCT_ID":        "",
			"DEVICE_NAME":       "",
			"DEVICE_PSK":        "",
			"SUB_PRODUCT_ID":    "",
			"SUB_DEV_NAME":      "",
			"SUB_PRODUCT_KEY":   "",
			"TEST_TOPIC":        "",
			"SHADOW_TEST_TOPIC": "",
			"PRODUCT_KEY":       ""
 }
```

The SDK supports two authentication methods: certificate authentication and key authentication, which should be selected and set according to the authentication type of the created product.
- For key authentication, you need to enter the parameters corresponding to `PRODUCT_ID`, `DEVICE_NAME`, and `DEVICE_PSK` in the configuration information in [app-config.json](https://github.com/tencentyun/iot-device-java/blob/master/hub/hub-android-demo/app-config.json). The SDK will automatically generate a signature based on the device configuration information as a credential for connection to IoT Hub.
- For certificate authentication, you need to enter the `PRODUCT_ID` and `DEVICE_NAME` in the configuration information in [app-config.json](https://github.com/tencentyun/iot-device-java/blob/master/hub/hub-android-demo/app-config.json) and read the content of the device certificate and private key files in either of the following two ways:
 - Read through `AssetManager`. In this case, you need to create the `assets` directory under the `hub/hub-android-demo/src/main` path of the project and place the device certificate and private key files in it.
 - Read through `InputStream`. In this case, you need to pass in the full path information of the device certificate and private key files.
   1. After successfully reading the certificate and private key files, you need to set the `mDevCertName` certificate name and `mDevKeyName` private key name in [IoTMqttFragment.java](https://github.com/tencentyun/iot-device-java/blob/master/hub/hub-android-demo/src/main/java/com/tencent/iot/hub/device/android/app/IoTMqttFragment.java).
```
	private String mDevCertName = "YOUR_DEVICE_NAME_cert.crt";
	private String mDevKeyName  = "YOUR_DEVICE_NAME_private.key";
```
   2. After the configuration is completed, call the MQTT connection APIs of the SDK in the project to complete device connection.
   ``` java
    mMqttConnection = new TXGatewayConnection(mContext, mBrokerURL, mProductID, mDevName, mDevPSK,null,null ,mMqttLogFlag, mMqttLogCallBack, mMqttActionCallBack);
    mMqttConnection.connect(options, mqttRequest);
   ```

