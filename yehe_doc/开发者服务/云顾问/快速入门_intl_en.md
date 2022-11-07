This document describes how to quickly perform resource inspections in the Tencent Smart Advisor console.

## Step 1. Log in to the Tencent Smart Advisor console[](id:Step1)

Log in to the [Tencent Smart Advisor console](https://console.qcloud.com/advisor).


<dx-alert infotype="explain" title="">
If you don't have an account yet, sign up as instructed in [Signing up for a Tencent Cloud Account](https://www.qcloud.com/document/product/378/8415).
</dx-alert>



## Step 2. Authorize the service[](id:Step2)
If this is your first time using Tencent Smart Advisor, you need to grant permissions to it, so that it can access the Tencent Cloud services. If you have authorized it, skip this step.
On the [**Authorization**](https://console.qcloud.com/advisor/auth) page, toggle on **Service Authorization**.
![](https://qcloudimg.tencent-cloud.cn/raw/ed2eff6f1985dafb2522da0e4b21911b.png)


## Step 3. Start risk assessment[](id:Step3)
Select [**Risk Assessment**](https://console.cloud.tencent.com/advisor/assess) on the left sidebar and click **Start Assessing**. Then, the system will perform the assessment automatically.
<dx-alert infotype="explain" title="">
- By default, the system performs an automatic inspection every day. You can also manually trigger it.
- An assessment operation may take dozens of seconds to minutes subject to the Tencent Cloud resource size and number of assessment items. The result is dynamically refreshed on the page until the assessment is complete.
</dx-alert>



## Step 4. View the assessment result[](id:Step4)
After the assessment, you can view the result on the [**Risk Assessment**](https://console.cloud.tencent.com/advisor/assess) page.


### Overall description
The console UI is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/9207f55730067bbdce03e2d0ae63b47f.png)

- **Last Assessment Time**: Time of the last assessment.
- **Color**: Red indicates "high-risk items", orange "mid-risk items", and green "healthy".
- **Overview**: Collects and displays the assessment results of all items.
- **Security**: Collects and displays the assessment results of items by [**Security**](https://intl.cloud.tencent.com/document/product/1079/41573).
- **Reliability**: Collects and displays the assessment results of items by [**Reliability**](https://intl.cloud.tencent.com/document/product/1079/41573).
- **Performance**: Collects and displays the assessment results of items by [**Performance**](https://intl.cloud.tencent.com/document/product/1079/41573).
- **Cost**: Collects and displays the assessment results of items by [**Cost**](https://intl.cloud.tencent.com/document/product/1079/41573).
- **Service Restriction**: Collects and displays the assessment results of items by [**Service Restriction**](https://intl.cloud.tencent.com/document/product/1079/41573).

### Risk item details
Click to expand a risk item and view its details.
![](https://qcloudimg.tencent-cloud.cn/raw/0453e4ae143e4e74174f4b48c319729d.png)

 - **Alarm Condition**: Alarm condition for triggering the risk item.
 - **Optimization Advice**: Suggested measures to avoid the risk item.
 - **Resource List**: List of resources with high- and mid-risk items in this assessment.



## Step 5. Download the assessment report[](id:Step5)
You can generate a report by module or risk item in the following steps:
1. Go to the [**Risk Assessment**](https://console.cloud.tencent.com/advisor/assess) page, find the target module or risk item, and click **Generate Report**.
![](https://qcloudimg.tencent-cloud.cn/raw/5b5159ae3257e8866ede0e1da2ee723b.png)
2. After the report is generated, click **Download Report**.
3. In the **Download Assessment Report** pop-up window, select **Assessment report in Excel** or **Assessment report in PDF** as needed and click **OK**.


## Step 6. Get the expert explanation of the assessment report (optional)[](id:Step6)
You can get the expert explanation of the assessment report in this step.

1. Service authorization
Go to the [**Authorization**](https://console.qcloud.com/advisor/auth) page and enable **Report Access** to have Tencent Cloud architects read the report for you.
![](https://qcloudimg.tencent-cloud.cn/raw/c60af511c770de824ab02f8d6163b940.png)
2. Expert explanation
To reach Tencent Cloud architects and have their insights into your report, [contact us](https://www.tencentcloud.com/document/product/1079/50825).

