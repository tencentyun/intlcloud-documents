## Operation Scenarios
After configuring the function, submitting the code, and passing the online test, you can fix the version of the function by publishing the version to avoid errors or execution failures of your online business caused by subsequent modification and testing of the code. You can publish a version at any time, and in all releases, the `$LATEST` version is always the latest version.

## Directions
> A function has the `$LATEST` version attribute upon its creation. The `$LATEST` version points to the currently editable version and is always present and editable. 
>
1. Log in to the SCF Console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. At the top of the "Function Service" page, select the region and namespace where the function to be viewed resides as shown below:
![](https://main.qcloudimg.com/raw/b862bd3fea499ed033147cd09c1f96ca.png)
3. Click the function name to enter the function information page.
4. Select **Operation** > **Publish New Version** in the top-right corner of the function information page as shown below:
![](https://main.qcloudimg.com/raw/f6294a74fe4eb8d0ad8df3d4d581819c.png)
5. In the pop-up "Publish New Version" window, enter the version description and click **Submit** to publish the version as shown below:
![](https://main.qcloudimg.com/raw/f140a1072fc595070c913d6232c3afd8.png)
>
> - When the release is submitted, the SCF platform will generate a copy of the configuration and code content of the current `$LATEST` version of the function and save it as version content.
> - After a version is published, the version number of the release will be generated, which starts from 1 and increases progressively with each release. The version number has no upper limit.
> - The published version only records and fixes the configuration and code of the current `$LATEST` version of the function but not the trigger configuration of the function. A newly published function version does not have any triggers.



