### 实例管理相关接口
<table>
<thead>
<tr>
<th align="left" style="width:15%">API 名称及描述</th>
<th align="left" style="width:10%">资源类型</th>
<th align="left">资源六段式示例</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">CreateInstance<br>创建实例</td>
<td align="left">instance</td>
<td align="left"><code>qcs::tcr:$region:$account:instance/$instanceid</code></td>
</tr>
<tr>
<td align="left">DescribeInstanceStatus<br>查询实例状态</td>
<td align="left">instance</td>
<td align="left"><code>qcs::tcr:$region:$account:instance/*</code>  <code>qcs::tcr:$region:$account:instance/$instanceid</code></td>
</tr>
<tr>
<td align="left">DescribeInstances<br>查询实例信息</td>
<td align="left">instance</td>
<td align="left"><code>qcs::tcr:$region:$account:instance/*</code>  <code>qcs::tcr:$region:$account:instance/$instanceid</code></td>
</tr>
<tr>
<td align="left">CreateInstanceToken<br>创建实例访问凭证</td>
<td align="left">instance</td>
<td align="left"><code>qcs::tcr:$region:$account:instance/$instanceid</code></td>
</tr>
<tr>
<td align="left">DeleteInstanceToken<br>删除长期访问凭证</td>
<td align="left">instance</td>
<td align="left"><code>qcs::tcr:$region:$account:instance/$instanceid</code></td>
</tr>
<tr>
<td align="left">ModifyInstanceToken<br>更新实例长期访问凭证</td>
<td align="left">instance</td>
<td align="left"><code>qcs::tcr:$region:$account:instance/$instanceid</code></td>
</tr>
<tr>
<td align="left">DescribeInstanceToken<br>查询长期访问凭证信息</td>
<td align="left">instance</td>
<td align="left"><code>qcs::tcr:$region:$account:instance/$instanceid</code></td>
</tr>
</tbody></table>


### 命名空间相关接口
<table>
<tr>
<th align="left" style="width:15%">API 名称及描述</th>
<th align="left" style="width:10%">资源类型</th>
<th align="left">资源六段式示例</th>
</tr>
<tr>
<td align="left">CreateNamespace<br>创建命名空间</td>
<td align="left">repository</td>
<td align="left"><code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName</code></td>
</tr>
<tr>
<td align="left">DeleteNamespace<br>删除命名空间</td>
<td align="left">repository</td>
<td align="left"><code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName</code></td>
</tr>
<tr>
<td align="left">ModifyNamespace<br>更新命名空间信息</td>
<td align="left">repository</td>
<td align="left"><code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName</code></td>
</tr>
<tr>
<td align="left">DescribeNamespaces<br>查询命名空间信息</td>
<td align="left">repository</td>
<td align="left">
<code>qcs::tcr:$region:$account:repository/$instanceId/*</code><br><code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName</code></td>
</tr>
</table>

### 镜像仓库相关接口
<table>
<tr>
<th align="left" style="width:15%">API 名称及描述</th>
<th align="left" style="width:10%">资源类型</th>
<th align="left">资源六段式示例</th>
</tr>
<tr>
<td align="left">CreateRepository<br>创建镜像仓库</td>
<td align="left">repository</td>
<td align="left">
<code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName/$repositoryName</code></td>
</tr>
<tr>
<td align="left">DeleteRepository<br>删除镜像仓库</td>
<td align="left">repository</td>
<td align="left">
<code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName/$repositoryName</code></td>
</tr>
<tr>
<td align="left">ModifyRepository<br>更新镜像仓库信息</td>
<td align="left">repository</td>
<td align="left">
<code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName/$repositoryName</code></td>
</tr>
<tr>
<td align="left">DescribeImages<br>查询容器镜像信息</td>
<td align="left">repository</td>
<td align="left">
<code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName/$repositoryName/*</code></td>
</tr>
<tr>
<td align="left">DescribeImages<br>查询镜像仓库信息</td>
<td align="left">repository</td>
<td align="left">
<code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName/*</code><br>
<code>qcs::tcr:$region:$account:repository/$instanceId/$namespaceName/$repositoryName</code></td>
</tr>
</table>


