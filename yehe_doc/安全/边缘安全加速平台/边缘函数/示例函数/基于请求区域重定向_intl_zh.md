该示例通过判断客户端所属区域，自动重定向到所属区域的目标网址。实现了，使用边缘函数，根据客户端所属区域，分发请求。

## 示例代码

```typescript
// 所有区域网址集
const urls = {
  CN: 'https://developer.mozilla.org/zh-CN/docs/Web/API',
  US: 'https://developer.mozilla.org/en-US/docs/Web/API',
};

// 默认重定向网址
const defaultUrl = 'https://developer.mozilla.org/en-US/docs/Web/API';

/**
 * 根据当前请求所在的区域，重定向到目标网址
 * @param { Request } request
 */
function handleRequest(request) {
  // 获取当前请求所在区域
  const alpha2code = request.eo.geo.countryCodeAlpha2;
  // 重定向目标网址
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

## 示例预览

在浏览器地址栏中输入匹配到边缘函数触发规则的 URL，即可预览到示例效果。

<img src="https://qcloudimg.tencent-cloud.cn/raw/2dcaa1354be75d4abefeccdce47c281f.png" width=809px>

## 相关参考
- [Runtime APIs: Request](https://www.tencentcloud.com/document/product/1145/52690)
- [Runtime APIs: Response](https://www.tencentcloud.com/document/product/1145/52691)