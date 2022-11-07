## Overview
Tencent Smart Advisor allows you to ignore and exclude the following resources from inspections: 
 - Resources with a specified tag key and value
 - Instances

Resources set to **Ignored** can be added to inspections again as needed.

<dx-alert infotype="explain" title="">
To add or ignore resources through tag keys and values, you need to add tags to resources. For detailed directions, see [Creating Tags and Binding Resources](https://intl.cloud.tencent.com/document/product/651/41575).
</dx-alert>




## Directions

### Ignoring resources
You can specify resources to be excluded from inspections in the following ways:

<dx-tabs>
::: Ignoring resources by tag
1. Log in to the Tencent Smart Advisor console and select [**Assessment Items**](https://console.cloud.tencent.com/advisor/switch) on the left sidebar.
2. On the **Assessment Settings** page, select the **Ignored Resources** tab and click **+ Tag**.
![](https://qcloudimg.tencent-cloud.cn/raw/3ec18201554a5f4a364b0f2c15050a4a.png)
3. Expand the **Tag Key** and **Tag Value** drop-down lists and select the tag key and value to be ignored.
4. Click **Save**, and resources with the selected tag key and value will be excluded from inspections.


:::
::: Ignoring resources by instance
1. Log in to the Tencent Smart Advisor console and select [**Risk Assessment**](https://console.cloud.tencent.com/advisor/assess) on the left sidebar.
2. Click the assessment items to expand them, click the **Assessed Resource** tab, and select the target instance.
![](https://qcloudimg.tencent-cloud.cn/raw/a320e03137f1a0e5ea5e043c7eb9491d.png)
3. Click **Ignore**, and the instance will be excluded from inspections.

:::
</dx-tabs>





### Adding resources
You can add ignored resources to inspections in the following ways:

<dx-tabs>
::: Adding resources by tag

1. Log in to the Tencent Smart Advisor console and select [**Assessment Items**](https://console.cloud.tencent.com/advisor/switch) on the left sidebar.
2. On the **Assessment Settings** page, select the **Ignored Resources** tab.
3. Modify or delete a configured tag key and value as needed to add corresponding resources to inspections:
  - **Edit**: Click **Edit** on the right of the target tag and modify the information as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/5365bb3e9e6cfeafb8a366830af55ed8.png)
  - **Delete**: Click **Delete** on the right of the target tag to delete it.
![](https://qcloudimg.tencent-cloud.cn/raw/2401d97110d782660af8c2e2e5b0b8ce.png)

:::
::: Adding resources by instance

1. Log in to the Tencent Smart Advisor console and select [**Risk Assessment**](https://console.cloud.tencent.com/advisor/assess) on the left sidebar.
2. Click the assessment items to expand them, click the **Ignored Resources** tab, and select the target instance.
![](https://qcloudimg.tencent-cloud.cn/raw/4ca282c519b5b6b4091d9e42748b431a.png)
3. Click **Add**, and the instance will be added to inspections.


:::
</dx-tabs>

