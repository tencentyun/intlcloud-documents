In this sample edge function, the [Fetch API](https://www.tencentcloud.com/document/product/1145/52687) is called to fetch a remote jQuery.js resource, and the [Cache API](https://www.tencentcloud.com/document/product/1145/52684) is called to cache the resource to an EdgeOne edge node. The cache duration is set to 10s.

## Sample Code 

```typescript
async function fetchJquery(event, request) {
  const cache = caches.default;
  // If the resource is not found in the cache, fetch the resource from the origin server and cache the resource.
  let response = await fetch(request);
  
  // Add the Cache-Control field to the response header and set the cache duration to 10s.
  response.headers.append('Cache-Control', 's-maxage=10');
  event.waitUntil(cache.put(request, response.clone()));
  
  // Add an identifier indicating that the resource is not found in the cache to the response header.
  response.headers.append('x-edgefunctions-cache', 'miss');
  return response;
}

async function handleEvent(event) {
  // The resource URL, which is also used as the cache key.
  const request = new Request('https://static.cloudcachetci.com/qcloud/main/scripts/release/common/vendors/jquery-3.2.1.min.js');
  // Obtain the default cache instance.
  const cache = caches.default;

  try {
    // Fetch the associated resource from the cache. If the resource is already cached, the API does not fetch the resource from the origin server, and a 504 error code is returned.
    let response = await cache.match(request);

    // If the resource is not found in the cache, re-fetch the remote resource.
    if (!response) {
      return fetchJquery(event, request);
    }

    // Add an identifier indicating that the resource is found in the cache to the response header.
    response.headers.append('x-edgefunctions-cache', 'hit');

    return response;
  } catch (e) {
    await cache.delete(request);
    // If the cache duration of the resource times out or another error occurs, re-fetch the remote resource.
    return fetchJquery(event, request);
  }
}

addEventListener('fetch', (event) => {
  event.respondWith(handleEvent(event));
});
```

## Sample Preview

In the address bar of the browser, enter a URL that matches a trigger rule of the edge function to preview the effect of the sample code.

- The resource is not found in the cache.

<img src="https://qcloudimg.tencent-cloud.cn/raw/45da06feda14ed3fc64a55959d9fff9e.png" width=609px>

- The resource is found in the cache.

<img src="https://qcloudimg.tencent-cloud.cn/raw/66b0ac34804739b86883612930354eb4.png" width=609px>


## References
- [Runtime APIs: Cache](https://www.tencentcloud.com/document/product/1145/52684)
- [Runtime APIs: Fetch](https://www.tencentcloud.com/document/product/1145/52687)
- [Runtime APIs: FetchEvent](https://www.tencentcloud.com/document/product/1145/52688)
- [Runtime APIs: Response](https://www.tencentcloud.com/document/product/1145/52691)
