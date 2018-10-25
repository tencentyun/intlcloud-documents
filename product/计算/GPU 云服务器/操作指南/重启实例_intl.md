Restart is usually used for the maintenance of GPU instances. Restarting a GPU instance is equivalent to restarting the operating system of a local PC.

## Overview
 - **Preparation for restart:** The instance cannot provide service during restart. Make sure GPU instance has stopped receiving service requests before restart.
 
 - **How to perform restart:** It is recommended to restart an instance using the restart operation provided by Tencent Cloud, instead of running the restart command in the instance (such as restart command under Windows and Reboot command under Linux).
 
 - **Restart period:**Generally, it takes only a few minutes to restart an instance.
 
 - **Physical attributes of instances:** Restarting an instance does not change any of its physical attributes, so the public IP, private IP, and any data stored on the instance will remain unchanged.
 
 - **Billing:** Restarting instances will not start a new billing period.

## Restarting an Instance on the Console

 1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).

 2. Restart an instance: Select the instance to be restarted, and click **Restart** at the top of the list, or click **More** -> **CVM Status** -> **Restart** in the Operation column on the right side.

 3. Restart multiple instances: Select all the instances to be restarted and click **Restart** at the top of the list.  Reasons are given for instances that cannot be restarted.

## Restart instance using API
For more information, see [RebootInstances API](/doc/api/213/9396).

