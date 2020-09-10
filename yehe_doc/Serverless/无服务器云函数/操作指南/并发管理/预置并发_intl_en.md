Provisioned concurrence can start concurrent instances in advance according to the configuration, instead of starting them when accepting requests. You can use this feature to set the number of provisioned concurrent instances for a specified function version, so as to prepare computing resources in advance and reduce the duration for cold start and initialization of concurrent instances and business code.



## Provisioned Concurrence and Concurrence Expansion
Provisioned concurrence is to start provisioned concurrent instances on the specified version in advance instead of limiting the concurrence. When the business traffic increases and exceeds the load limit of provisioned concurrent instances, the SCF backend will start more elastic concurrent instances to sustain the excessive business traffic until the total number of concurrent instances reaches the concurrence limit of the function.

Provisioned concurrence and elastic concurrence have the same expansion speed, which is subject to the function's [concurrence expansion speed limit](https://intl.cloud.tencent.com/document/product/583/37040).


## Provisioned Concurrence Operation Limits
- Provisioned concurrence can be configured only on published versions of a function but not the `$LATEST` version.
- The total number of provisioned concurrent instances of a function should be configured as the total number of concurrent instances of the function minus 100. For example, if a function has 300 concurrent instances by default, the total number of provisioned concurrent instances that can be configured will be 200; if 150 provisioned concurrent instances have been configured on v1, only up to 50 ones can be configured on v2.



## Provisioned Concurrence Operations

### Adding provisioned concurrence
For a published function version, you can set a desired number of provisioned concurrent instances in the following steps:
1. Log in to the SCF Console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. On the "Function Service" list page, select the name of the target function to enter the "Function Management" page.
3. On the "Function Management" page, select "Concurrence Management" on the left sidebar to enter the "Concurrence Management" page.
4. On the "Concurrence Management" page, click **Add Provisioned Concurrence** as shown below:
![](https://main.qcloudimg.com/raw/cc67dfc7eb685db6009ca313f531154b.png)
5. In the "Add Provisioned Function Concurrence" window that pops up, select the desired version and the number of provisioned concurrent instances and click **Submit**.
After completing the settings, you can view the configuration status in "Provisioned Concurrence". It will take some time for the SCF backend to add the instances and display the number of ready-to-start concurrent instances and completion status in the list.

### Updating provisioned concurrence
After the SCF backend adds the provisioned concurrent instances, you can modify the number of concurrent instances as needed in the following steps:
1. Enter the "Concurrence Management" page of the target function.
2. On the "Concurrence Management" page, select **Set** on the right of the target version as shown below:
![](https://main.qcloudimg.com/raw/dcfb189dbb17334d4653ba32f79c541b.png)
3. In the "Update Provisioned Function Concurrence" window that pops up, update the set value and click **Submit**.
After the settings are completed, the SCF platform will adjust the number of concurrent instances according to your modification in a certain period of time.


### Deleting provisioned concurrence
If you no longer use a provisioned concurrence configuration, you can delete it in the following steps:
1. Enter the "Concurrence Management" page of the target function.
2. On the "Concurrence Management" page, select **Delete** on the right of the target version as shown below:
![](https://main.qcloudimg.com/raw/516542314836b4dcb2a1e91612f47ac6.png)
3. In the pop-up window, click **OK**. After the configuration is deleted, the SCF backend will gradually repossess concurrent instances.



