### Do I have to install BHLoader?
Yes. Ops engineers have to install BHLoader, as it is used to invoke local applications, create connections through them, and access the target resources.

### After installing BHLoader, do I have to install connection tools such as SecureCRT and Xshell?
Yes. You need to install connection tools locally, as BHLoader is mainly used to invoke local applications, and connection tools such as SecureCRT and Xshell are required to complete the connection process and perform local operations on CVM.

### Are the admin permissions required for an OS account to install BHLoader?
Yes.

### Does an asset account have to be a real user of CVM?
The asset account must be an existing user of the target CVM instance (for example, `root` and `administrator`), as BH itself does not create CVM users.

### Can I customize the timeout period for automatic disconnection when no operations are performed within a certain period of time after I log in to the BH Ops page?
Yes. The admin can set the web idle timeout period.

### Can I disable two-factor authentication?
Two-factor authentication must be enabled for SaaS BH for security reasons. Currently, you can use password + OTP or password + SMS.

### What is an access allowlist? Why is there an IP address in it before I add one?
- An access allowlist is a list of IPs from which users can connect to BH by using local tools (such as SecureCRT, Xshell, and MSTSC). It is similar to a CVM security group.
- When you successfully access the Ops page, your public IP address will be automatically or can be manually added to the allowlist.

### What should I do if the connection via a tool fails after I have logged in to the Ops page?
This problem may be caused by multiple public IP addresses at your network egress. In particular, the IP address added after login to the Ops page is not the one used to connect to BH via a local tool. You can manually add your IP range to the allowlist.

### What should I do if I find that the server list is empty after logging in to the Ops page?
Log in to the BH management page as an admin, click **Create access permission** or **Edit** on the **Access permissions** page, and select the target asset or asset group in step 3 to create or modify an access permission.
