


## Configuration Overview

Tencent Cloud CDN uses the `Key-Value` format to map resources during caching, where `Key` is the cache key and a unique identifier of the cached resource. By configuring cache key rules, you can configure the Ignore Query String and Cache Ignore URL Case features for the content of different file types to optimize cache keys.



### Ignore Query String

- When a user accesses the resource through a URL, the access request may carry some parameters for special purposes. For example, the following URLs are used to represent two different images:
`http://cloud.tencent.com/1.jpg?version=1`
`http://cloud.tencent.com/1.jpg?version=2`
In this scenario, you need to disable Ignore Query String and use a complete URL as the cache key to cache images and distinguish between resources.

- If you use the timestamp signature parameter for access authentication in an audio/video scenario:
`http://cloud.tencent.com/1.mp4?sign=XXXXXX`
In this scenario, you need to enable Ignore Query String and use the URL part before "?" (i.e., `http://cloud.tencent.com/1.mp4`) as the cache key. The node will then only cache one resource, and the cache can be directly hit through signature authentication even if the timestamp signature keeps changing.

### Cache Ignore URL Case

If the letter case of resource URL paths is relevant to the resource content in your business, you can disable "Cache Ignore URL Case".
If the letter case of resource URL paths is irrelevant to the resource content in your business, you can enable "Cache Ignore URL Case" to improve the hit rate.
>!The platform is being upgraded and Cache Ignore URL Case cannot be enabled currently.

## Configuration Guide

### Viewing the configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Select the **Cache Configuration** tab to find the **Cache Key Rule Configuration** section.

When adding an acceleration domain name, the Ignore Query String is enabled or disabled by default based on different acceleration business types.

- If static acceleration is selected, the Ignore Query String is disabled by default. In the cache key configuration, the Ignore Query String of all file rules will be synced to **Not Filter**.
- If downloading or streaming VOD acceleration is selected, the Ignore Query String is enabled by default. In the cache key configuration, the Ignore Query String of all file rules will be synced to **Filter All**.


![](https://main.qcloudimg.com/raw/1f53ed863618b442233dd3e1bba6229b.png)

### Adding rules

You can add cache rules as needed.
<img src="https://main.qcloudimg.com/raw/48becf925518b2595097eddf7b4ec6d5.png" height="250" width="438" />

#### Configuration limitations

- Each domain name can be configured with up to 20 cache key rules (including the default ones).
- Rule priority can be adjusted: rules at the bottom of the list have higher priority (the priority of default rules cannot be adjusted).
- In each rule of specified file type, folder, and full-path file, up to 100 groups of contents can be entered. Please use ";" to separate different contents, e.g., "Specified file type - jpg;png".
- Ignore Query String - Reserve Specified Parameters.
  - All files: up to 6 parameter names can be entered; each one can contain up to 20 characters.
  - Specified file type/folder/full-path file: up to 5 parameter names can be entered; each one can contain up to 20 characters.
    Separate each parameter name with ";". For example: key1;key2;key3.

### Modifying rules

You can click **Modify** to modify the added cache key rules.

>!The default rules support modifying Ignore Query String and Cache Ignore URL Case configurations, while the type and content cannot be modified.

### Deleting rules

You can click **Delete** to delete the added cache key rules (except the default ones).


## Configuration Samples

If the cache key rule configuration of the acceleration domain name `www.test.com` is as follows:
![](https://main.qcloudimg.com/raw/8c3f7f534c5fa849ca1594a0a244d840.png)

Then the actual access will be as follows:

A client accessed the resources `www.test.com/abc.jpg?version=1&colour=red` and `www.test.com/abc.JPG?version=1&colour=red`, the two requests arrived at the CDN node X, on which the resources are not cached.

- The origin server will be pulled for the image `abc.jpg`, and the image will be cached on the CDN node X. As Ignore Query String is enabled and **Filter All** is selected, the URL part `www.test.com/abc.jpg` before "?" will be used as the cache key.
- The client accessed the resource `www.test.com/abc.JPG?version=1&colour=red`, and as the Cache Ignore URL Case is disabled, the cached resource `www.test.com/abc.jpg` will not be hit, the origin server will be pulled for the image `abc.JPG`, the image will be cached on the CDN node X, and `www.test.com/abc.JPG` will be used as the cache key.



