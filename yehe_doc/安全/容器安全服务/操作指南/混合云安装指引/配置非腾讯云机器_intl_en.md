## Step 1. Install the TCSS agent
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Asset Management** on the left sidebar.
2. On the **Asset Management** page, click **Servers** > **Install a TCSS agent** to pop up the **Installation guide** window on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/f47c48cc83f4435e43db21f118f21026.png)
3. In the pop-up window, select the **Server vendor**, **Server type**, and **Network**. To connect over Direct Connect, select **Direct Connect**; otherwise, select **Public network**.
 - Connect over the public network: Click ![](https://qcloudimg.tencent-cloud.cn/raw/2842d2736fb96f3fcf71aa60afe040cf.png) to copy and run the corresponding command to install the TCSS agent. Pay attention to the command validity.
 ![](https://qcloudimg.tencent-cloud.cn/raw/6a45778d752b5927cac485667fd17332.png)
 - Connect over Direct Connect: Select the VPC connected to Direct Connect and click ![](https://main.qcloudimg.com/raw/ee7c3909138988a9d940625444e5611e.png) to copy and run the corresponding command to install the TCSS agent. **Pay attention to the command validity**.
>?
>- For more information on Direct Connect, click **Learn about Direct Connect** to go to the Direct Connect console.
>- To allow the target IP in the firewall, grant the permission as instructed below.

![](https://qcloudimg.tencent-cloud.cn/raw/e0f97fc5afa82e67914b36f49eadc45a.png)

## Step 2. Check whether the installation is successful
1. Check whether the installation command runs successfully according to the installation guide. Open the task manager and check whether the YDLive process is running, and if so, the installation is successful.
 - Run the `ps -ef | grep YD` command to check whether the YDService and YDLive processes are running.
 - If not, the root user can run the `/usr/local/qcloud/YunJing/YDEyes/YDService` command to manually start the program.
 ![](https://qcloudimg.tencent-cloud.cn/raw/5b1cf7f0707a2c3518521ded4d90bd6a.png)
2. After the successful installation, go to the [**Servers**](https://console.cloud.tencent.com/tcss/asset/host) page and select **Server source** > **Non-Tencent Cloud server**.
![](https://qcloudimg.tencent-cloud.cn/raw/a0e083e9685b81c2f3a1585f9c75e89e.png)
3. If the **Agent status** is **Online**, the installed service is online.
>? If it is not online, [contact us](https://intl.cloud.tencent.com/contact-us) for assistance.

![](https://qcloudimg.tencent-cloud.cn/raw/c6a6e56f5d0c7d014960ab55256e71da.png)
