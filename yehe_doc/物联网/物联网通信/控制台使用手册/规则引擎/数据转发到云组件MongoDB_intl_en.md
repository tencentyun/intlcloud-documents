## Overview
The rule engine allows you to configure forwarding rules to forward eligible data reported by devices to TencentDB for MongoDB. After you create an instance in the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb) or through TencentCloud API, device messages can be written to the corresponding TencentDB for MongoDB set.

The figure below shows the entire process of forwarding data to TencentDB for MongoDB by the rule engine:
![](https://main.qcloudimg.com/raw/ce65ecf23f563cf2226c17e690cdcf1d.png)

## Configuration
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and click **Rule Engine** on the left sidebar.
2. Go to the rule engine page and click the name of the rule to be configured.
3. On the rule details page, click **Add Action**.
>?You will be prompted to authorize access to TencentDB for MongoDB upon the first use. You need to click **Authorize Now** before you can proceed.
![](https://main.qcloudimg.com/raw/e8a768ff185aafebf79b63db710bccc9.jpg)
4. On the action adding page, select **Forward data to TencentDB for MongoDB**.
![](https://main.qcloudimg.com/raw/c4be9f3dfa1ec60dad5a9246db29f40d.jpg)
5. After successful authorization, you need to configure the TencentDB for MongoDB instance information as shown below. The configuration is divided into the following steps:
    1. Select the region and TencentDB for MongoDB instance. If there is no instance under the account, click **Create Instance** to redirect to the TencentDB for MongoDB console and create one.
    2. Enter the username of the TencentDB for MongoDB instance (`mongouser` by default).     
    3. Enter the login password of the TencentDB for MongoDB instance.
    4. Enter the name of the database to be written to.
    5. Enter the name of the set to be written to.
![](https://main.qcloudimg.com/raw/5afe47d64dac569a759a69dc9c02fbd5.jpg)

## Resending Mechanism

The resending mechanism is used to send the message again in case of a failure in the message forwarding process, which makes sure that the message is received. The details are as follows:
- If message forwarding fails, the system will retry forwarding at intervals of 1s, 3s, and 10s in sequence. If all three retries fail, the message will be discarded.
- If you have configured the "action for forwarding failure", then after three unsuccessful retries, the message will be forwarded again according to the configured action. If forwarding still fails, the message will be discarded.
