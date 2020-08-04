If an API call fails, the `code` field in the final response will not be 0, and the `message` field will show a detailed error message. You can use `code` and `message` fields to check the error information on the [Error Codes](https://intl.cloud.tencent.com/document/product/214/11602) page.
Error response sample:

```
{
    "code": "5100",
    "message": "(100004) incorrect projectId"
}
```
