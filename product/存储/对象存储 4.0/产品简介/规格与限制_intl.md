<table>
    <tr>
        <th>Category</th> 
        <th>Specifications and Limits</th> 
    			<th>Detailed Description</th> 
   </tr>
    <tr>
        <td>QPS</td>
    			<td>Limit</td>
    			<td>1,200 QPS per account by default. For higher QPS, see <a href="/document/product/436/13653">Request Rate and Performance Optimization</a>. </td>
    </tr>
    	 <tr>
        <td rowspan="3">Types of Storage</td>
    			<td>COS Standard</td>
    			<td>Billing limits:<br>There is no limit imposed on the storage time and storage size.<br>For more information on COS standard billing, see <a href="https://cloud.tencent.com/document/product/436/6239">Billing</a></td>.
    </tr>
    	 <tr>
        <td>COS Infrequent Access</td>
    			<td>Billing limits:<br>Storage time less than 30 days is calculated by 30 days.<br>Storage size less than 64 KB is calculated by 64 KB.<br>For more information on COS Infrequent Access billing, see <a href="https://cloud.tencent.com/document/product/436/6239">Billing</a></td>.
    </tr>
    	 <tr>
        <td>Archive Storage</td>
    			<td>Billing limits:<br>Storage time less than 90 days is calculated by 90 days.<br>Storage size less than 48 KB is calculated by 48 KB.<br>For more information on Archive Storage billing, see <a href="https://cloud.tencent.com/document/product/436/6239">Billing</a></td>.				
    </tr>
     <tr>
        <td rowspan="3">Bucket</td>
    			<td>Limit</td>
    			<td>1. When the bucket has been created, the name and region cannot be modified.<br>2. The names of all buckets under the same user account are unique and cannot be changed.<br>3. The name only supports lowercase letters, numbers [a-z, 0-9], dashes (-) and the combination of them with a length of 1-40 characters.</td>
     </tr>
    	 <tr>
    			<td>Number of buckets</td>
    			<td>Up to 200 buckets per account (default)</td>
    		</tr>
    			<td>Number of objects</td>
    			<td>For each bucket, the number of objects is not limited.</td>
    		<tr>
    			<td rowspan="4">Object</td>
    			<td>Limit</td>
					<td >Object key length should be between 1 byte and 850 bytes. For more information, see <a href="https://cloud.tencent.com/document/product/436/13324">Object Overview</a></td>.
    		</tr>
    			<tr>
    			<td>Upload</td>
    			<td>1. The maximum size of an object to be uploaded from the console is 512 GB.<br>2. The maximum size of an object to be uploaded via API/SDK is 48.82 TB (50,000 GB)<br>Upload API specifications:<br>&nbsp;&nbsp;a) Simple upload: 5 GB at most. For more information, see <a href="https://cloud.tencent.com/document/product/436/14113">Simple Upload</a>.<br>&nbsp;&nbsp;b) Multipart upload: 48.82 TB at most. The part size is 1 MB to 5 GB. The size of the last part can be less than 1 MB, and the number of parts is 1 to 10,000. For more information, see <a href="https://cloud.tencent.com/document/product/436/14112">Multipart Upload</a></td>.
    		</tr>
    		<tr>
    			<td >Copy</td>
    			<td >1. Regional/Cross-region object copy is supported.<br>2. Object copy in the same region is free of charge. Cross-region object copy incurs traffic charges. For more information, see Traffic Fee in <a href="https://cloud.tencent.com/document/product/436/6239">Billing</a>.<br>3. Copy API specifications:<br>&nbsp;&nbsp;a) Simple copy: 5 GB at most. For more information, see <a href="https://cloud.tencent.com/document/product/436/14117">Simple Copy.</a><br>&nbsp;&nbsp;b) For size of more than 5 GB, multipart copy must be applied. The maximum size of an object to be copied is 48.82 TB. For more information, see <a href="https://cloud.tencent.com/document/product/436/14118">Multipart Copy</a></td>.
    		</tr>
    		<tr>
    			<td>Batch deletion</td>
    			<td>Up to 1,000 objects can be deleted in batch via API/SDK.</td>
    		</tr>
    		 <tr>
    			<td >Access policy</td>
    			<td >Number of rules</td>
    			<td >The sum of the number of object and bucket ACLs and the number of bucket policies is limited to 1,000 per account.</td>
    		</tr>
    		<tr>
    			<td rowspan="3">Lifecycle</td>
    			<td>Number of rules</td>
    			<td >Up to 1,000 rules can be created for a bucket.</td>
    		</tr>
    		<tr>
    			<td >Storage class transition</td>
    			<td >COS Standard to COS Infrequent Access: 1 day at least<br>COS Standard/COS Infrequent Access to Archive Storage: 1 day at least</td>
    		</tr>
    		 <tr>
    			<td >Expired object deletion</td>
    			<td >Expired object deletion for COS Standard/COS Infrequent Access/Archive Storage: 1 day at least</td>
    		</tr>         
    		<tr>
    			<td colspan="2">SDK language</td>
    			<td >10 languages: <br>Andriod/C/C++/Go/iOS/Java/JavaScript/Node.js/PHP/Python</td>
    </tr>
</table>

