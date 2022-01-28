### Why is there no data in the console?

If you cannot see data in the console, troubleshoot the problem as follows:
- Check whether the currently logged-in account and the account that called the API are the same.
- Console data under the root account and sub-accounts as well as console data under different sub-accounts are independent of each other and invisible to each other.
- Data is displayed in the console according to the T+1 policy; that is, data of a day can be viewed in the console on the next day.

### Why can't a sub-account see the data under the root account and other sub-accounts?

The TMS data in the console under the root account and sub-accounts as well as data under different sub-accounts are independent of each other. If a sub-account wants to view data under the root account or other sub-accounts, it needs to be authorized by the root account by associating it with the `QcloudCamReadOnlyAccess` policy on the **Policies** page in the [CAM console](https://console.cloud.tencent.com/cam/policy) as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

### Can I configure a threshold for a risk model in the console?

No. If you have such needs, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance with configuration on the backend.