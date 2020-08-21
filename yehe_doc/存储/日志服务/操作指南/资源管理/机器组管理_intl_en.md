A server group is a server object configured to collect logs by LogListener in Tencent Cloud CLS. Generally, different server groups are configured based on various business scenarios to help you manage CLS.

## Creating a Server Group

You can quickly create a server group on the CLS Console as instructed below:

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Click **Server Group Management* in the left sidebar.
3. Select the region of your CLS, e.g. Guangzhou, and then click **Create Server Group**.
4. Select either [server IP address](#.E6.9C.BA.E5.99.A8-ip-.E9.85.8D.E7.BD.AE.E6.9C.BA.E5.99.A8.E7.BB.84) or [server ID](#.E6.9C.BA.E5.99.A8.E6.A0.87.E8.AF.86.E9.85.8D.E7.BD.AE.E6.9C.BA.E5.99.A8.E7.BB.84) to configure the server group.  

### Configuring the server group by server IP address
Enter the server group name and the server IP address, and click **OK** after confirmation to complete the creation of the server group.

> !
> - Enter one IP in a line. Windows system is not supported.
> - If you are using Tencent Cloud servers in the same region, you can enter private IPs directly, with one IP per line.

### Configuring the server group by server ID
If you choose server IP address to configure a server group, you have to modify the configuration each time when one server IP address changes, which is annoying. However, CLS supports dynamically configuring the server group by server ID. You only need to fill in the server ID in the configuration information of Loglistener, and CLS can identify and automatically add the server to the server group.
> !
> - This feature is only supported by Loglistener 2.3 and later versions. If you use an earlier version, see [installation guide](https://intl.cloud.tencent.com/document/product/614/17414) to manually update it.
> - Enter one server ID in a line. Windows system is not supported.

1. Enter the server group name and the server ID, and click **OK** after confirmation to complete the creation of the server group.

2. Log in to the target server and modify the `/etc/loglistener.conf` file in the Loglistener installation directory (`/user/local` in this example):
```plaintext
vi /usr/local/loglistener-2.3.0/etc/loglistener.conf
```
3. Press **i** on the keyboard to enter the edit mode.
4. Replace the information after `group_label` with your server IDs separated by comma.
<img src="https://main.qcloudimg.com/raw/1d17d38a70cdfbfb963a60fbec3b0c1b.png" width="80%">
5. Press **Esc**, enter **:wq** and press **Enter** to save and close the file.
6. Run the following command to restart LogListener.
```plaintext
/etc/init.d/loglistenerd restart
```


## Viewing Server Status

A server group uses the heartbeat mechanism to maintain its connection with the CLS system. The server group with LogListener installed regularly sends heartbeat to CLS.

1. Click **View** under the **Operation** column and check the status of the server group to see if the server is running normally.
   ![](https://main.qcloudimg.com/raw/4163e320b011c1593c345b80cb52e0ed.png)
2. If the status is normal, the server communicates with Tencent Cloud CLS normally.
   ![](https://main.qcloudimg.com/raw/f3c7d75d5282758fadecded57bdedb1a.png)

## Deleting a Server Group

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Select the server group to be deleted, and click **Delete**.
   ![](https://main.qcloudimg.com/raw/a5499d33aa8c2323697388334dc27584.png)
3. Click **Delete** in the dialog box.
   ![](https://main.qcloudimg.com/raw/e99130ce78d418e04c4f573fbcd112d0.png)

> !Once the server group is deleted, logs are no longer collected under the associated log topics.
