Restarting an instance is a common approach for troubleshooting. Restarting a GPU instance is equivalent to restarting the operating system of a local PC.

## Overview
 - **Preparation:** The instance cannot provide service during restart. Make sure the GPU instance has stopped receiving service requests before you restart it.
 
 - **How to restart:** It is recommended to restart an instance in the Tencent Cloud console, instead of running the restart command in the instance (such as `restart` command under Windows and `reboot` command under Linux).
 
 - **Restart period:** Generally, it takes only a few minutes to restart an instance.
 
 - **Physical attributes of instances:** Restarting an instance does not change any of its physical attributes, so the public IP, private IP, and any data stored on the instance will remain unchanged.
 
 - **Billing:** Restarting instances will not start a new billing period.

## Restarting an Instance in the Console

 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).

 2. Select the instance to restart, and click **Restart** at the top of the list, or click **More** -> **CVM Status** -> **Restart** in the Operation column on the right side.

 3. To restart multiple instances, select all the instances to restart, and click **Restart** at the top of the list. 

## Restarting an Instance Using API
For more information, see [RebootInstances API](https://intl.cloud.tencent.com/document/product/213/33243).

