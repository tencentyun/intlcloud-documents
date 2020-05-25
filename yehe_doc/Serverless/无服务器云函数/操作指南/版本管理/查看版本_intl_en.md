## Operation Scenarios

This document describes how to view the version configuration, code, and other information of a specified function.

## Directions
1. Log in to the SCF Console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the "Function Service" page, select the region and namespace where the function to be viewed resides:
3. Click a function name to enter the function details page.
3. Select the "Version" drop-down list in the top-right corner on the function details page and click the name of the version you want to view. This document takes viewing version `1` as an example as shown below:
![](https://main.qcloudimg.com/raw/03212c17658b0e15ba2cd41d04d4c362.png)
Here, you can view version information as shown below:
![](https://main.qcloudimg.com/raw/03fc7f742d7505dea5b4ec9aeb075f53.png)
>
> - After you switch to the desired version, the **Function Configuration**, **Function Code**, **Layer Management**, **Monitoring Info**, and **Log Query** tabs will display contents of the corresponding version. For more information on the tabs, please see [Querying Functions](https://intl.cloud.tencent.com/document/product/583/19809).
>- After you switch to a non-`$LATEST` version, the function configuration and code will remain in the state upon release and cannot be modified.
>- Triggers can be configured differently for different versions.
>- The logs and monitoring information respectively display the specific invocation logs and monitoring data of the corresponding version.




