## Overview

- Video dragging generally happens in VOD scenarios. When a user drags the video progress bar, a request similar to the one as shown below will be sent to the server:
`http://www.test.com/test.flv?start=10`
  In this case, data will be returned starting from the 10th byte. Video files in VOD scenarios are all cached on various CDN nodes; therefore, the nodes can directly respond to such requests once this configuration is enabled.
- The Ignore Query String configuration should be enabled for video dragging. That is, the Ignore Query String of all rules in [Cache Key Rule Configuration(https://intl.cloud.tencent.com/document/product/228/35316) should be configured as "Ignore All", and the origin server should support Range requests. Supported file formats are MP4, FLV, and TS.

| File Type | Meta Information                                                 | Parameter Description (start)             | Request Sample                                       |
| :------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| MP4 | For a video on the origin server, the meta information must be located in the file header. Videos with meta information located at the file end are not supported. | The parameter `start` specifies a time point (in seconds) and uses a decimal to specify a millisecond. For example, "start = 1.01" means that the start time is at 1.01s. CDN will locate the last keyframe before the time specified by `start` if `start` is not a keyframe. | `http://www.test.com/demo.mp4?start=10` indicates that the video will be played back starting from the 10th second. |
| FLV      | The video on the origin server must have meta information.                                   | The parameter `start` specifies a byte. CDN will automatically locate the last keyframe before the byte specified by `start` if `start` is not a keyframe.| `http://www.test.com/demo.flv?start=10` indicates that the video will be played back starting from the 10th byte. |
| TS       | –                                                   | The `start` parameter defines a start byte. CDN will automatically locate the beginning byte. | `http://www.test.com/demo.ts?start=10` indicates that the video is played from the 10th byte.  |


## Viewing the Configuration
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click a streaming VOD acceleration domain name to enter the configuration page. Open the **Access Control** tab to find the **Video Dragging** section. Video dragging is disabled by default.
![img](https://main.qcloudimg.com/raw/515a46c56b93b9932f5bbcab39a8293e.png)
