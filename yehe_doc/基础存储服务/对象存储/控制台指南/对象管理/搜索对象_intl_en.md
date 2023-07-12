## Overview
You can search for uploaded objects and folders in the COS console, which supports prefix and fuzzy search modes.

- Prefix search: Objects are searched for by prefix, and objects and folders with the specified object prefix are displayed.
- Fuzzy search: Objects are searched for by custom keyword, and objects and folders whose name contains the specified keyword are displayed.

>? 
>- The object prefix entered for object search is case-sensitive.
>- In addition, you can also use COSBrowser for fuzzy search as detailed in [COSBrowser Overview](https://intl.cloud.tencent.com/document/product/436/11366).


## Directions
### Searching for objects by prefix

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left.
5. In the search box in the top-right corner of the page, enter the object name prefix and click ![](https://main.qcloudimg.com/raw/eeaf7547492ba4358671f820cf242ff1.png). Then, the system will display objects or folders with the **same name prefix** in the current bucket. For example, if you enter `img`, objects and folders with the name prefix `img` will be displayed.



### Searching for objects by keyword

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left.
5. In the search box in the top-right corner of the page, enter the keyword and click ![](https://main.qcloudimg.com/raw/eeaf7547492ba4358671f820cf242ff1.png). Then, the system will display objects and folders whose name contains the keyword in the current bucket. For example, if you enter `t`, objects and folders whose name contains `t` will be displayed.

