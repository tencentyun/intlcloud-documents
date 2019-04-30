Purge and prefetch is the update mechanism for resources cached in CDN nodes. Tencent Cloud VOD purges and prefetches resources based on the FileId. A FileId is the ID of an audio or video media file in VOD. The outputs of transcoding or screencapturing of a video belong to its FileId. Therefore, when a FileId is purged or prefetched, the operation will take effect on the original video file as well as its output files such as transcodes and screenshots.
- When you perform a cache purge, the system will delete the caches of the video on all CDN nodes on the entire network. When a user requests arrives at a node, the node will pull the corresponding resource from the origin server, return the request, and cache the resource to the node so as to ensure that the user can obtain the latest resource.
- When you prefetch a resource, it will be cached in advance to all the CDN nodes on the entire network. When a user request arrives at a node, the resource can be directly obtained, thereby reducing the response time.

### Cache Purge
Log in to the [VOD Console](https://console.cloud.tencent.com/video/cdnlog), select **Distribution and Playback** > **Purge and Prefetch** in the left navigation pane, select the **Purge Cache** tab, enter the FileId of the resource to be purged, and press `Enter`. A single purge supports up to 10 entries. Click **Submit** to start the purge, which will take around 10 minutes. Please wait patiently.
![](https://main.qcloudimg.com/raw/f3528737a65ac4794cfa738acefc7a28.png)

### Prefetch Content
Log in to the [VOD Console](https://console.cloud.tencent.com/video/cdnlog), select **Distribution and Playback** > **Purge and Prefetch** in the left navigation pane, and select the **Prefetch Content** tab.
Enter the FileId of the resource to be prefetched, and press `Enter`. A single prefetch supports up to 10 entries. Click **Submit** to start the prefetch, which will take around 10 minutes. Please wait patiently.
![](https://main.qcloudimg.com/raw/c32dabd5ec37fca01113a20aa20d9b3e.png)

### Action History
Log in to the [VOD Console](https://console.cloud.tencent.com/video/cdnlog), select **Distribution and Playback** > **Purge and Prefetch** in the left navigation pane, and select the **Operation Log** tab where you can view the records of purge and prefetch actions, as well as the type, object, time, status and current progress of each action.
![](https://main.qcloudimg.com/raw/b2245d7a6447896a1dd0939c48df3d12.png)
