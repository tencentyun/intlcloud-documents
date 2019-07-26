

## Application Scenario
EMR supports component configuration modification in the console, as shown below.

## Operation Guide
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select **Parameter Configuration** > **Modify Parameters** in the left sidebar, select the project, region, and configuration file, and click **Next**.
![](https://main.qcloudimg.com/raw/90c6c2ce0ec50f04331eafd0709b08e6.png)
2. Enter the parameter modification page, then you can add, edit, or delete parameters. For parameters without specified values, the default values will be assigned.
 ![](https://main.qcloudimg.com/raw/3fdb884f72c225c401f2709536d9ec50.png)
 ![](https://main.qcloudimg.com/raw/1fa93be6f791461acde15736f8c2fbb3.png)
3. After the editing is completed, click **Next** to enter the task verification page, where you can add a note to the modifications and double check the parameters that will be changed. After confirming everything is correct, click **Submit and Distribute Configuration**.
Please wait for the parameter modification task to be submitted. You can choose to restart the component immediately or restart at a scheduled time that works the best.
>!If you are using EMR Console to modify component parameters which have been updated using Shell command lines, the latest modification will overwrite the previous one.
>
![](https://main.qcloudimg.com/raw/f67fc1ae619f36186f3f4157347186b6.png)
