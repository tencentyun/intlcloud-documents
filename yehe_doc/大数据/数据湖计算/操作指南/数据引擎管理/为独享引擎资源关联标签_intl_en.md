## Overview
A tag is used to categorize and manage resources. It consists of a tag key and a tag value. A tag key can correspond to multiple values. You can create tags and bind them to cloud resources for easier management. Data Lake Compute supports binding tags to private engines in the console or on the purchase page, thereby enabling multidimensional category management and bill breakdown for private engine resources.

## Creating a Tag and Binding a Resource
Create a tag and bind it to a private engine for resource categorization and unified management.
### Directions
1. Log in to the [Tag console](https://console.cloud.tencent.com/tag) to create a tag as instructed in [Creating Tags and Binding Resources](https://intl.cloud.tencent.com/document/product/651/41575).
2. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc).
3. Click **Data engine** on the left sidebar to enter the **Data engine list** page.
4. Click a resource name to enter the resource details page. Click **Edit** to pop up the tag edit window and select a tag for binding.
![]()
5. Click **Confirm** to bind the tag to the private engine. You can click **Edit** again to unbind or modify the tag.
![]()

## Binding a Tag on the Purchase Page
You can bind a tag when purchasing a private engine resource in both monthly subscription and pay-as-you-go billing modes.
![]()

## Filtering Resources by Tag
You can filter resources by tag on the **Data engine** page in the Data Lake Compute console.
### Directions
1. Log in to the Data Lake Compute console and select **Data engine**.
2. Select a tag in the tag search box. You can filter resources by tag key or tag key-value.
![]()
![]()
3. Click the search icon to get the list of engines with that tag.
![]()

## Allocating Costs by Tag
You can bind tags in the organization or business dimension for cost allocation by department, project team, region, etc.
### Directions
1. Log in to the [Tag console](https://console.cloud.tencent.com/tag) and create a tag.
2. Bind the tag to an engine resource in the tag console, on the **Data engine** page in the Data Lake Compute console, or on the purchase page.
3. Go to the [Billing Center](https://console.cloud.tencent.com/expense/overview) to set a cost allocation tag. For more information, see [Cost Allocation Tags](https://intl.cloud.tencent.com/document/product/555/32276).
4. Go to the [Bill Overview](https://console.cloud.tencent.com/expense/bill/overview) page, select the aggregation by tag tab, and view the column chart and list of resources aggregated by tag key.
