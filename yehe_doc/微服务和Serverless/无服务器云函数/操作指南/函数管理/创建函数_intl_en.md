
SCF offers multiple function creation methods. This document describes how to create a function through the console and command line tool.

## Creating functions via the console

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and click **Function Service** on the left sidebar.
2. Select the region and namespace where to create a function at the top of the **Functions** page and click **Create** to enter the function creation process as shown below: 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/wnBG038_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219142236.png)
3. On the **Create function** page, select a function creation method as needed.
  - **Template**: You need to enter the required function name and use configuration items in the function template to create the function.
  - **Create from scratch**: You need to enter the required function name and runtime environment to create the function.
  - **Use TCR image**: You can create a function based on a TCR image. For more information, see [Usage](https://intl.cloud.tencent.com/document/product/583/41077).
4. Configure the basic information of the function.
<dx-tabs>
::: Create from template
1. Add a tag in **Fuzzy search** to find a template as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/8X3I157_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219142541.png)
2. Select the template and click **Next**.
3. Enter the basic information of the function.
	- **Function name**: The function name is automatically populated by default and can be modified as needed.
	- **Region**: The region is automatically populated by default and can be modified as needed.
	- **Time zone**: SCF uses the UTC time by default, which you can modify by configuring the `TZ` environment variable. After you select a time zone, the `TZ` environment variable corresponding to the time zone will be added automatically.
:::
::: Create from scratch
Enter the basic information of the function.
- **Function type**: Select **Event-triggered function** or **HTTP-triggered function**.
  - Event-triggered function: Receives JSON-formatted events from TencentCloud API or various triggers to trigger the function execution. For more information, see [Basic Concepts](https://intl.cloud.tencent.com/document/product/583/9210).
  - HTTP-triggered function: Directly receives HTTP requests to trigger the function execution in web service scenarios. For more information, see [Function Overview](https://intl.cloud.tencent.com/document/product/583/40688).
- **Function name**: The function name is automatically populated by default and can be modified as needed.
- **Region**: The region is automatically populated by default and can be modified as needed.
- **Runtime environment**: The runtime environment is automatically populated by default and can be modified as needed.
- **Time zone**: SCF uses the UTC time by default, which you can modify by configuring the `TZ` environment variable. After you select a time zone, the `TZ` environment variable corresponding to the time zone will be added automatically.
:::
::: Use TCR image
Enter the basic information of the function.
- **Function type**: Select **Event-triggered function** or **HTTP-triggered function**.
  - Event-triggered function: Receives JSON-formatted events from TencentCloud API or various triggers to trigger the function execution. For more information, see [Basic Concepts](https://intl.cloud.tencent.com/document/product/583/9210).
  - HTTP-triggered function: Directly receives HTTP requests to trigger the function execution in web service scenarios. For more information, see [Function Overview](https://intl.cloud.tencent.com/document/product/583/40688).
- **Function name**: The function name is automatically populated by default and can be modified as needed.
- **Region**: Select the region where the function is deployed, which must be the same as the region where the image repository is located.
- **Time zone**: SCF uses the UTC time by default, which you can modify by configuring the `TZ` environment variable. After you select a time zone, the `TZ` environment variable corresponding to the time zone will be added automatically.
:::
</dx-tabs>
5. Configure the function code.
<dx-tabs>
::: Create from template
The runtime environment and execution method are automatically populated by default as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/USNv964_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219143734.png)
:::
::: Create from scratch
Select the function code submitting method and execution method as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/HzWL458_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219144056.png)
- **Submitting method**: **Online editing**, **Local ZIP file**, **Local folder**, and **Upload a ZIP pack via COS** are supported.
  - For scripting languages: You can directly use the function code editor.
  - For non-scripting languages: You can submit the function code by uploading a zip package or through COS and then edit it.
- **Execution**: It specifies the starting file and function while invoking the cloud function. For more information, see [Function Overview](https://intl.cloud.tencent.com/document/product/583/19805).
:::
::: Use TCR image
Enter the image information as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/bykn557_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219145120.png)
- **Image**: Select an image already built in the image repository in the current region.
- **ENTRYPOINT**: (Optional) Set the startup command of the container. Enter an executable command (such as python). If it's left blank, the Entrypoint in the Dockerfile is used.
- **CMD**: (Optional) Set the startup parameters of the container. Separate each parameter with a space. If it's left blank, the CMD in the Dockerfile is used.
- **Image acceleration**: It is disabled by default. After it is enabled, SCF will pulling image much more quickly. It takes over 30 seconds to enable this option; therefore, wait patiently.
:::
</dx-tabs>
6. In **Log configuration**, choose whether to enable log delivery as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QNye895_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219145400.png)
Log delivery is disabled by default. After it is enabled, the execution logs of the function can be delivered to the specified location in real time. For more information, see [Log Delivery Configuration](https://intl.cloud.tencent.com/document/product/583/39778).
<dx-alert infotype="notice" title="">
Currently, you cannot select the log template for image-based functions and HTTP-triggered functions.
</dx-alert>
7. In **Advanced configuration**, configure the environment, permission, layer, and network of the function as needed. For more information, see [Function Overview](https://intl.cloud.tencent.com/document/product/583/19805).
8. In **Trigger configurations**, choose whether to create a trigger. If you select **Custom**, see [Trigger Overview](https://intl.cloud.tencent.com/document/product/583/9705).
9. Click **Complete**. You can view the created function on the [Functions](https://console.cloud.tencent.com/scf/list) page.



## Creating Function on CLI 

You can create a function as needed in more ways as detailed below:
- Use Serverless Cloud Framework CLI to create a function. For more information, see [Creating Functions on Serverless Cloud Framework](https://intl.cloud.tencent.com/document/product/583/32743).

