### What is COS origin-pull?

When the data you want to access is not stored in COS, you can use COS’s origin-pull feature to pull data from a specified origin server (e.g., a local IDC, or the origin server/bucket of other cloud vendors).

Origin-pull is mainly used for hot data migration, redirection for specified requests, and other scenarios. You can configure it as needed. For detailed directions, please see [Setting Origin-Pull](https://intl.cloud.tencent.com/document/product/436/31508).

After an origin-pull rule is set, if the requested object does not exist in the bucket, the object can be found from the configured origin server address using the origin-pull rule and returned to the user. Likewise, when you need to redirect specific requests, the origin-pull rule can be used for COS to access data in the origin server.

### How can the client know whether a COS request pulls from an origin server?

If the origin-pull is asynchronous, after origin-pull is configured, 302 will be returned for the first COS request, and the client’s second request will be forwarded to the origin server. If the origin-pull is synchronous, COS will pull data from the origin server in real time and return it to the client, and also dump the data to the server.

### How will I be notified after the offline origin-pull upload succeeds?

SLA of the offline origin-pull module is not always successful. If you want to know whether the origin-pull upload is successful, you can go to the SCF console to set a callback that is triggered by the offline origin-pull. For more information about SCF’s COS triggers, please see [COS Trigger](https://intl.cloud.tencent.com/document/product/583/9707).

### What is an origin-pull address for?

An origin-pull address is usually an IP or a domain name. It specifies where the data you need to pull is stored. When COS does not have the resource you want to access, you can use the origin-pull address to pull the resource in real time.

### After origin-pull is configured, if COS does not have the resource/path corresponding to the origin-pull address, will COS upload the resource and create a path after the user’s initial access?

Yes. COS will pull the resource automatically and create a path.

