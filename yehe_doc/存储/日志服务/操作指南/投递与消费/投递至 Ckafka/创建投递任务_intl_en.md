## Overview

CLS uses CKafka instances to consume log topic data. This document describes how to enable CKafka consumption for a log topic.

## Prerequisite

Tencent Cloud CKafka has been activated, and a CKafka consumption instance and a message queue topic have been created in the same region as the log topic.

>? For details about how to create a CKafka instance, see [Creating Instances and Topics](https://intl.cloud.tencent.com/document/product/597/40039).
> 
## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Click **Log Topic** in the left sidebar.
3. Click the log topic name/ID for which CKafka consumption needs to be configured to go to its details page.
4. Click the **CKafka Consumption** tab.
5. Click **Edit** on the right. Toggle the switch to enable **Ship to CKafka**, and select a CKafka instance for consumption and a corresponding message queue topic.
<img src="https://main.qcloudimg.com/raw/43a9878b5bf8f0500c1ba19b668b7766.png" width="700px">
6. Click **Save**. If the status of **Ship to CKafka** is displayed as "Enabled", it has been enabled successfully.
<img src="https://main.qcloudimg.com/raw/f964f0a141123a7926b8fd1a1eb1b5ba.png" width="700px">
> ! 
> - The `CleanUp.policy` attribute of the CKafka topic shipped must be set to `delete`. Otherwise, the shipping will fail.
> - To cleanse the log data before shipping to CKafka, please see [CLS Dump to CKafka](https://intl.cloud.tencent.com/document/product/614/38885).
> 
