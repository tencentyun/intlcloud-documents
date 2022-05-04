## Symptoms

- **Symptom 1**: A single URL points to different files.
- **Symptom 2**: After I updated a file, I still accessed the old version of it.

## Possible Causes

- The Content Delivery Network (CDN) cache has not expired.
- The browser did not disable cache.
- The accessed file is hijacked. As a result, the accessed file content is not as expected.

## Troubleshooting Procedure

### Check whether the CDN cache has expired

Check whether the CDN cache has expired by referring to [How do I tell whether user access has hit the CDN cache](https://intl.cloud.tencent.com/document/product/228/11207).
 - If yes, [check whether your browser has disable cache](#DisableCaching).
 - If not, purge CDN URLs or directories by referring to [Purge Cache](https://intl.cloud.tencent.com/document/product/228/6299).

<span id="DisableCaching"></span>
### Check whether your browser has disabled cache

>? The following uses Chrome as an example.
>
1. Open Chrome.
2. Press F12 to open the Developer Tools.
3. Select the **Network** tab and check whether **Disable cache** is selected.
![](https://main.qcloudimg.com/raw/453ea5fdaa0d69be6f13fd809a815d22.png)
 - If yes, [check whether the file is hijacked](#UseHTTPS).
 - If not, select **Disable cache** and restart your browser.

<span id="UseHTTPS"></span>
### Check whether the file is hijacked

If the file accessed is not as expected (for example, the `content-length` or response headers are not as expected), your file has been hijacked. In this case, you are advised to access it over HTTPS.




