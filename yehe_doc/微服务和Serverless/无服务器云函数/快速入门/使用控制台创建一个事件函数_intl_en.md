This document describes how to quickly create an event-triggered function in the console.
Compared with event-triggered functions, the HTTP-triggered functions provided by SCF focus more on optimizing web services. Click [here](https://intl.cloud.tencent.com/document/product/583/40689) to understand and quickly create an HTTP-triggered function.


## Step 1. Sign up for a Tencent Cloud account

If you already have a Tencent Cloud account, ignore this step.

<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://www.tencentcloud.com/en/account/register" target="_blank"  style="color: white; font-size:13px;">Sign Up for Tencent Cloud</a></div>

## Step 2: Topping Up Online

New SCF users are entitled to a certain monthly free tier of resource usage and invocations within three months of activation. SCF can be billed in a prepaid (subscription package) or postpaid (pay-as-you-go) manner. If you need to use other postpaid Tencent Cloud resources, top up your account first as instructed in [Payment Methods](https://www.tencentcloud.com/document/product/555/7425) before making purchases.



## Step 3. Authorizing TKE

Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/), select **Products** > **Serverless Cloud Function** to enter the SCF console, and follow the prompts to authorize SCF. (If you have already authorized SCF, skip this step.)

<div style="background-color:#00A4FF; width: 150px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/scf/index?rid=1" target="_blank"  style="color: white; font-size:13px;">Click here to authorize TKE</a></div>



## Step 4. Create a function

<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/scf/list-create?rid=1&ns=default&createType=empty" target="_blank"  style="color: white; font-size:13px;">Click here to enter the function creation page</a></div>

<br>



1. Click **Function Service** on the left sidebar to enter the **Function Service** page.
2. Select **Guangzhou** at the top of the page and click **Create** as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Azbs372_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219114446.png)
3. On the **Create function** page, select **Create from scratch** as shown below:  
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fJUF908_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219164315.png)
4. Configure the basic information of the function as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4GUF836_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219164534.png)
	- **Function type**: Select **Event-triggered function**.
	- **Function name**: The function name is automatically populated by default and can be modified as needed.
	- **Region**: The region is automatically populated by default and can be modified as needed.
	- **Runtime environment**: **Python 3.7** is automatically populated by default and can be modified as needed.
	- **Time zone**: SCF uses the UTC time by default, which you can modify by configuring the `TZ` environment variable. After you select a time zone, the `TZ` environment variable corresponding to the time zone will be added automatically.
5. Keep the default options for **Function codes**, **Log configuration**, and **Advanced configuration**.
6. Select **Create trigger** > **Custom** to create a trigger as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/McmV228_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219164650.png)
  - **Trigger method**: Select **API Gateway trigger**.
  - **Integration Response**: Deselect **Enable integration response**.
    Keep the default options for other parameter.
7. Click **Complete**. You can view the created function on the [Functions](https://console.cloud.tencent.com/scf/list?rid=1&ns=default) page.

## Step 5. Test in the cloud
<dx-tabs>
::: Function deployment test
On the **Function Management** page, select **Function code** and click **Test** to run the code with the test result returned as shown below: 
![](https://main.qcloudimg.com/raw/3758f32893e46b38d94d25cb71666542.png)
<dx-alert infotype="explain" title="">

- If you need to replace the test template or its content, you can directly edit the function content or select **Current test template**, replace it, and then click **Save** as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/AWuW723_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219170038.png)
- Different test templates simulate different trigger message sources, and the messages passed between different triggers and SCF are data structures agreed upon in advance. For more information, see [Trigger Overview](https://intl.cloud.tencent.com/document/product/583/9705).
</dx-alert>

The following information will appear:
![](https://main.qcloudimg.com/raw/7d5c5d7fc1b7b79f37861df7b3b8d1eb.png)
During this test, SCF will get the data structures of the "Hello World event template" in the `event` parameter of the `main_handler`.

```
{
  "key1": "test value 1",
  "key2": "test value 2"
}
```

:::
::: Trigger configuration test
On the **Trigger Management** page, view the trigger details.
1. After a trigger is successfully created, an access path will be generated on the **Trigger management** page of the function as shown below: 
![](https://qcloudimg.tencent-cloud.cn/raw/1f97c60e8cffc2b089d41c187d7b4609.png)
2. Open the access path in a browser. If "Hello World" is displayed, the function is successfully deployed.
:::
</dx-tabs>


## Step 6. View logs and monitoring data
<dx-tabs>
::: View logs
On the details page of a created function, select **Log Query** on the left to view the detailed logs of the function as shown below: 
![](https://main.qcloudimg.com/raw/d1150d2144bab8a023294554d3c1c170.png)
For more information on logs, see [Viewing Execution Logs](https://intl.cloud.tencent.com/document/product/583/32740).

:::
::: View monitoring data
On the **Function Management** page, select **Monitoring information** of the created function to view metrics such as function invocations and execution duration as shown below: 

<dx-alert infotype="notice" title="">
The minimal granularity of monitoring statistics collection is 1 minute. You need to wait for 1 minute before you can view the current monitoring record.

</dx-alert>



![](https://qcloudimg.tencent-cloud.cn/raw/820ae3b24fc7a0ca30de878ea201599a.png)
For more information on monitoring, see [Descriptions of monitoring metrics](https://intl.cloud.tencent.com/document/product/583/32739).
:::
::: Configure alarms
On the details page of a created function, click **click here** to configure an alarm policy for the function to monitor its running status as shown below: 
![](https://qcloudimg.tencent-cloud.cn/raw/34d0c93904c98c189cead318e9a7a090.png)
For more information on how to configure an alarm, see [Configuring Alarms](https://intl.cloud.tencent.com/document/product/583/32738).

:::
</dx-tabs>


## Step 7. Delete the function
After the function starts running, it consumes resources. In order to avoid unnecessary fees, this step shows you how to clear all resources.
1. Select **Functions** on the left sidebar, select the function to be deleted, and click **Delete** as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/7m2W196_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219165433.png)
2. Confirm the information in the **Delete Function** pop-up window and click **OK**.



## FAQs
See [General](https://intl.cloud.tencent.com/document/product/583/9180) for solutions.
If the problem persists, [submit a ticket](https://console.tencentcloud.com/workorder/category) for assistance.