## Overview
You can manage file categories and storage regions in the **Upload Storage** section of the VOD console.

## Category Management
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/overview), and click **Upload Storage** > **Category Management** on the left sidebar to enter the **Category Management** page.
![](https://qcloudimg.tencent-cloud.cn/raw/95d60acb6d5c9bbfbb4c602ef27f5b4e.png)
2. Click **Add Category**, enter a category name in the pop-up, and click **OK**.
3. The newly added category will be displayed in the category list on this page, where you can rename or delete a category or add a subcategory.
	- Rename: click the target category name, and then click the edit icon to rename the category.
	- Delete: click **Delete** in the row of the target category to delete it. If it contains subcategories, you need to delete the subcategories first.
	- Add subcategory: click **Add Subcategory** in the row of the target category, enter a subcategory name in the pop-up, and then click **OK**.

>?
>- The subcategory name supports up to 64 characters. Only letters, digits, and () are allowed.
>- You can also use APIs to view, modify, delete, and bind files for category management.
>- You can add up to 4 levels of categories, meaning you cannot add subcategories for a level-4 category.
>- After adding a category for a video file, you can modify it on the **Video Management** page in the console. For details, please see [Modifying Video Category](https://intl.cloud.tencent.com/document/product/266/33893).
>- By default, there is a category named "Others" on the **Category Management** page, and you cannot rename or delete it or add subcategories for it. After a category is deleted, the files in it will be categorized as "Others".

## Storage Region
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/overview), and click **Upload Storage** > **Storage Region** on the left sidebar.
![](https://qcloudimg.tencent-cloud.cn/raw/f6239d2a24ad590e9a67fd7e61b2f6a2.png)
2. Toggle **Status** on for the target region to enable it. You can set an enabled region as the default region.
>?
>- You can enable multiple regions, but can set only one default region.
>- When a region is enabled, you cannot perform operations on it until it is successfully configured. Enabling a region takes effect in 5-10 minutes. **Once enabled, a region cannot be disabled**.

#### Storage rules
- If only the default region is enabled, all files will be stored in it.
- If other regions are also enabled:
	- If an IP is **within the upload storage range of a nearby enabled region**, files will be uploaded to the region.
	- If an IP is **outside the upload storage range of any enabled regions**, files will be uploaded to the default region.

For more information on storage regions, please see [Practice of Optimizing Upload Quality](https://intl.cloud.tencent.com/document/product/266/37548).




