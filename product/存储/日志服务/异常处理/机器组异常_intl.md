## Problem Description
An exception occurred with log collection, and the associated server group is found to be exceptional.

## Possible Cause
The heartbeat between the server group and the CLS system is interrupted, resulting in a failure to collect and report logs. Possible causes of the server group exception include:
1. IP address is incorrect.
2. Network is disconnected.
3. LogListener processes fail.
4. LogListener is incorrectly configured.

## Solution
Troubleshoot problems according to the above causes.

## Dealing Steps
1. Check whether the IP address added to the server group is correct.
2. Confirm whether the network is connected using the following command:
```shell
telnet <region>.cls.myqcloud.com 80
```
`<region>` is the abbreviation for the region where CLS resides. For more information about regions, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).
The following code will apprear under normal network connection . Connection will fail under abnormal connection. Check the network and ensure normal connection.
![](https://main.qcloudimg.com/raw/2660316a4496ac356b6e7ca5cdeb9daa.png)

3. Check whether LogListener processes are running normally. Enter the installation directory and execute the following command:
```shell
cd loglistener/tools && ./p.sh
```
Normally, there are three processes:
```shell
bin/loglistenerm -d                                #Daemon
bin/loglistener --conf=etc/loglistener.conf       #Main process
bin/loglisteneru -u --conf=etc/loglistener.conf    #Update process
```
**If any process fails**, it needs to be restarted. Enter the installation directory and execute the following command:
```shell
cd loglistener/tools && ./start.sh
```
4. Check whether the key and the IP are correctly configured in LogListener. Configuration file path: `/loglistener/etc/loglistener.conf`.
![](https://main.qcloudimg.com/raw/cfa012cfb136cbbcf78667d4d1307d26.png)
 - The key is the API key for the Tencent Cloud account or the collaborator. The project key is not supported.
 - group_ip in the configuration file must be consistent with the IP entered in the server group on the console. Since LogListener obtains the server IP automatically, check the consistency regularly when the server is bound with multiple ENIs.

