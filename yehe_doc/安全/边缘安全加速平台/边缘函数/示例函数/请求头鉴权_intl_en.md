This example demonstrates how to use an edge function to perform simple permission control by verifying the value of the `x-custom-token` request header. If the value is token-123456, access is allowed. Otherwise, access is denied.

## Sample Code

```typescript
async function handleRequest(request) {
  const token = request.headers.get('x-custom-token');

  if (token === 'token-123456') {
    return new Response('hello world');
  }

  // Incorrect key supplied. Reject the request.
  return new Response('Sorry, you have supplied an invalid token.', {
    status: 403,
  });
}

addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request));
});
```

## Sample Preview

In the address bar of the browser, enter a URL that matches a trigger rule of the edge function to preview the effect of the sample code.

- If authentication fails, access is denied.<br><img src="https://qcloudimg.tencent-cloud.cn/raw/a25e988334af3145c7be185030b98970.png" width=609px>
- If authentication is successful, access is allowed.<br><img src="https://qcloudimg.tencent-cloud.cn/raw/c73ae6ae3e6fd3efcf91a05f32c37aa9.png" width=609px>


## References
- [Runtime APIs: Headers](https://www.tencentcloud.com/document/product/1145/52689)
- [Runtime APIs: Response](https://www.tencentcloud.com/document/product/1145/52691)