

Click **Settings** > **Service settings** to activate Config and set the scope of resources to be monitored.

### Activating Config

You can **activate** or **deactivate** Config on the **Resource monitoring** page. When you enable the feature for the first time, you need to authorize and create a Config role (`Config_QCSLinkedRoleInConfigRecorder`) and select the target resource type. For more information, see [Supported Resource Types](https://www.tencentcloud.com/document/product/1164/51495).
![](https://qcloudimg.tencent-cloud.cn/raw/10e01aa95fc41cfd197cdb4e0826f167.png)

### Deactivating Config

If you no longer need to use Config, you can toggle off to**deactivate** it. Then, Config will no longer monitor or update the resource configuration. The resource configuration data, created rules, and compliance results stored in Config will be cleared and cannot be recovered. Data that has been delivered to COS buckets will not be affected.
![](https://qcloudimg.tencent-cloud.cn/raw/9241ff9d66f29a8eccfb323afe744785.png)
![](https://qcloudimg.tencent-cloud.cn/raw/0f336c6bbcaa7e89fd86cd678aeac182.png)

### Modifying the monitoring scope

If you have activated Config, you can click **Modify** to change the monitored resource types. Then, the resource list and timelines will be updated, and the existing rules and conformance packs under your account will be audited again. This takes 10-15 minutes.
![](https://qcloudimg.tencent-cloud.cn/raw/426809d3709636e224c065aa3862438a.png)
![](https://qcloudimg.tencent-cloud.cn/raw/32633468f031071a2d40ee3dded2e00e.png)

