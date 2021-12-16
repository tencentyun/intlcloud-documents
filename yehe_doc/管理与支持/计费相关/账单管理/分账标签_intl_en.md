## Overview

Tags help you manage your resources. You can use tags to categorize, search for, and aggregate your Tencent Cloud resources. Tags are the labels you attach to Tencent Cloud resources and can be used for cost allocation. A tag consists of a tag key and a tag value. A tag key can have multiple values.

To display a tag in your bills, you need to set the tag as a cost allocation tag. Each cost allocation tag is a column in bills, and the values of a tag are displayed in the corresponding rows of the resources they are attached to. Tags not set as cost allocation tags are not displayed in bills.

## Prerequisites

You have logged in to the [Tag console](https://intl.cloud.tencent.com/login).

## Directions

### Creating tag

1. On the left sidebar, click **Tag List**.

2. Click **Create Tag**.

3. In the pop-up window, enter a tag key and value, and click **OK**.

![](https://qcloudimg.tencent-cloud.cn/raw/d85103ed5a7819eb68d2cfcfeba47371.png)

### Attaching tag

1. On the left sidebar, click **Resource Tag**.

2. Select a region and resource type based on your needs and click **Query resource**.

>? You can query and tag resources on this page. A tag can be attached to multiple resources, and a resource can have multiple tags.
> 

![](https://qcloudimg.tencent-cloud.cn/raw/c7dff2fa642d1d9d0268d23f2d962811.png)

### Setting cost allocation tag

1. Go to the [Billing Center](https://console.intl.cloud.tencent.com/expense). On the left sidebar, click **Bills** > **Cost Allocation Tags**.

2. Select the target tag keys and click **Set as Cost Allocation Tag**.

![](https://qcloudimg.tencent-cloud.cn/raw/d11e6f8d5db09066ee0782f665ea3d52.png)

3. In the pop-up window, click **Confirm**.

>? You can set up to 15 cost allocation tags, but we recommend you set only one as this makes cost management easier. Each cost allocation tag occupies a column in bills, based on which you can filter and categorize your costs.
>

## Tag Display

You will see tag information in your bills starting from the month of setting cost allocation tags.

>! Bills generated before the setting will not change and will not include tag information.

### In **Bill Overview**

1. Go to [Bill Overview](https://console.intl.cloud.tencent.com/expense/bill/overview).

2. Select the **By Tag** tab and choose a tag key. You will see a list of the tagged resources and a bar graph.

![](https://qcloudimg.tencent-cloud.cn/raw/a08aabceadf985aa664932804f37c3a8.png)

### In **Bill Details**

1. Go to **Bill Details**.

2. Based on your needs, select the **Bill by Instance** or **Bill Details** tab. You will find in the list below a column for each cost allocation tag.

![](https://qcloudimg.tencent-cloud.cn/raw/4b318a0341b4563d2b648125faad7c73.png)

The column name is in the format of “Tag Key: xxx”. You can filter bills by tag.

### In bill files

After setting cost allocation tags, you will see the tags in the bill files you download, regardless of the bill type. You can use tag keys to filter your bills or perform other operations.

1. Tag display in L1 bills (by product and project)
In L1 bills, you will find a sheet named “summaryByTagAndProduct”, in which you can view bill details by tag key. If you haven’t assigned a tag value for a resource, the content of the corresponding cell will be `-`.

 ![](https://qcloudimg.tencent-cloud.cn/raw/ef896c6cf2d4b82be8ce95ad3639b6db.png)

2. Tag display in L2 bills (by resource ID)
In L2 bills, you will see tag key columns on the right and tag values in the cells of the columns. If you haven’t assigned a tag value for a resource, the content of the corresponding cell will be `-`.

 ![](https://qcloudimg.tencent-cloud.cn/raw/53f6525ad2baaf69201383069a968895.png)

3. Tag display in L3 bills (bill details)
In L3 bills, you will see tag key columns on the right and tag values in the cells of the columns. If you haven’t assigned a tag value for a resource, the content of the corresponding cell will be `-`.

![](https://qcloudimg.tencent-cloud.cn/raw/b3c46e60151273d0f99d4dbadb18aaf9.png)

## Query by API

You can also use APIs to query tag information starting from the month of setting cost allocation tags.

Call the `DescribeBillDetail`, `DescribeBillResourceSummary`, `DescribeBillSummaryByProject`, or `DescribeBillSummaryByTag` API and you will get bill data and the corresponding tag information.

## FAQs

### When can I see tags in bills after tagging resources and setting cost allocation tags?

Tagging takes effect immediately, but there is a delay in bill data, so tags will not be displayed until the cache data of bills is refreshed.
