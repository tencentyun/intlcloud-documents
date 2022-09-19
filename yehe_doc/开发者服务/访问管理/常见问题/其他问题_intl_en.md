
### How do I manage project resource permissions in a refined manner?
You can implement refined permissions management as instructed in [Authorization by Tag](https://intl.cloud.tencent.com/document/product/598/47827).


### Can I view the resources consumed for a project?
No. However, you can view the consumption details in the [CAM console](https://console.cloud.tencent.com/project).
![](https://qcloudimg.tencent-cloud.cn/raw/a76b6760667723c351fbeddc31ddbb99.png)
You can view all the resources used under the current account on the [Overview](https://console.cloud.tencent.com/) page in the console.
![](https://qcloudimg.tencent-cloud.cn/raw/7399078b020486dfa9c3891cd2292383.png)


### What should I do if the message “Failed to verify the SAML with a certificate” is prompted when I log in to Tencent Cloud as a sub-user?
You can troubleshoot as follows:
1. Use the [ SAML tool](https://www.samltool.com/validate_response.php) to verify whether the SAML response format is correct.
2. Check whether the required parameters (especially role-related parameters) are provided in the SAML response in correct format.
3. Check whether the parameters in the previous step have been used to create an IdP and a role as instructed in [Accessing Tencent Cloud Console as SAML 2.0 Federated Users](https://intl.cloud.tencent.com/document/product/598/32672).

If the problem persists, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
