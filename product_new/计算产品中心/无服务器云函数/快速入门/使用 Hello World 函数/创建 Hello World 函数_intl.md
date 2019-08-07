1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1) and enter the **Functions** page.
2. Select **Guangzhou** region and click **Create** to enter the function creating page.
3. Enter the following parameter information and click **Next**.
 - Creation method: Select "Blank function".
 - Function name: "hello-world".
 - Runtime environment: Select "Python 2.7".
4. Keep the default configuration and click **Finish** to complete the function creation. See the figure below:![](https://main.qcloudimg.com/raw/1f8dc3b1f5789a54a1429c61335ab197.png)
![](https://main.qcloudimg.com/raw/245c2641dc883ed7cb47e308726962fe.png)
 - Execution is set to "index.main_handler", indicating that the SCF console will automatically save this snippet of code as a `index.py` file, compress, and upload it to SCF for creating the function.
 - `main_handler` in the sample code is the entry-point function, which has the following two input parameters:
    - `event` parameter: Gets information of triggering source.
    - `context` parameter: Gets the environment and configuration information of this function.

 >After the function is created, you can view information such as the function configuration in **Function configuration** or edit the code online in **Function code**.

