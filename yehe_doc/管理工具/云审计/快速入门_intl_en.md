You can get started with CloudAudit easily in the Tencent Cloud Console, where you can view operation records, create and delete a tracking set, edit its storage location, and disable its logging feature.


## Signup and Login
- [Sign up](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F%3FfromSource%3Dgwzcw.184926.184926.184926%26gclid%3DEAIaIQobChMIoaGVwcT21gIVFSNoCh3VxAi-EAAYASAAEgId7PD_BwE) for a Tencent Cloud account if you don't have one yet, and then complete identity verification as instructed in [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).
- If you have already signed up for a Tencent Cloud account and completed identity verification, you can directly log in to [Tencent Cloud](https://console.cloud.tencent.com/) and click **Tencent Cloud Services** > **Management and Audit** > **CloudAudit** to enter the CloudAudit page.

## Viewing Operation Records
### List
1. Log in to the [CloudAudit Console](https://console.cloud.tencent.com/cloudaudit).
2. On the left sidebar, click **Event History** to enter the event history page.
3. On the event history page, you can view related operation records by username, resource type, resource name, event source, event ID, keyword, or corresponding operation event time. The queried operation records will be displayed in a list. By default, only partial data is displayed. You can **click to load more**.
![](https://main.qcloudimg.com/raw/124225c642c747a52cbdb1c001e2b6d2.jpg)

### Details
In the operation record list, you can click <img src="https://main.qcloudimg.com/raw/8b58051804db873ddf14a5f897711c9c.png" style="margin:0;"> on the left of an operation to get its details, including event time, username, event name, access key, event ID, source IP address, resource region, CAM error code, event region, event source, and request ID. You can also click **View Event** to view the details of the event.
![](https://main.qcloudimg.com/raw/48d2fabf59096d2839b7924dadfd7394.jpg)

## Using Tracking Set
1. **Create a tracking set**
 1. Log in to the [CloudAudit Console](https://console.cloud.tencent.com/cloudaudit) and click **Tracking Set** > **Create** on the left sidebar to enter the tracking set creation page. 
![](https://main.qcloudimg.com/raw/ee793193029d08b873d46186b98039df.jpg)
>!You can create only one tracking set.
 2. Enter the tracking set name, storage location, and other related information on the page and click **Complete**.
![](https://main.qcloudimg.com/raw/022556d2c29e653523f5d5d4615683cf.jpg)
2. **Disable/Enable the tracking set's logging feature**
 1. After you create a tracking set, it is **enabled** by default.
![](https://main.qcloudimg.com/raw/653c413004625b1add79a1eb4d6b5c3d.jpg)
 2. Click the tracking set name (**test**) and you will see the following page.
![](https://main.qcloudimg.com/raw/76376149a048ab52a7ce479287573a0a.jpg)
 3. Click the switch button next to **Logging** on the right to **disable or enable** the tracking set's logging feature.
3. **Edit the storage location**
Click **Edit** on the page of **disabling/enabling the tracking set's logging feature** to edit the bucket and log file prefix. Then, click **Save**.
 ![](https://main.qcloudimg.com/raw/1f720f70cccb6daf0e7bcea5affc8aba.jpg)
4. **Delete the tracking set**
Click **Delete Tracking Set** on the page of **disabling/enabling the tracking set's logging feature**.
