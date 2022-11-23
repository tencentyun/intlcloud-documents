You can view the errors that occurred during live streaming in the CSS console.

## Prerequisites
You have logged in to the [CSS Console](https://console.cloud.tencent.com/live).

## Directions
1. Select **Event Center** > [Errors](https://console.cloud.tencent.com/live/event/error-event) on the left sidebar.
2. Enter a stream ID to query the errors the stream encountered in the last seven days. The time frame cannot be longer than three hours.
![](https://qcloudimg.tencent-cloud.cn/raw/d4a6f79951032f8cc34d1fdc9bd6d8a1.png)


[](id:erro_code)
## Error Types
Below is a list of errors that may occur during live streaming. 

| Error Type                |
| ----------------------- |
| The video timestamp moved backwards          |
| The audio timestamp moved backwards          |
| The video timestamp increased notably      |
| The audio timestamp increased notably      |
| Chunk size too big          |
| Two consecutive video frames arrived late  |
| Two consecutive audio frames arrived late  |
| The video codec changed    |
| The audio codec changed    |
| No codec header before a video frame arrived |
| No codec header before an audio frame arrived |