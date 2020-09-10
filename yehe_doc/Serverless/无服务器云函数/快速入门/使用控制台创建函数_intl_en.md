## Overview
This document describes how to develop a simple `Hello World` web service in the Serverless Cloud Function (SCF) Console.

## Prerequisites
- You have already registered a Tencent Cloud account. If you haven't done so yet, click [here](https://intl.cloud.tencent.com/register) to sign up.
- You have already logged in to the [SCF Console](https://console.cloud.tencent.com/scf).

## Directions
### Writing function
1. Click **Function Service** on the left sidebar to enter the "Function Service" page.
2. Select **Guangzhou** at the top of the page and click **Create** as shown below:
![](https://main.qcloudimg.com/raw/357444d5a2960b99c9541f7ec3b9c52b.png)
3. Enter the basic information of the function on the "Create Function" page and click **Next** as shown below: 
![](https://main.qcloudimg.com/raw/93feca3fcec8ab28334fb223c3da59a7.png)
 - **Function name**: enter `helloworld`.
 - **Runtime environment**: select "Python 2.7".
 - **Create Method**: select "Function Template".
 - **Filter**: after entering `helloworld`, press "Enter" to search for and select the "helloworld" template.
4. Keep the default function configuration and click **Complete** as shown below:
After the function is created, you will be automatically redirected to its "Function configuration" page where you can view its configuration information.
![](https://main.qcloudimg.com/raw/b044618a0a43e8659739fafc82a62ab4.png)
 - "Execution" is set to "index.main_handler", indicating that the SCF Console will automatically save this snippet of code as an `index.py` file, compress it, and upload it to SCF for function creation.
 - `main_handler` in the sample code is the entry function, which has the following main parameters:
    - `event` parameter: gets information of the triggering source.
    - `context` parameter: gets the environment and configuration information of this function.
5. Select the **Function code** tab to view or edit the function code online as shown below:
![](https://main.qcloudimg.com/raw/4e750791cc30a2b0de4d18a592776161.png)


### Deploying function (with trigger configured)
1. After editing the function code online, click **Save** and the function will be deployed.
2. On the details page of the created function, select **Trigger Management** on the left and click **Create a Trigger**.
3. In the **Create a Trigger** window that pops up, set "Trigger Method" to "API Gateway Trigger" and keep other parameters as default as shown below:
![](https://main.qcloudimg.com/raw/b5c410ac87e63e5af8286f073e1b00f8.png)
4. Click **Submit** to complete the function deployment and trigger configuration.

### Cloud test
#### Testing function deployment
Select **Function code** and click **Test** to run the code and return the test result as shown below:
>?
>- If you need to replace the test template or its content, you can directly edit the function content or select **Current Test Template**, replace it, and then click **Save**.
>- Different test templates simulate different trigger message sources, and the messages passed between different triggers and SCF are data structures agreed upon in advance. For more information, please see [Trigger Overview](https://intl.cloud.tencent.com/document/product/583/9705).
>
![](https://main.qcloudimg.com/raw/a8d5d4542aa06ccacedc7fc08dfa4077.png)
During this test, SCF will get the data structures of the "Hello world event template" in the `event` parameter of the `main_handler`.
```
{
  "key1": "test value 1",
  "key2": "test value 2"
}
```

#### Testing trigger configuration
1. After a trigger is successfully created, an access path will be generated on the "Trigger Method" page of the function as shown below:
![](https://main.qcloudimg.com/raw/e7e4581a2d69565f201fdff55287bf31.png)
2. Open the access path in a browser. If "hello from scf" is displayed, the function is successfully deployed.

### Viewing logs
On the details page of a created function, select **Log Query** on the left to view the detailed logs of the function as shown below:
![](https://main.qcloudimg.com/raw/e9f6df7e49d1b19be99c8961c1397e88.png)
For more information on logs, please see [Viewing Execution Logs](https://intl.cloud.tencent.com/document/product/583/32740).

<span id="see"></span>
#### Viewing monitoring information
On the details page of a created function, select **Monitoring information** to view metrics such as function invocations and execution duration as shown below:
>!The minimal granularity of monitoring statistics collection is 1 minute. You need to wait for 1 minute before you can view the current monitoring record.
>
![](https://main.qcloudimg.com/raw/978e0f5ff56ab6199f6dbe307b37c389.png)
For more information on monitoring, please see [Description of Monitoring Metrics](https://intl.cloud.tencent.com/document/product/583/32739).

<sapn id="config"></span>
#### Configuring alarm
On the details page of a created function, click **click here** to configure an alarm policy for the function to monitor its running status as shown below:
![](https://main.qcloudimg.com/raw/7ee322b492ab6d28048a242a5a66d21b.png)
For more information on how to configure an alarm, please see [Configuring Alarm](https://intl.cloud.tencent.com/document/product/583/32738).
