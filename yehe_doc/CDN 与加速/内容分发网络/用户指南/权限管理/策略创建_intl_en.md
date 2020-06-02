To make it easier for you to configure domain name queries and manage permissions at a higher level of granularity, the CDN permission policies have been completely upgraded. This allows you to grant permissions at the domain name level through custom policy statements.

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview) and click **Policies** to access the policy management page. Then, click **Create Custom Policy**:

2. Select **Create by Policy Generator**:

3. Select **CDN** in the service drop-down list and select the actions to be authorized. If you want to grant full read/write permission, check **Action Name** to select all actions. To map specific actions with console features, please see [Console Permissions](https://intl.cloud.tencent.com/document/product/228/35229).

4. Enter the domain name to be authorized as the resource. Then, click **Add Statement** and **Next** to create a policy. Then, associate the created policy with existing users and user groups for further authorization:
	- All domain names: enter `*` for resource description.
- One/multiple domain names: you need to enter them in the six-segment CDN resource format (`qcs::cdn::$account:domain/$domain`) where `$account` is described using `uin`, i.e., the account ID of the root account. Take the domain names `www.test1.com` and `www.test2.com` as examples:
	 - One domain name: `qcs::cdn::uin/123456789:domain/www.test1.com`
	 - Multiple domain names: separate them with `,`, such as `qcs::cdn::uin/123456789:domain/www.test1.com,qcs::cdn::uin/123456789:domain/www.test2.com`
	


