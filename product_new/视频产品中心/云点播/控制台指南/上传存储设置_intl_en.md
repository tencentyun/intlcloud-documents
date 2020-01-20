## Operation Scenarios
The upload storage settings in VOD consist of category management and storage region management, helping you manage the files in the console more conveniently.

## Category Management Directions
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview), and click **Upload Storage** > **Category Management** on the left sidebar to enter the "Category Management" page.
![](https://main.qcloudimg.com/raw/32907d7786d94234bde68649e22cb592.png)
2. Click **Add Category** to pop up the "Add Category" dialog box, enter the category name, and click **OK**.
3. The newly added category will be displayed in the category list on this page, where you can rename or delete a category or add a subcategory.
	- Rename: click the target category name and an edit icon will appear to the right of the name. Then, click the icon to rename the category.
	- Delete: click **Delete** in the row of the target category to delete it. If it contains a subcategory, you need to delete the subcategory first.
	- Add Subcategory: this can be done in the same way as **adding a category**.

>
>- The category name can contain up to 25 letters, digits, and ().
>- In category management, you can also view, modify, delete, and associate files with categories.
>- Category management supports a 4-level structure, and subcategories cannot be added for a level-4 category.
>- After adding a category, you can also modify the category of a video file in the media assets section in the console. For more information, please see [Modifying Video Categories](https://intl.cloud.tencent.com/document/product/266/33893).
>- By default, there is a category named "Other" in category management, and you cannot rename or delete it or add subcategories for it. After a category is deleted, existing files in it will be categorized as "Other".

## Storage Region Directions
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview), and click **Upload Storage** > **Storage Region** on the left sidebar to enter the "Storage Region" page.
![](https://main.qcloudimg.com/raw/dde696a1aa4a23fcc3e29786410d70d2.png)
2. Click the status button on the row of the target region to enable the region. An enabled region can be set as the default region.
>
	- You can choose to enable multiple regions, but only one of them can be set as the default region.
	- When a region is enabled, it cannot be manipulated until it is successfully configured. After the region is enabled, it will take 5–10 minutes to take effect.
	- If you need to enable an overseas region (such as Hong Kong (China), Singapore, Moscow, Frankfurt, Mumbai, or Seoul), please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

#### Storage Rules
- If no other regions are enabled, all files will be transferred to the default region by default.
- If other regions have been enabled:
	- If an IP is **within the nearby upload storage range of the enabled region**, files will be uploaded to the nearby enabled region.
	- If an IP is **outside the nearby upload storage range of the enabled region**, files will be uploaded to the default region.

For more information on storage region, please see [Practice of Optimizing Upload Quality](https://intl.cloud.tencent.com/document/product/266/33904).



