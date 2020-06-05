<table>
    <tr>
        <th>Category</th> 
        <th>Specifications and Limits</th> 
    			<th>Description</th> 
   </tr>
    <tr>
        <td>QPS</td>
    			<td>Limits</td>
    			<td>Mainland China: by default, a quota of 30,000 QPS is provided to each bucket in public cloud regions, and 3,000 QPS to each bucket in finance cloud regions. For buckets in regions of Hong Kong (China) and outside Mainland China, a quota of 3,000 QPS is provided by default.  For higher QPS, see <a href="https://intl.cloud.tencent.com/document/product/436/13653">Request Rate and Performance Optimization.</a> </td>
    </tr>
		    <tr>
        <td>Bandwidth</td>
    			<td>Limits</td>
    			<td>COS puts no limits on the upload and download bandwidth. The upload and download speed depends on your local bandwidth.<td>
    </tr>
    	 <tr>
        <td rowspan="4">COS Storage Class</td>
    			<td nowrap="nowrap">MAZ_STANDARD Limits</td>
    			<td>Billing limits:<br>there is no limit imposed on the storage duration.<br>Storage size less than 128 KB is calculated by 128 KB.<br>For more information on COS MAZ_STANDARD billing, see <a href="https://intl.cloud.tencent.com/document/product/436/6239">Product Pricing.</a></td>
    </tr>
    	 <tr>
    			<td>STANDARD Limits</td>
    			<td>Billing limits:<br>there is no limit imposed on the storage duration or storage size.<br>For more information on COS STANDARD billing, see <a href="https://intl.cloud.tencent.com/document/product/436/6239">Product Pricing.</a></td>
    </tr>
    	 <tr>
        <td>STANDARD_IA Limits</td>
    			<td>Billing limits:<br>storage duration shorter than 30 days is calculated by 30 days.<br>Storage size less than 64 KB is calculated by 64 KB.<br>For more information on COS STANDARD_IA billing, see <a href="https://intl.cloud.tencent.com/document/product/436/6239">Product Pricing</a></td>.
    </tr>
    	 <tr>
        <td>ARCHIVE Limits</td>
    			<td>Billing limits:<br>storage duration shorter than 90 days is calculated by 90 days.<br>Storage size less than 64 KB is calculated by 64 KB.<br>For more information on COS Archive Storage billing, see <a href="https://intl.cloud.tencent.com/document/product/436/6239">Product Pricing</a></td>.				
    </tr>
     <tr>
        <td rowspan="3">Bucket</td>
    			<td>Limits</td>
    			<td>1. Once a bucket is created, its name and region cannot be modified.<br>2. The name of each bucket in a user account is unique and cannot be changed.<br>3. The name only supports lowercase letters, numbers [a-z, 0-9], hyphens (-) and the combination of them with a length of 1-50 characters.</td>
     </tr>
    	 <tr>
    			<td> Number of buckets</td>
    			<td>A maximum of 200 (default) buckets per root account</td>
    		</tr>
    			<td> Number of objects</td>
    			<td> For each bucket, the number of objects is not limited.</td>
    		<tr>
    			<td rowspan="4">Object</td>
    			<td>Limits</td>
					<td >An object key should be between 1 byte and 850 bytes. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/13324">Object Overview</a></td>
    		</tr>
    			<tr>
    			<td>Upload</td>
    			<td>1. The maximum size of an object to be uploaded from the console is 512 GB.<br>2. The maximum size of a single object to be uploaded via API/SDK is 48.82 TB (50,000 GB).<br>Upload API specifications:<br>&nbsp;&nbsp;a) Simple upload: 5 GB maximum for a single object. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/14113">Simple upload</a> <br>&nbsp;&nbsp;b) Multipart upload: 48.82 TB maximum for a single object. The part size is 1 MB to 5 GB. The size of the last part can be less than 1 MB, and the number of parts is 1 to 10,000. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/14112">Multipart Upload</a><br>3. Currently, objects stored into MAZ_STANDARD Class can be uploaded only to buckets with MAZ configuration enabled.</td>
    		</tr>
    		<tr>
    			<td >Replication</td>
    			<td >1. You can perform intra-region or cross-region object replication with a Tencent Cloud account.<br>2. The intra-region object replication is free of charge while the cross-region object replication incurs traffic charges. For more information, see traffic fees in <a href="https://intl.cloud.tencent.com/document/product/436/6239">Product Pricing.</a>   <br>3. Replication API specifications:<br>&nbsp;&nbsp;(a) Simple replication: 5 GB maximum for a single object. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/14117">Simple Replication</a><br>&nbsp;&nbsp;(b) Multipart replication is required for an object larger than 5 GB, allowing a maximum size of 48.82 TB for a single object. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/14118">Multipart Replication</a><br>4. Currently, objects stored in MAZ_STANDARD class can be replicated only into the same class.</td>
    		</tr>
    		<tr>
    			<td>Batch Deletion</td>
    			<td>Up to 1,000 objects can be deleted in batch via API/SDK.</td>
    		</tr>
    		 <tr>
    			<td >Access Policy</td>
    			<td >Number of Rules</td>
    			<td >Each root account (APPID) can have up to 1,000 bucket ACL rules.</td>
    		</tr>
    		<tr>
    			<td rowspan="3">Lifecycle</td>
    			<td>Number of Rules</td>
    			<td >Up to 1,000 rules can be created for a bucket.</td>
    		</tr>
    		<tr>
    			<td >Storage Class Transition</td>
    			<td >STANDARD to STANDARD_IA: 1 day at least<br>STANDARD/STANDARD_IA to ARCHIVE: 1 day at least<br>Note that currently, MAZ_STANDARD does not allow you to transition objects to STANDARD_IA and ARCHIVE.</td>
    		</tr>
    		 <tr>
    			<td >Expired Object Deletion</td>
    			<td >Expired object deletion for COS STANDARD/STANDARD_IA/ARCHIVE Storage: 1 day at least</td>
    		</tr>         
    		<tr>
    			<td colspan="2">SDK Types</td>
    			<td >12 types:<br>Andriod, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, Wechat Mini Program</td>
    </tr>
</table>
