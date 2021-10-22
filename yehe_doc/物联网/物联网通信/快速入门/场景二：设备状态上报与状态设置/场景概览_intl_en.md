## Operation Scenario

If you need to set a device target temperature and report device status information in a smart home scenario (this is not a real product but only used to demonstrate IoT Hub's capabilities), you can follow the steps in this document.
![](https://main.qcloudimg.com/raw/74ee56cdeb3836ce4c7dc5a21d9540fd.png)

## Setting Device Target Temperature
![](https://main.qcloudimg.com/raw/93d2e910859d326de663f3793d4be9b1.png)
The management backend uses the cloud APIs provided by IoT Hub to update device shadow's configuration and registration parameters, and associate the corresponding callback function to update the configuration locally.
For the implementation of relevant TencentCloud APIs for device shadow, please download [iotcloud_RestAPI_python.zip](https://mc.qcloudimg.com/static/archive/c6b492abe009de1c47b91b8bfd93c7d2/iotcloud_RestAPI_python.zip). You need to configure your profile according to the RESTful API description. You can customize the features by modifying the parameters in `airConditionerCtrl.py` in the `RestAPI` folder.

## Reporting Device Status Information

![](https://qcloudimg.tencent-cloud.cn/raw/6dd0a5a0162ee02ad2d5801f0a409587.png)
The device reports its own status data to the device shadow, and the home appliance management backend directly gets data from the device shadow through the RESTful API.
