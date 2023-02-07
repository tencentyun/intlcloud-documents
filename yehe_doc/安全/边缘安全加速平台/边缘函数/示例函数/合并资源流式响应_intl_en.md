In this example, three video clips are merged into one video, and the merged video is played on a client based on the order in which the video clips are merged. This example demonstrates how to use an edge function to fetch multiple remote resources, read and merge the resources in streaming mode, and respond to a client request by using the merged resource in streaming mode.

## Sample Code

```typescript
async function combine(readableVideos, destination) {
  for (const readable of readableVideos) {
    // Send a streaming response.
    await readable.pipeTo(destination, {
      preventClose: true
    });
  }

  const writer = destination.getWriter();
  writer.close();
  writer.releaseLock();
}

async function handleRequest(request) {
  // The URLs of the video clips.
  const urls = [
    'https://laputa-1257579200.cos.ap-guangzhou.myqcloud.com/stream-01.mov',
    'https://laputa-1257579200.cos.ap-guangzhou.myqcloud.com/stream-02.mov',
    'https://laputa-1257579200.cos.ap-guangzhou.myqcloud.com/stream-03.mov',
  ];

  const requests = urls.map(url => fetch(url));
  const responses = await Promise.all(requests);
  // Obtain the readable streams of the video clips.
  const readableVideos = responses.map(res => res.body);

  const { readable, writable } = new TransformStream();
  // Merge the video clips.
  combine(readableVideos, writable);

  return new Response(readable, {
    headers: {
      'content-type': 'video/mp4',
    }
  });
}

addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request));
});

```

## Sample Preview

In the address bar of the browser, enter a URL that matches a trigger rule of the edge function to preview the merged video. View the response header and verify that the video is transferred in chunked mode.

<img src="https://qcloudimg.tencent-cloud.cn/raw/ad723c7f68ae0b7ae5511e2e997ca274.png" width=809px>

## References
- [Runtime APIs: TransformStream](https://www.tencentcloud.com/document/product/1145/52698)
- [Runtime APIs: Response](https://www.tencentcloud.com/document/product/1145/52691)
