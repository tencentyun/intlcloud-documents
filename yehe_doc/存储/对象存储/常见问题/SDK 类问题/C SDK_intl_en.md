### How do I implement checkpoint restart with C SDK?

You can use the [advanced upload API of C SDK](https://intl.cloud.tencent.com/document/product/436/31518#uploading-an-object-(checkpoint-restart)) to implement the checkpoint restart feature. To use checkpoint restart, you need to set the upload control parameter to **COS_TRUE**, for example, `clt_params = cos_create_resumable_clt_params_content(p, 0, 1, COS_TRUE, NULL)`.

