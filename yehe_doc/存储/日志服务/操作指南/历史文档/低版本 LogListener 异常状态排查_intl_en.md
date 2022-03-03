>This document provides troubleshooting information for LogListener 2.2.4 and earlier. For information on troubleshooting the latest version, see [Server Group Exceptions](https://intl.cloud.tencent.com/document/product/614/17424).


## Error Description
An exception occurred with log collection, and the associated server group is found to be exceptional.

## Possible Causes
The heartbeat between the server group and the CLS system is interrupted, resulting in failure to collect and report logs. Possible causes for the server group exception include:
1. The IP address is incorrect.
2. The network is disconnected.
3. LogListener process failure.
4. LogListener is configured incorrectly.

## Solution
Troubleshoot problems according to the above causes.

## Directions
1. Check whether the IP address added to the server group is correct.
 1. Check the IP address obtained by LogListener by running the following command:
```shell
cd loglistener/tools && ./check.sh
```
![image](https://main.qcloudimg.com/raw/a50f79f3157d86e88915fa1e069e48f2.png)
 2. Log in to the [Cloud Log Service Console](https://console.cloud.tencent.com/cls), and click **Server Group** in the leftside bar. On the Server Group Management page, check the IP address of the server group. The IP address must be the same as that for collection.

2. Check whether the network is connected by running the following command:
```shell
telnet <region>.cls.myqcloud.com 80
```
`<region>` is the abbreviation for the region where CLS resides. For more information on regions, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).
The following code appears upon normal network connection. Otherwise, connection fails. Check the network and ensure normal connection.
![](https://main.qcloudimg.com/raw/2660316a4496ac356b6e7ca5cdeb9daa.png)
3. Check whether LogListener processes are running normally. Go to the installation directory and run the following command:
```shell
cd loglistener/tools && ./p.sh
```
Normally, there are three processes:
```shell
bin/loglistenerm -d                                #Daemon process
bin/loglistener --conf=etc/loglistener.conf        #Main process    
bin/loglisteneru -u --conf=etc/loglistener.conf    #Update process
```
**If any process fails**, restart it. Go to the installation directory and run the following command:
```shell
cd loglistener/tools && ./start.sh
```
4. Check whether the key and IP address are correctly configured in LogListener. Go to the installation directory to check the configuration information by running the following command:
```shell
cd loglistener/etc && cat loglistener.conf
```
See the following figure:
![](https://main.qcloudimg.com/raw/d724e95ba7d4557d33368b6bd7ab4b58.png)
 - The key is the API key for the Tencent Cloud account or the collaborator. Project keys are not supported.
 - group_ip in the configuration file must be consistent with the IP address entered in the server group on the console. Since LogListener obtains the server IP address automatically, check the consistency regularly when the server is bound to multiple ENIs.
