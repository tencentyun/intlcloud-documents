You can set the cache validity period of resources on the origin server on CDN nodes in **Node Cache Validity** to adjust the cache update frequency of origin server resources on the CDN nodes. You can configure the resource cache validity period by directory, file extension, and full file path based on your business needs.

## Overview
CDN will determine whether a resource cached on a CDN node expires based on the cache validity period configured in **Node Cache Validity**.
- If the cache of a resource accessed by an end user doesn't expire on the CDN node, the node will directly return the cached resource to the user.
- If a resource accessed by an end user is not cached, or the resource cache has expired on the CDN node, the node will pull the latest resource from the origin server to cache it and return it to the user.

After a resource on the origin server is updated, its cache on the CDN node must be updated immediately. You can use the [cache purge](https://console.cloud.tencent.com/cdn/refresh) feature to update unexpired caches on the CDN node, so as to ensure that resources cached on the CDN node and stored on the origin server are consistent.

## Notes
- As the cache validity period affects the origin-pull frequency, we recommend you set the resource cache validity period based on your business needs. If it is too short, CDN will perform origin-pull frequently, thereby increasing the bandwidth usage of the origin server. If it is too long, caches on CDN nodes will be updated slowly, making end users unable to get the latest resources.
- CDN nodes cache resources based on the [CDN cache rule and priority](#m1). However, resources cached on a CDN node may be deleted from the node before the expiration time due to a low request frequency.
- We recommend you use different filenames before and after updating a resource on the origin server. For example, name resources with different content by version numbers `img-v1.jpg` and `img-v2.jpg`, to prevent CDN nodes from returning the old but unexpired resource to the end user after the resource content is changed on the origin server.
- If you still use the legacy version (in basic mode) of the node cache validity configuration, we recommend you submit the advanced mode configuration to upgrade the node cache validity configuration to the latest version so as to support more features. Note that after the upgrade to the advanced mode, you cannot restore to the basic mode. For more information on the legacy version of the node cache validity configuration, see [Node Caching Rule Configuration (Legacy)](https://intl.cloud.tencent.com/document/product/228/35317).
- The origin server can set the `Cache-Control` response header to control the cache validity period on CDN nodes (when **Cache Option** is **Follow Origin Server**). Then, CDN nodes will pass the `Cache-Control` header to the end user to control the browser cache validity period. If you want CDN nodes to set the browser cache validity period, you can modify the `Cache-Control` header returned by CDN nodes to the user in [Browser Cache Validity](https://intl.cloud.tencent.com/document/product/228/38932).


## Configuration Description
### Directions
1. Log in to the [CDN console](https://console.cloud.tencent.com/cdn).
2. Click **Domain Management** on the left sidebar to enter the domain name management list.
3. Select the target domain name and click **Manage** to enter the domain name configuration page.
4. Click **Cache Configuration** to switch to the **Cache Configuration** tab, and you can view the **Node Cache Validity**.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/cd08be49dbf25e88f28b32f019284231.png" width="850px">
<br>
5. Click **Add Rule** to enter the **Add Rule** page and add a node cache validity rule.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/a57bc131850fc1a49c69e2aa86d0050e.png" width="450px">
<br>
<table>
<thead>
<tr>
<th>Configuration Item</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Type</td>
<td>You can select <b>All Files</b>, <b>File Extension</b>, <b>File Directory</b>, <b>Full Path</b>, or <b>Homepage</b>.<br> All Files: Set the rule for all files. This is the default option.<br> File Extension: Set the rule for the specified file extension.<br> File Directory: Set the rule for the specified file directory.<br> Full Path: Set the rule for the specified full file path.<br> Homepage: Set the rule for the specified domain name root directory.</td>
</tr>
<tr>
<td>Content</td>
<td>Enter the content based on the selected file type.</br>If <b>Type</b> is <b>All Files</b>, the content is fixed to all files.</br>If <b>Type</b> is <b>File Extension</b>, you can enter one or multiple file extensions separated by ";", such as `jpg;png;css`.</br>If <b>Type</b> is <b>File Directory</b>, you can enter one or multiple file directories separated by ";", and the entered content cannot end with "/", such as `/test;/a/b/c`.</br>If <b>Type</b> is <b>Full Path</b>, you can enter one or multiple full file paths separated by ";", such as `/index.html;/test/.jpg`.</td>
</tr>
<tr>
<td>Cache Option</td>
<td>You can select <b>Follow Origin Server</b>, <b>Cache</b>, or <b>Do not cache</b>.<br> Follow Origin Server: The CDN node cache validity period will be set based on the `Cache-Control` origin server header, and heuristic caching can be enabled.<br>Cache: You can customize the CDN node cache validity period and enable force cache.<br>Do not cache: CDN nodes will not cache any resources.<br></td>
</tr>
</tbody></table>

[](id:m1)	
### CDN cache rule and priority
#### **Cache Option** is **Follow Origin Server**
<img src="https://qcloudimg.tencent-cloud.cn/raw/0d0086b11c0e9968707865af46a4c23d.jpg" width="850px">



The cache validity period will be set on CDN nodes based on the `Cache-Control` origin server response header.
- If the field in the `Cache-Control` origin server response header is `max-age`, the CDN node cache validity period will be set based on the value of `max-age`. For example, if `Cache-Control: max-age=300` is configured, the cache validity period will be 300 seconds.
	- If the field in the `Cache-Control` origin server response header is `no-cache`, `no-store`, or `private`, the CDN node will not cache resources.
	- If there is no `Cache-Control` or `Expires` origin server response header, the cache rule will be set based on the heuristic caching status:
		- If heuristic caching is disabled and there is no `Cache-Control` or `Expires` origin server response header, the cache validity period will be 600 seconds.
		- If heuristic caching is enabled and there is no `Cache-Control` or `Expires` origin server response header, the heuristic cache validity period will be set according to the following rules:
		 i. **Default Configuration**: If there is the `Last-Modified` origin server response header, the cache validity period will be calculated as follows: (current time - `Last-Modified`) \* 0.1. If there is no `Last-Modified` origin server response header, the cache validity period will be 600 seconds by default.
		 <br>
		 <img src="https://qcloudimg.tencent-cloud.cn/raw/80612ba1e40f345e14b188939cb7b557.png" width="450px">
		 <br>
		 ii. <b>Custom Policy</b>: You can customize the heuristic cache validity period.
		 <br>
		 <img src="https://qcloudimg.tencent-cloud.cn/raw/06629eb849a9e56ee0c16db1f8bfe3c6.png" width="450px">
		 <br>

#### **Cache Option** is **Cache**
<img src="https://qcloudimg.tencent-cloud.cn/raw/dc781cff77d79f57fa3c9df800e21a4d.jpg" width="850px">

You can customize the cache validity period on the CDN node.	
- If force cache is disabled:
	- If the field in the `Cache-Control` origin server response header is `max-age` or there is no `Cache-Control` header, resources will be cached according to the custom CDN node cache rule.
	- If the field in the `Cache-Control` origin server response header is `no-cache`, `no-store`, or `private`, CDN nodes will not cache resources.
	<br>
	<img src="https://qcloudimg.tencent-cloud.cn/raw/35f0cf1d08f6395e541ec9c1c5ae364b.png" width="450px">
	<br>
- If force cache is enabled: The `Cache-Control` origin server response header will be ignored, and resources will be cached according to the custom CDN node cache rule.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/fb2670449e6c40f5df4e8231c8f050b0.png" width="450px">
<br>

#### **Cache Option** is **Do not cache**
CDN nodes are configured to not to cache resources. For each user request to access a resource, CDN nodes will directly perform origin-pull to get the resource and return it to the user.
<img src="https://qcloudimg.tencent-cloud.cn/raw/621483c2535ca8e950e7a36c46c96983.png" width="450px">
<br>

#### Priority of multiple cache rules
If multiple cache rules are configured, the lower the rule position, **the higher the priority**. You can click **Adjust Priority** to drag and drop cache rules to change their order and adjust the priority.
<img src="https://qcloudimg.tencent-cloud.cn/raw/dcdbba45c63c0a18022fa73ecb76cb13.png" width="850px">	

### Recommended configuration
- For seldom updated static files, such as images and large files, we recommend you set the cache validity period to 30 days.
- For frequently updated static files, such as .js and .css files, we recommend you set the cache validity period based on the update frequency of your business.
- For dynamic files, such as .php, .jsp, .asp, and .aspx files, <b>you need to set Cache Option to Do not cache</b>.
- For other requests involving direct interaction with the origin server, such as **site login** (`/wp-admin` directory for WordPress backend login, for example) or **API-based query**, <b>you need to set Cache Option to Do not cache</b>; otherwise, an access error may occur.

	
### Configuration limitations
- You can add up to 100 cache rules for a domain name.
- If there are multiple cache rules, the lower the rule position, the higher the priority.
- If **Type** is set to **File Extension**, **File Directory**, or **Full Path**, you can enter up to 100 items and separate them by ";", such as `jpg;png` (when **Type** is set to **File Extension**).	
- If no rules are configured or the request fails to hit any configured rules, the cache validity period will be set on CDN nodes based on the `Cache-Control` origin server response header. If there is no `Cache-Control` header, CDN nodes will cache the resource for 600 seconds.
- CDN nodes only cache content requested by GET and HEAD requests. Content requested by POST and OPTIONS requests won't be cached on CDN nodes.


## Configuration Samples
### Sample 1
The original cache rules specify that CDN doesn't cache .php, .jsp, .asp, and .aspx files and caches other files for 30 days.
<img src="https://qcloudimg.tencent-cloud.cn/raw/5129af6e01dd139afcf5c44a7ba97ef3.png" width="850px">
<br>
You need to add a rule to cache .jpg and .png files for 10 days while ignoring the `Cache-Control` origin server response header (i.e., enabling force cache), and change **Cache Option** in the cache rule for **All Files** to **Follow Origin Server**.

1. Click **Add Rule**, set **Type** to **File Extension**, **Content** to `jpg;png`, **Cache Option** to **Cache**, **Cache Validity** to **10 days**, and **Force Cache** to **Yes**, and click **OK**.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/a1db0f8cbc470efa0b5749114ca8ea07.png" width="450px">
<br>
2. Select the cache rule for **All Files**, click **Modify**, change **Cache Option** to **Follow Origin Server**, and click **OK**.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/c0442f19e230b69456f59d1874d784a9.png" width="450px">
<br>
3. After the adjustment, the cache rules are:
	- .jpg and .png files will be cached for 10 days with force cache enabled.
	- .php, .jsp, .asp, and .aspx won't be cached.
	- Other files will be cached for 30 days.
	<br>
	<img src="https://qcloudimg.tencent-cloud.cn/raw/bfc24f2fca1ab9a184b0bf415c85a0f4.png" width="850px">
	<br>
	Below are actual caching results:
	-  The `www.test.com/abc.jpg` resource will be cached on the node for 10 days, even though the field in the `Cache-Control` origin server response header is `no-cache`, `no-store`, or `private`.
	-  The `www.test.com/def.php` resource won't be cached to the node.

	
### Sample 2
**Suggestions on configuring node cache validity rules for a site built based on WordPress:**
- For resources under the domain name `/wp-admin` directory for backend login, you need to set **Cache Option** to **Do not cache**; otherwise, backend login resources will be cached and login errors will occur. If there are any API resources, you also need to set **Cache Option** to **Do not cache** for them.
- For .php, .jsp, .asp, and .aspx dynamic files, you need to set **Cache Option** to **Do not cache** (default cache rule of CDN).
- As .html, .js, and .css files are updated frequently, you need to set the cache validity period based on the update frequency. We recommend you set the cache validity period to 7 days and disable force cache.
- Other files are cached for 30 days (default cache rule of CDN).

**Add cache rules while retaining the default CDN cache rules:**
1. Click **Add Rule**, set **Type** to **File Directory**, **Content** to `/wp-admin`, and **Cache Option** to **Do not cache**, and click **OK**.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/93a9e55ac5c35bbe1e955eda302f41f1.png" width="450px">
<br>
2. Click **Add Rule**, set **Type** to **File Extension**, **Content** to `html;js;css`, **Cache Option** to **Cache**, **Cache Validity** to **7 days**, and **Force Cache** to **No**, and click **OK**.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/1e0248cf175dd0158f73300d3bf7dc2f.png" width="450px">
<br>
3. As the lower the rule position, the higher the priority, click **Adjust Priority** and drag and drop the rule of not caching files in the `/wp-admin` directory to the bottom to grant it the highest priority.
<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/ba9b0809fc20a354ebadfbed4f19eee5.png" width="850px">
<br>
4. After the adjustment, the cache rules are:
	- All resources under the `/wp-admin` directory will not be cached.
	- .html, .js, and .css files will be cached for 7 days.
	- .php, .jsp, .asp, and .aspx won't be cached.
	- Other files will be cached for 30 days.
	<br>
	<img src="https://qcloudimg.tencent-cloud.cn/raw/da6e9921da144c97f7b80e569f2d8444.png" width="850px">
	<br>

## FAQs
- [If the file changes on the origin server, will the cache on CDN cache nodes be updated in real time?](https://intl.cloud.tencent.com/document/product/228/11203)
- [How do I tell whether user access has hit the CDN cache?](https://intl.cloud.tencent.com/document/product/228/11203)
