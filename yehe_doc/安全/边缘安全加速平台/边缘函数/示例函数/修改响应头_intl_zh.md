该示例使用 [Fetch API](https://www.tencentcloud.com/document/product/1145/52687) 获取远程资源 jQuery.js，并修改响应头，返回客户端。

## 示例代码

```typescript
async function handleRequest() {
  const response = await fetch('https://static.cloudcachetci.com/qcloud/main/scripts/release/common/vendors/jquery-3.2.1.min.js');

  // 添加自定义响应头
  response.headers.append('x-edgefunctions-header', 'Hello world from edgefunction');

  // 删除响应头
  response.headers.delete('x-cos-request-id');
  response.headers.delete('x-cos-hash-crc64ecma');

  // 修改请求头
  response.headers.set('access-control-allow-methods', 'GET');

  return response;
}

addEventListener('fetch', event => {
    event.respondWith(handleRequest());
});
```

## 示例预览

在浏览器地址栏中输入匹配到边缘函数触发规则的 URL，即可预览到示例效果。
<img src="https://qcloudimg.tencent-cloud.cn/raw/a32764d7821feaca0325ca02c4f3981a.png" width=609px>

## 相关参考
- [Runtime APIs: Headers](https://www.tencentcloud.com/document/product/1145/52689)
- [Runtime APIs: Response](https://www.tencentcloud.com/document/product/1145/52691)