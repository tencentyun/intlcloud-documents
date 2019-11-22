<table>
    <tr>
        <th>Category</th> 
        <th>Specifications and Limits</th> 
    			<th>Description</th> 
   </tr>
    <tr>
      <td>QPS</td>
    			<td>Limits</td>
      <td>1200 QPS per root account. For higher QPS, see <a href="https://intl.cloud.tencent.com/document/product/436/13653"> Request Rate and Performance Optimization</a></td>
    </tr>
    	 <tr>
      <td>Bandwidth</td>
      <td>Limit</td>
      <td>COS does not limit upload and download bandwidth, and the speed of the upload and download depends on your local bandwidth.</td>
   </tr>
   <tr>
        <td rowspan="3">Storage Class</td>
    			<td>COS Standard</td>
    			<td>Billing limits:<br>There is no limit imposed on the storage time and storage size.<br>For more information on COS standard billing, see <a href="https://intl.cloud.tencent.com/document/product/436/6239">Product Pricing</a></td>
    </tr>
    	 <tr>
        <td>COS Infrequent Access</td>
    			<td>Billing limits:<br>Storage time less than 30 days is calculated by 30 days.<br>Storage size less than 64 KB is calculated by 64 KB.<br>For more information on COS Infrequent Access billing, see <a href="https://intl.cloud.tencent.com/document/product/436/6239">Product Pricing</a></td>
    </tr>
    	 <tr>
        <td>Archive Storage</td>
    			<td>Billing limits:<br>Storage time less than 90 days is calculated by 90 days.<br>Storage size less than 64 KB is calculated by 64 KB.<br>For more information on Archive Storage billing, see <a href="https://intl.cloud.tencent.com/document/product/436/6239">Product Pricing</a></td>		
    </tr>
     <tr>
        <td rowspan="3">Bucket</td>
    			<td>Limits</td>
    			<td>1. When the bucket has been created, the name and region cannot be modified.<br>2. The names of all buckets under the same user account are unique and cannot be changed.<br>3. The name only supports lowercase letters, numbers [a-z, 0-9], dashes (-) and the combination of them with a length of 1-50 characters.</td>
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
					<td >Object key length should be between 1 byte and 850 bytes. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/13324">Object Overview</a></td>
    		</tr>
    			<tr>
    			<td>Upload</td>
    			<td>1. The maximum size of an object to be uploaded from the console is 512 GB.<br>2. The maximum size of a single object to be uploaded via API/SDK is 48.82 TB (50,000 GB).<br>Upload API specifications:<br>&nbsp;&nbsp;a) Simple upload: 5 GB at most, For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/14113">Simple Upload</a><br>&nbsp;&nbsp;b) Multipart upload: 48.82 TB maximum for a single object. The part size is 1 MB to 5GB. The size of the last part can be less than 1 MB, and the number of parts is 1 to 10,000, For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/14112">Multipart Upload</a></td>
    		</tr>
    		<tr>
    			<td >Copy</td>
    			<td >1. Regional/Cross-region object copy is supported.<br>2. Object copy in the same region is free of charge. Cross-region object copy incurs traffic charges. For more information, see Traffic Cost in <a href="https://intl.cloud.tencent.com/document/product/436/6239">Product Pricing</a>.<br>3. Copy API specifications:<br>&nbsp;&nbsp;a) Simple copy: 5 GB at most, For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/14117">Simple Copy</a><br>&nbsp;&nbsp;b) For size of more than 5 GB, multipart copy must be applied. The maximum size of an object to be copied is 48.82 TB, For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/14118">Multipart Copy</a></td>
    		</tr>
    		<tr>
    			<td>Batch Deletion</td>
    			<td>Up to 1,000 objects can be deleted in batch via API/SDK.</td>
    		</tr>
    		 <tr>
    			<td >Access Policy</td>
    			<td >Number of Rules</td>
    			<td >The sum of policies associated with the ACLs, Policies and CAMs of buckets and objects is limited to 1,000 per each root account (with the same APPID).</td>
    		</tr>
    		<tr>
    			<td rowspan="3">Lifecycle</td>
    			<td>Number of Rules</td>
    			<td >Up to 1,000 rules can be created for a bucket.</td>
    		</tr>
    		<tr>
    			<td >Storage class transition</td>
    			<td >COS Standard to COS Infrequent Access: 1 day at least<br>COS Standard/COS Infrequent Access to Archive Storage: 1 day at least </td>
    		</tr>
    		 <tr>
    			<td >Expired Object Deletion</td>
    			<td >Expired object deletion for COS Standard/COS Infrequent Access/Archive Storage: 1 day at least</td>
    		</tr>         
    		<tr>
    			<td colspan="2">SDK Type</td>
    			<td >12 types:<br>Andriod, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, Mini Program SDK</td>
    </tr>
</table>

