该示例把三个视频合并为一个视频，在客户端按视频拼接顺序播放。实现了，使用边缘函数获取多个远程资源，并流式读取与拼接，最终流式响应客户端。

## 示例代码

```typescript
async function combine(readableVideos, destination) {
  for (const readable of readableVideos) {
    // 流式响应
    await readable.pipeTo(destination, {
      preventClose: true
    });
  }

  const writer = destination.getWriter();
  writer.close();
  writer.releaseLock();
}

async function handleRequest(request) {
  // 视频片段地址
  const urls = [
    'https://laputa-1257579200.cos.ap-guangzhou.myqcloud.com/stream-01.mov',
    'https://laputa-1257579200.cos.ap-guangzhou.myqcloud.com/stream-02.mov',
    'https://laputa-1257579200.cos.ap-guangzhou.myqcloud.com/stream-03.mov',
  ];

  const requests = urls.map(url => fetch(url));
  const responses = await Promise.all(requests);
  // 获取视频片段的可读流
  const readableVideos = responses.map(res => res.body);

  const { readable, writable } = new TransformStream();
  // 合并视频
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

## 示例预览

在浏览器地址栏中输入匹配到边缘函数触发规则的 URL，可预览到合并后的视频。查看响应头，视频以 chunked 方式传输。

<img src="https://qcloudimg.tencent-cloud.cn/raw/ad723c7f68ae0b7ae5511e2e997ca274.png" width=809px>

## 相关参考
- [Runtime APIs: TransformStream](https://www.tencentcloud.com/document/product/1145/52698)
- [Runtime APIs: Response](https://www.tencentcloud.com/document/product/1145/52691)
