## Overview
You can change upload storage settings including storage categories, storage regions, and upload acceleration to better manage files in the VOD console.


## Managing Categories
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/overview) and select **Application Management** on the left sidebar.
2. Select the target application.
3. Click **Upload Storage > Category Management** on the left sidebar.
![](https://qcloudimg.tencent-cloud.cn/raw/95d60acb6d5c9bbfbb4c602ef27f5b4e.png)
4. Click **Add Category**. In the pop-up window, enter the category name and click **OK**.
5. The newly added category will be displayed in the category list on this page, where you can rename or delete a category or add a subcategory.
	- Rename: Click the category name, and then click the edit icon next to it to change the name.
	- Delete: Click **Delete** in the **Operation** column to delete a category. If a category has subcategories, you need to delete the subcategories first.
	- Add subcategory: Click **Add Subcategory** in the **Operation** column. In the pop-up window, enter a subcategory name and click **OK**.

>?
>- The subcategory name supports up to 64 characters. Only letters, digits, and parentheses are allowed.
>- You can also use APIs to view, modify, and delete a category, as well as place files under a category.
>- You can add up to four levels of categories. This means you cannot add subcategories for a level-4 category.
>- You can modify the category of a file on the **Video/Audio Management** page of the console. For details, see [Quick Edit](https://intl.cloud.tencent.com/document/product/266/33893).
>- There is a default category named "Other", which you cannot rename, delete, or add subcategories for. If you delete a category, its files will be categorized under "Other".

## Configuring Storage Regions
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/overview) and select **Application Management** on the left sidebar.
2. Select the target application.
3. Click **Upload Storage > Storage Region** on the left sidebar.
![](https://qcloudimg.tencent-cloud.cn/raw/f6239d2a24ad590e9a67fd7e61b2f6a2.png)
4. To enable storage in a region, toggle on the button in the **Status** column. You can set an enabled storage region as the default.
>?
>- You can enable multiple storage regions, but you can set only one default region.
>- After you enable a region in the console, it takes about 5-10 minutes for the configuration to take effect, during which you cannot perform any actions on the region. **Once enabled, a region cannot be disabled.**

#### Storage rules
- If only the default region is enabled, all files will be stored in it.
- If other regions are also enabled:
	- If your IP address is **within the storage scope of an enabled region**, the files you upload will be saved to that region.
	- If your IP address is **not within the storage scope of any enabled region**, the files you upload will be saved in the default region.

For more information on storage regions, see [How to Increase the Speed and Success Rate of Media File Upload](https://intl.cloud.tencent.com/document/product/266/37548).


## Configuring Client Upload Acceleration
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/overview) and select **Application Management** on the left sidebar.
2. Select the target application.
3. Select **Upload Storage > Upload Acceleration** on the left sidebar.
4. Click **Edit** in the **Client upload acceleration** area to modify acceleration settings.
![](https://qcloudimg.tencent-cloud.cn/raw/1c7d3c5eb63e8412d8569c66d59aeb4e.jpg)
5. Toggle on or off **Global network acceleration** and **QUIC transmission** and click **Confirm**.
>? You can enable **QUIC transmission** only if **Global network acceleration** is on.
