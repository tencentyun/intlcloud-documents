If an API call fails, the `code` field in the final returned result will not be 0, and a detailed error message will be displayed in the `message` field. You can go to [Error Codes](https://intl.cloud.tencent.com/document/product/406/5903) and use `code` and `message` to check the error information.
Below is a sample error:

```
{
    "code": "5100",
    "message": "(100004) incorrect projectId",
}
```
