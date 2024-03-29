该示例通过计算 body 的 Sha-256 签名与源站生成的签名对比，若一致，则内容未被篡改，否则响应 416 状态码，表示内容被篡改。实现了，使用边缘函数校验源站响应内容是否被篡改。

>! 
>- 该示例要求与源站配合使用，即源站需要具备一致的签名算法与防篡改规则。
>- 现网使用该示例提供的防篡改规则，需要在计算签名时加 Salt，避免攻击者破解。

## 示例代码

```typescript
// 支持的文本文件类型
const textFileTypes = [
  'application/javascript',
  'text/html; charset=utf-8',
  'text/css; charset=utf-8',
  'text/xml; charset=utf-8'
];

// 支持的图片文件类型
const imageFileTypes = [
  'image/jpeg'
];

function uint8ArrayToHex(arr) {
  return Array.prototype.map
    .call(arr, (x) => (('0' + x.toString(16)).slice(-2)))
    .join('');
}

/**
 * 算法这里支持 MD5、SHA-1、SHA-256、SHA-384、SHA-512 之一, 大小写不敏感。
 * 需要注意：这里源站在计算签名时，不要直接对源文件的数据直接进行签名，而是应该加入混淆数据，避免外部攻击者破解。
 * 然后在此处，也使用同样的方式进行计算对比，从而达到防篡改的目的
 **/
async function checkAndResponse(response, hash, algorithm) {
  const headers = response.headers;

  let checkHash = 'sorry! not match';
  let data = null;
  const contentType = headers.get('Content-Type');
  if (textFileTypes.includes(contentType) || imageFileTypes.includes(contentType)) {
    data = await response.arrayBuffer();
  }
  let ret = await crypto.subtle.digest({name: algorithm}, data);
  checkHash = uint8ArrayToHex(new Uint8Array(ret));
  
  headers.append(`X-Content-${algorithm}-Check`, checkHash);
  // 实时计算签名与源站签名对比，校验不通过返回 416，语义为无法满足用户的请求
  if (checkHash !== hash) {
    return new Response(null, {
      headers,
      status: 416
    });
  }

  return new Response(data, {
    headers,
    status: 200
  });
}

async function handleEvent(event) {
  // 获取源站返回内容，若 EdgeOne 节点存在缓存，则不会回源
  const response = await fetch(event.request);
  if (response.status === 200) {
    const headers = response.headers;
    // 源站内容签名头
    const hash = headers.get('X-Content-Sha256');
    if (hash) {
      // 计算签名是否匹配，算法这里支持 MD5、SHA-1、SHA-256、SHA-384、SHA-512, 大小写不敏感。
      return checkAndResponse(response, hash, 'Sha-256');
    }
  }

  return response;
}

addEventListener('fetch', event => {
  event.respondWith(handleEvent(event));
});
```

## 示例预览

在浏览器地址栏中输入匹配到边缘函数触发规则的 URL，即可预览到示例效果。

- 边缘函数中计算签名与源站一致。

<img src="https://qcloudimg.tencent-cloud.cn/raw/18a0ee8b4cd2a2df1eb474b44c5dd54a.png" width=809px>

- 边缘函数中计算签名与源站不一致，返回状态码 416。

<img src="https://qcloudimg.tencent-cloud.cn/raw/e9d428b39cc0c0c63ff0050e74780f67.png" width=809px>

## 相关参考
- [Runtime APIs: Fetch](https://www.tencentcloud.com/document/product/1145/52687)
- [Runtime APIs: Web Crypto](https://www.tencentcloud.com/document/product/1145/52693)
- [Runtime APIs: Headers](https://www.tencentcloud.com/document/product/1145/52689)
- [Runtime APIs: Response](https://www.tencentcloud.com/document/product/1145/52691)
