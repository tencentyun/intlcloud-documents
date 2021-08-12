## Features

ECDN can automatically identify static and dynamic content access requests based on the configured rules and intelligently apply an appropriate acceleration scheme, satisfying your needs for accelerating access to sites with static, dynamic or hybrid content at one stop.

- For static content requests, the edge servers are preferentially used to cache the content for response, improving access efficiency and reducing origin-pull traffic usage.
- For dynamic content requests, resources are directly pulled from the origin servers through high-quality origin-pull and intelligent routing, lowering the average response latency.

>? If your application has been migrated to the CDN console, you can go to the console for operation by referring to [Content Delivery Network](https://cloud.tencent.com/document/product/228).
## Directions
1. Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Domain Management** on the left sidebar to enter the management page.
2. In the list, find the domain name to configure and click **Manage** under the "Operation" column on the right to enter the domain management page.   
3. On the "Cache Configuration" page, you can configure the content caching rules.   
   - Ignore Query String cache configuration:
     You can enable Ignore Query String cache to ignore parameters after "?" in a user request URL during caching. Suppose that content of the URL `http://www.example.com/1.jpg?version=1.1` is cached on nodes. When a user request comes in the cache, the cache_key `www.example.com/1.jpg` will be looked up to return a direct hit.
	![](https://main.qcloudimg.com/raw/99d0e9fe096ed15b1ec3ed42cfa7c1d3.png)
   - Content cache configuration:
   Click **Edit Cache Rule** to add a caching rule or modify an existing one and click **Save** for the rule to take effect.
     ![](https://main.qcloudimg.com/raw/2afa0aff85361ff74fe25912fe232328.png)

### Caching rule types  

<table style="display:table" width="100%">
	<tbody>
		<tr>
			<th colspan="1" style="text-align: center" width="15%"> Cache Type </th>
			<th colspan="1" style="text-align: center" width="30%"> Description </th>
			<th colspan="1" style="text-align: center" width="10%"> Example </th>
			<th width="45%">Remarks</th>
		</tr>
		<tr>
			<td style="text-align: center">File type</td>
			<td>Sets the caching time based on file extension</td>
			<td>.jpg;.png;.jsp</td>
			<td>1. The content is case-sensitive and must be a file extension starting with <code>.</code>.</br>2. Different file extensions should be separated with <code>;</code>.</td>
		</tr>
		<tr>
			<td style="text-align: center">Folder</td>
			<td>Sets the caching time based on folder</td>
			<td>/access;/pic</td>
			<td>1. The content is case-sensitive, and different paths should be separated with <code>;</code>.</br>2. It must be a folder starting with <code>/</code>.</br>3. It cannot end with <code>/</code>.</td>
		</tr>
		<tr>
			<td style="text-align: center">Full-path file</td>
			<td>Sets the caching time for a specified file</td>
			<td>/a.jpg;/b.png</td>
			<td>1. The content is case-sensitive, and files at different paths should be separated with <code>;</code>.</br>2. <code>*</code> can be used to match a type of files by regex, such as <code>/test/abc/*.jpg</code>.</br>3. It must be a folder starting with <code>/</code>.</td>
		</tr>
		<tr>
			<td style="text-align: center">Homepage</td>
			<td>Sets the caching time for the homepage</td>
			<td style="text-align: center">/</td>
			<td>The homepage content to cache is <code>/</code> by default and does not need to be modified.</td>
		</tr>
	</tbody>
</table> 



### Cache purge time  

<strong>Description</strong>  

- Cache purge time can be set by second, minute, hour, and day (up to 365 days).  
- If the cache purge time is 0, requests from the dynamic content will be directly passed through to the origin server, and the response content will not be cached.  
- If the cache purge time is greater than 0, requests come from the static content, and the edge caching feature will be enabled:
  - If the content accessed by the user has been cached on the edge server and the cache has not expired, the cached content can be directly accessed without making a request to the origin server.
  - If the content accessed by the user has not been cached on the edge server or the cache has expired, the content will be accessed after making a request to the origin server, and then will be cached on the edge server.


<strong>Suggested setting</strong>

<table style="display:table" width="100%">
	<tbody>
		<tr>
			<th colspan="1" style="text-align: center" width="40%"> File Type </th>
			<th colspan="1" style="text-align: center" width="30%"> Scenario Example </th>
			<th colspan="1" style="text-align: center" width="30%"> Recommended Caching Time </th>
		</tr>
		<tr>
			<td>Basically unchanged static content</td>
			<td>Images and audio/video files</td>
			<td>Set the cache purge time to 30 days.</td>
		</tr>
		<tr>
			<td>Static content that needs updates</td>
			<td>Files in formats such as .js and .css</td>
			<td>Set the caching time of days or hours based on the update frequency.</td>
		</tr>
		<tr>
			<td>Dynamic content that is frequently updated and shared by users</td>
			<td>Weather queries and region-specific content</td>
			<td>Set the caching time of minutes or seconds.</td>		
		</tr>
		<tr>
			<td>Content that is dynamically generated or cannot be accessed repeatedly by the same user</td>
			<td>User registration and login APIs</td>
			<td>Set the caching time to 0 to disable caching.</td>		
		</tr>
	</tbody>
</table> 



### Caching rule priority

You may get more than one hit result at the same time due to overlaps between caching rules you defined. Given this possibility, the setting of caching rule priority is included.  

- Rules at the bottom of the configuration list take priority over those on the top. A new caching rule takes the highest priority.
- A user request will be matched with caching rules by rule priority from high to low. The first hit rule determines the cache purge time of the request.
- You can adjust the priority of rules as needed.

Click **Edit Cache Rule**. You can <strong>drag the icon</strong> to change the rule priority.

![](https://main.qcloudimg.com/raw/67575a5f1c292ac2074f51fe17e032f7.png)

## Cache Inheritance

If you configure edge caching for static content, the ECDN system will handle static requests with the caching rules configured. ECDN nodes will not inherit and process the `Cache-Control` field in the response header from the origin server by default, and will not cache the content if this field is `private`, `no-store` or `no-cache`.
