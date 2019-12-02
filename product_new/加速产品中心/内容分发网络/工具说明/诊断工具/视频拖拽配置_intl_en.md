- Video dragging generally happens during on-demand video. When a user drags the video progress bar, a request similar to the one as shown below will be sent to the server: 
`http://www.test.com/test.flv?start=10`
In this case, data will be returned starting from the 10th byte. Video files in VOD scenarios are all cached on various CDN nodes; therefore, the nodes can directly respond to such requests once this configuration is enabled.
- When enabling video dragging, you need to enable the ignore query string feature too, and the origin server must support range requests. Files in MP4, FLV and TS are supported:

| File Type | meta Information | start Parameter Description | Sample Request |
| ---- | -------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| MP4 | For a video on the origin server, the meta information must be located in the file header. Videos with meta information located at the file end are not supported | The start parameter specifies a time (in seconds) and uses decimal to specify a millisecond (for example, start = 1.01 means that the starting time is at 1.01s). CDN will locate the last key frame before the time specified by the start parameter (if start is not a key frame)  | `http://www.test.com/demo.mp4?start=10`  </br>The video will be played back starting from the 10th second |
| FLV | The video on the origin server must have meta information | The start parameter specifies a byte. CDN will automatically locate the last key frame before the byte specified by the start parameter (if start is not a key frame) | `http://www.test.com/demo.flv?start=10`</br> The video will be played back starting from the 10th byte |
| TS | No special requirements | The start parameter specifies a time (in seconds) and uses decimal to specify a millisecond (for example, start = 1.01 means that the starting time is at 1.01s). CDN will locate the last key frame before the time specified by the start parameter (if start is not a key frame)  | `http://www.test.com/demo.ts?start=10` </br>The video will be played back starting from the 10th second |

## Configuration Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page.
2. Find the domain name you want to edit and click **Manage** in the operation column.
 ![](https://main.qcloudimg.com/raw/f5bc41a4fe8fd20dd8b2c098da3878a7.jpg)
3. Click the **Access Control** tab and configure the **Video Dragging** module.
Video dragging is disabled by default.
 ![](https://main.qcloudimg.com/raw/515a46c56b93b9932f5bbcab39a8293e.png)
4. Toggle the video dragging switch on. If the [Ignore Query String](https://intl.cloud.tencent.com/document/product/228/6291) feature is disabled, enabling video dragging will automatically enable that feature.
![](https://main.qcloudimg.com/raw/36d2c0ef77d57bb1fa180b8d89134369.jpg)
