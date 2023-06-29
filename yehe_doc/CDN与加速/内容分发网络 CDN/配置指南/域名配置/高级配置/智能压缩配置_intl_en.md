
## Overview
With the aid of smart compression, Tencent Cloud CDN can compress the returned resources with Gzip or Brotli according to set rules, which effectively reduces the size of transferred content and costs.

> ! 
> - If your domain name is configured for global acceleration, the smart compression configuration will take effect globally. This configuration does not distinguish between requests from the Chinese mainland and from outside the Chinese mainland.
> - The file type (content-type) and Brotli compression are currently not available in regions outside the Chinese mainland.


## Directions
### Viewing the configuration
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Advanced Configuration** tab to find the **Smart Compression** section. This configuration is enabled by default.
- After an acceleration domain name is connected, resources with sizes ranging from 256 bytes to 2 MB with file extensions .js, .html, .css, .xml, .json, .shtml, and .htm will be compressed with Gzip by default.

![](https://main.qcloudimg.com/raw/db292e0fcc2a0d993b72117756c76b63.png)

### Modifying the configuration
Click **Modify** to modify the compression rules:
![](https://main.qcloudimg.com/raw/887c62b7a53f6193f061ffc14b372de2.png)

**Configuration limitations**
- **Type**: supports **All Files**, **File Extension**, and **File Content-Type**. It is set to **File Extension** by default.
- If **File Extension** is selected, the maximum content length is 200 characters.
- If **File Content-Type** is selected, the default content is as follows: `text/html, text/xml, text/plain, text/css, text/javascript, application/json, application/javascript, application/x-javascript, application/rss+xml, application/xmltext, image/svg+xml, image/tiff`. You can edit the content as needed. Note that you can enter up to 100 groups of content separated with semicolons (;). Each group can have up to 50 characters.
- Some platforms are being upgraded and do not support the file type (content-type) and Brotli compression.


>? 
> - The configuration can be modified when disabled, but will not be officially deployed until it is enabled.
> - If Gzip and Brotli are both selected, the compressed files will be returned according to the request compression header.
> - If Brotli is selected only and the request compression header does not support it, the original resources will be returned without being compressed.


