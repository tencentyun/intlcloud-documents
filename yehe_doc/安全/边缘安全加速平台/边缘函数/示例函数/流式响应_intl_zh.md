该示例使用 [Fetch API](https://www.tencentcloud.com/document/product/1145/52687) 获取远程资源 jQuery.js 并流式响应给客户端。

## 示例代码

```typescript
async function handleRequest(request) {
  const response = await fetch('https://static.cloudcachetci.com/qcloud/main/scripts/release/common/vendors/jquery-3.2.1.min.js');

  if (response.status !== 200) {
    return response;
  }

  // 生成可读端与可写端
  const { readable, writable } = new TransformStream();
  // 流式响应客户端
  response.body.pipeTo(writable);

  return new Response(readable, response);
}

addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request));
});
```

## 示例预览

在浏览器地址栏中输入匹配到边缘函数触发规则的 URL，即可预览到示例效果。

<img src="https://qcloudimg.tencent-cloud.cn/raw/0de7a6228c5e4d937154e201fb53fbd4.png" width=609px>

## 相关参考
- [Runtime APIs: TransformStream](https://www.tencentcloud.com/document/product/1145/52698)
- [Runtime APIs: Response](https://www.tencentcloud.com/document/product/1145/52691)