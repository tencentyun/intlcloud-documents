Provisioned concurrency can start concurrent instances in advance according to the configuration, instead of starting them when accepting requests. You can use this feature to set the quota of provisioned concurrent instances for a specified function version, so as to prepare computing resources in advance and reduce the duration for cold start and initialization of runtime environment and business code.



## Provisioned Concurrency and Concurrency Expansion

Provisioned concurrency is to start provisioned concurrent instances on the specified version in advance instead of limiting the concurrency. When the business traffic increases and exceeds the load limit of provisioned concurrent instances, the SCF backend will start more elastic concurrent instances to sustain the excessive business traffic until the total number of concurrent instances reaches the concurrency limit of the function.

Provisioned concurrency and elastic concurrency have the same expansion speed, which is subject to the function's [concurrency expansion speed limit](https://intl.cloud.tencent.com/document/product/583/37040).


## Provisioned Concurrency Operation Limits
- Provisioned concurrency can be configured only on published versions of a function but not the `$LATEST` version.
- The configured provisioned concurrency quota is subject to the account and function reserved quota.
- If the function has the reserved concurrency quota set, then the sum of all provisioned concurrency quotas for all versions of the function must be less than or equal to the reserved concurrency quota.
- If the function does not have the reserved concurrency quota set, then the configurable version provisioned concurrency quota is subject to the configurable quota at the account level. If the account has no remaining configurable quota, the version provisioned concurrency cannot be configured. In this case, you can free up the quota by deleting or reducing the concurrency of less used versions.



## Provisioned Concurrency Operations

### Adding provisioned concurrency
For a published function version, you can set a desired number of provisioned concurrent instances.
>! Provisioned concurrency can be set for a function version only after the [version is published](https://intl.cloud.tencent.com/document/product/583/15371).
>
1. Log in to the SCF Console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. On the "Function Service" list page, select the name of the target function to enter the "Function Management" page.
3. On the "Function Management" page, select "Concurrency Quota" on the left sidebar to enter the "Concurrency Quota" page.
4. On the "Concurrency Quota" page, click **Add Provisioned Concurrency** as shown below:
![](https://main.qcloudimg.com/raw/896d0ae8b0276a9316cf8f22f0c714bc.png)
5. In the "Add Function Provisioned Concurrency" window that pops up, select the desired version and the number of provisioned concurrent instances and click **Submit** as shown below:
![](https://main.qcloudimg.com/raw/d3749d4f21e7a17b7a23ddcf53171de6.png)
After completing the settings, you can view the configuration status in "Provisioned Quota". It will take some time for the SCF backend to add the instances and display the number of ready-to-start concurrent instances and completion status in the list.

### Updating provisioned concurrency
After the SCF backend adds the provisioned concurrent instances, you can modify the number of concurrent instances as needed.
1. Log in to the SCF Console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. On the "Function Service" list page, select the function for which to update the provisioned concurrency to enter the "Function Management" page.
3. On the "Function Management" page, select "Concurrency Quota" on the left sidebar to enter the "Concurrency Quota" page.
4. On the "Concurrency Quota" page, select **Set** on the right of the target version as shown below:
![](https://main.qcloudimg.com/raw/d3749d4f21e7a17b7a23ddcf53171de6.png)
5. In the "Set Function Provisioned Concurrency" window that pops up, update the set value and click **Submit**.
After the settings are completed, the SCF platform will adjust the number of concurrent instances according to your modification in a certain period of time.



### Deleting provisioned concurrency
If you no longer use a provisioned concurrency configuration, you can delete it.
1. Log in to the SCF Console and select **[Function Service](https://console.cloud.tencent.com/scf/list)** on the left sidebar.
2. On the "Function Service" list page, select the function for which to delete the provisioned concurrency to enter the "Function Management" page.
3. On the "Function Management" page, select "Concurrency Quota" on the left sidebar to enter the "Concurrency Quota" page.
4. On the "Concurrency Quota" page, select **Delete** on the right of the target version as shown below:
![](https://main.qcloudimg.com/raw/6c79a835ef99bd709c3349051cabef3d.png)
5. In the "Delete Function Provisioned Concurrency Quota" window that pops up, click **OK**.
    After the configuration is deleted, the SCF backend will gradually repossess concurrent instances.



