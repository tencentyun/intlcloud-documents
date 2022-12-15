## View statistics
1. Log on to the [Security Operation Center Console](https://console.cloud.tencent.com/ssav2/config). In the left navigation pane, click **Cloud Security Configuration Management** -> **Configuration Check Results** to go to the Configuration Check Results page.
2. On the Configuration Check Results page, select ** Configuration Check Policy** to view the enabled check policies, statistics of check results based on the selected policies, and details list. By default, the check results based on all configuration check policies are displayed.
![](https://qcloudimg.tencent-cloud.cn/raw/2be97aaf257b17e260ea2603c64f1445.png)
 - View the number of enabled configuration check policies
![](https://qcloudimg.tencent-cloud.cn/raw/5b2e25914d3c3f11165f6bb4ba9a4c73.png)
>? To enable or disable the configuration check policies, please go to [Configuration Check Policies](https://www.tencentcloud.com/document/product/1008/51774).

 - View statistics of configuration check results
The statistics of the cloud security configuration check results include the numbers of four check results (shown in different colors) and the total number of all check results. Move the pointer over the donut chart of check results. The number of the corresponding check results appears.
![](https://qcloudimg.tencent-cloud.cn/raw/e59090d96bdd8449941d2f1df6ac8e73.png)

## Search results
In the list of [Configuration Check Results](https://console.cloud.tencent.com/ssav2/config/result), you can view the check details of each configuration requirement. The "Total Assets" column displays the numbers of compliant and noncompliant assets in different colors. You can also perform operations such as searching, filtering, handling, and checking now.

 - **Search**
In the upper-right corner of the list of configuration check results, you can search check results by entering the keywords of configuration requirements.
![](https://qcloudimg.tencent-cloud.cn/raw/c76753c9766d3b1374e7ffbd29277079.png)

 - **Filter**
In the list of configuration check results, click the header "Check Type", "Check Object", or "Check Result" to filter the configuration check results.
![](https://qcloudimg.tencent-cloud.cn/raw/acf1838daf13a3bef676072c2b5631e0.png)

## View the list of results 
#### View details
1. In the list of [Configuration Check Results](https://console.cloud.tencent.com/ssav2/config/result), click **View Details** in the Operation column to go to the Check Details page of that check item.
![](https://qcloudimg.tencent-cloud.cn/raw/d6613c792b3cb0bffcf5633c628cfb4a.png)
2. On the Check Details page, you can view the basic information, related information, noncompliant resources, compliant resources, unchecked resources, and ignored resources.
![](https://qcloudimg.tencent-cloud.cn/raw/f1960ccaebecb61940d56ae411bc4d78.png)
>? Some check items are common configurations for the cloud platform, for example, log audit. The Check Details page displays only the basic and related information of the check results, and the total number of assets is 1.

- **View check policies**
Click the check policy name in the "Basic information" section to go to the list of configuration check policies, where you can view the policy and perform other actions.
![](https://qcloudimg.tencent-cloud.cn/raw/1020d98b4c2eae23843ee162b99410d4.png)
- **View Help Documentation**
Click the **Help Documentation link** in the "Related information" section to view the online Help Documentation for the current configuration fixing suggestions.
- **Search the resources for configuration check**
In the upper-right corner of the lists of noncompliant resources, compliant resources, unchecked resources, and ignored resources, you can search by asset ID, Uid, asset name, private IP, or username keywords.
![](https://qcloudimg.tencent-cloud.cn/raw/ffe45303dfd6be4b1e04ed209dc3951d.png)
- **View configuration risks of resources**
In the lists of noncompliant resources, compliant resources, unchecked resources, and ignored resources, you can click **asset name** to go to the configuration risk list of that asset, where you can view configuration risks and perform other actions.
- **Export data of noncompliant resources**
In the upper-right corner of the list of noncompliant resources, click ![](https://qcloudimg.tencent-cloud.cn/raw/379331a670d33c07e5e347eb8426794f.png) to export the data of noncompliant resources to an Excel file.
>? You can export the first 5,000 pieces of data only.

![](https://qcloudimg.tencent-cloud.cn/raw/8a8106b688a515bab53ab96a19efe1b7.png)
 - **Handle now**
In the list of noncompliant resources, click **Handle Now** in the Operation column to go to the Asset Details page, where you can view details and perform other actions.
![](https://qcloudimg.tencent-cloud.cn/raw/415e85ae153778a64fff615f81c26e5d.png)
 - **Check Now**
In the list of noncompliant resources, select one or more assets and click **Check Now** to perform configuration check on the selected assets. At the end of the check, a message "Operation successful" pops up on this page.
![](https://qcloudimg.tencent-cloud.cn/raw/4a0aa268da69be4f8f5663a9681ae62a.png)
 - **Ignore check results**
In the list of noncompliant resources, select one or more assets and click **Ignore**, and enter the reason for ignoring in the pop-up box. The configuration check results of the selected assets are ignored after you confirm them in the confirmation prompt box.
![](https://qcloudimg.tencent-cloud.cn/raw/6b735716f8bdc8f6b202dbe8a8a5a291.png)

#### Handle now
In the list of [Configuration Check Results](https://console.cloud.tencent.com/ssav2/config/result), click **Handle Now** in the Operation column to go to the edit page of the configuration check, where you can modify configuration requirements.
>? The **Handle Now** button is grayed out for some check items, indicating that the configuration requirement cannot be modified.

![](https://qcloudimg.tencent-cloud.cn/raw/c7bffea5ba7bd13ccfa2c59a1707d663.png)

#### Check now
In the list of [Configuration Check Results](https://console.cloud.tencent.com/ssav2/config/result), click **Check Now** in the Operation column to start the configuration check. At the end of the check, a message "Operation successful" pops up on this page.
![](https://qcloudimg.tencent-cloud.cn/raw/069db997d909fa6031712cd940c22415.png)