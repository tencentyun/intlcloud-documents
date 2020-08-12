<table>
    <tr>
        <th>Category</th> 
        <th>Specifications and Limits</th> 
    			<th>Description</th> 
   </tr>
    <tr>
        <td>QPS</td>
    			<td>Limits</td>
    			<td>Chinese Mainland: by default, a quota of 30,000 QPS is provided to each bucket in a public cloud region. For buckets in Hong Kong (China) or outside the Chinese mainland, a quota of 3,000 QPS is provided by default. For higher QPS, see <a href="https://intl.cloud.tencent.com/document/product/436/13653">Request Rate and Performance Optimization.</a> </td>
    </tr>
		    <tr>
        <td>Bandwidth</td>
    			<td>Limits</td>
    			<td>COS puts no limits on upload and download bandwidth. The upload and download speed depends on your local bandwidth and local disk IO.<td>
    </tr>
    	 <tr>
        <td rowspan="3">Storage class</td>
    			<td>STANDARD limits</td>
    			<td>Billing limits:<br>there is no limit imposed on storage duration or storage size.<br>For more information on COS STANDARD billing, see <a href="https://intl.cloud.tencent.com/document/product/436/6239">Product Pricing.</a></td>
    </tr>
    	 <tr>
        <td>STANDARD_IA limits</td>
    			<td>Billing limits:<br>a storage duration of less than 30 days is calculated based on 30 days.<br>A storage size of less than 64 KB is calculated based on 64 KB.<br>For more information on COS STANDARD_IA billing, see <a href="https://cloud.tencent.com/document/product/436/6239">Product Pricing</a></td>.
    </tr>
    	 <tr>
        <td>ARCHIVE limits</td>
    			<td>Billing limits:<br>a storage duration of less than 90 days is calculated based on 90 days.<br>A storage size of less than 64 KB is calculated based on 64 KB.<br>For more information on COS Archive Storage billing, see <a href="https://intl.cloud.tencent.com/document/product/436/6239">Product Pricing</a></td>.				
    </tr>
     <tr>
        <td rowspan="3">Bucket</td>
    			<td>Limits</td>
    			<td>1. Once a bucket is created, its name and region cannot be modified.<br>2. The name of each bucket under a given account is unique and cannot be changed.<br>3. Bucket names only support a sequence or combination of lowercase letters [a-z], numbers [0-9], and hyphens (-), with a total length of 1-50 characters.</td>
     </tr>
    	 <tr>
    			<td> Number of buckets</td>
    			<td>A maximum of 200 (default) buckets is allowed per root account</td>
    		</tr>
    			<td> Number of objects</td>
    			<td> For each bucket, there is no limit on the number of objects.</td>
    		<tr>
    			<td rowspan="4">Object</td>
    			<td>Limits</td>
					<td >An object key should be between 1 byte and 850 bytes. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/13324">Object Overview</a></td>
    		</tr>
    			<tr>
    			<td>Upload</td>
    			<td>1. The maximum size of an object to be uploaded via the console is 512 GB.<br>2. The maximum size of a single object to be uploaded via API/SDK is 48.82 TB (50,000 GB).<br>Upload API specifications:<br>&nbsp;&nbsp;a) Simple upload: 5 GB at most. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/14113">Simple Upload</a> <br>&nbsp;&nbsp;b) Multipart upload: 48.82 TB at most for a single object. The part size can range from 1 MB to 5 GB, and the size of the last part can be less than 1 MB. The number of parts can range from 1 to 10,000. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/14112">Multipart Upload</a></td>.
    		</tr>
    		<tr>
    			<td >Replication</td>
    			<td >1. You can perform intra-region or cross-region object replication with a Tencent Cloud account.<br>2. Intra-region object replication is free of charge while cross-region object replication incurs traffic fees. For more information, see traffic fees in <a href="https://intl.cloud.tencent.com/document/product/436/6239">Product Pricing.</a>  <br>3. Replication API specifications:<br>&nbsp;&nbsp;(a) Simple replication: 5 GB maximum for a single object. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/14117">Simple Copy</a><br>&nbsp;&nbsp;(b) Multipart replication is required for an object larger than 5 GB, allowing a maximum size of 48.82 TB for a single object. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/14118">Multipart Copy</a></td>
    		</tr>
    		<tr>
    			<td>Batch Deletion</td>
    			<td>Up to 1,000 objects can be deleted in a batch operation via API/SDK.</td>
    		</tr>
    		 <tr>
    			<td >Access policy</td>
    			<td >Number of polices</td>
    			<td >Each root account (APPID) can configure up to 1,000 bucket ACLs</td>
    		</tr>
    		<tr>
    			<td rowspan="3">Lifecycle</td>
    			<td>Number of rules</td>
    			<td >Each bucket can have up to 1,000 lifecycle rules</td>
    		</tr>
    		<tr>
    			<td >Storage Class Transition</td>
    			<td >STANDARD to STANDARD_IA: 1 day at least<br>STANDARD/STANDARD_IA to ARCHIVE: 1 day at least </td>
    		</tr>
    		 <tr>
    			<td >Expired Object Deletion</td>
    			<td >Expired object deletion for COS STANDARD/STANDARD_IA/ARCHIVE Storage: 1 day at least</td>
    		</tr>         
    		<tr>
    			<td colspan="2">SDK Types</td>
    			<td >12 types:<br>Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, Wechat Mini Program</td>
    </tr>
</table>