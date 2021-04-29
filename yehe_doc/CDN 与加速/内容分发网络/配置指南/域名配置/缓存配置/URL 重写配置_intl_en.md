## Configuration Scenario

If you need to modify the actual access URL to the URL that matches the origin server, you can use the URL rewriting configuration feature in Tencent Cloud CDN.

You can custom URL rewrite configuration to redirect URL 302 to destination URL.

## Configuration Guide

### Viewing the configuration

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** in the **Operation** column of a domain name to enter its configuration page, and switch to the **Cache Configuration** tab to find **URL Rewrite**.

**URL Rewrite** is disabled by default.
![](https://main.qcloudimg.com/raw/01f93aaa70c523ae0bb1ab5debae8558.png)


### Adding rules

You can add rewrite rule as needed and enable **URL Rewrite**.

**Configuration Limitations**
+ A single domain name can have up to 10 rewrite rules.
+ You can adjust the priority for multiple rules. The rule at the bottom will have the highest priority.
+ URL to be rewritten: full-path matching (starting with ‘/’) and regular expression are supported.
+ Destination URL: start it with "/".
+ URL to be rewritten and destination URL can contain up to 1,024 characters.

Click **Add Rewrite Rule**:
![](https://main.qcloudimg.com/raw/97ea8713395f3af8654c39be97f124d3.png)
After a rule is added, as the overall configuration is disabled by default, the service in the production network environment will not be affected.

>?The configuration below can be modified when it is disabled, but the configuration will not be deployed in the production network environment until it is enabled.

You can enable **URL Rewrite** to deploy the added rewrite rule in the production network environment.
![](https://main.qcloudimg.com/raw/214b034e578d5eaac0a63cacd49f1e2d.png)

If the requested URL matches the currently configured rule, the request will be redirected by 302 to the corresponding destination URL.

### Modifying rules

You can click **Modify** in the **Operation** column of a rewrite rule to modify the added rewrite rule.

### Deleting rules

You can click **Delete** in the **Operation** column of a rewrite rule to delete the added rewrite rule.



>! If your acceleration domain name is configured for global acceleration, **URL Rewrite Configuration** will take effect globally. This configuration does not distinguish between requests from and outside of Mainland China.

## Configuration Samples

If the **URL Rewrite Configuration** of the acceleration domain name `www.test.com`is as follows:
![](https://main.qcloudimg.com/raw/19edbf944b4e727b7c62270f2d8078cf.png)

The actual access status will be as follows:

+ The client requests `www.test.com/access`, CDN node returns the content of ‘www.test.com/origin/index.html’.
+ The client requests `www.test.com/test/a.jpg`, CDN node returns the content of ‘www.test.com/testnew/b.jpg’.



