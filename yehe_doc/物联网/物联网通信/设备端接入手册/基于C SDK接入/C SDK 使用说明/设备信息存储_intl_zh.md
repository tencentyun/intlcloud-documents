
## 概述
腾讯云物联网平台为每个创建的产品分配唯一标识 ProductID，用户可以自定义 DeviceName 标识设备，用产品标识 + 设备标识 + 设备证书/密钥来验证设备的合法性。设备端需要存储这些设备身份信息。C-SDK 提供了读写设备信息的接口及参考实现，可根据实际情况进行适配。

## 设备身份信息
 - 证书设备要通过平台的安全认证，必须具备四元组信息：产品 ID（ProductId）、设备名（DeviceName）、设备证书文件（DeviceCert）、设备私钥文件（DevicePrivateKey），其中证书文件和私钥文件由平台生成，且一一对应。
 - 密钥设备要通过平台的安全认证，必须具备三元组信息：产品 ID（ProductId）、设备名（DeviceName）、设备密钥（DeviceSecret），其中设备密钥由平台生成。

## 设备身份信息烧录
设备信息烧录分为预置烧录和动态烧录，两者在应用的便捷性和安全性上有区别。

#### 预置烧录
创建产品后，在 [物联网通信控制台](https://console.cloud.tencent.com/iotcloud) 或者通过云 API逐个创建设备，并获取对应的设备信息，将上述的四元组或者三元组信息，在设备生产的特定环节，烧录到非易失介质中，设备 SDK 运行时读取存放的设备信息，进行设备认证。

#### 动态烧录
 - 预置烧录：需要在量产过程执行个性化生产动作，影响生产效率，为增加应用的便捷性，平台支持动态烧录的方式。实现方式：产品创建后使能产品的动态注册功能，则会生成产品密钥（ProductSecret）。同一产品下的所有设备在生产过程可以烧录统一的产品信息，即产品 ID（ProductId）、产品密钥（ProductSecret）。设备出厂后，通过动态注册的方式获取设备身份信息并保存，然后用申请到的三元组或者四元组信息进行设备认证。
 - 动态烧录设备名（DeviceName）的生成：若使能动态注册的同时使能自动设备创建，则设备名是可以设备自己生成的，但必须保证同一产品 ID（ProductId）下的设备名不重复，一般取 IMEI 或者 MAC 地址。若使能动态注册的同时不使能自动设备创建，则需要把设备名预先录入平台，设备动态注册时会校验所申请的设备名是否为合法录入的设备名，此种方式能在一定程度降低产品密钥泄露后的安全风险。

>!动态注册需要确保产品密钥（ProductSecret）的安全，否则会产生较大的安全隐患。

## 设备信息读写接口

SDK 提供了设备信息读写的 HAL 接口，必须实现。可以参考 Linux 平台 HAL_Device_Linux.c 中设备信息读写的实现。

设备信息 HAL 接口 ：

| HAL_API                            | 说明                                 |
| -----------------------------------| ----------------------------------  |
| HAL_SetDevInfo                  	| 设备信息写入    |
| HAL_GetDevInfo                   	| 设备信息读取    |

## 开发阶段设备信息配置

创建设备之后，需要将设备信息（`ProductID/DeviceName/DeviceSecret/Cert/Key`文件）配置在 SDK 中才能正确运行示例。在开发阶段，SDK 提供两种方式存储设备信息：
1. 存放在代码中（编译选项 DEBUG_DEV_INFO_USED = ON），则在`platform/os/xxx/HAL_Device_xxx.c`中修改设备信息，在无文件系统的平台下可以使用这种方式。

```
/* product Id  */
static char sg_product_id[MAX_SIZE_OF_PRODUCT_ID + 1]	 = "PRODUCT_ID";

/* device name */
static char sg_device_name[MAX_SIZE_OF_DEVICE_NAME + 1]  = "YOUR_DEV_NAME";

#ifdef DEV_DYN_REG_ENABLED
/* product secret for device dynamic Registration  */
static char sg_product_secret[MAX_SIZE_OF_PRODUCT_SECRET + 1]  = "YOUR_PRODUCT_SECRET";
#endif

#ifdef AUTH_MODE_CERT
/* public cert file name of certificate device */
static char sg_device_cert_file_name[MAX_SIZE_OF_DEVICE_CERT_FILE_NAME + 1]      = "YOUR_DEVICE_NAME_cert.crt";
/* private key file name of certificate device */
static char sg_device_privatekey_file_name[MAX_SIZE_OF_DEVICE_SECRET_FILE_NAME + 1] = "YOUR_DEVICE_NAME_private.key";
#else
/* device secret of PSK device */
static char sg_device_secret[MAX_SIZE_OF_DEVICE_SECRET + 1] = "YOUR_IOT_PSK";
#endif
```

2. 存放在配置文件中（编译选项 DEBUG_DEV_INFO_USED = OFF），则在`device_info.json`文件修改设备信息，此方式下更改设备信息不需重新编译 SDK，在 Linux/Windows 平台下开发推荐使用这种方式。

```
{
    "auth_mode":"KEY/CERT",

    "productId":"PRODUCT_ID",
    "productSecret":"YOUR_PRODUCT_SECRET",
    "deviceName":"YOUR_DEV_NAME",

    "key_deviceinfo":{    
        "deviceSecret":"YOUR_IOT_PSK"
    },

    "cert_deviceinfo":{
        "devCertFile":"YOUR_DEVICE_CERT_FILE_NAME",
        "devPrivateKeyFile":"YOUR_DEVICE_PRIVATE_KEY_FILE_NAME"
    },

    "subDev":{
        "sub_productId":"YOUR_SUBDEV_PRODUCT_ID",
        "sub_devName":"YOUR_SUBDEV_DEVICE_NAME"
    }
}
```

##  应用示例
-  初始化连接参数

```
static DeviceInfo sg_devInfo;

static int _setup_connect_init_params(MQTTInitParams* initParams)
{
	int ret;
	
	ret = HAL_GetDevInfo((void *)&sg_devInfo);	
	if(QCLOUD_ERR_SUCCESS != ret){
		return ret;
	}
		
	initParams->device_name = sg_devInfo.device_name;
	initParams->product_id = sg_devInfo.product_id;
	 ......
}	
```

-  密钥设备鉴权参数生成

```
static int _serialize_connect_packet(unsigned char *buf, size_t buf_len, MQTTConnectParams *options, uint32_t *serialized_len) {
			......
			......
    int username_len = strlen(options->client_id) + strlen(QCLOUD_IOT_DEVICE_SDK_APPID) + MAX_CONN_ID_LEN + cur_timesec_len + 4;
    options->username = (char*)HAL_Malloc(username_len);
    get_next_conn_id(options->conn_id);
	HAL_Snprintf(options->username, username_len, "%s;%s;%s;%ld", options->client_id, QCLOUD_IOT_DEVICE_SDK_APPID, options->conn_id, cur_timesec);

#if defined(AUTH_WITH_NOTLS) && defined(AUTH_MODE_KEY)
     if (options->device_secret != NULL && options->username != NULL) {
    	 char                sign[41]   = {0};
    	 utils_hmac_sha1(options->username, strlen(options->username), sign, options->device_secret, options->device_secret_len);
    	 options->password = (char*) HAL_Malloc (51);
    	 if (options->password == NULL) IOT_FUNC_EXIT_RC(QCLOUD_ERR_INVAL);
		 HAL_Snprintf(options->password, 51, "%s;hmacsha1", sign);
     }
#endif
			......
}
```


