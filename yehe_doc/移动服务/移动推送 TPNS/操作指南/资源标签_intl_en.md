
**Resource tag** is a resource management tool provided by Tencent Cloud. You can assign tags to TPNS applications and then manage all applications under a certain resource tag in a unified way.

Resource tag has the following two capabilities:

- [Cost allocation by tag](#.E6.8C.89.E6.A0.87.E7.AD.BE.E5.88.86.E8.B4.A6)
- [Authorization by tag](#.E6.8C.89.E6.A0.87.E7.AD.BE.E6.8E.88.E6.9D.83)

Resource tag divides into tag keys and tag values. One tag key can correspond to multiple tag values. You can authorize and allocate cost by tag in the following steps.

## Use Cases

For example, if both the **application 1** and **application 2** created in TPNS are owned by the **product department**, you can assign the tag `Department: Product Department` to both of them. Then, you can:

1. View the aggregated bill for all Tencent Cloud resources under the `Department: Product Department` tag, i.e., the total usage of the product department in Tencent Cloud.
2. Directly grant Tom (a new employee in the product department) permissions to manage all resources under the tag `Department: Product Department`.

The following describes how to use resource tags on the TPNS platform:

## Preparations

### Step 1. Create a tag

1. Go to the [Tag List](https://console.cloud.tencent.com/tag/taglist) page.
2. Click **Create** to access the tag creation page and enter the tag key and the corresponding tag value.  
	 ![](https://main.qcloudimg.com/raw/04ed0ff85cf0133724dd6c40a5eac14b.png)
3. Click **OK**. You can view the creation result in the list at the bottom of the page.

### Step 2. Assign tags to resources

You can assign tags to TPNS applications in the **Tag** or **TPNS** console.

#### Tag console

1. After creating a tag, click **Resource Tag** on the left sidebar to enter the resource tag page.  
2. You can enter the tag assignment page:
	- **Resource Type**: select "TPNS application".
	- **Region**: select the "service access point" you selected when creating the product in the TPNS console.
3. After selecting **Resource Type** and **Region**, click **Query resource** to view all the applications you have created on the TPNS platform. The **Resource ID** corresponds to the **AccessID** of a TPNS application.
![](https://main.qcloudimg.com/raw/660bdf2a7a3689d7c3ca4ae7820950ff.png)
4. Select multiple applications in the list below and click **Edit tag value** above the list to assign the corresponding tag key-value pair to the selected applications.
![](https://main.qcloudimg.com/raw/d924052be7d8633ef545f8b26cf976d3.png)

#### TPNS console

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns), click **Configuration Management** > **Basic Configuration** on the left sidebar to view the basic configuration items of an application. (You can use the application selector at the top of the page to select the application for which to assign a tag.)
2. Click the edit icon on the right of the **Tag** attribute in the **Application Information** block.
![](https://main.qcloudimg.com/raw/527471d53f6a6851b7816e4a14a8190f.png)
3. Then, the tag management module will pop up, where you can assign tags to the application.
![](https://main.qcloudimg.com/raw/480950db293840860bc00213c2511c08.png)

## Cost Allocation by Tag

### Step 1. Set a cost allocation tag

1. To use the tag feature for bills, you need to go to the [Billing Center](https://console.cloud.tencent.com/expense) and select **Bills** > ** Cost Allocation Tags** on the left sidebar. The tag key set as a cost allocation tag will be displayed as a separate column of the bill. You can filter and categorize bills based on this tag key.
2. On this page, you can view the list of created tag keys. Select the tag key to be displayed and click **Set as Cost Allocation Tag** to set the tag key as a cost allocation tag in the bill.
   ![](https://main.qcloudimg.com/raw/e93636181da696a321153cefc064e42b.png)

> ?You can set 5 cost allocation tags at most. We recommend that you select one tag key as the cost allocation tag, which makes it easier for you to manage your expenses.

### Step 2. Display bills by tag

You can view and click the new option **By Tag** on the **[Bill Overview](https://console.cloud.tencent.com/expense/bill/overview)** page. Then, you can select a specific **tag key** to view the histogram and list of relevant resources aggregated by the tag key.
![](https://main.qcloudimg.com/raw/9d42e05b5a0270a37a52dd978d345495.png)

## Authorization by Tag

Authorization by tag means to quickly authorize resources under the same tag to a user or user group. The steps are as follows:

1. Go to the [Policy](https://console.cloud.tencent.com/cam/policy) page and click **Create Custom Policy** in the top-left corner.
2. In the creation method selection window that pops up, click **Authorize by Tag** to enter the "Authorize by Tag" page.
   ![](https://main.qcloudimg.com/raw/80ed332af4e4b8eba71ac769bf04b1d1.png)
3. On the "Authorize by Tag" page, select the following information and click **Next** to enter the check page.
	- **Authorized Users/User Groups**: select the users/user groups to be authorized (choose one option).
	- **Tag Keys**: select the tag key to be authorized (required).
	- **Tag Values**: select the tag value to be authorized (required).
	- **Resources**: the management permission is granted by default.
4. Click **Next**, check the policy (whose name can be customized), and click **Complete**.


At this point, you have completed authorization by tag. For more use cases of the tag feature, please see [Product Overview](https://intl.cloud.tencent.com/document/product/651/13334).

