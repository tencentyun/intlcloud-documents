## Feature Overview

ECDN can automatically detect static/dynamic content access requests based on the configured rules and intelligently choose the most appropriate acceleration scheme, satisfying your needs for accelerating access to sites with static/dynamic hybrid content at one stop.

- For static content requests, the edge servers are preferentially used to cache the content for response, improving access efficiency and reducing origin-pull traffic usage.
- For dynamic content requests, resources are directly pulled from the origin servers through high-quality caching and intelligent routing, reducing the average response latency.

## Feature Configuration Guide
1. Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Domain Management** on the left sidebar to enter the management page.
2. In the list, find the domain name to be configured and click **Manage** in the "Operation" column on the right to enter the domain management page.   
3. On the "Cache Configuration" page, manage configuration of content caching rules.   
   - Ignore Query String cache configuration:
     You can enable Ignore Query String cache to ignore parameters after "?" in the user request URL during caching. For example, when a node caches a resource whose URL is `http://www.example.com/1.jpg?version=1.1`, the corresponding `cache_key` will be `www.example.com/1.jpg`, and parameters after "?" will be ignored. When a user initiates a request, parameters after "?" will also be ignored. The system will use the `cache_key` whose value is `www.example.com/1.jpg` to search for the resource, which can be hit directly.
	![](https://main.qcloudimg.com/raw/99d0e9fe096ed15b1ec3ed42cfa7c1d3.png)
   - Content cache configuration:
   Click **Modify Caching Rule** to add a caching rule or modify an existing one and click **Save** for the rule to take effect.
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
			<td style="text-align: center">File Type</td>
			<td>Sets the caching time based on file extension</td>
			<td>.jpg; .png; .jsp</td>
			<td>1. The content is case-sensitive and must be a file extension starting with `.`.</br>2. Different file types should be separated with `;`.</td>
		</tr>
		<tr>
			<td style="text-align: center">Folder</td>
			<td>Sets the caching time based on folder</td>
			<td>/access; /pic</td>
			<td>1. The content is case-sensitive, and different paths should be separated with `;`.</br>2. It must be a folder starting with `/`.</br>3. It cannot end with `/`.</td>
		</tr>
		<tr>
			<td style="text-align: center">Full-path file</td>
			<td>Sets the caching time for a specified file</td>
			<td>/a.jpg; /b.png</td>
			<td>1. The content is case-sensitive, and files at different paths should be separated with `;`.</br>2. `*` can be used to match a type of files by regex, such as `/test/abc/*.jpg`.</br>3. It must be a folder starting with `/`.</td>
		</tr>
		<tr>
			<td style="text-align: center">Homepage</td>
			<td>Sets the caching time for the homepage</td>
			<td style="text-align: center">/</td>
			<td>The homepage content to be cached is "/" by default and does not need to be modified.</td>
		</tr>
	</tbody>
</table> 



### Cache purge time  

<strong>Cache purge time description</strong>  

- Cache purge time can be set by second, minute, hour, and day (up to 365 days).  
- If the cache purge time is 0, it indicates dynamic content, all requests will be directly passed through to the origin server, and the response content will not be cached.  
- If the cache purge time is greater than 0, it indicates static resource, and the edge caching feature will be enabled:
  - If the content accessed by the user has been cached on the edge server, and the cache has not expired, then the request does not need to be forwarded to the origin server, and the cached content will be directly returned, so that the user can enjoy nearby access to the content.
  - If the content accessed by the user has not been cached on the edge server, or the cache has expired, then the request needs to be forwarded to the origin server to get the content, which will be returned to the user and cached on the edge server.


<strong>Suggestions on setting cache purge time</strong>

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
			<td>Static content that needs to be frequently updated</td>
			<td>Files in formats such as .js and .css</td>
			<td>Set the caching time generally at the day or hour level based on the update frequency.</td>
		</tr>
		<tr>
			<td>Dynamic content that is frequently updated and shared by users</td>
			<td>Weather queries and region-specific portal content</td>
			<td>Set the caching time at the minute or second level.</td>		
		</tr>
		<tr>
			<td>Content that is dynamically generated or cannot be accessed twice by the same user</td>
			<td>User registration and login APIs</td>
			<td>Set the caching time to 0 to disable caching.</td>		
		</tr>
	</tbody>
</table> 



### Caching rule priority

If multiple caching policies are set, there may be overlapping rules, and a request may hit multiple rules. Therefore, there is priority order for caching rules.  

- The rule at the bottom of the configuration list has higher priority than that on the top, and a new caching rule has the highest priority by default.
- A user request will be matched with caching rules by rule priority from high to low. The first hit rule determines the cache purge time of the request.
- You can adjust the priority of rules.

Click **Edit Caching Rule**. You can <strong>drag the icon</strong> to adjust the rule priority.

![](https://main.qcloudimg.com/raw/67575a5f1c292ac2074f51fe17e032f7.png)

## Cache Inheritance

- When you configure edge caching for static content, the ECDN system will use the caching rules configured on the platform to process static user requests by default. The `Cache-Control` field in the response header from the origin server will not be inherited by the node for processing by default.
