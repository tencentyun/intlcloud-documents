## Overview

**Tags** are key-value pairs provided by Tencent Cloud for easy resource identification. You can use tags to categorize and manage your CVM resources.
Tencent Cloud will not use your tags, they are solely used by you to manage your CVM resources.

## Use Limits
Note the following limits when using tags:
- Quantity limits: each Tencent Cloud resource allows up to 50 tags.
- Tag key limits:
 - Tag keys cannot start with `qcloud`, `tencent`, or `project`.
 - A tag key can contain up to 255 characters, including numbers, letters, and `+=.@-`.
- Tag value limits: a tag value can contain up to 127 characters, including numbers, letters and `+=.@-`. It can be left empty if necessary.

## Directions and Cases

### Use case

A company has purchased six CVM instances, of which the business group, scope and owners are as follows:

| Instance ID | Business Group | Business Scope | Owner |
|---------|---------|---------|--------|
| ins-abcdef1 | E-commerce | Marketing campaigns | John Smith |
| ins-abcdef2 | E-commerce | Marketing campaigns | Chris |
| ins-abcdef3 | Games | Game A | Jane Smith |
| ins-abcdef4 | Games | Game B | Chris |
| ins-abcdef5 | Entertainment | Post-production | Chris |
| ins-abcdef6 | Entertainment | Post-production | John Smith  |

Taking ins-abcdef1 as an example, we can add the following 3 sets of tags to the instance:
<table id="table02">
	<tr><th>Tag Key</th><th>Tag Value</th></tr>
	<tr><td>dept</td><td>ecommerce</td></tr>
	<tr><td>business</td><td>mkt</td></tr>
	<tr><td>owner</td><td>John Smith</td></tr>
</table>

Similarly, you can add tag key-value pairs to other instances based on the business group, scope and owners.

### Setting tags in the CVM console
Take the preceding case as an example. After designing the tag key-value pairs, you can log in to the CVM console to specify the tags.

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. On the **Instance** page, select the target instance and click **More** > **Instance Settings** > **Edit Tags** in the **Operation** column.
2. Set the tags in the "1 resource selected" section of the pop-up window.
For example, you can add [three tag key-value pairs](#table02) to the ins-abcdef1 instance.
3. Click **OK**. The system displays a message indicating that the modification was successful.


### Filtering instances by tags

To filter instances by tag, follow the steps below:

1. Click the search box and select **Tag** from the drop-down list.
2. Enter the tag, and click <img src="https://main.qcloudimg.com/raw/3cca38f08eaa87087cdd1b81eaf08a0a.png" style="margin: 0;"> to search.
You can filter instances using tags. For example, you can search instances that are bound with tags `key1` or `key2` by entering `Tag: key1|key2` in the search box.
