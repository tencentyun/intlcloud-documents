## Feature Overview

ECDN can automatically detect static/dynamic content access requests based on the configured rules and intelligently choose the appropriate acceleration scheme, satisfying your needs for accelerating access to sites with hybrid static/dynamic content at one stop.

- For static content requests, the edge servers are preferentially used to cache the content for response, improving access efficiency and reducing origin-pull traffic.
- For dynamic content requests, high-quality resources are directly pulled from the origin servers through intelligent routing, reducing the average response latency.

## Feature Configuration Guide
1. Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Domain Management** on the left sidebar to enter the management page.
2. In the list, find the domain name to be configured and click **Manage** in the "Operation" column on the right to enter the domain name management page.   
3. On the "Cache Configuration" page, manage configuration of content cache rules.   
   - Ignore Query String cache configuration:
     You can enable Ignore Query String cache to ignore parameters after "?" in the user request URL during caching. For example, when a node is storing a resource whose URL is `http://www.example.com/1.jpg?version=1.1`, the corresponding `cache_key` will be `www.example.com/1.jpg`, and parameters after "?" will be ignored. When a user initiates a request, parameters  after "?" will also be ignored. The system will use the `cache_key` whose value is `www.example.com/1.jpg` to search for the resource, which can be hit directly.
	![](https://main.qcloudimg.com/raw/c8090cdfe705cab673e8b7ff6842691a.png)
   - Content cache configuration:
   Click **Modify Cache Rule** to add a cache rule or modify an existing rule and click **Save** for the rule to take effect.
     ![](https://main.qcloudimg.com/raw/49ab04c890048cf45b2c70ff42a5d74b.png)

### Cache rule types  

<table style="display:table" width="100%">
	<tbody>
		<tr>
			<th colspan="1" style="text-align: center" width="15%"> Cache Type </th>
			<th colspan="1" style="text-align: center" width="30%"> Description </th>
			<th colspan="1" style="text-align: center" width="10%"> Setting Example </th>
			<th width="45%">Precautions</th>
		</tr>
		<tr>
			<td style="text-align: center">File Type</td>
			<td>Sets the cache time based on the file extension</td>
			<td>.jpg; .png; .jsp</td>
			<td>1. The content is case-sensitive and must be a file extension starting with ".".</br>2. Different file types are separated with ";".</td>
		</tr>
		<tr>
			<td style="text-align: center">Folder</td>
			<td>Sets the cache time based on the folder</td>
			<td>/access; /pic</td>
			<td>1. The content is case-sensitive, and different paths are separated with ";".</br>2. It must be a folder starting with "/".</br>3. The content cannot be ended with "/".</td>
		</tr>
		<tr>
			<td style="text-align: center">Full-path file</td>
			<td>Sets the cache time for a specified file</td>
			<td>/a.jpg; /b.png</td>
			<td>1. The content is case-sensitive, and files with different paths are separated with ";".</br>2. "*" can be used to regex-match a type of files, e.g., "/test/abc/*.jpg".</td>
		</tr>
		<tr>
			<td style="text-align: center">Homepage</td>
			<td>Sets the cache time of the specified homepage</td>
			<td style="text-align: center">/</td>
			<td>The homepage content to be cached is "/" by default and does not need to be modified.</td>
		</tr>
	</tbody>
</table> 



### Purge cache time  

<strong>Purge cache time description</strong>  

- Purge cache time can be set by second, minute, hour, and day and can be set to up to 30 days.  
- If the purge cache time is 0, it indicates dynamic content. All requests will directly pass through the origin server, and the response content is not cached.  
- If the purge cache time is greater than 0, it indicates static resource, and the edge caching feature will be enabled:
  - When the content accessed by the user has been cached on the edge server, and the cache time does not expire, this request will not need origin-pull, and the cached content will directly be used for response, so that the user can have a nearby access to the content.
  - When the content accessed by the user has not been cached on the edge server, or the cache time expires, this request will need origin-pull to get the content for the user through a response and cache it on the node.
- When a domain name is connected, the purge cache time of all files is 0 second by default, indicating that the dynamic acceleration service is not used by default.

<strong>Purge cache time setting suggestion</strong>

<table style="display:table" width="100%">
	<tbody>
		<tr>
			<th colspan="1" style="text-align: center" width="40%"> File Type </th>
			<th colspan="1" style="text-align: center" width="30%"> Scenario Example </th>
			<th colspan="1" style="text-align: center" width="30%"> Recommended Cache Time </th>
		</tr>
		<tr>
			<td>Basically unchanged static content</td>
			<td>Image and audio/video files</td>
			<td>The purge cache time is set to 30 days.</td>
		</tr>
		<tr>
			<td>Static content that needs to be frequently updated</td>
			<td>Files in types such as .js and .css</td>
			<td>The cache time should be set based on the update frequency. Generally, it is set at a day or hour level.</td>
		</tr>
		<tr>
			<td>Dynamic content that is frequently updated and shared by users</td>
			<td>Weather query and region-specific portal content</td>
			<td>The cache time should be at a minute or second level.</td>		
		</tr>
		<tr>
			<td>Content that is dynamically generated or cannot be accessed twice by the same user without being updated</td>
			<td>User registration and login API</td>
			<td>The purge cache time should be set to 0 to disable caching.</td>		
		</tr>
	</tbody>
</table> 



### Cache rule priority

When multiple cache policies are set, there may be repeated rules, and a request may meet multiple rules. Therefore, there is priority for cache rules.  

- The rule at the bottom of the configuration list has higher priority than that on the top, and a new cache rule has the highest priority by default.
- User requests will be matched with rules by rule priority from high to low. The first hit cache rule determines the purge cache time of this request.
- You can adjust the priority of rules.

Click **Edit Cache Rule**. You can <strong>drag the icons</strong> to adjust the cache rule priority.

![](https://main.qcloudimg.com/raw/9bc37411df24d906571d394a2bb0ab84.png)

## Cache Inheritance Issues

- When you configure static content with edge caching, the ECDN system will use the cache rules configured on the platform to process user static requests by default. The `Cache-Control` field in the response header on the origin server is not inherited by the node for processing by default.
- If you want to set special cache rules for certain content on the origin server, you can set cache rules in the <strong>full-path file</strong> type.
