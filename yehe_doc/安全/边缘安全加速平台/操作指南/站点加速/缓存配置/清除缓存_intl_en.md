## Overview
Cache purge is to clear resources cached on nodes. After purge, when a user accesses a resource, the latest resource will be obtained through origin-pull for response.
>!After cache purge, as there is no cache of the resource on nodes, the resource can be obtained only through origin-pull, and the number of origin-pull requests will increase for a short period, which will compromise the acceleration effect. If many cached resources are purged, a large number of origin-pull requests will be generated, bringing pressure on the origin server.

## Use Cases
#### New resource release
When a resource is updated on the business origin server, you need to purge the old resource cached on nodes to prevent users from getting the old resource. After the cache is purged in the entire network, users can get the latest resource.

#### Non-compliant resource clearing
If there are non-compliant resources at your business site, you need to clear them and rectify your site promptly. As such resources may still be cached on nodes, you need to purge them from nodes.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Site Acceleration** > **Cache configuration** on the left sidebar.
2. On the cache configuration page, select the target site and click **Purge cache** in the cache purge module.
![](https://qcloudimg.tencent-cloud.cn/raw/4488d444245ae27e789b8e62e1d56e37.png)
3. In the pop-up window, enter the target resource content and click **Clear**.
<table>
<thead>
<tr>
<th width="15%">Supported Type</th>
<th width="85%">Details</th>
</tr>
</thead>
<tbody><tr>
<td>URL</td>
<td>The URL(s) matched by the resource cached on the node, for example, <code>https://www.example.com/path/foo.jpg</code>.</td>
</tr>
<tr>
<td>Prefix</td>
<td>The prefix path matched by the resource cached on the node, for example, <code>https://www.example.com/path</code>.</td>
</tr>
<tr>
<td>Hostname</td>
<td>The hostname(s) matched by the resource cached on the node, for example, <code>www.example.com</code>.<br>Note: You cannot submit URLs in the format of <code>http://*.test.com/</code>, i.e., domain names cannot contain <code>*</code>. You need to specify the corresponding subdomain names.</td>
</tr>
<tr>
<td>Cache-Tag</td>
<td>Cache purge with matched tag(s) of the <code>Cache-Tag</code> response header in the HTTP response packet, for example, <code>Cache-Tag: tag1,tag2,tag3</code>.<ul><li>It applies only to the Enterprise plan.</li><li> EdgeOne can identify the <code>Cache-Tag</code> response header of the origin server. You need to add tag(s) to the header.<ul><li>A header can be up to 6 KB in size.</li><li> Separate tags by comma. A tag can contain up to 128 characters. There can be up to 1,000 tags.</li><li>Tags are case-insensitive, which means `Tag1` and `tag1` are the same.</li></td>
</tr>
<tr>
<td>Cache all</td>
<td>All cached resources of the site on nodes.<br>Note: If a wildcard domain name under the current site (example.com) such as <code>*.foo.example.com</code> is connected, this option cannot take effect, and you need to submit the cache purge task for each subdomain name separately.</td>
</tr>
</tbody></table>

4. Click **View history** to view the history in a specified time period and of a specified purge type.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fIQc461_QQ20221116-121021.png)

## Notes
### Content specifications
Check whether the submitted content meets the following specifications:
- Do not submit the content of a site that is disabled, locked, or not connected to the current account.
- If you submit tasks by file upload, make sure that the file is in .txt format and doesn't exceed 10 MB in size.
- If the content contains non-ASCII characters, toggle **URL-encoding** on to convert the encoding.
 - The encoding rules must comply with RFC 3986.
 - Spaces must be encoded to `%20` no matter where they are.
 - If encoding conversion is involved, only resources matched after encoding conversion will be purged.

### Submission limit
- Different plans have different quotas. For billing details, see [Billing Overview](https://www.tencentcloud.com/document/product/1145/48705).
- If you select file upload as the URL submission method, there is no limit on the number of URLs that can be submitted each time, but the number of submitted URLs will be deducted from the daily quota.
