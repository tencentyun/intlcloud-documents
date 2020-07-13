

## Pay-as-You-Go TencentDB Instance
> !For pay-as-you-go resources no longer used, **terminate them as soon as possible** to avoid fee deduction.
> Because your actual resource consumption changes constantly, the timing of a balance alert may deviate.

### Alerts
- Pay-as-you-go resources are billed by the hour. When your account balance becomes negative, the system will send an alert to your Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, and other methods which are configured in message subscription in the [Message Center](https://console.cloud.tencent.com/message).


### Arrears Processing
1. **From the moment your account balance becomes negative:**
 - You can continue to use your TencentDB instance for 24 hours from the moment your account balance becomes negative. We will continue to bill you for this period.
 - When your account has been in arrears for 24 hours, **your TencentDB instance will automatically shut down**, and we will stop billing you for this service.

2. **After automatic shutdown:**
 - Within 3 days of automatic shutdown, if the overdue payment is paid, you can start up your TencentDB instance and billing continues; if your balance remains negative, you will not be able to start up your TencentDB instance.
 - If the balance remains negative for 3 days after shutdown, the TencentDB instance will be repossessed. All data will be erased and cannot be recovered. Tencent Cloud account creator, global resource collaborators, and financial collaborators will be notified via email, SMS, etc.
 
![](https://main.qcloudimg.com/raw/cf4e2d01d9ebaffd3c34a0055ffd3eba.png)
