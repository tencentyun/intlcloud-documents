[//]: # (chinagitpath:XXXXX)

Device firmware upgrade, also known as OTA, is an important part of the IoT Hub service. When an IoT device has new features or vulnerabilities that need to be fixed, firmware upgrade can be quickly performed for the device through the OTA service.

### Firmware Upgrade Topic
During the firmware upgrade process, the device needs to subscribe to the following two topics to communicate with the cloud:
```php
$ota/report/${productID}/${deviceName}
Used to publish (uplink) messages; the device reports the version number and the download and upgrade progress to the cloud.

$ota/update/${productID}/${deviceName}
Used to subscribe to (downlink) messages; the device receives the upgrade messages from the cloud.

```

![OTA topic](https://main.qcloudimg.com/raw/0046e2a294c541e109fc0b6829d180cc.jpg)

### The Firmware Upgrade Process
The following shows a MQTT device firmware upgrade process:
![OTA sequence diagram](https://main.qcloudimg.com/raw/a2f10ab90959a23b1675201b1e2311e0.jpg)

1. The device reports the current version number.
The device sends a message in JSON format with the following content to the topic ```$ota/report/${productID/${deviceName}``` through the MQTT protocol to report the version number:
```json
{
	"type": "report_version",
	"report":{
    	"version": "1.0.0"
	}
}
// type: message type
// version: the reported version number
```

2. You upload the firmware in the console.
3. You operate in the console to upgrade the specified device to the specified version.
4. After the firmware upgrade operation is initiated, the device receives a firmware upgrade message with the following content through the subscribed topic ```$ota/update/${productID}/${deviceName}```:
``` json
{
	"type": "update_firmware",
	"version": "1.0.0",
	"url": "https://ota-1254092559.cos.ap-guangzhou.myqcloud.com",
	"md5sum": "cc03e747a6afbbcbf8be7668acfebee5",
	"file_size": 31242
}
// type: the message type is update_firmware
// version: upgraded version
// url: URL of the downloaded firmware
// md5asum: MD5 value of the firmware
// file_size: firmware size in bytes
```

5. After receiving the firmware upgrade message, the device downloads the firmware from the URL. During the download process, the device-side SDK keeps reporting the download progress with the following content through the topic ```$ota/report/${productID}/${deviceName}```:
```json
{
	"type": "report_progress",
	"report":{
   		"progress":"{
       	    "state":"downloading",
       	    "percent":"10",
       	    "result_code":"0",
       	    "result_msg":""
	    },
	    "version": "1.0.0"
	}
}
// type: message type
// state: the state is "downloading"
// percent: the current download progress in percentage
```

6. After downloading the firmware, the device needs to report an upgrade start message with the following content through the topic ```$ota/report/${productID}/${deviceName}```:
```json
{
	"type": "report_progress",
	"report":{
		"progress":"{
	       	"state":"burning",
    	   	"result_code":"0",
       		"result_msg":""
		}
		"version": "1.0.0"
	}
}
// type: message type
// state: the status is "burning"
```

7. After the device firmware upgrade is completed, the device reports an upgrade success message with the following content to the topic ````$ota/report/${productID}/${deviceName}```:
```json
{
	"type": "report_progress",
	"report":{
		"progress":"{
       		"state":"done",
       		"result_code":"0",
       		"result_msg":""
		},
		"version": "1.0.0"
	}
}
// type: message type
// state: the status is "completed"
```

>Please note if a failure occurs during the firmware download or upgrade, a fail to update message will be reported via topic ```$ota/report/${productID}/${deviceName}``` as following:
```json
{
	"type": "report_progress",
	"report":{
		"progress":"{
       		"state":"fail",
       		"result_code":"-1",
       		"result_msg":"time_out"
		},
		"version": "1.0.0"
	}
}
// state: the status is "failed"
// result_code: error code; -1: download timed out; -2: file does not exist; -3: signature expired; -4: MD5 does not match; -5: firmware update failed
// result_msg: error message
```

