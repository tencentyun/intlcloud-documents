CLB will upgrade the authentication feature for certain APIs on April 27, 2021 (Beijing time). After the upgrade, sub-users need to [apply for CAM policy authorization](#cam) from the root account to use the upgraded APIs, or the API calls may fail.

## Related APIs
<table>
<tr><th>API</th><th>Feature</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/214/33806">DescribeClassicalLBByInstanceId</a></td><td>Queries the classic CLB instances bound to a real server</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/214/33799">ReplaceCertForLoadBalancers</a></td><td>Replaces the certificate associated with a CLB instance
</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/214/33800">DescribeLoadBalancerListByCertId</a></td><td>Queries CLB instances by a certificate ID
</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/214/38187">DescribeQuota</a></td><td>Queries quotas
</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/214/37093">DescribeBlockIPList</a></td><td>Queries the IP blocklist of a CLB instance
</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/214/37091">DescribeBlockIPTask</a></td><td>Queries the execution status of an async IP blocking task
</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/214/37092">ModifyBlockIPList</a></td><td>Modifies the IP blocklist of a CLB instance
</td></tr>
</table>

<span id="cam"></span>
## Authorizing Sub-users
Please complete the policy authorization for your sub-users as instructed below to prevent failed calls to the upgraded APIs.
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. Click **Policies** on the left sidebar.
3. Click **All Policies**.
4. Click **Associate Users/Groups** on the right of the target policy.
5. [](id:step4) In the pop-up window, select target users from the box on the left to the **Selected** box on the right, and click **Confirm**.
![](https://main.qcloudimg.com/raw/4f9af5773b60505393707c9b2bbe9517.png)
6. It is optional: if you need to associate a user group, please click **Switch to User Groups** -> **User Groups** in the pop-up window, and repeat the operations in <a href="#step4">step 5</a>.
![](https://main.qcloudimg.com/raw/276164b1c4bf81979ba8c4f3d382336b.png)


