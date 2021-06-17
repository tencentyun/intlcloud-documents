### 使用 C SDK 如何实现断点续传？

可以使用 [C SDK 高级上传](https://intl.cloud.tencent.com/document/product/436/31518) 接口实现断点续传功能。使用断点续传时，需设置上传控制参数为 **COS_TRUE**，例如：`clt_params = cos_create_resumable_clt_params_content(p, 0, 1, COS_TRUE, NULL)`。

