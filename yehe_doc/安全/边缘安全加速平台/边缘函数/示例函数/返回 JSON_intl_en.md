In this example, an edge function is used to generate a JSON object, and the JSON object is accessed and previewed from a browser.

## Sample Code

```typescript
const data = {
  content: 'hello world',
};

async function handleRequest(request) {
  // Convert the JSON object to the String format.
  const result = JSON.stringify(data, null, 2);

  return new Response(result, {
    headers: {
      'content-type': 'application/json; charset=UTF-8',
    },
  });
}

addEventListener('fetch', event => {
  return event.respondWith(handleRequest(event.request));
});
```

## Sample Preview

In the address bar of the browser, enter a URL that matches a trigger rule of the edge function to preview the effect of the sample code.
<img src="https://qcloudimg.tencent-cloud.cn/raw/100dee7845fcef3db6a2300eac803846.png" width=609px>

## References
- [Runtime APIs: addEventListener](https://www.tencentcloud.com/document/product/1145/52683)
- [Runtime APIs: Response](https://www.tencentcloud.com/document/product/1145/52691)