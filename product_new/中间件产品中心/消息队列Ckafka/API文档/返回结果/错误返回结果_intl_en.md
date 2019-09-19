> **This is a legacy API and may be deprecated in the future. It is currently not displayed on the left sidebar. We recommend using [CVM API v3.0], which is more standardized and has much lower access latency [API Category](https://intl.cloud.tencent.com/document/api/213/15689).**
>

If an API call fails, the `code` field in the final returned result will not be 0, and a detailed error message will be displayed in the `message` field. You can go to [Error Codes](https://intl.cloud.tencent.com/document/product/377/8946) and use `code` and `message` to check the error information.
Below is a sample of an error: 

```
{
    "code": "5100",
    "message": "(100004) incorrect projectId"
}
```

