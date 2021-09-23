## Overview
If you need to achieve the features as shown below in a smart home scenario (this is not a real product but only used to demonstrate IoT Hub's capabilities), you can follow the steps in this document.
![come_home](https://main.qcloudimg.com/raw/7a705176f8cba804b72d1e4519e93151.png)


## Solution
Two types of smart devices (door and air conditioner) can be created in the IoT Hub SDK and connected with each other based on cross-device messaging and the rule engine as shown below:
![rule_engine_for_smart_home](https://main.qcloudimg.com/raw/f4c5186f03f8636eb8f8d80622b49b02.png)


>! `airConditioner1` cannot achieve message communication by directly subscribing to the update messages of `door1`. For the reason, please see [Feature Components - Permission Management](https://intl.cloud.tencent.com/document/product/1105/41500).
