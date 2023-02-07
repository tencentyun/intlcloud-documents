The `Fetch` API is designed based on the standard Web API [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API). You can use `fetch` to initiate an async request to obtain remote resources during the runtime of an edge function.

## Overview 
```typescript
function fetch(request: string | Request, init?: RequestInit): Promise<Response>
```

### Parameters

<table>
  <thead>
    <tr>
      <th width="15%">Parameter</th>
      <th width="15%">Type</th>
      <th width="10%">Required</th>
      <th width="60%">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>request</td>
      <td>
        string | <br>
        <a href="https://www.tencentcloud.com/document/product/1145/52690">Request</a>
      </td>
      <td>Yes</td>
      <td>The requested resource.</li>
      </td>
    </tr>
    <tr>
      <td>init</td>
      <td><a href="https://www.tencentcloud.com/document/product/1145/52690#RequestInit">RequestInit</a></td>
      <td>No</td>
      <td>
        The initial configuration items of the request object. For more information, see <a href="https://www.tencentcloud.com/document/product/1145/52690#RequestInit">RequestInit</a>.
      </td>
    </tr>
  </tbody>
</table>

## CDN Back-to-origin
In Edge Functions, if you use `fetch(request)` to initiate a subrequest, Edge Functions directly initiates an HTTP request over the public network. However, If you use `fetch(event.request)` to initiate a request, the request is taken over by the CDN Server and the `EdgeOne CDN` configurations of the current domain name are applied. If the requested data does not exist in the CDN cache, data is pulled from the origin server.

>! In this version of the service, only requests that are initiated by using `fetch(event.request)` support `EdgeOne CDN` back-to-origin. `EdgeOne CDN` back-to-origin is not supported in the following scenarios:
>- Construct a Request object for `fetch(request)` to perform CDN back-to-origin.
>- Pass a second parameter (containing the initial configuration items of the request object) for `fetch(request)` to perform CDN back-to-origin.

Sample code

```typescript
addEventListener('fetch', async (event) => {
  // Initiate a request to perform EdgeOne CDN back-to-origin.
  const response = await fetch(event.request);
  event.respondWith(response);
});
```

## Redirect

`fetch` supports `3xx` redirect status codes. You can use a second parameter `init.redirect` to specify the redirect status code. For more information about redirect settings, see [RequestInit](https://www.tencentcloud.com/document/product/1145/52690#RequestInit).


- Redirect rules conform to the [Fetch Standard](https://fetch.spec.whatwg.org/#http-redirect-fetch). The follow rules vary based on the status code.

<table>
  <thead>
    <tr>
      <th width="30%">Status Code</th>
      <th width="70%">Redirect Rule</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>301, 302</td>
      <td>Replaces the <code>POST</code> method with the <code>GET</code> method.</td>
    </tr>
    <tr>
      <td>303</td>
      <td>Replaces all methods except for <code>HEAD</code> and <code>GET</code> with the <code>GET</code> method.</td>
    </tr>
    <tr>
      <td>307, 308</td>
      <td>Retains the original method.</td>
    </tr>
  </tbody>
</table>

>! The redirect address is obtained from the `Location` response header. The redirect action cannot be performed without this response header.
- The value of the `Location` response header can be an absolute URL or a relative URL. For more information, see [RFC-3986: URI Reference](https://www.rfc-editor.org/rfc/rfc3986#section-4.1).

## Runtime Limits
If you use `fetch` to initiate a request in an edge function, take note of the following limits:
- Number of times: Each time an edge function runs, `fetch` can be initiated for a maximum of 64 times. If the number of `fetch` requests exceeds the upper limit, the exceeding requests fail and exceptions are returned.
- Number of concurrencies: Each time an edge function runs, `fetch` can be initiated at a maximal concurrency of 8. If the number of concurrent `fetch` requests exceeds the upper limit, the exceeding requests will be delayed until a running `fetch` is resolved.

>! Each redirect is counted as a request and has a higher priority than a new `fetch` request that is initiated.

## Sample Code
```js
async function handleEvent(event) {
  const response = await fetch('https://www.tencentcloud.com/');
  return response;
}

addEventListener('fetch', (event) => {
  event.respondWith(handleEvent(event));
});
```

## References 
- [MDN documentation: Fetch](https://developer.mozilla.org/en-US/docs/Web/API/fetch)
- [Sample Functions: Obtaining Remote Resources and Responding to the Client](https://www.tencentcloud.com/document/product/1145/52704)
