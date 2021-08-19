

IoT Hub device SDK for Java relies on a secure and powerful data channel to enable IoT developers to quickly connect devices to the cloud for two-way communication. You only need to complete the corresponding project configuration to connect devices.

## Prerequisites
Products and devices have been created as instructed in [Device Connection Preparations](https://intl.cloud.tencent.com/document/product/1105/41476).
## How to Import
- If you need to use JAR import for project development, you can add dependencies in `build.gradle` in the `module` directory as follows:
```
dependencies {
    ...
    implementation 'com.tencent.iot.hub:hub-device-java:x.x.x'
}
```
>?You can set the above x.x.x to the latest version according to [SDK for Java Release Notes](https://intl.cloud.tencent.com/document/product/1105/41858).
- If you need to develop a project through code integration, you can download the SDK for Java source code from [GitHub](https://github.com/tencentyun/iot-device-java/tree/master/hub/hub-device-java).

## Connection Authentication ##

Two device authentication methods are supported: key authentication and certificate authentication.
- Key authentication requires `ProductID`, `DevName`, and `DevPSK`.
- Certificate authentication requires `ProductID`, `CertFile`, and `PrivateKeyFile`.

Below is the sample code for connection authentication:
``` 
private String mProductID = "YOUR_PRODUCT_ID";
private String mDevName = "YOUR_DEVICE_NAME";
private String mDevPSK = "YOUR_DEV_PSK";
private String mCertFilePath = null;
private String mPrivKeyFilePath = null;
TXMqttConnection mqttconnection = new TXMqttConnection(mProductID, mDevName, mDevPSK, new callBack());
mqttconnection.connect(options, null);
try {
		Thread.sleep(20000);
} catch (InterruptedException e) {
	// TODO Auto-generated catch block
	e.printStackTrace();
}
mqttconnection.disConnect(null);
```
