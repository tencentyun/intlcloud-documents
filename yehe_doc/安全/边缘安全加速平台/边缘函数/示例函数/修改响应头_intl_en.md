In this example, the [Fetch API](https://www.tencentcloud.com/document/product/1145/52687) is called to fetch a remote jQuery.js resource, and a response header is modified before the response is sent to a client.

## Sample Code

```typescript
async function handleRequest() {
  const response = await fetch('https://static.cloudcachetci.com/qcloud/main/scripts/release/common/vendors/jquery-3.2.1.min.js');

  // Add a custom response header.
  response.headers.append('x-edgefunctions-header', 'Hello world from edgefunction');

  // Delete specific response headers.
  response.headers.delete('x-cos-request-id');
  response.headers.delete('x-cos-hash-crc64ecma');

  // Modify a response header.
  response.headers.set('access-control-allow-methods', 'GET');

  return response;
}

addEventListener('fetch', event => {
    event.respondWith(handleRequest());
});
```

## Sample Preview

In the address bar of the browser, enter a URL that matches a trigger rule of the edge function to preview the effect of the sample code.
<img src="https://qcloudimg.tencent-cloud.cn/raw/a32764d7821feaca0325ca02c4f3981a.png" width=609px>

## References
- [Runtime APIs: Headers](https://www.tencentcloud.com/document/product/1145/52689)
- [Runtime APIs: Response](https://www.tencentcloud.com/document/product/1145/52691)