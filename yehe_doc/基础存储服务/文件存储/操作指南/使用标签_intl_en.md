## Overview

[Tags](https://intl.cloud.tencent.com/document/product/651) are key-value pairs provided by Tencent Cloud for easy resource identification. You can use tags to categorize and manage cloud resources. Tencent Cloud will not use your tags, they are solely used by you to manage your resources. This document describes how to edit tags for file storage resources.

## Use Limits

Note the following limits when editing tags:

- **Quantity**: each file system allows up to 50 tags.
- **Tag key**:A tag key can only contain `numbers`, `letters`, and `+=.@-`. It cannot exceed 255 characters in length.
- **Tag value**: a tag value can only contain `empty strings or numbers`, `letters`, and `+=.@-`. It cannot exceed 127 characters in length.

## Directions and Use Cases

### Use case

A company has purchased 6 file systems, of which the business group, scope and owners are as follows:

| File System ID  | Business Group | Business Scope | Owner |
| ----------- | -------- | -------- | ------ |
| cfs-abcdef1 | E-commerce | Marketing campaigns | John Smith |
| cfs-abcdef2  | E-commerce | Marketing campaigns | Chris   |
| cfs-abcdef3 | Games | Game A | Jane Smith |
| cfs-abcdef4 | Games | Game B | Ada |
| cfs-abcdef5  | Entertainment | Post-production | Chris       |
| cfs-abcdef6 | Entertainment | Post-production | John Smith |

Taking cfs-abcdef1 as an example, we can add the following 3 sets of tags to the file system:

<table id="table02">
	<tr><th>Tag Key</th><th>Tag Value</th></tr>
	<tr><td>dept</td><td>ecommerce</td></tr>
	<tr><td>business</td><td>mkt</td></tr>
	<tr><td>owner</td><td>John Smith</td></tr>
</table>



Similarly, you can add tag key-value pairs to other file systems based on the business group, scope and owners.




## Directions


### Tagging a new file system

#### Prerequisites
Make sure you have a tag that you can use before creating a file system. If you do not have any tags, go to the [Tag Console](https://console.cloud.tencent.com/tag/taglist) and create one.

1. Log in to the [CFS Console](https://console.cloud.tencent.com/cfs).
2. In the File System List page, click **Create**.
3. In the “Create File System” pop-up window, find **Tag** down below, and click **Add** to add a tag to the file system. Only existing tags can be added in this step.

4. Click **OK**, and the tag will be bound to the created file system.

>?For more information on creating file systems, see [Creating File Systems and Mount Targets](https://intl.cloud.tencent.com/document/product/582/9132).


### Adding, modifying, or deleting a tag on an existing file system

1. On the File System List page, locate the file system and click **Edit Tag** in the Operation column.

2. Add, modify or delete a tag as needed in the pop-up window.

3. Click **OK**.



### Filtering file systems by tags

To filter file systems by tag, follow the steps below:

1. Click the search box and select **Tag** from the dropdown menu.
2. Enter tag key and tag value, and click <img src="https://main.qcloudimg.com/raw/3cca38f08eaa87087cdd1b81eaf08a0a.png" style="margin: 0;">, or press Enter to search as shown below:
For example, if you want to find file systems tagged with a `business` tag key, do a search for `Tag:business`. If you want to find file systems tagged with a `business` tag key and `mkt` tag value, do a search for `Tag:business:mkt`.
