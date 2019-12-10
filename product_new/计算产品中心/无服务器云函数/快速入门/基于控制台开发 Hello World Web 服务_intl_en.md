## Operation Scenarios
This document describes how to develop a simple `Hello World` web service in the Serverless Cloud Function (SCF) Console.

## Prerequisites
- You have already registered a Tencent Cloud account. If you haven't, [Click Here](https://intl.cloud.tencent.com/register) to sign up.
- You have already logged in to the [SCF Console](https://console.cloud.tencent.com/scf).

### Directions
### Writing Function
1. Click **Functions** on the left sidebar to enter the "Functions" page.
2. Select **Guangzhou** at the top of the page and click **Create**, as shown below:
![](https://main.qcloudimg.com/raw/357444d5a2960b99c9541f7ec3b9c52b.png)
3. Enter the basic information of the function on the "Create Function" page and click **Next**, as shown below: 
![](https://main.qcloudimg.com/raw/93feca3fcec8ab28334fb223c3da59a7.png)
 - Function Name: "hello-world".
 - Runtime Environment: Select "Python 2.7".
 - Creation Method: Select "Template Function".
 - Template Search: After entering "helloworld", press "Enter" to search for and select the "helloworld" template.
4. Keep the default function configuration and click **Finish**, as shown below:
After the function is created, you will be automatically redirected to the "Function Configuration" page where you can view the configuration information.
![](https://main.qcloudimg.com/raw/b044618a0a43e8659739fafc82a62ab4.png)
 - The parameter of "Execution Method" is set to "index.main_handler", indicating that the SCF console will automatically save this code as an `index.py` file, compress and upload it to SCF for function creation.
 - The entry function in the sample code is `main_handler`, which has the following main parameters:
    - `event` parameter: Gets information of the triggering source.
    - `context` parameter: Gets the environment and configuration information of this function.
5. Select **Function Code** to view or edit the function code online.
![](https://main.qcloudimg.com/raw/4e750791cc30a2b0de4d18a592776161.png)


### Deploying a function (with trigger configured)
1. After editing the function code online, click **Save** and the function will be deployed.
2. On the details page of the created function, select **Triggers** and click **Add a Trigger**, as shown below:
![](https://main.qcloudimg.com/raw/9ed5e34157ec44b209bcee698ecab983.png)
3. On the **Add a Trigger** page, set "Trigger Type" to "API Gateway Trigger" and keep other default parameters, as shown below:
![](https://main.qcloudimg.com/raw/b5c410ac87e63e5af8286f073e1b00f8.png)
4. Click **Save** to complete the function deployment and trigger configuration.

### Cloud Test
### Testing function deployment
Select **Function Code** and click **Test** to run the code and return the test result, as shown below:
>
>- If you need to replace the test template or its content, edit the function content directly or select **Current Test Template**, replace it, and then click **Save**.
>- Different test templates simulate different trigger message sources, and the messages passed between different triggers and SCF have predetermined data structures. For more information, see [Trigger Overview](https://intl.cloud.tencent.com/document/product/583/9705)
>
![](https://main.qcloudimg.com/raw/a8d5d4542aa06ccacedc7fc08dfa4077.png)
![](https://main.qcloudimg.com/raw/ae5143eed5b9477380bd7f7228e7418d.png)
During this test, SCF will get the data structure of the "Hello world event template" in the `event` parameter of `main_handler`.
```
{
  "key1": "test value 1",
  "key2": "test value 2"
}
```

#### Testing Trigger configuration
1. After a trigger is successfully created, an access path will be generated on the "Triggers" page of the function, as shown below:
![](https://main.qcloudimg.com/raw/e7e4581a2d69565f201fdff55287bf31.png)
2. If "hello from scf" is displayed when you open the access path in a browser, the function is successfully deployed.

### Viewing Log
On the details page of a created function, select **Execution Logs** to view the detailed logs of the function, as shown below:
![](https://main.qcloudimg.com/raw/e9f6df7e49d1b19be99c8961c1397e88.png)
For more information on logs, see [Function Logs](https://intl.cloud.tencent.com/document/product/583/32740).

<span id="see"></span>
#### Viewing monitoring information
On the details page of a created function, select **Monitoring Information** to view metrics such as the number of function invocations and execution runtime, as shown below:
>The minimal granularity of monitoring statistics is 1 minute. You need to wait for 1 minute before you can view the current monitoring record.
>
![](https://main.qcloudimg.com/raw/978e0f5ff56ab6199f6dbe307b37c389.png)
For more information on monitoring, see [Descriptions of monitoring metrics](https://intl.cloud.tencent.com/document/product/583/32739).

<sapn id="config"></span>
## Configuring an alarm
On the details page of a created function, click **Create Alarm** to configure an alarm policy for the function to monitor its health status, as shown below:
![](https://main.qcloudimg.com/raw/7ee322b492ab6d28048a242a5a66d21b.png)
For more information on how to configure an alarm, see [Alarm configuration description](https://intl.cloud.tencent.com/document/product/583/32738).
