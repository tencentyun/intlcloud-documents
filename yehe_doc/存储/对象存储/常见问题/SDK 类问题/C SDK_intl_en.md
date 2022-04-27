### How do I implement checkpoint restart with C SDK?

You can use the [advanced upload API of C SDK](https://intl.cloud.tencent.com/document/product/436/43553) to implement the checkpoint restart feature. To use checkpoint restart, you need to set the upload control parameter to **COS_TRUE**, for example, `clt_params = cos_create_resumable_clt_params_content(p, 0, 1, COS_TRUE, NULL)`.

### Why does the `HttpIOError` error occur when I use C SDK?

Error description: When you use the SDK, all APIs cannot be used or return `requestid`. By analyzing the captured packets, you find that no HTTP requests are sent successfully as shown in the following logs:
```
transport failure curl code:1 error:Unsupported protocol
status->code: -996
status->error_code: HttpIoError
status->error_msg: Unsupported protocol
status->req_id:
```

This error occurs because the HTTPS protocol is used, but the libcurl library doesn't support HTTPS. Therefore, the OpenSSL library is not used or the versions mismatch during libcurl compilation.
**Solution:** Check the running environment and reinstall the libcurl library (if you install it by compiling the source code, enable SSL) or update the OpenSSL library.
