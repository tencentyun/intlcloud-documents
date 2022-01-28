### Can I modify the default QPS (queries per second) for text?

If you have such needs, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance with modification on the backend.

### Is QPS for the account dimension or `Biztype` dimension?

QPS is for each root account/sub-account. By default, it is 100 for images and 1,000 for text, and all `Biztype` values share the 1,000 QPS.

### Can I set the `Biztype` field of API 4.0 on my own?

Yes, but it will be generated on the backend only after you [submit a ticket](https://console.cloud.tencent.com/workorder/category). `Biztype` can contain 3–32 letters, digits, and underscores. Before configuring it, you need to inform the desired format, which cannot be changed after being configured.

### Will the `Review` field of API 4.0 be output for each tag?

It will be output for only tags with a score output by auto review but not for such tags as ad and QR code.