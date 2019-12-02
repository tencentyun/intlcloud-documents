You can get started with CloudAudit easily on the Tencent Cloud console where you can view operation records, create a tracking set and edit its storage location. You can also delete the created tracking set, and disable the tracking set's logging feature.

 
## Register and Login
- [Register](https://intl.cloud.tencent.com/register) a Tencent Cloud account if you don't have one, and then complete identity verification according to [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).
- If you have registered a Tencent Cloud account and completed the identity verification, [log in to Tencent Cloud](https://intl.cloud.tencent.com/login). 
 Click **Products** -> **Management Tools** -> **CloudAudit** to enter the CloudAudit page.
 
## View Operation Records
### List
 1. Log in to the CloudAudit console, click **Operation Record** on the left navigation pane to enter the operation record page.

 2. On the operation record page, you can view related operation records according to user name, resource type, resource name, event source, event ID, keyword or corresponding operation event time. The queried operation records will be displayed in a list. By default, only the first two lines are displayed. You can **click to load more**.


### Details
After you get the operation record list, you can click **▼** on the left side of the operation record for more details. You will then receive details of this operation record, including access key, region, error code, event ID, event name, event source, event time, request ID, source IP address and user name. You can also click **View Event** to learn more information about the event.


## Use Tracking Set
1. **Create a tracking set**
  1. Log in to the CloudAudit console, click **Tracking Set** -> **New** on the left navigation pane to enter the tracking set creation page. 
  2. Enter the tracking set name, storage location and other related information. Then, click **Save**.

> **Note:**
> You can create only one tracking set.
>


2. **Disable/Enable the tracking set's logging feature**
 1. After you create a tracking set, it is **enabled** by default.
 
 2. Click the tracking set name (**test**) and you will see the following page.
 
 3. Click the switch button next to **Logging** on the right to **disable or enable** the tracking set's logging feature.
3. **Edit the storage location**
Click **Edit** on the page of **disabling/enabling the tracking set's logging feature** to edit the bucket and log file prefix. Then, Click **Save**.

4. **Delete the tracking set**
Click **Delete** on the page of **disabling/enabling the tracking set's logging feature**.


