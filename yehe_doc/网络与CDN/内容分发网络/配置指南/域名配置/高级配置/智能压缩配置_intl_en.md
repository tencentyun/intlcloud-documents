## Configuration Overview
With the aid of smart compression, Tencent Cloud CDN can compress the returned resources with Gzip or Brotli according to set rules, which effectively reduces the size of transferred content and costs.

> ! 
> - Smart compression currently is supported only for two service types: static acceleration and download acceleration.
> - If your domain name is configured for global acceleration, the smart compression configuration will take effect globally. This configuration does not distinguish between requests from the Chinese mainland and from outside the Chinese mainland.
> - Brotli compression is currently not supported in regions outside the Chinese mainland.


## Configuration Guide
### Viewing the configuration
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Advanced Configuration** tab to find the **Smart Compression** section. This configuration is enabled by default.
- After an acceleration domain name is connected, resources with sizes ranging from 256 bytes to 2 MB with file extensions .js, .html, .css, .xml, .json, .shtml, and .htm will be compressed with Gzip by default.

![](https://main.qcloudimg.com/raw/db292e0fcc2a0d993b72117756c76b63.png)

### Modifying the configuration
Click **Modify** to modify the compression rules:
![](https://main.qcloudimg.com/raw/887c62b7a53f6193f061ffc14b372de2.png)

**Configuration limitations**
- The file type allows up to 200 characters.
- The file size should be within 30 MB.
- Brotli compression is currently not supported on some platforms being upgraded.

>? 
> - The configuration can be modified when disabled, but will not be officially deployed until it is enabled.
> - If Gzip and Brotli are both selected, the compressed files will be returned according to the request compression header.
> - If only Brotli is selected and the request compression header does not support it, the original resources will be returned without being compressed.


