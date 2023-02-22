## Overview
Video dragging can be enabled to specify the start point of a video. Only MP4, FLV and TS files are supported.

## Use Cases
Video dragging generally happens in VOD scenarios. When a user drags the video progress bar, a request similar to the one as shown below will be sent to the server:
```js.
http://www.test.com/test.flv?start=10
```
In this case, data will be returned starting from the 10th byte. VOD files are all cached on nodes, so the nodes can directly respond to such requests once this configuration is enabled.

## Notes
- The origin must support Range requests, or the origin-pull may fail.
- You can optimize node cache with query string. A video URL may carry different query strings. When it's cached with the query strings, even for the same requested resource, multiple cache IDs will be generated (due to different query strings), resulting in multiple origin-pull requests for the same resource. For more information, see [Query String](https://intl.cloud.tencent.com/document/product/1145/46174).
- Supported file formats: MP4, FLV and TS. 
<table>
<thead>
<tr>
<th align="left">File Type</th>
<th align="left">Meta Information</th>
<th align="left">Start Parameter</th>
<th align="left">Request Sample</th>
</tr>
</thead>
<tbody><tr>
<td align="left">MP4</td>
<td align="left">The meta information must be included in the file header, instead of at the end of the file.</td>
<td align="left">The parameter `start` specifies a time point (in seconds) and indicates milliseconds with decimals. For example, "start = 1.01" means that the start time is 1.01s. Nodes will locate the last keyframe before the time specified by `start` if `start` is not a keyframe.</td>
<td align="left"><code>http://www.test.com/demo.mp4?start=10</code> indicates that the video plays from the 10th second.</td>
</tr>
<tr>
<td align="left">FLV</td>
<td align="left">The video on the origin must contain meta information.</td>
<td align="left">The parameter `start` specifies a byte. Nodes will automatically locate the last keyframe before the byte specified by `start` if `start` is not a keyframe.</td>
<td align="left"><code>http://www.test.com/demo.flv?start=10</code> indicates that the video plays from the 10th byte.</td>
</tr>
<tr>
<td align="left">TS</td>
<td align="left">No special requirements</td>
<td align="left">The `start` parameter specifies a start byte. Nodes will automatically locate the byte at the beginning.</td>
<td align="left"><code>http://www.test.com/demo.ts?start=10</code> indicates that the video plays from the 10th byte.</td>
</tr>
</tbody></table>


## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Rule Engine** on the left sidebar.
2. On the page that displays, select the target site and create rules for video dragging as needed. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1145/46151).
