Purge and prefetch are the mechanisms for managing resources in the CDN cache. Tencent Cloud VOD purges and prefetches resources based on the FileID. A FileID is the unique ID of an audio or video media file in VOD, and the outputs of the operations such as transcoding and screen-capturing on a video links to its FileID. Therefore, when purging or prefetching a FileID, all of the operation associated with this FileID will take effect on the original video file as well as its output files such as transcodes and screenshots.
- To purge content from the CDN cache, the system deletes all the cache on the CDN nodes in the entire network. When a user request arrives at a node, the node will pull the corresponding resource from the origin server, return the request, and cache the resource on the CDN node to ensure that the user can obtain the latest resource.
- To prefetch content, the system prefetches origin content to the CDN cache in advance. When a user request arrives at a CDN node, they can access content directly, effectively reducing the response time. 

### Purge CDN Cache
Log in to [VOD Console](https://console.cloud.tencent.com/video/cdnlog), select **Distribution and Playback** > **Purge and Prefetch** in the left sidebar, select the **Purge Cache** tab, enter the FileID of the resource to be purged, and press `Enter`. One purge supports up to 10 entries. Click **Submit** to purge, and please allow about 10 minutes for the process to be completed.
![](https://main.qcloudimg.com/raw/f3528737a65ac4794cfa738acefc7a28.png)

### Prefetch Content 
Log in to [VOD Console](https://console.cloud.tencent.com/video/cdnlog), select **Distribution and Playback** > **Purge and Prefetch** in the left sidebar, and select the **Prefetch Content** tab.
Enter the FileID of the resource to prefetch, and click `Enter`. One prefetch supports up to 10 entries. Click **Submit** to prefetch, and please allow about 10 minutes for the process to be completed.
![](https://main.qcloudimg.com/raw/c32dabd5ec37fca01113a20aa20d9b3e.png)

### Action History
Log in to [VOD Console](https://console.cloud.tencent.com/video/cdnlog), select **Distribution and Playback** > **Purge and Prefetch** in the left sidebar, and select **Operation Log**, where you will find the purge and prefetch records, as well as the type, object, time, status and current progress of each action.
![](https://main.qcloudimg.com/raw/b2245d7a6447896a1dd0939c48df3d12.png)
