In this example, an edge function is used to determine the region where a client resides and automatically redirect a request from the client to the target URL in the region. This example demonstrates how to use an edge function to route a request from a client based on the region where the client resides.

## Sample Code

```typescript
// The collection of URLs in all regions.
const urls = {
  CN: 'https://developer.mozilla.org/zh-CN/docs/Web/API',
  US: 'https://developer.mozilla.org/en-US/docs/Web/API',
};

// The default redirect URL.
const defaultUrl = 'https://developer.mozilla.org/en-US/docs/Web/API';

/**
 * Redirect to the target URL based on the region of the current request.
 * @param { Request } request
 */
function handleRequest(request) {
  // Obtain the region of the current request.
  const alpha2code = request.eo.geo.countryCodeAlpha2;
  // The target URL that you want to use for redirection.
  const url = urls[alpha2code] || defaultUrl;

  return new Response(null, {
    headers: {
      location: url
    },
    status: 302
  });
}

addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request));
});
```

## Sample Preview

In the address bar of the browser, enter a URL that matches a trigger rule of the edge function to preview the effect of the sample code.

<img src="https://qcloudimg.tencent-cloud.cn/raw/2dcaa1354be75d4abefeccdce47c281f.png" width=809px>

## References
- [Runtime APIs: Request](https://www.tencentcloud.com/document/product/1145/52690)
- [Runtime APIs: Response](https://www.tencentcloud.com/document/product/1145/52691)