## Overview
You can search for uploaded objects/folders or objects in uploaded folders. COS supports searching for objects/folders as well as hierarchical folders and their objects in the current bucket.

>? 
>- The object prefix entered for object search is case-sensitive.
>- The COS console supports only prefix match, but not fuzzy match. If you want to use fuzzy match, the COSBrowser tool is recommended. For details on COSBrowser, see [COSBrowser Overview](https://intl.cloud.tencent.com/document/product/436/11366).

## Directions
### Searching for Current Objects in a Bucket

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left.
5. In the search box in the top-right corner of the page, enter the object name prefix and click ![](https://main.qcloudimg.com/raw/eeaf7547492ba4358671f820cf242ff1.png). Then, the system will display objects or folders with the **same name prefix** in the current bucket. To search for a specific object, enter the full object key, such as `exampleobject.txt`.
![](https://main.qcloudimg.com/raw/9eadf9e5e0244cea5d94b52ca004309e.png)

### Searching for Objects in Hierarchical Folders

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left.
5. In the search box in the top-right corner of the page, enter the full object path (or folder name) and the full or partial object prefix and click ![](https://main.qcloudimg.com/raw/eeaf7547492ba4358671f820cf242ff1.png). The system will display search results with the **same object prefix** in the same folder.

