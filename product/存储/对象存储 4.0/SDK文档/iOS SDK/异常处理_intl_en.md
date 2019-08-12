

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.
There are mainly three types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons, custom error codes returned by the SDK client at the network layer, and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes returned by the Tencent Cloud SDK client at the network layer are mainly for network exceptions, invalid certificates, and parameter verification failures as shown below:

| Error Code | Error Message | Error Description |
| ---- | ---- | ---- |
|10000| InvalidArgument| Invalid parameter |
|10001| InvalidCredentials| Invalid certificate |
|10004| UnsupportOperation| Unsupported operation |
|20001| InvalidArgument| The server returned invalid data |
|20004| PoorNetwork| Data integrity check failed |
|30000| UserCancelled| Canceled by user |
|30002| AlreadyFinished| Task already completed |
