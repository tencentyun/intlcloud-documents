You can get started with CloudAudit easily on the Tencent Cloud console where you can view operation records, create a tracking set and edit its storage location. You can also track and delete the created tracking set, and disable the tracking set's logging feature.

 
## Register and Login
- [Register](https://cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F%3FfromSource%3Dgwzcw.184926.184926.184926%26gclid%3DEAIaIQobChMIoaGVwcT21gIVFSNoCh3VxAi-EAAYASAAEgId7PD_BwE) a Tencent Cloud account if you don't have one, and then complete identity verification according to [Identity Verification Guide](https://cloud.tencent.com/document/product/378/3629).
- If you have registered a Tencent Cloud account and completed the identity verification, [log in to Tencent Cloud](https://cloud.tencent.com/login?s_url=https%3A%2F%2Fcloud.tencent.com%2F%3FfromSource%3Dgwzcw.184926.184926.184926%26gclid%3DEAIaIQobChMIoaGVwcT21gIVFSNoCh3VxAi-EAAYASAAEgId7PD_BwE). 
 Click **Products** -> **Management Tools** -> **CloudAudit** to enter the CloudAudit page.
 
## View Operation Records
### List
 1. Log in to the CloudAudit console, click **Operation Record** on the left navigation pane to enter the operation record page.
![](//mc.qcloudimg.com/static/img/2188705c1326c9924b2f9f1411c4fa7e/image.png)
 2. On the operation record page, you can view related operation records according to user name, resource type, resource name, event source, event ID, keyword or corresponding operation event time. The queried operation records will be displayed in a list. By default, only the first two lines are displayed. You can **Click to load more**.
![](//mc.qcloudimg.com/static/img/a83e486ba997acc90fa737b157b92b52/image.png)

### Details
After you get the operation record list, you can click **▼** on the left side of the operation record to view more. Then, you can get the details of this operation record, including access key, region, error code, event ID, event name, event source, event time, request ID, source IP address and user name. Besides, you can click **View Event** to learn more information about the event.
![](//mc.qcloudimg.com/static/img/7d233b2d18e021e3902786251dbe7ec3/image.png)

## Use Tracking Set
1. **Create a tracking set**
 1. Log in to the CloudAudit console, click **Tracking Set** -> **New** on the left navigation pane to enter the tracking set creation page. 
 ![](//mc.qcloudimg.com/static/img/2f1078b545ae3eee0520a43174e4dc3d/image.png)
> **Note:**
> You can create only one tracking set.
 2. Enter the tracking set name, storage location and other related information. Then, click **Save**.
![](//mc.qcloudimg.com/static/img/4c1eefa5c16049cd7d525d8510efc445/image.png)
2. **Disable/Enable the tracking set's logging**
 1. After you create a tracking set, it is **enabled** by default.
 ![](//mc.qcloudimg.com/static/img/7d154b1ba8d7ea49e390b1c11167872b/image.png)
 
 2. Click the tracking set name (**test**) and you will see the following page.
 ![](//mc.qcloudimg.com/static/img/90a2e1140a1c465f949dd734ab6315e4/image.png)
 3. Click the switch button next to **Logging** on the right to **disable or enable** the tracking set's logging.
3. **Edit the storage location**
Click **Edit** on the page of **disabling/enabling the tracking set's logging** to edit the bucket and log file prefix. Then, Click **Save**.
 ![](//mc.qcloudimg.com/static/img/d52bf9a7432e03dc6c8147c98f82db70/image.png)
4. **Delete the tracking set**
Click **Delete** on the page of **disabling/enabling the tracking set's logging**.

## More Resources

In addition to getting started with CloudAudit on the console, you can easily view the usage of CloudAudit through [Experiments in Developer Lab](https://cloud.tencent.com/developer/labs/lab/10328).

