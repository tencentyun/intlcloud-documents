You can get started with CloudAudit easily in the Tencent Cloud console, where you can view operation records, create and delete a tracking set, edit its storage location, and disable its logging feature.


## Signup and Login
- [Sign up](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F%3FfromSource%3Dgwzcw.184926.184926.184926%26gclid%3DEAIaIQobChMIoaGVwcT21gIVFSNoCh3VxAi-EAAYASAAEgId7PD_BwE) for a Tencent Cloud account if you don't have one yet, and then complete identity verification as instructed in [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).
- If you have already signed up for a Tencent Cloud account and completed identity verification, you can directly log in to the [Tencent Cloud console](https://console.cloud.tencent.com/) and click **Products** > **Management and Audit** > **CloudAudit** to enter the CloudAudit page.

## Viewing Operation Records
### List
1. Log in to the [CloudAudit console](https://console.cloud.tencent.com/cloudaudit).
2. Click **Event history** in the left sidebar to enter the event history page.
3. On the event history page, you can view related operation records by username, operation type, resource event name, resource name, resource ID, API error code, key IP, and corresponding operation event time. The queried operation records will be displayed in a list. By default, only partial data is displayed.

### Details
In the operation record list, you can click <img src="https://main.qcloudimg.com/raw/be1649be0251749641c35e81db22535e.png" style="margin:-3px 0px;"> on the left of an operation to get its details, including event time, username, event name, access key, event ID, source IP address, resource region, CAM error code, event region, event source, and request ID. You can also click **View Event** to view the details of the event as shown below:
![](https://main.qcloudimg.com/raw/48d2fabf59096d2839b7924dadfd7394.jpg)

## Using Tracking Set
1. **Create a tracking set**
 1. Log in to the [CloudAudit console](https://console.cloud.tencent.com/cloudaudit) and select **Tracking Set** > **Create** on the left sidebar to enter the tracking set creation page. 
 2. On the **Tracking Set** page, click **Create** as shown below:
![](https://main.qcloudimg.com/raw/ee793193029d08b873d46186b98039df.jpg)
<dx-alert infotype="notice" title="">
You can create up to 5 tracking sets.
</dx-alert>
 2. Enter the tracking set name, storage location, and other relevant information on the page and click **Creation completed** as shown below:
![](https://main.qcloudimg.com/raw/022556d2c29e653523f5d5d4615683cf.jpg)
2. **Disable/Enable the tracking set's logging feature**
 1. After you successfully create a tracking set, it is **Enabled** by default as shown below:
![](https://main.qcloudimg.com/raw/653c413004625b1add79a1eb4d6b5c3d.jpg)
 2. Click the name of the tracking set in the **Name** column or **Edit** on the right on the tracking set row to enter the tracking set details page as shown below:
![](https://main.qcloudimg.com/raw/76376149a048ab52a7ce479287573a0a.jpg)
 3. Click <img src="https://main.qcloudimg.com/raw/9d9892843390a003afe42d52123fd500.png" style="margin:-3px 0px"> on the right of **Enable Logging** in the top-right corner of the page to **disable or enable** the tracking set's logging feature (which is enabled in the screenshot).
3. **Edit the storage location**
Click **Edit** in the **Shipping Location** section on the tracking set details page. You can choose to ship to a COS bucket or CLS. After editing, click **Save** as shown below:
![](https://main.qcloudimg.com/raw/1f720f70cccb6daf0e7bcea5affc8aba.jpg)
4. **Delete the tracking set**
Click **Delete** on the right on a tracking set row on the **Tracking Set** page or click **Delete Tracking Set** on the tracking set details page.

