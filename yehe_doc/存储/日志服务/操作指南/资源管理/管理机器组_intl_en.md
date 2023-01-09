## Overview

A machine group is a server object configured to collect logs by LogListener of CLS. You can configure machine groups through the CLS console, and categorize them by use cases.

## Directions

### Creating a machine group by machine group IP

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Click **Machine Group** in the left sidebar.
3. Select the region of your CLS, such as Shanghai, and then click **Create Machine Group**.
4. Configure the following information in the pop-up:

 - Logset Name: enter `cls_test` for example.
 - Configuration Mode: select **Configure machine group IP**.
 - IP: enter IPs of machines.
 >! 
 > - Enter one IP per line. Do not enter IPs of Windows machines.
 > - If you are using Tencent Cloud machines in the same region, you can enter private IPs directly, with one IP per line.
 > - If you are using machine groups of different regions, enter public IPs.
 > 
 - LogListener Auto Upgrade: disclosed by default and can be configured.
 - LogListener Service Logs: enabled by default. This feature records logs of the running status and log collection among other aspects of LogListener. For details, see [LogListener Service Logs](https://intl.cloud.tencent.com/document/product/614/40232).
5. Click **OK**.

### Creating a machine group by machine ID

If your machine IPs change frequently, you need to modify machine group configuration once the IPs change.
To avoid the trouble, you can use CLS to configure machine groups dynamically by machine ID. You just need to enter the machine IDs when configuring LogListener, CLS will recognize and add these machines into the machine group automatically.
>! Configuring machine groups by machine ID is supported only on LogListener v2.3.0 and above. You need to upgrade lower versions manually to use this feature.
> 
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Click **Machine Group** in the left sidebar.
3. Select the region of your CLS, such as Guangzhou, and then click **Create Machine Group**.
4. In the pop-up, configure the following items:

 - Logset Name: enter `cls_test` for example
 - Configuration Mode: select **Configure machine ID**
 - Machine ID: enter machine IDs.
 >! Enter one machine ID per line, and do not enter Windows machine IDs.
 >
 - LogListener Auto Upgrade: you’re advised to enable this feature. For more information, see [LogListener Upgrade Guide](https://intl.cloud.tencent.com/document/product/614/40233).
 - LogListener Service Logs: enabled by default. This feature records logs of the running status and log collection among other aspects of LogListener. For details, see [LogListener Service Logs](https://intl.cloud.tencent.com/document/product/614/40232).
5. Click **OK**.
6. Log in to a machine added above, run the following command, open the `/etc/loglistener.conf` file under the installation directory of LogListener.
Take the `/user/local` installation directory as an example:
```plaintext
vi /usr/local/loglistener-2.3.0/etc/loglistener.conf
```
7. Press **i** to enter the edit mode.
8. Find the `group_label` parameter, and enter your custom machine IDs and separate them with a comma (,).
![img](https://main.qcloudimg.com/raw/1d17d38a70cdfbfb963a60fbec3b0c1b.png)
9. Press **Esc** to exit the edit mode.
10. Enter **:wq**, and press **Enter** to save the settings.
11. Run the following command, restart LogListener, and then the machine group will be created.
```plaintext
/etc/init.d/loglistenerd restart
```


### Viewing Machine Status

A machine group uses the heartbeat mechanism to maintain its connection with the CLS system. A machine group with LogListener installed regularly sends heartbeats to CLS.

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Click **Machine Group** in the left sidebar.
3. Find the target machine group, click **View**.

4. View the machine group status in the pop-up.
You can view the machine group status to see if it works normally. If so, your server can communicate with CLS normally.



### Deleting a machine group

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Click **Machine Group** in the left sidebar.
3. Find the target machine group, click **Delete**.

4. In the pop-up, click **OK**.
</br><img src="https://main.qcloudimg.com/raw/e99130ce78d418e04c4f573fbcd112d0.png" alt="image-20210512174816939" style="zoom:50%;" />

>! Once the machine group is deleted, logs will no longer be collected under its associated log topics.
>
