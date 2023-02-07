In this example, cookies are used to count the number of access requests. When a browser accesses the Edge Functions service, the number of access requests is increased by 1.

## Sample Code

```typescript
async function handleRequest(request) {
  // Obtain the number of cookies for the current request. 
  const cookies = request.getCookies();
  const cookieCount = cookies.get('count');
  // Increase the number by 1.
  const count = Number(cookieCount && cookieCount.value || 0) + 1;
  // Update the number of cookies.
  cookies.set('count', String(count));

  const response = new Response(`The count is: ${count}`);
  // Configure the response cookies.
  response.setCookies(cookies);
  return response;
}
  
addEventListener('fetch', (event) => {
  event.respondWith(handleRequest(event.request));
});
```

## Sample Preview

In the address bar of the browser, enter a URL that matches a trigger rule of the edge function to preview the effect of the sample code.

<img src="https://qcloudimg.tencent-cloud.cn/raw/410eba1391e680c2b7fb108bbfe5a5bd.png" width=709px>

## References
- [Runtime APIs: Cookies](https://www.tencentcloud.com/document/product/1145/52685)
- [Runtime APIs: Response](https://www.tencentcloud.com/document/product/1145/52691)
- [Runtime APIs: Request](https://www.tencentcloud.com/document/product/1145/52690)