### Instance Management APIs
<table>
<thead>
<tr>
<th align="left" style="width:15%">APIs and Description</th>
<th align="left" style="width:10%">Resource Type</th>
<th align="left">Six-segment Example of Resource</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">CreateInstance<br>Creating an instance</td>
<td align="left">instance</td>
<td align="left"><code>qcs::tcr:$region:$account:instance/$instanceid</code></td>
</tr>
<tr>
<td align="left">DescribeInstanceStatus<br>Querying the instance status</td>
<td align="left">instance</td>
<td align="left"><code>qcs::tcr:$region:$account:instance/*</code>  <code>qcs::tcr:$region:$account:instance/$instanceid</code></td>
</tr>
<tr>
<td align="left">DescribeInstances<br>Querying the instance information</td>
<td align="left">instance</td>
<td align="left"><code>qcs::tcr:$region:$account:instance/*</code>  <code>qcs::tcr:$region:$account:instance/$instanceid</code></td>
</tr>
<tr>
<td align="left">CreateInstanceToken<br>Creating an instance access credential</td>
<td align="left">instance</td>
<td align="left"><code>qcs::tcr:$region:$account:instance/$instanceid</code></td>
</tr>
<tr>
<td align="left">DeleteInstanceToken<br>Deleting a long-term access credential</td>
<td align="left">instance</td>
<td align="left"><code>qcs::tcr:$region:$account:instance/$instanceid</code></td>
</tr>
<tr>
<td align="left">ModifyInstanceToken<br>Updating the instance’s long-term access credential</td>
<td align="left">instance</td>
<td align="left"><code>qcs::tcr:$region:$account:instance/$instanceid</code></td>
</tr>
<tr>
<td align="left">DescribeInstanceToken<br>Querying the long-term access credential information</td>
<td align="left">instance</td>
<td align="left"><code>qcs::tcr:$region:$account:instance/$instanceid</code></td>
</tr>
</tbody></table>


### Namespace APIs
<table>
<tr>
<th align="left" style="width:15%">APIs and Description</th>
<th align="left" style="width:10%">Resource Type</th>
<th align="left">Six-segment Example of Resource</th>
</tr>
<tr>
<td align="left">CreateNamespace<br>Creating a namespace</td>
<td align="left">repository</td>
<td align="left"><code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName</code></td>
</tr>
<tr>
<td align="left">DeleteNamespace<br>Deleting a namespace</td>
<td align="left">repository</td>
<td align="left"><code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName</code></td>
</tr>
<tr>
<td align="left">ModifyNamespace<br>Updating the namespace information</td>
<td align="left">repository</td>
<td align="left"><code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName</code></td>
</tr>
<tr>
<td align="left">DescribeNamespaces<br>Querying the namespace information</td>
<td align="left">repository</td>
<td align="left">
<code>qcs::tcr:$region:$account:repository/$instanceId/*</code><br><code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName</code></td>
</tr>
</table>

### Image Repository APIs
<table>
<tr>
<th align="left" style="width:15%">APIs and Description</th>
<th align="left" style="width:10%">Resource Type</th>
<th align="left">Six-segment Example of Resource</th>
</tr>
<tr>
<td align="left">CreateRepository<br>Creating an image repository</td>
<td align="left">repository</td>
<td align="left">
<code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName/$repositoryName</code></td>
</tr>
<tr>
<td align="left">DeleteRepository<br>Deleting an image repository</td>
<td align="left">repository</td>
<td align="left">
<code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName/$repositoryName</code></td>
</tr>
<tr>
<td align="left">ModifyRepository<br>Updating the image repository information</td>
<td align="left">repository</td>
<td align="left">
<code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName/$repositoryName</code></td>
</tr>
<tr>
<td align="left">DescribeImages<br>Querying the container image information</td>
<td align="left">repository</td>
<td align="left">
<code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName/$repositoryName/*</code></td>
</tr>
<tr>
<td align="left">DescribeImages<br>Querying the image repository information</td>
<td align="left">repository</td>
<td align="left">
<code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName/*</code><br>
<code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName/$repositoryName</code></td>
</tr>
</table>


