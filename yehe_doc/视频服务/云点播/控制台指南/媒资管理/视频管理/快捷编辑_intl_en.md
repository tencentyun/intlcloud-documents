## Overview
This document describes how to quickly edit and modify the attributes of media assets in the VOD console.


## Directions

1. Log in to the VOD console and select **Media Assets** > **[Video Management](https://console.cloud.tencent.com/vod/media)**. The **Uploaded** page is displayed.
2. Select the target video, click **Quick Edit** above the list, modify the media asset information of the video file, and click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/71356f5f97a8f2d656edcff385291fd4.png)

>?
>- Quick edit is supported for configuration items of category, label, playback prohibition, and expiration time. If you don't select a configuration item, it will stay unchanged.
>- For more information on how to manage audio/video file categories, see [Category Management](https://intl.cloud.tencent.com/document/product/266/18874).

- **Category**: you can manage the categories of media asset files. A file can belong to only one category, and you can specify its category for easier operations.
- **Label**: you can manage the labels of media asset files. A file can have multiple labels, and you can filter it by label.
- **Playback Prohibited**: you can prohibit the playback of media asset files. Once prohibited, a file cannot be accessed on CDN nodes until the prohibition is canceled. Prohibition takes effect in about 5 minutes.
- **Expiration Time**: you can delete media asset files by expiration time. Once expired, a file will be deleted by VOD to reduce the storage costs.
>! Once deleted, a file cannot be recovered. Therefore, delete files with caution.

| Item | Description |
|---------|---------|
| Category | It is used for media asset categorization. Each media asset has only one category. |
| Label | It is used to label the content of media assets. Each media asset can have multiple labels. |
| Playback Prohibited | It is used to stop video delivery. After it is enabled, a media asset will become inaccessible over the public network. The time for it to take effect is 5 minutes, and the video status will change to **Playback Prohibited**. |
| Expiration Time | It is used to specify the deletion time of media assets. They will be deleted at the specified time and cannot be recovered. |
