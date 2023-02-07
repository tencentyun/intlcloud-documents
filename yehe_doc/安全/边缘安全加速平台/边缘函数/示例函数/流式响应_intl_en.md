In this example, the [Fetch API](https://www.tencentcloud.com/document/product/1145/52687) is called to fetch a remote jQuery.js resource, and the resource is sent to a client in streaming mode in response to a request from the client.

## Sample Code

```typescript
async function handleRequest(request) {
  const response = await fetch('https://static.cloudcachetci.com/qcloud/main/scripts/release/common/vendors/jquery-3.2.1.min.js');

  if (response.status !== 200) {
    return response;
  }

  // Generate readable streams and writeable streams.
  const { readable, writable } = new TransformStream();
  // Respond to the client in streaming mode.
  response.body.pipeTo(writable);

  return new Response(readable, response);
}

addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request));
});
```

## Sample Preview

In the address bar of the browser, enter a URL that matches a trigger rule of the edge function to preview the effect of the sample code.

<img src="https://qcloudimg.tencent-cloud.cn/raw/0de7a6228c5e4d937154e201fb53fbd4.png" width=609px>

## References
- [Runtime APIs: TransformStream](https://www.tencentcloud.com/document/product/1145/52698)
- [Runtime APIs: Response](https://www.tencentcloud.com/document/product/1145/52691)