若 API 调用失败，则最终返回结果中的错误码 code 不为0，message 字段会显示详细错误信息。您可以根据 code 和 message 在 [错误码](https://intl.cloud.tencent.com/document/product/406/5903) 页面查询具体的错误信息。
错误返回示例如下：

```
{
    "code": "5100",
    "message": "(100004)projectId不正确",
}
```
