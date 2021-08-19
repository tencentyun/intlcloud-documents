## MQTT Protocol Description

Currently, IoT Hub supports MQTT standard protocol access (compatible with v3.1.1). For more information, please see [MQTT Version 3.1.1](http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html).

### Differences from standard MQTT

1. PUB, SUB, PING, PONG, CONNECT, DISCONNECT, and UNSUB messages of MQTT are supported.
2. `cleanSession` is supported.
3. `will` and `retain msg` are not supported.
4. QoS 2 is not supported.

### Security level of MQTT channel

TLSv1, TLSv1.1, and TLSv1.2 protocols are supported to establish secure connections, delivering a high security level.

### Topic specification

By default, after a product is created, all devices under it will have the permissions of the following topic classes:

1. `${productId}/${deviceName}/control` for subscribing
2. `${productId}/${deviceName}/event` for publishing
3. `${productId}/${deviceName}/data` for subscribing and publishing
4. `$shadow/operation/${productId}/${deviceName}` for publishing. It is distinguished by the internal type of the packet (`update` or `get`, corresponding to updating or pulling the device shadow document).
5. `$shadow/operation/result/${productId}/${deviceName}` for subscribing. It is distinguished by the internal type of the packet (`update`, `get`, or `delta`). `update` and `get` correspond to updating and pulling the device shadow document respectively. After you modify the device shadow document through the RESTful API, the server will publish messages through this topic, whose type will be `delta` at this time.
6. `$ota/report/${productID}/${deviceName}` for publishing, through which the device reports the version number and the download/upgrade progress to the cloud.
7. `$ota/update/${productID}/${deviceName}` for subscribing, through which the device receives the upgrade message from the cloud.

## MQTT Connection

The MQTT protocol supports connection to the IoT Hub platform through two methods: device certificate and key signature. You can choose a method according to your own business scenario. The connection parameters are as follows:

| Connection Authentication Method | Connection Domain Name and Port | `Connect` Message Parameters |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Certificate | MQTT server connection address. For devices in the Guangzhou region, enter `${productId}.iotcloud.tencentdevices.com`, where `${productId}` is a variable parameter, and you need to enter the product ID automatically generated when you create the product, such as `1A17RZR3XX.iotcloud.tencentdevices.com`. Port: 8883 | <li> KeepAlive: the time to keep the connection alive, which ranges from 0 to 900s. If IoT Hub does not receive the client's data in more than 1.5 times the `KeepAlive` value, it will disconnect from the client. <br><li> ClientId: `${productId}${deviceName}`, which is a string combination of the product ID and device name. <br><li>UserName: `${productId}${deviceName};${sdkappid};${connid};${expiry}`. For more information, please see the `username` part in the "Guide to connecting key-authenticated device" section below. <br><li>PassWord: password, which can be any value. |
| Key  | The MQTT server connection address is the same as that for certificate authentication. Port: 1883 | <li>KeepAlive: the time to keep the connection alive, which ranges from 0 to 900s. <br><li>ClientId: `${productId}${deviceName}`. <br><li>UserName: `${productId}${deviceName};${sdkappid};${connid};${expiry}`. For more information, please see the `username` part in the "Guide to connecting key-authenticated device" section below. <br><li>PassWord: password. For more information, please see the `password` part in the "Guide to connecting key-authenticated device" section below. |

> ?The `PassWord` field will not be verified when a certificate-authenticated device is connected, so you can enter any value for it during certificate authentication.

### Guide to connecting certificate-authenticated device

IoT Hub uses TLS encryption to ensure the security of devices when transferring data. When a certificate-authenticated device is connected, after getting the certificate, key, and CA certificate files of the device, set the values of `KeepAlive`, `ClientId`, `UserName`, `PassWord`, etc. (this step is not required for devices connected through the Tencent Cloud device SDK, as the SDK can automatically generate the parameters based on the device information). Then, the device uploads the authentication files to the URL (connection domain name and port) corresponding to certificate authentication, and sends an `MqttConnect` message after successful authentication to complete the TCP-based MQTT connection.

### Guide to connecting key-authenticated device

IoT Hub supports HMACSHA256 and HMACSHA1 algorithms to generate digest signatures based on device keys. The process of connecting to IoT Hub through signature is as follows:
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud). You can create products, add devices, and get device keys in the console.
2. Generate the `username` field according to the requirements of IoT Hub in the following format:
``` plaintext
The format of the `username` field is as follows:
${productId}${deviceName};${sdkappid};${connid};${expiry}
Note: `${}` indicates a variable and is not a concatenating symbol.
```The descriptions of each field are as follows:
	- productId: product ID
	- deviceName: device name
	- sdkappid: fixed at `12010126`
	- connid: a random string
	- expiry: signature validity period, which is a UTF-8 string of the number of seconds since 00:00:00 UTC on January 1, 1970.
3. Base64-decode the device key to get the raw key `raw_key`.
4. Use the `raw_key` generated in step 3 to generate a digest string for the `username` with the HMACSHA1 or HMACSHA256 algorithm, which is referred to as a token.
5. Generate the `password` field according to the requirements of IoT Hub in the following format:
```plaintext
The format of the `password` field is as follows: 
${token};hmac signature algorithm
Enter the digest algorithm used in step 3 in the `hmac signature algorithm` field. Valid values include `hmacsha256` and `hmacsha1`.
```
As a comparison, the code samples for generating signatures in Python, Java, Node.js, JavaScript, and C are as follows:
The code in Python is as follows:
<dx-codeblock>
:::  Python
#!/usr/bin/python
# -*- coding: UTF-8 -*-
import base64
import hashlib
import hmac
import random
import string
import time
import sys
# Generate a random string of the specified length
def RandomConnid(length):
    return  ''.join(random.choice(string.ascii_uppercase + string.digits) for _ in range(length))
# Generate the parameters required for connection to IoT Hub
def IotHmac(productID, devicename, devicePsk):
     # 1. Generate `connid` as a random string to facilitate troubleshooting on the backend
     connid   = RandomConnid(5)
     # 2. Generate the expiration time of the signature, which is a UTF-8 string of the number of seconds since 00:00:00 UTC on January 1, 1970
     expiry   = int(time.time()) + 60 * 60
     # 3. Generate the `clientid` part of MQTT in the format of `${productid}${devicename}`
     clientid = "{}{}".format(productID, devicename)
     # 4. Generate the `username` part of MQTT in the format of `${clientid};${sdkappid};${connid};${expiry}`
     username = "{};12010126;{};{}".format(clientid, connid, expiry)
     # 5. Sign the `username` to generate a token
     secret_key = devicePsk.encode('utf-8')  # convert to bytes
     data_to_sign = username.encode('utf-8')  # convert to bytes
     secret_key = base64.b64decode(secret_key)  # this is still bytes
     token = hmac.new(secret_key, data_to_sign, digestmod=hashlib.sha256).hexdigest()
     # 6. Generate the `password` field according to the rules of IoT Hub platform
     password = "{};{}".format(token, "hmacsha256")
     return {
        "clientid" : clientid,
        "username" : username,
        "password" : password
     }
if __name__ == '__main__':
    print(IotHmac(sys.argv[1], sys.argv[2], sys.argv[3]))
:::
</dx-codeblock>
Save the above code in `IotHmac.py` and run the following command. Here, replace `YOUR_PRODUCTID`, `YOUR_DEVICENAME`, and `YOUR_PSK` with the product ID, device name, and device key of the device you actually created.
```
python3 IotHmac.py "YOUR_PRODUCTID" "YOUR_DEVICENAME" "YOUR_PSK" 
```
The code in Java is as follows:
<dx-codeblock>
:::  java
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import java.util.*;
public class IotHmac {
 public static void main(String[] args) throws Exception {
System.out.println(IotHmac("YOUR_PRODUCTID","YOUR_DEVICENAME","YOUR_PSK"));
}
public static Map<String, String> IotHmac(String productID, String devicename, String 
devicePsk) throws Exception {
					final Base64.Decoder decoder = Base64.getDecoder();
			//1. Generate `connid` as a random string to facilitate troubleshooting on the backend
			String connid = HMACSHA256.getRandomString2(5);
			//2. Generate the expiration time of the signature, which is a UTF-8 string of the number of seconds since 00:00:00 UTC on January 1, 1970
			Long expiry = Calendar.getInstance().getTimeInMillis()/1000 +600;
			//3. Generate the `clientid` part of MQTT in the format of `${productid}${devicename}`
			String clientid = productID+devicename;
			//4. Generate the `username` part of MQTT in the format of `${clientid};${sdkappid};${connid};${expiry}`
			String username = clientid+";"+"12010126;"+connid+";"+expiry;
			//5. Sign the `username` to generate a token. Then, generate the `password` field according to the rules of IoT Hub platform
			String password = HMACSHA256.getSignature(username.getBytes(), decoder.decode(devicePsk)) + ";hmacsha256";
			Map<String,String> map = new HashMap<>();
			map.put("clientid",clientid);
			map.put("username",username);
			map.put("password",password);
			return map;
		}
		public static class HMACSHA256 {
			private static final String HMAC_SHA256 = "HmacSHA256";
			/**
			 * Generate the signature data
			 *
			 * @param data The data to be encrypted
			 * @param key The key used for encryption
			 * @return The generated hexadecimal string
			 */
			public static String getSignature(byte[] data, byte[] key)  {
					try {
							SecretKeySpec signingKey = new SecretKeySpec(key, HMAC_SHA256);
							Mac mac = Mac.getInstance(HMAC_SHA256);
							mac.init(signingKey);
							byte[] rawHmac = mac.doFinal(data);
							return bytesToHexString(rawHmac);
					}catch (Exception e) {
							e.printStackTrace();
					}
					return null;
			}
        /**
         * Convert the `byte[]` array into a hexadecimal string
         *
         * @param bytes The byte array to be converted
         * @return Converted result
         */
        private static String bytesToHexString(byte[] bytes) {
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < bytes.length; i++) {
                String hex = Integer.toHexString(0xFF & bytes[i]);
                if (hex.length() == 1) {
                    sb.append('0');
                }
                sb.append(hex);
            }
            return sb.toString();
        }
        public static String getRandomString2(int length) {
            Random random = new Random();
            StringBuffer sb = new StringBuffer();
            for (int i = 0; i < length; i++) {
                int number = random.nextInt(3);
                long result = 0;
                switch (number) {
                    case 0:
                        result = Math.round(Math.random() * 25 + 65);
                        sb.append(String.valueOf((char) result));
                        break;
                    case 1:
                        result = Math.round(Math.random() * 25 + 97);
                        sb.append(String.valueOf((char) result));
                        break;
                    case 2:
                        sb.append(String.valueOf(new Random().nextInt(10)));
                        break;
                }
            }
            return sb.toString();
        }
    }
}
:::
</dx-codeblock>



The code in Node.js and JavaScript is as follows:
<dx-codeblock>
:::  JavaScript
// The following is the way to import the node. If a browser is used, use the corresponding way to import the `crypto-js` library
const crypto = require('crypto-js')

// Function for generating random numbers
const randomString = (len) => {
　　len = len || 32;
　　var chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
　　var maxPos = chars.length;
　　var pwd = '';
　　for (let i = 0; i < len; i++) {
　　　　pwd += chars.charAt(Math.floor(Math.random() * maxPos));
　　}
　　return pwd;
}
// The product ID, device name, and device key are required
const productId = 'YOUR_PRODUCTID';
const deviceName = 'YOUR_DEVICENAME';
const devicePsk = 'YOUR_PSK';

// 1. Generate `connid` as a random string to facilitate troubleshooting on the backend
const connid =  randomString(5);
// 2. Generate the expiration time of the signature, which is a UTF-8 string of the number of seconds since 00:00:00 UTC on January 1, 1970
const expiry = Math.round(new Date().getTime() / 1000) + 3600 * 24;
// 3. Generate the `clientid` part of MQTT in the format of `${productid}${devicename}`
const clientId = productId + deviceName;
// 4. Generate the `username` part of MQTT in the format of `${clientid};${sdkappid};${connid};${expiry}`
const userName = `${clientId};12010126;${connid};${expiry}`;
//5. Sign the `username` to generate a token. Then, generate the `password` field according to the rules of IoT Hub platform
const rawKey = crypto.enc.Base64.parse(devicePsk);   // Base64-decode the device key
const token =  crypto.HmacSHA256(userName, rawKey);
const password = token.toString(crypto.enc.Hex) + ";hmacsha256";
console.log(`userName:${userName}\npassword:${password}`);
:::
</dx-codeblock>
The code in C is as follows:

>?For more information on the code in C, please see [here](https://github.com/tencentyun/qcloud_iot_mqtt_sign).
>

<dx-codeblock>
:::  c
#include "limits.h"
#include <stdint.h>
#include <stdio.h>
#include <stdlib.h>

#include "HAL_Platform.h"
#include "utils_base64.h"
#include "utils_hmac.h"

/* Max size of base64 encoded PSK = 64, after decode: 64/4*3 = 48*/
#define DECODE_PSK_LENGTH 48

/* MAX valid time when connect to MQTT server. 0: always valid */
/* Use this only if the device has accurate UTC time. Otherwise, set to 0 */
#define MAX_ACCESS_EXPIRE_TIMEOUT (0)

/* Max size of conn Id  */
#define MAX_CONN_ID_LEN (6)

/* IoT C-SDK APPID */
#define QCLOUD_IOT_DEVICE_SDK_APPID     "21****06"
#define QCLOUD_IOT_DEVICE_SDK_APPID_LEN (sizeof(QCLOUD_IOT_DEVICE_SDK_APPID) - 1)

static void HexDump(char *pData, uint16_t len)
{
    int i;

    for (i = 0; i < len; i++) {
        HAL_Printf("0x%02.2x ", (unsigned char)pData[i]);
    }
    HAL_Printf("\n");
}

static void get_next_conn_id(char *conn_id)
{
    int i;
    srand((unsigned)HAL_GetTimeMs());
    for (i = 0; i < MAX_CONN_ID_LEN - 1; i++) {
        int flag = rand() % 3;
        switch (flag) {
            case 0:
                conn_id[i] = (rand() % 26) + 'a';
                break;
            case 1:
                conn_id[i] = (rand() % 26) + 'A';
                break;
            case 2:
                conn_id[i] = (rand() % 10) + '0';
                break;
        }
    }

    conn_id[MAX_CONN_ID_LEN - 1] = '\0';
}

int main(int argc, char **argv)
{
    char *product_id    = NULL;
    char *device_name   = NULL;
    char *device_secret = NULL;

    char *username     = NULL;
    int   username_len = 0;
    char  conn_id[MAX_CONN_ID_LEN];

    char password[51]      = {0};
    char username_sign[41] = {0};

    char   psk_base64decode[DECODE_PSK_LENGTH];
    size_t psk_base64decode_len = 0;

    long cur_timestamp = 0;

    if (argc != 4) {
        HAL_Printf("please ./qcloud-mqtt-sign product_id device_name device_secret\r\n");
        return -1;
    }

    product_id    = argv[1];
    device_name   = argv[2];
    device_secret = argv[3];

    /* first device_secret base64 decode */
    qcloud_iot_utils_base64decode((unsigned char *)psk_base64decode, DECODE_PSK_LENGTH, &psk_base64decode_len,
                                  (unsigned char *)device_secret, strlen(device_secret));
    HAL_Printf("device_secret base64 decode:");
    HexDump(psk_base64decode, psk_base64decode_len);

    /* second create mqtt username
     * [productdevicename;appid;randomconnid;timestamp] */
    cur_timestamp = HAL_Timer_current_sec() + MAX_ACCESS_EXPIRE_TIMEOUT / 1000;
    if (cur_timestamp <= 0 || MAX_ACCESS_EXPIRE_TIMEOUT <= 0) {
        cur_timestamp = LONG_MAX;
    }

    // 20 for timestampe length & delimiter
    username_len = strlen(product_id) + strlen(device_name) + QCLOUD_IOT_DEVICE_SDK_APPID_LEN + MAX_CONN_ID_LEN + 20;
    username     = (char *)HAL_Malloc(username_len);
    if (username == NULL) {
        HAL_Printf("malloc username failed!\r\n");
        return -1;
    }

    get_next_conn_id(conn_id);
    HAL_Snprintf(username, username_len, "%s%s;%s;%s;%ld", product_id, device_name, QCLOUD_IOT_DEVICE_SDK_APPID,
                 conn_id, cur_timestamp);

    /* third use psk_base64decode hamc_sha1 calc mqtt username sign crate mqtt
     * password */
    utils_hmac_sha1(username, strlen(username), username_sign, psk_base64decode, psk_base64decode_len);
    HAL_Printf("username sign: %s\r\n", username_sign);
    HAL_Snprintf(password, 51, "%s;hmacsha1", username_sign);

    HAL_Printf("Client ID: %s%s\r\n", product_id, device_name);
    HAL_Printf("username : %s\r\n", username);
    HAL_Printf("password : %s\r\n", password);

    HAL_Free(username);

    return 0;
}
:::
</dx-codeblock>

6. Finally, enter the parameters generated above in the corresponding MQTT `connect` message.
7. Enter the `clientid` value in the `clientid` field of the MQTT protocol.
8. Enter the `username` value in the `username` field of the MQTT protocol.
9. Enter the `password` value in the `password` field of the MQTT protocol and send a `MqttConnect` message to the domain name and port of key authentication to connect to IoT Hub.

