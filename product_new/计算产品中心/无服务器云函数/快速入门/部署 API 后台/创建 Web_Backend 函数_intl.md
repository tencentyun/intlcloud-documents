1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1) and enter the **Functions** page.
2. Select **Guangzhou** region and click **Create** to enter the function creating page.
3. Enter the following parameter information and click **Next**. See the figure below:
![](https://main.qcloudimg.com/raw/5749b6161b101eff5009649e08c29da8.png)
 - Creation method: Select "Blank function".
 - Function name: "web_backend".
 - Filter: Select "Python2.7" and choose "APIGW Basic Demo".
4. Keep the default configuration and click **Finish** to complete the function creation.
5. On the details page of the created function, select the **Function configuration** tab to view the basic information of function configuration.
6. On the details page of the created function, select the **Function code** tab to view or online edit the function code.
Main parameters include:
 - Execution is set to "api_gw_basic_demo.main_handler", indicating that the SCF console will automatically save this snippet of code as a `api_gw_basic_demo.py` file, compress, and upload it to SCF for creating the function.
 - `main_handler` in the sample code is the entry-point function, which has the following two input parameters:
    - `event` : Gets the information of triggering source.
    - `context` : Gets the environment and configuration information of this function.
7. On the details page of the created function, select the **Triggers** tab and click **Add a trigger**.
8. On the **Add a trigger** page, set "Trigger type" to "API Gateway trigger", keep other default parameters, and click **Save**. See the figure below:
 ![](https://main.qcloudimg.com/raw/dd31e56eadc9c8a92fe12537553b8455.png)
