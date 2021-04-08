### Namespace APIs
<table>
<thead>
<tr>
<th align="left"  style="width:39%">APIs and Description</th>
<th align="left" style="width:1%">Resource<br>Type</th>
<th align="left" style="width:58%">Six-segment Example of Resource</th>
</tr>
</thead>
<tbody><tr>
<td align="left">CreateNamespacePersonal<br>Creating a namespace of Personal Edition</td>
<td align="left">repo</td>
<td align="left"><code>qcs::tcr:$region:$account:repo/$namespace</code></td>
</tr>
<tr>
<td align="left">DeleteNamespacePersonal<br>Deleting a namespace of Personal Edition</td>
<td align="left">repo</td>
<td align="left"><code>qcs::tcr:$region:$account:repo/$namespace</code></td>
</tr>
</tbody></table>

### Image Repository APIs
<table>
<thead>
<tr>
<th align="left" style="width:49%">APIs and Description</th>
<th align="left" style="width:1%">Resource<br>Type</th>
<th align="left" style="width:49%">Six-segment Example of Resource</th>
</tr>
</thead>
<tbody><tr>
<td align="left">DescribeRepositoryOwnerPersonal<br>Querying all repositories of Personal Edition</td>
<td align="left">repo</td>
<td align="left"><code>qcs::tcr:$region:$account:repo/*</code></td>
</tr>
<tr>
<td align="left">CreateRepositoryPersonal<br>Creating an image repository of Personal Edition</td>
<td align="left">repo</td>
<td align="left"><code>qcs::tcr:$region:$account:repo/$namespace/$repo</code></td>
</tr>
<tr>
<td align="left">DeleteRepositoryPersonal<br>Deleting an image repository of Personal Edition</td>
<td align="left">repo</td>
<td align="left"><code>qcs::tcr:$region:$account:repo/$namespace/$repo</code></td>
</tr>
<tr>
<td align="left">BatchDeleteRepositoryPersonal<br>Deleting the image repositories of Personal Edition in batches</td>
<td align="left">repo</td>
<td align="left"><code>qcs::tcr:$region:$account:repo/$namespace/*</code></td>
</tr>
<tr>
<td align="left">DeleteImagePersonal<br>Deleting the repository tag of Personal Edition</td>
<td align="left">repo</td>
<td align="left"><code>qcs::tcr:$region:$account:repo/$namespace/$repo</code></td>
</tr>
<tr>
<td align="left">BatchDeleteImagePersonal<br>Deleting the repository tags of Personal Edition in batches</td>
<td align="left">repo</td>
<td align="left"><code>qcs::tcr:$region:$account:repo/$namespace/$repo</code></td>
</tr>
<tr>
<td align="left">PullRepositoryPersonal<br>Pulling the images in the image repository of Personal Edition</td>
<td align="left">repo</td>
<td align="left"><code>qcs::tcr:$region:$account:repo/$namespace/$repo</code></td>
</tr>
<tr>
<td align="left">PushRepositoryPersonal<br>Pushing the images in the image repository of Personal Edition</td>
<td align="left">repo</td>
<td align="left"><code>qcs::tcr:$region:$account:repo/$namespace/$repo</code></td>
</tr>
</tbody></table>


