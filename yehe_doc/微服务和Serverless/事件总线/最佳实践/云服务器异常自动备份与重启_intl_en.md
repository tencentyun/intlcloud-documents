## Overview
A monitoring and alarming system is indispensable for a business production environment. Complete monitoring, prompt alarming, and automated alarm handling can help you quickly locate and fix problems to reduce possible economic losses.

Tencent Cloud EventBridge is a secure, stable, and efficient serverless event management platform. EventBridge in Event Center can receive real-time events and relevant data streams from your applications, SaaS services, and Tencent Cloud services. By integrating notification message and SCF, it can send alarm messages in real time and automatically handle alarms.

This document uses a server exception as an example to describe how to implement real-time alarm message push and automatic snapshot-based disk rollback with the aid of EventBridge and SCF after your CVM instances generate alarm events. In this way, you can quickly build an automated OPS architecture.

## Architecture Design
The overall architecture is as shown below. When a CVM instance triggers an exception alarm, CVM will automatically generate an alarm event and actively push it to EventBridge. After the alarm is filtered by the alarm rules bound to EventBridge, the alarm message will be pushed to users promptly through the specified notification channels, and SCF will be triggered at the same time to call an API to quickly roll back the disk based on snapshot, so as to recover the business in time.
![](https://qcloudimg.tencent-cloud.cn/raw/6d4f60b898b898fad9b5db4ccbdbe2fc.png)

The basic process is as follows:      
An instance generates an alarm event > The event is filtered by the EventBridge rules > The event is delivered to notification message and SCF > SCF calls an API to back up the disk data and restart the instance > The alarm event is pushed to users after the restart

## Directions

### Step 1. Create a function to implement the snapshot creation and restart logic[](id:step1)

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf).
2. Create a function as instructed in [Creating Event-Triggered Function in Console](https://intl.cloud.tencent.com/document/product/583/32742).
3. Write the code logic of calling the API. Below is the sample code:
```js
exports.main_handler = async (event, context) => {
    // Depends on tencentcloud-sdk-nodejs version 4.0.3 or higher
const tencentcloud = require("tencentcloud-sdk-nodejs");

const CvmClient = tencentcloud.cvm.v20170312.Client;
const CbsClient = tencentcloud.cbs.v20170312.Client;
var secretId = process.env.secretId // Pass in `secretId` of your account to the environment variable
var secretKey = process.env.secretKey // Pass in `secretKey` of your account to the environment variable
var insID = event.subject

const clientConfig1 = {
  credential: {
    secretId: secretId,
    secretKey: secretKey,
  },
  region: "ap-guangzhou",
  profile: {
    httpProfile: {
      endpoint: "cvm.tencentcloudapi.com",
    },
  },
};

const client1 = new CvmClient(clientConfig1);
const params1 = {
    "InstanceIds": [
        ${Replace it with the ID of the instance to be restarted}
    ],
    "StopType": "SOFT"
};
client1.RebootInstances(params1).then(
  (data) => {
    console.log(data);
  },
  (err) => {
    console.error("error", err);
  }
);

const clientConfig2 = {
  credential: {
    secretId: secretId,
    secretKey: secretKey,
  },
  region: "ap-guangzhou",
  profile: {
    httpProfile: {
      endpoint: "cbs.tencentcloudapi.com",
    },
  },
};

const client2 = new CbsClient(clientConfig2);
const params2 = {
    "DiskId": ${Replace it with the ID of the disk to be backed up}
};
client2.CreateSnapshot(params2).then(
  (data) => {
    console.log(data);
  },
  (err) => {
    console.error("error", err);
  }
);
};

```
You can also use [API Explorer](https://console.cloud.tencent.com/api/explorer?Product=scf) to quickly generate the sample code.

### Step 2. Create en event rule and filter alarm events
1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb?regionId=1).
2. Select **Tencent Cloud service event bus** > **default** in **Event Bus**.
3. In the **details of the default event bus**, click **Manage Event Rules**.
4. In **Event Rule**, click **Create Event Rule** to create rules to filter and convert events.
    1. Taking the **CVM disk is read-only** event as an example, create rules as follows:
      - **Rule 1: receive the disk read-only exception events**
    ![](https://qcloudimg.tencent-cloud.cn/raw/a4a84e607086ae16c6b88e60470297ad.png)
      - **Rule 2: receive instance restart events**
    ![](https://qcloudimg.tencent-cloud.cn/raw/278a00f457a60ec604dc5cc5775bb92f.png)
    2. You can also customize the event rules based on your actual needs as follows:
      - Filter all **CVM** events in the **Guangzhou** region.
```json
 {
  "source":"cvm.cloud.tencent",
  "region":"ap-guangzhou"
  }
```
      - Filter **CVM** events with the specified instance ID.
```json
 {
  "source":"cvm.cloud.tencent",
  "subject":[
    "ins-xxxxxx",
    "ins-xxxxxx"
    ]
  }
```

### Step 3. Bind event targets and backend processing logic and set the push target

After creating rules, you can bind delivery targets to the rules as prompted. The above demo is used as an example here:
- For **rule 1**, you need to bind two targets: **notification message** and **SCF**.
<dx-tabs>
::: Notification message
Select a method to receive alarm messages.
![](https://qcloudimg.tencent-cloud.cn/raw/fd02099eca15edf5accfcc06796a8c33.png)
:::
::: SCF
Bind the function created in [step 1](#step1) to implement automated processing of alarm events.
![](https://qcloudimg.tencent-cloud.cn/raw/dcf950f24483b3addc2131b9d6bdb126.png)
:::
</dx-tabs>

- For **rule 2**, you only need to bind the notification message target.
![](https://qcloudimg.tencent-cloud.cn/raw/fd02099eca15edf5accfcc06796a8c33.png)



### Step 4. Send a simulated event to check whether the process works normally

At this point, you have built the automated alarm processing link. You can use a simulated alarm event to test whether the process can run normally:

- Successful function invocation:
![](https://qcloudimg.tencent-cloud.cn/raw/8cf494ce56a93498fc81e43fa85ef766.png)

- Instance restart:
![](https://qcloudimg.tencent-cloud.cn/raw/ef949c0699318772f79ef5e89fb7331e.png)

- Snapshot creation:
![](https://qcloudimg.tencent-cloud.cn/raw/94518ef824038026a0840ba327a90b3e.png)

- Alarm message receipt:
<img src="https://qcloudimg.tencent-cloud.cn/raw/789a5c49442ced2448f41792dbdae27b.png" style="zoom:40%;" />

- Restart email receipt:
<img src="https://qcloudimg.tencent-cloud.cn/raw/4759d639cc0bfa2ff5f12ad629ea66ab.png" style="zoom: 40%;" />
