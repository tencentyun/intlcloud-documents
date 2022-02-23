## Overview
Purge and prefetch is the update mechanism for resources cached in CDN nodes. This document describes how to purge and prefetch resources based on `FileId` and `URL` in VOD.
>?
>- A `FileId` is the ID of an audio/video media file in VOD. A `FileId` is used for all operational outputs (e.g., transcoding or screencapturing) of a file. Therefore, when you purge or prefetch a `FileId`, both the original video file and the output files (e.g., transcoded videos and screenshots) will take effect.
>- `URL` is the audio/video URL in VOD. `URL` is specific to an audio/video media file. Therefore, when you purge or prefetch a `URL`, only the corresponding file will take effect.


## Cache Purge
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Distribution and Playback** > **Purge and Prefetch** on the left sidebar to enter the "Cache Purge" page by default.
2. Enter the FileId or URL of the resources to be purged and separate them line by line. You can submit up to 10 FileIds or 20 URLs at a time.
Click **Submit** to start the purge. It will take around 10 minutes to complete.

>?Once you perform a cache purge on a resource, the system will delete the existing cache of the resource from the CDN nodes across the network. When a user request arrives at a node, the node will pull the corresponding resource from the origin server, return the request, and cache the resource, ensuring that the user obtains the latest resource.

## Content Prefetch
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Distribution and Playback** > **Purge and Prefetch** on the left sidebar to enter the "Cache Purge" page by default.
2. Click **Content Prefetch** to enter the "Content Prefetch" page.
3. Enter the FileId or URL of the resources to be prefetched and separate them by line by line. You can submit up to 10 FileIds or 20 URLs at a time.
Click **Submit** to start the prefetch. It will take around 10 minutes to complete.

>?When a resource is prefetched, it will be cached in advance to all the CDN nodes across the network. When a user request arrives at a node, the resource can be directly obtained, and response time is shortened.

## Operation Record
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Distribution and Playback** > **Purge and Prefetch** on the left sidebar to enter the "Cache Purge" page by default.
2. Click **Operation Record** to enter the "Operation Record" page.
3. This page displays your purge and prefetch records, including operation type, operation object, operation time, status, and progress. You can query by time or content.




