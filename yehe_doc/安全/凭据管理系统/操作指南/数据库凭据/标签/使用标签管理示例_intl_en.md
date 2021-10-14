This document describes how to set tags and filter secrets by tag.
## Scenarios

- A tag is used for resource categorization and permission management from different dimensions.
- For [SSM](https://console.cloud.tencent.com/ssm), a tag is used to manage user secrets.
- You can tag your secrets to make it easy to categorize, track, and manage them. Also, you use the tags to check your secrets.



## Usage Limits

There are limits on using tags (tag key and tag value). For more information, see [Usage Limits](https://intl.cloud.tencent.com/document/product/651/13354).

## Directions

### Setting tags

1. Log in to the [SSM Console](https://console.cloud.tencent.com/ssm) and click **Database Credential** on the left sidebar.
![](https://main.qcloudimg.com/raw/66121c6c3d612ff9baea5a19e1a37ff8.png)
2. Click the drop-down button in the top left corner of the credential list to modify the region.
   ![](https://main.qcloudimg.com/raw/5512889ad52011ef76f5f7b7ed1151db.png)
3. Select a credential to edit its tag and click **Edit Tag** on the right.
![](https://main.qcloudimg.com/raw/2e157356ff5041655d94e9d5fd56cda1.png)
4. In the pop-up window, click **Add** to set tags as shown below:
![](https://main.qcloudimg.com/raw/01ff5fbde8c2b61c18a9ca3e0527debc.png)
5. Click **OK**. You should see a message indicating success of your modification. 

      

### Filtering credentials by tag
1. Log in to the [SSM Console](https://console.cloud.tencent.com/ssm) and click **Database Credential** on the left sidebar.
![](https://main.qcloudimg.com/raw/66121c6c3d612ff9baea5a19e1a37ff8.png)
2. Click the drop-down button in the top left corner of the credential list to modify the region.
   ![](https://main.qcloudimg.com/raw/5512889ad52011ef76f5f7b7ed1151db.png)
3. Select **Tag** as your filter criteria at the top of the search bar, enter the tag content, and then press Enter.
   For example, to filter the keys owned by alex, you can enter the tag "owner:alex" and press Enter.
   ![](https://main.qcloudimg.com/raw/2e157356ff5041655d94e9d5fd56cda1.png)
