## Problems

- **Problem 1**: The same URL points to different files.
- **Problem 2**: After a file is updated, its old version is still accessed.

## Possible Causes

- The CDN cache has not expired.
- The browser cache is not disabled.
- The accessed file is hijacked, so the accessed file content is not as expected.

## Troubleshooting

### Check whether the CDN cache has expired

Check whether the CDN cache has expired as instructed in [Cache Configuration FAQs](https://intl.cloud.tencent.com/document/product/228/11203).
 - If so, [check whether the browser cache is disabled](#DisableCaching).
 - If not, purge CDN URLs or directories as instructed in [Purge Cache](https://intl.cloud.tencent.com/document/product/228/6299).

<span id="DisableCaching"></span>
### Check whether the browser cache is disabled

>? The following uses Chrome as an example.
>
1. Open Chrome.
2. Press **F12** to open the Developer tools.
3. Select the **Network** tab and check whether **Disable cache** is selected.
![](https://main.qcloudimg.com/raw/453ea5fdaa0d69be6f13fd809a815d22.png)
 - If so, [check whether the file is hijacked](#UseHTTPS).
 - If not, select **Disable cache** and restart the browser.

<span id="UseHTTPS"></span>
### Check whether the file is hijacked

If the file accessed is not as expected (for example, the `content-length` or response headers are not as expected), the file has been hijacked. In this case, we recommend you access it over HTTPS.


