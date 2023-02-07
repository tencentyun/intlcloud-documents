In this example, the [Fetch API](https://www.tencentcloud.com/document/product/1145/52687) is called to fetch a remote jQuery.js resource and send the resource to a client in response to a request from the client.

## Sample Code

```typescript
async function handleRequest(request) {
  // Fetch a remote resource.
  const response = await fetch('https://static.cloudcachetci.com/qcloud/main/scripts/release/common/vendors/jquery-3.2.1.min.js');
  return response;
}

addEventListener('fetch', event => {
    return event.respondWith(handleRequest(event.request));
});
```

## Sample Preview

In the address bar of the browser, enter a URL that matches a trigger rule of the edge function to preview the effect of the sample code.

<img src="https://qcloudimg.tencent-cloud.cn/raw/52b7c14d70e81ac27ca8a55e651e9599.png" width=609px>

## References
- [Runtime APIs: Fetch](https://www.tencentcloud.com/document/product/1145/52687)