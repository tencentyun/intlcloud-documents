## Error Description

When the machine group is configured, LogListener may have an exception, such as disconnection from the CLS server and log upload failure. In this case, the machine group is exceptional, as shown below:

![](https://main.qcloudimg.com/raw/cffaee990badc81785d85714169d848b.png)

## Troubleshooting Directions

>?These troubleshooting steps only apply to LogListener 2.2.4 or later. If you’re using an earlier version, see [Troubleshooting Earlier LogListener Versions](https://intl.cloud.tencent.com/document/product/614/35675).

#### 1. Use the LogListener diagnostic tool

This tool helps you quickly check the LogListener operation, heartbeat and configuration.
Run the following CLI commands.

```shell
/etc/init.d/loglistenerd check
```

The following output indicates that LogListener is running properly.

![1574426236479](https://main.qcloudimg.com/raw/2ce4b6ea0fffeb659afba91b290bac65.png)

#### LogListener process exception

  If the result returns “[ERROR\] loglistener is not running” as shown in the following figure, it indicates that LogListener is not started. Run the `/etc/init.d/loglistenerd start` command to start it. For more information about the operation commands, see [Using LogListener](https://intl.cloud.tencent.com/document/product/614/17414).

  ![img](https://main.qcloudimg.com/raw/3a3af6de53301f1ace8722239dfbbc62.jpg)

#### LogListener heartbeat exception

  If the result returns “[ERROR] check loglistener heartbeat fail”, it indicates that LogListener has a heartbeat exception.



Many causes can lead to a LogListener heartbeat exception. Possible causes include:

- Network error

```shell
telnet <cls domain name> 80
```

  Check the network connectivity. For more information about the CLS domain name, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940). 

- Incorrect key

To check the LogListener key, access the LogListener installation directory and run the following command.

 ```shell
grep secret etc/loglistener.conf
```
![](https://main.qcloudimg.com/raw/6e0d20896aa1e8293ae74084ed5752d2.jpg)


#### 2. Check for the IP address of the machine group

Check that the IP address added to the machine group is the one configured on LogListener during installation. Run the following command to check the IP address configured on LogListener.

```shell
grep group_ip etc/loglistener.conf
```

![](https://main.qcloudimg.com/raw/4afe8d3a3b7c4f16e6795e35544a38e7.png)

Log in to the [CLS console](https://console.cloud.tencent.com/cls), and select **Server Group** in the left sidebar. On the **Server Group Management** page, view and verify that the IP address of the machine group is the same as that configured on LogListener.
![](https://main.qcloudimg.com/raw/ea8e833b596e1cf000f4f58f8f99dd29.png)
