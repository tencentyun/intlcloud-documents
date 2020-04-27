## Configuration Scenario
With the aid of smart compression, Tencent Cloud CDN can compress the returned resources with Gzip or Brotli according to set rules, which effectively reduces the size of transferred content and costs.

>
> - When a new resource is requested for the first time, as the CDN node does not have it, the request will be forwarded to the origin server, and the uncompressed version of the resource will be returned (uncompressed on the origin server). In subsequent requests, the compressed version of the resource processed by the node will be returned.
> - Smart compression currently is supported only for two service types: static acceleration and download acceleration.

## Configuration Guide
### Viewing the configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click the domain name to enter its configuration page. You will find the smart compression configuration on the **Advanced Configuration** tab:
- After an acceleration domain name is connected, resources 256 bytes–2,048 KB in size with file extensions .js, .html, .css, .xml, .json, .shtml, and .htm will be compressed with Gzip by default.

![](https://main.qcloudimg.com/raw/db292e0fcc2a0d993b72117756c76b63.png)

### Modifying the configuration
You can click **Edit** on the right to specify the file extensions and size range of files to be compressed:
![](https://main.qcloudimg.com/raw/887c62b7a53f6193f061ffc14b372de2.png)
**Configuration description**

- Gzip can compress files 0–30 MB in size.
- Currently, compression with Brotli is being upgraded and cannot be enabled.

> If your domain name is configured for global acceleration, the smart compression configuration will take effect globally. This configuration does not distinguish between requests from Mainland China and from outside Mainland China.

