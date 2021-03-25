## Overview
TPNS provides two billing modes: monthly subscription and pay-as-you-go. If your account has been in arrears for a certain period of time, the system will suspend your service and repossess resources. For more information, please see the following sections.


## Pay-as-You-Go (Postpaid) Mode
Pay-as-you-go billing is an elastic billing mode of TPNS. You can activate or terminate the service at any time, and the service fees will be charged by the number of daily active users (DAUs) and settled daily. This mode has relatively high prices and is suitable for scenarios where the number of DAUs fluctuates greatly.
After purchasing the pay-as-you-go service, please ensure that your account balance is always sufficient. If your account is in arrears for more than 24 hours, the pay-as-you-go service will be suspended.

### Service suspension mechanism
- At 06:00 every day, the system will settle the fees incurred the previous day, generate a bill, and deduct the fees from your account balance. If your account balance is insufficient or the sum of available balance and frozen amount is negative, and the deduction cannot be completed, your account will fall into arrears.
- The system will push arrears reminders when your account falls into arrears through phone call, SMS, WeChat, email, and Message Center (subject to the actual receipt channels and recipients configured in [Message Center](https://console.cloud.tencent.com/message/subscription)).
- If you fail to top up your account to a positive balance in 24 hours, the service will be officially suspended. If you top up your account in 24 hours, the service will remain available.
>!
>- After the service is suspended, the device registration, account, and tag binding logic can be used normally, but the push feature will become unavailable.
>- If you have activated the non-stop feature offered to key accounts, the service will not be suspended due to arrears of your account, you can continue to use it, and fees will continue to be charged. If you haven't activated this feature, you can [contact sales](https://console.cloud.tencent.com/workorder/category) to apply for activation.
>

### Repossession mechanism
After the service is suspended, if you fail to top up your account to a positive balance in seven days, the repossession policy will start.
>!After resources are repossessed, your application token information, account and tag information, push history, and other resource data will be deleted immediately and cannot be recovered.
