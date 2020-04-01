## Scenario

A **tag** is a key-value pair provided to identify resources on the Tencent Cloud. Tags allow you to flexibly classify and manage your CVM resources by service, purpose, owner, and other aspects.
Note that tags are not used by Tencent Cloud. They only help you to manage CVM resources.

## Use Limits
Note the following limits when using tags:
- Quantity limits: Each Tencent Cloud resource can be bound to a maximum of 50 tags.
- Tag key limits:
 - Do not create tag keys prefixed with `qcloud`, `tencent`, and `project`, because they are reserved for the system.
 - A tag key can only contain digits, letters, and `+=.@-`. It cannot exceed 255 characters in length.
- Tag value limits: A tag value can only contain empty strings or digits, letters, and `+=.@-`. It cannot exceed 127 characters in length.

## Directions and Cases

### Case description

Case: A company purchased six CVM instances. The following table lists the information about the deployment departments, business scope, and owners of the six CVM instances.

| Instance ID | Deployment Department | Business Scope | Owner |
|---------|---------|---------|--------|
| ins-abcdef1 | E-commerce | Marketing campaigns | John Smith |
| ins-abcdef2 | E-commerce | Marketing campaigns | Wangwu |
| ins-abcdef3 | Games | Game A | Jane Smith |
| ins-abcdef4 | Games | Game B | Wangwu |
| ins-abcdef5 | Entertainment | Post-production | Wangwu |
| ins-abcdef6 | Entertainment | Post-production | John Smith  |

For example, we can add the following tag key-value pairs to the ins-abcdef1 instance:
<table id="table02">
	<tr><th>Tag Key</th><th>Tag Value</th></tr>
	<tr><td>dept</td><td>ecommerce</td></tr>
	<tr><td>business</td><td>mkt</td></tr>
	<tr><td>owner</td><td>johnsmith </td></tr>
</table>

Similarly, you can add tag key-value pairs to other instances based on the different settings of deployment departments, business scopes, and owners.

### Specify one or more tags in the CVM console
Take the preceding case as an example. After designing the tag key-value pairs, you can log in to the CVM console to specify the tags.

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm).
2. On the Instances page, select the instance to be bound to the tags. In the Operation column, click **More** and then choose **Instance Settings** > **Edit Tags**.
2. In the **You have selected 1 resource** window that appears, specify the tags as required.
For example, you can add [three tag key-value pairs](#table02) to the ins-abcdef1 instance.
3. Click **OK**. The system displays a message indicating that the modification was successful.


### Filters instances by tag

If you need to query instances bound to a specified class of tags, you can perform filtering as follows:

1. In the search box, select **Tag**.
2. After **Tag**, enter the specified tag key-value pair and then click <img src="https://main.qcloudimg.com/raw/3cca38f08eaa87087cdd1b81eaf08a0a.png" style="margin: 0;"> to search for the tags.
For example, if you need to query CVM resources owned by John Smith, you can enter `Tag:owner:johnsmith`.

