In this example, cookies are used to store session information and perform A/B testing on requests. This example demonstrates how to use an edge function to perform A/B testing.

## Sample Code

```typescript
// The name of the cookie.
const cookieName = 'ABTest';
// The values of the cookie.
const valueA = 'value-a';
const valueB = 'value-b';
// The paths of the webpage.
const pathA = '/path-a';
const pathB = '/path-b';

async function handleRequest(request) {
  const urlInfo = new URL(request.url);

  // If path A or path B is specified in the request, return the content in path A or path B.
  if (urlInfo.pathname.startsWith(pathA) || urlInfo.pathname.startsWith(pathB)) {
      return fetch(request);
  }

  // Obtain the cookie of the current request.
  const cookies = request.getCookies();
  const cookie = cookies.get(cookieName);
  const cookieValue = cookie && cookie.value;

  // If the value of the cookie is valueA, return the content in path A.
  if (cookieValue === valueA) {
      urlInfo.pathname = pathA + urlInfo.pathname;
      return fetch(urlInfo.toString());
  }
  
  // If the value of the cookie is valueB, return the content in path B.
  if (cookieValue === valueB) {
      urlInfo.pathname = pathB + urlInfo.pathname;
      return fetch(urlInfo.toString());
  }

  // Randomly route the current request to path A or B.
  const testValue = Math.random() < 0.5 ? valueA : valueB;
  const path = testValue === valueA ? pathA : pathB;
  urlInfo.pathname = path + urlInfo.pathname;

  const response = await fetch(urlInfo.toString());

  cookies.set(cookieName, testValue, { path: '/' });

  response.setCookies(cookies);
  return response;
}

addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request));
});
```

## Sample Preview

In the address bar of the browser, enter a URL that matches a trigger rule of the edge function to preview the effect of the sample code.

<img src="https://qcloudimg.tencent-cloud.cn/raw/87dc9103e8079d15571118e7da72a78d.png" width=809px>

## References
- [Runtime APIs: Cookies](https://www.tencentcloud.com/document/product/1145/52685)
- [Runtime APIs: Response](https://www.tencentcloud.com/document/product/1145/52691)
