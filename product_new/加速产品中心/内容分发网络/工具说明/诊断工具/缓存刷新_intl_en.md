Cache purge includes URL purge, directory purge, and URL prefetch. URL purge purges the cache on a file-by-file basis. Directory purge purges all the files under a directory. URL prefetch prefetches resources on a file-by-file basis.
Purge vs. prefetch:
- Once a resource is purged, its cache on all the CDN nodes across the entire network will be deleted. When a user requests arrives at a node, the node will pull the corresponding resource from the origin server, return it to the user, and cache it to the node so as to ensure that the user can obtain the latest resource.
- When a resource is prefetched, it will be cached in advance to all the CDN nodes across the entire network. When a user request arrives at a node, the resource can be directly obtained on the node.

After you update a resource on the origin server, if you want the user to access the updated resource directly, you can use the **URL purge** or **directory purge** feature. If you want CDN to proactively cache the resource from the origin server to the CDN nodes, you can use the **URL prefetch** feature.
> The update mechanism for resources cached on the CDN nodes is generally controlled by cache expiration time. Configuring a reasonable cache expiration time policy can effectively reduce origin-pull rate. For more information, see [Cache Expiration Configuration](https://intl.cloud.tencent.com/doc/product/228/6290).

## URL Purge
> + A maximum of 10,000 URLs can be purged each day, and a maximum of 1,000 URLs can be submitted for each purge task. It takes about 5 minutes for purges to take effect.
> + Because it takes about 5 minutes for URL purges to take effect, if the cache validity period set for a file is less than 5 minutes, we recommend waiting for updates after timeout instead of using the purge tool.
> + Purges only support URLs that contain English characters. If a URL contains any non-English characters, it should be escaped first before submitting it for purging. 

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), click **Purge Cache** on the left sidebar to enter the cache purge page, and select **Purge URL**.
![](https://main.qcloudimg.com/raw/5e86a9b882255155dbdfcbb8afbe2eff.jpg)
Enter the object URL to be purged in the text box. Prefixes such as "http://" or "https://" must be included and only enter one entry per row. For example:
<blockquote style="background-color:#F5F5F5">http://www.abc.com/test.html<br/>
http://www.def.com/image.png</blockquote>

Click **Submit and Purge**. After submission, you can view the remaining available URL purges for today in the bottom-left corner of the page.

## Directory Purge
> + A maximum of 100 directories can be purged each day, and a maximum of 20 URL directories can be submitted for each purge task. It takes about 5 minutes for purges to take effect.
> + Because it takes about 5 minutes for directory purges to take effect, if the cache validity period set for a file is less than 5 minutes, we recommend waiting for updates after timeout instead of using the purge tool.

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), click **Purge Cache** on the left sidebar to enter the cache purge page, and select **Purge Directory**. Purge Directory offers two ways of purging:

+ Purge updated resources: Purge only modified resources by checking against the Last-Modify time.
+ Purge all resources: Purge all resources. Please note that this will delete all resources in the directory on all the CDN nodes across the entire network, leading to more origin-pulls and increasing pressure on the origin server. 

![](https://main.qcloudimg.com/raw/f132ce7a7b23a8d1e1d4019a8aee8f12.jpg)
Enter the directory URL to be purged. Prefixes such as "http://" or "https://" must be included and only enter one entry per row. For example:
<blockquote style="background-color:#F5F5F5">http://www.abc.com/test/<br/>
http://www.def.com/image/</blockquote>

Then, click **Submit and Purge**. After the task is submitted, you can view the remaining available directory purges for today in the bottom-left corner of the page.

## URL Prefetch
> + URL prefetch currently only available for whitelisted CDN accounts.
> + If the CDN nodes already have cached resources that has not expired, the resources will not be updated to the latest version. If you need to update the resource on all nodes to the latest version, you can purge it before prefetch.
> + A maximum of 1,000 URLs can be prefetched each day, and a maximum of 20 URLs can be submitted for each prefetch task. It takes about 5 to 30 minutes for the prefetch to take effect, depending on the file size;

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), click **Purge Cache** on the left sidebar to enter the cache purge page, and select **Prefetch URL**.

![](https://main.qcloudimg.com/raw/8f537c3ca716fb315bb350b976ccdfe9.jpg)



Enter the object URL to be prefetched. Prefixes such as "http://" or "https://" must be included and only enter one entry per row. For example:
<blockquote style="background-color:#F5F5F5">http://www.abc.com/test.html<br/>
http://www.def.com/image.png</blockquote>

Then, click **Submit and Prefetch**. After the task is submitted, you can view the remaining available URL prefetches for today in the bottom-left corner of the page.

## Records
You can view the record of URL purges, directory purges, and URL prefetches for a specified period of time.
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), go to the **Purge Cache** page, and select **History**. Select a **date** and **query type**, enter a **URL or domain name**, and click **Query**. The records will be displayed in the table below:

![](https://main.qcloudimg.com/raw/23e7bbf27b30f84ca275810866cecf77.jpg)
