## Operation Scenarios
Purge and prefetch is the update mechanism for resources cached in CDN nodes. This document describes how to purge and prefetch resources based on `FileId` in VOD.
A `FileId` is the ID of an audio/video media file in VOD, which is used for all the outputs of operations (e.g., transcoding or screencapturing) in the same file. Therefore, when a `FileId` is purged or prefetched, the operation will take effect on the original video file as well as its output files like transcoded videos and screenshots.


## Cache Purge
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod) and click **Distribution and Playback** > **Purge and Prefetch** on the left sidebar to enter the "Cache Purge" page by default.
2. Enter up to 10 FileIds of the resources to be purged and separate them by carriage return.
3. Click **Submit** to start the purge, which will take around 10 minutes to complete.

>Once cache purge is performed on a resource, the system will delete its existing cache on all the CDN nodes across the entire network. When a user request arrives at a node, the node will pull the corresponding resource from the origin server, return it to the user, and cache it to the node so as to ensure that the user can get the latest resource.

## Content Prefetch
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod) and click **Distribution and Playback** > **Purge and Prefetch** on the left sidebar to enter the "Cache Purge" page by default.
2. Click **Prefetch Content** to enter the "Prefetch Content" page.
3. Enter up to 10 FileIds of the resources to be prefetched and separate them by carriage return.
4. Click **Submit** to start the prefetch, which will take around 10 minutes to complete.

>When a resource is prefetched, it will be cached in advance to all the CDN nodes across the entire network. When a user request arrives at a node, the resource can be directly obtained, which shortens the response time.

## Operation Record
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod) and click **Distribution and Playback** > **Purge and Prefetch** on the left sidebar to enter the "Cache Purge" page by default.
2. Click **Operation Log** to enter the "Operation Record" page.
3. This page displays purge and prefetch records, including operation type, operation object, operation time, status, and progress, which can be queried by time and searched for by content.

