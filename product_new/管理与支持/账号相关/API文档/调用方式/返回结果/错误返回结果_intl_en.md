If an API call fails, the `code` field in the final returned result will be a value other than 0, and an error message will be displayed in the `message` field. You can reference `code` and `message` to see the error details of the error on [Error Codes](https://intl.cloud.tencent.com/document/product/378/34714).
Below is a sample of an error:

```
{
	"code": 5100,
	"message": "(100004) incorrect projectId"
}
```
