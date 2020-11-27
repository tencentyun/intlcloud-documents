<table>
    <tr>
        <th>Category</th> 
        <th>Specifications and Limits</th> 
    			<th>Description</th> 
   </tr>
    <tr>
        <td>QPS</td>
    			<td>Limits</td>
    			<td>1. READ/WRITE requests: by default, each bucket enjoys up to 30,000 QPS in public cloud regions in Chinese mainland, and up to 3,000 QPS in any other regions.
<br>2. LIST requests: by default, each bucket enjoys up to 1,200 QPS in any region.
<br>3. RETRIEVE requests: each bucket enjoys up to 100 QPS in any region.
<br>To increase your QPS limit, please see <a href="https://intl.cloud.tencent.com/document/product/436/13653">Request Rate and Performance Optimization</a>.</td>
    </tr>
		    <tr>
        <td>Bandwidth</td>
    			<td>Limits</td>
    			<td>By default, the bandwidth limit on each account is 15 Gbit/s in each public cloud region in Chinese mainland, and 10 Gbit/s in any other regions. If this threshold is exceeded, traffic throttling will be triggered for requests. To increase this limit, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</td>
    </tr>
    	 <tr>
        <td rowspan="5">Storage Class</td>
    			<td>STANDARD limits</td>
    			<td>Billing limits:<br>There is no limit imposed on storage duration or storage size.<br>For more information on COS STANDARD billing, please see <a href="https://buy.cloud.tencent.com/price/cos">Product Pricing</a>.</td>
    </tr>
    	 <tr>
        <td>STANDARD_IA limits</td>
    			<td>Billing limits:<br>An object stored less than 30 days is billed as 30 days.<br>An object less than 64 KB is billed as 64 KB.<br>For more information on COS STANDARD_IA billing, please see <a href="https://buy.cloud.tencent.com/price/cos">Product Pricing</a>.</td>
    </tr>
    	 <tr>
        <td>INTELLIGENT TIERING limits</td>
    			<td>Billing limits:<br>There is no limit imposed on storage duration or storage size.<br>For more information on COS INTELLIGENT TIERING billing, please see <a href="https://buy.cloud.tencent.com/price/cos">Product Pricing</a>.</td>
    </tr>
    	 <tr>
        <td>ARCHIVE limits</td>
    			<td>Billing limits:<br>An object stored less than 90 days is billed as 90 days.<br>An object less than 64 KB is billed as 64 KB.<br>For more information on COS ARCHIVE billing, please see <a href="https://buy.cloud.tencent.com/price/cos">Product Pricing</a>.</td>
    </tr>
    	 <tr>
        <td>DEEP ARCHIVE limits</td>
    			<td>Billing limits:<br>An object stored less than 180 days is billed as 180 days.<br>An object less than 64 KB is billed as 64 KB.<br>For more information on COS ARCHIVE billing, please see <a href="https://buy.cloud.tencent.com/price/cos">Product Pricing</a>.</td>
    </tr>
     <tr>
        <td rowspan="4">Bucket</td>
    			<td>Limits</td>
    			<td>1. Once a bucket is created, its name and region cannot be modified.<br>2. The name of each bucket under a given account is unique and cannot be changed.<br>3. A bucket name can only be lowercase letters [a-z], numbers [0-9], hyphens (-) or a combination thereof, and is up to 50 characters.</td>
     </tr>
    	 <tr>
    			<td> Number of buckets</td>
    			<td>A maximum of 200 (default) buckets is allowed per root account.</td>
    		</tr>
				<tr>
    			<td> Number of objects</td>
    			<td> For each bucket, there is no limit on the number of objects.</td>
    		</tr>
				<tr>
    			<td> Bucket tagging</td>
    			<td>Each bucket can have up to 50 different bucket tags.</td>
    		</tr>
    		<tr>
    			<td rowspan="5">Object</td>
    			<td>Limits</td>
					<td >An object key should be between 1-850 bytes. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/13324">Object Overview</a>.</td>
    		</tr>
    			<tr>
    			<td>Upload</td>
    			<td>1. The maximum size of an object to be uploaded via the console is 512 GB.<br>2. The maximum size of an object to be uploaded via APIs/SDKs is 48.82 TB (50,000 GB).<br>Upload API requirements:<br>&nbsp;&nbsp;(a) Simple upload: uploads a single object of up to 5 GB. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/14113">Simple upload</a>.<br>&nbsp;&nbsp;(b) Multipart upload: uploads a single object of up to 48.82 TB in a maximum of 10,000 parts. Each part should be 1 MB to 5 GB in size, except the last one that can be less than 1 MB. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/14112">Multipart Upload</a>.<br>3. Currently, objects can be uploaded into the INTELLIGENT TIERING storage class only if the INTELLIGENT TIERING configuration has been enabled on the bucket. How objects are moved between the access tiers depends on the configuration.</td>
    		</tr>
    		<tr>
    			<td >Replication</td>
    			<td >1. You can perform intra-region or cross-region object replication with a Tencent Cloud account.<br>2. The intra-region object replication is free of charge while the cross-region object replication incurs traffic charges. For more information, please see traffic fees in <a href="https://buy.cloud.tencent.com/price/cos">Product Pricing</a>.<br>3. Replication API requirements:<br>&nbsp;&nbsp;(a) Simple replication: replicates a single object of up to 5 GB. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/14117">Simple Replication</a>.<br>&nbsp;&nbsp;(b) Multipart replication must be used for an object larger than 5 GB and up to 48.82 TB. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/14118">Multipart Replication</a>.<br>4. Currently, objects cannot be replicated from STANDARD, STANDARD_IA or INTELLIGENT TIERING to INTELLIGENT TIERING.</td>
    		</tr>
    		<tr>
    			<td>Deleting multiple objects</td>
    			<td>Up to 1,000 objects can be deleted in a single request via APIs/SDKs.</td>
    		</tr>
				<tr>
    			<td>Object tagging</td>
    			<td>Each object can have up to 10 different tags.</td>	
    		</tr>
    		 <tr>
    			<td >Access policy</td>
    			<td >Number of ACLs</td>
    			<td >Each root account (APPID) can have up to 1,000 bucket ACLs.</td>
    		</tr>
    		<tr>
    			<td rowspan="3">Lifecycle</td>
    			<td>Number of rules</td>
    			<td >Each bucket can have up to 1,000 lifecycle rules.</td>
    		</tr>
    		<tr>
    			<td >Storage class transition</td>
    			<td >STANDARD to STANDARD_IA: 1 day after creation at least.<br>STANDARD/STANDARD_IA to ARCHIVE or DEEP ARCHIVE: 1 day after creation at least.</td>
    		</tr>
    		 <tr>
    			<td >Expired object deletion</td>
    			<td >STANDARD/STANDARD_IA/ARCHIVE: 1 day at least.</td>
    		</tr>         
    		<tr>
    			<td colspan="2">SDKs</td>
    			<td >12 SDKs:<br>Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, WeChat Mini Program.</td>
    </tr>
</table>
