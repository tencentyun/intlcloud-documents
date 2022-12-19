<table>
    <tr>
        <th>Category</th> 
        <th>Specifications/Limits</th> 
    			<th>Description</th> 
   </tr>
    <tr>
        <td>QPS</td>
    			<td>Limits</td>
    			<td><ul  style="margin: 0;"><li>Read/Write requests: 30,000 for each bucket residing in a public cloud region in the Chinese mainland, and 3,000 for each bucket in other regions</li>
					<li> LIST requests: 1,000 QPS for all regions.</li>
					<li>Data retrieval requests: 100 QPS for all regions.</li>
					<li>Single-file upload/deletion/listing requests for traffic throttling: 50 QPS.</li>
					<li>Single-file download requests for traffic throttling: 1,000 QPS.
<br>To raise your QPS threshold, see <a href="https://intl.cloud.tencent.com/document/product/436/13653">Request Rate and Performance Optimization</a>.</li></ul></td>
    </tr>
		    <tr>
        <td>Bandwidth</td>
    			<td>Limits</td>
					<td>15 Gbps of upstream and downstream bandwidth for a single bucket residing in a public cloud region in the Chinese mainland, and 10 Gbps for any bucket in other regions. If this threshold is reached, requests will trigger traffic throttling. To raise the threshold, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</td>	
    </tr>
    	 <tr>
        <td rowspan="5">Storage class</td>
    			<td>MAZ_STANDARD/STANDARD limits</td>
    			<td>Billing limits: <br>There are no limits on storage duration or object size. <br>For STANDARD pricing, see <a href="https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=">Pricing | Cloud Object Storage</a>.</td>
    </tr>
    	 <tr>
        <td>MAZ_STANDARD_IA/STANDARD_IA limits</td>
    			<td>Billing limits: <ul  style="margin: 0;"><li>An object stored less than 30 days is billed as 30 days.</li>
					<li>An object smaller than 64 KB is billed as 64 KB. A larger object is billed based on its actual size. <br>For STANDARD_IA pricing, see <a href="https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=">Pricing | Cloud Object Storage</a>.</li></ul></td>
    </tr>
    	 <tr>
        <td>MAZ_INTELLIGENT TIERING/INTELLIGENT TIERING limits</td>
    			<td>Billing limits: <br>An object smaller than 64 KB is always stored in the frequent access tier. Objects are billed based on their actual sizes. <br>For INTELLIGENT TIERING pricing, see <a href="https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=">Pricing | Cloud Object Storage</a>.</td>
    </tr>
    	 <tr>
        <td>ARCHIVE limits</td>
    			<td>Billing limits: <ul  style="margin: 0;"><li>An object stored less than 90 days is billed as 90 days.</li>
					<li>An object smaller than 64 KB is billed as 64 KB. A larger object is billed based on its actual size. <br>For ARCHIVE pricing, see <a href="https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=">Pricing | Cloud Object Storage</a>.</li></ul></td>
    </tr>
    	 <tr>
        <td>DEEP ARCHIVE limits</td>
    			<td>Billing limits: <ul  style="margin: 0;"><li>An object stored less than 180 days is billed as 180 days.</li>
					<li>An object smaller than 64 KB is billed as 64 KB. A larger object is billed based on its actual size. <br>For DEEP ARCHIVE pricing, see <a href="https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=">Pricing | Cloud Object Storage</a>.</li></ul></td>
    </tr>
     <tr>
        <td rowspan="4">Bucket</td>
    			<td>Limits</td>
    			<td><ul  style="margin: 0;"><li>Once a bucket is created, you cannot modify its name or region.</li>
					<li>Names of buckets belonging to the same account must be unique and cannot be renamed.</li>
					<li> A bucket name cannot start with a hyphen and can contain only lowercase letters, digits, and hyphens. The length of a bucket name is limited by the number of characters in the region abbreviation as described in <a href="https://intl.cloud.tencent.com/document/product/436/6224">Regions and Access Endpoints</a> and `APPID`. A complete request domain name can contain up to 60 characters.</li></ul></td>
     </tr>
    	 <tr>
    			<td> Number of buckets</td>
    			<td>Each root account can have up to 200 (default) buckets.</td>
    		</tr>
				<tr>
    			<td> Number of objects</td>
    			<td> There is no limit on the number of objects stored in each bucket.</td>
    		</tr>
				<tr>
    			<td> Number of bucket tags</td>
    			<td>Each bucket can have up to 50 different bucket tags.</td>
    		</tr>
    		<tr>
    			<td rowspan="5">Object</td>
    			<td>Limits</td>
					<td >An object key can be 1 to 850 bytes. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/13324">Object Overview</a>.</td>
    		</tr>
    			<tr>
    			<td>Upload</td>
    			<td><ul  style="margin: 0;"><li>A single object to upload via the console can be up to 512 GB.</li>
					<li> A single object to upload via an API/SDK can be up to 48.82 TB (50,000 GB).
						<br>Limits on upload APIs:
						<ul  style="margin: 0;"><li>Simple upload: A single object can be up to 5 GB. For details, see <a href="https://intl.cloud.tencent.com/document/product/436/14113">Simple Upload</a>.</li>
						<li>Multipart upload: A single object can be up to 48.82 TB, and the part size should be 1 MB to 5 GB. The last part can be smaller than 1 MB. There can be 1 to 10,000 parts. For details, see <a href="https://intl.cloud.tencent.com/document/product/436/14112">Multipart Upload</a>.</li></ul>
					</li>
					<li>Currently, for a bucket with MAZ configuration enabled, objects can be uploaded to MAZ storage classes (MAZ_STANDARD or MAZ_STANDARD_IA). If intelligent tiering configuration is also enabled for the bucket, objects can also be uploaded to the MAZ_INTELLIGENT TIERING storage class.</li>
					<li>You can only upload objects to the INTELLIGENT TIERING storage class if you have enabled INTELLIGENT TIERING for the bucket. How objects are transitioned between tiers depends on the INTELLIGENT TIERING configurations.</li></ul></td>
    		</tr>
    		<tr>
    			<td >Replication</td>
    			<td ><ul  style="margin: 0;"><li>Objects belonging to the same account can be copied within and across buckets.</li>
					<li> Intra-region replication is free of charge, while cross-region replication incurs traffic fees. For more information, see <a href="https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=">Pricing | Cloud Object Storage</a>. </li>
					<li>Copy APIs limits:
						<ul  style="margin: 0;"><li>Simple copy: A single object to copy can be up to 5 GB. For details, see <a href="https://intl.cloud.tencent.com/document/product/436/14117">Simple Copy</a>.</li>
						<li>If an object is larger than 5 GB, you must use multipart copy. A single object to copy can be up to 48.82 TB. For details, see <a href="https://intl.cloud.tencent.com/document/product/436/14118">Multipart Copy</a>.</li></ul>
					</li>
					<li>Objects in MAZ buckets cannot be replicated to an OAZ bucket.</li>
					<li>Currently, you cannot copy STANDARD, STANDARD_IA, or INTELLIGENT TIERING objects to the INTELLIGENT TIERING storage class.</li></ul></td>
    		</tr>
    		<tr>
    			<td>Batch deletion</td>
    			<td>Up to 1,000 objects can be deleted in a single request via APIs/SDKs.</td>
    		</tr>
				<tr>
    			<td>Number of object tags</td>
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
    			<td >STANDARD to STANDARD_IA: At least 1 day.<br>STANDARD/STANDARD_IA to ARCHIVE/DEEP ARCHIVE: At least 1 day.<br>Note: <br>1. Objects in the MAZ_STANDARD or MAZ_STANDARD_IA storage class cannot be transitioned to the STANDARD, STANDARD_IA, or ARCHIVE storage class.<br>2. Objects smaller than 64 KB will not be transitioned.</td>
    		</tr>
    		 <tr>
    			<td >Expired object deletion</td>
    			<td >STANDARD/STANDARD_IA/ARCHIVE: At least 1 day.</td>
    		</tr>         
    		<tr>
    			<td colspan="2">SDKs</td>
    			<td >12 SDKs:<br>Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, WeChat Mini Program.</td>
    		</tr>        
    		<tr>
    			<td colspan="2">API reserved fields</td>
    			<td >All API fields involved in the API documentation are COS reserved fields, including: <br>acl, uploads, policy, cors, delete, versions, location, referer, lifecycle, versioning, notification, replication, website, logging, tagging, accelerate, domain, inventory, origin, object-lock, live, encryption, intelligenttiering, symlink.</br></td>
    		</tr>
</table>


