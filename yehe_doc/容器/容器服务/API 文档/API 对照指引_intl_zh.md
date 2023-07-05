**[容器服务 API 2.0 ](https://intl.cloud.tencent.com/document/product/457/9458) 将于2020年3月底下线， 建议您使用 [容器服务 API 3.0](https://intl.cloud.tencent.com/document/product/457/32029)。3.0版本接口定义更加规范，访问时延下降显著，您可参考下文 API 接口对照映射表开始使用。**

>下表中部分容器服务 API 3.0 接口及 Kubernetes API 文档将于近期上线，请注意官方文档变化。

<table>
	<tr>		<th colspan=2>模块</th>		<th>API 2.0</th>		<th>API 3.0</th>	</tr>
	<tr>
		<td rowspan=20 colspan=2>集群相关</td>
		<td>创建集群（CreateCluster）</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32027">创建集群（CreateCluster）</a></td>
	</tr>
	<tr>
		<td>删除集群（DeleteCluster）</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/33870"> 删除集群（DeleteCluster）</a></td>
	</tr>
	<tr>
		<td>查询集群列表（DescribeCluster）</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/32025">查询集群列表（DescribeCluster）</a></td>
	</tr>
	<tr>
		<td>扩展集群节点（ AddClusterInstances）</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/33862">扩展集群节点（CreateClusterInstances）</a></td>
	</tr>
	<tr>
		<td>添加已存在云服务器到集群（AddClusterInstancesFromExistedCvm）</td>
		<td>添加已经存在的实例到集群（AddExistedInstances）</td>
	</tr>
	<tr>
		<td>删除集群节点（DeleteClusterInstances）</td>
		<td>删除集群中的节点（DeleteClusterInstances）</td>
	</tr>
	<tr>
		<td>查询集群节点列表（DescribeClusterInstances）</td>
		<td>查询集群节点信息（DescribeClusterInstances）</td>
	</tr>
	<tr>
		<td>获取集群外网访问凭据（DescribeClusterSecurityInfo ）</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/33865">集群的密钥信息（DescribeClusterSecurity）</a></td>
	</tr>
	<tr>
		<td>校验 CIDR（CheckClusterCIDR）</td>
		<td>检查集群的 CIDR 是否冲突（CheckClusterCIDR）</td>
	</tr>
	<tr>
		<td>查询加入集群的主机列表（DescribeExistedCvmForAddClusterInstances）</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/33861">查询已经存在的节点（DescribeExistedInstances）</a></td>
	</tr>
	<tr>
		<td>查询集群 Request 和 Limit 信息（DescribeClusterRequestLimitInfo）</td>
		<td rowspan=2>Kubernetes API</td>
	</tr>
	<tr>
			<td>修改节点 Label（ModifyClusterNodeLabel）</td>
	</tr>
	<tr>
		<td>修改集群属性（ModifyClusterAttributes）</td>
		<td rowspan=2>修改集群属性（ ModifyClusterAttribute）</td>
	</tr>
	<tr>
		<td>修改集群所属项目（ModifyProjectId）</td>
	</tr>
	<tr>
		<td>修改集群命名空间描述（ModifyNamespaceDescription）</td>
		<td>Kubernetes API</td>
	</tr>
	<tr>
		<td><ul class="params"><li>操作集群外网访问地址（OperateClusterVip） </li><li>查询异步任务结果（DescribeClusterTaskResult）</li></td>
		<td><ul class="params"><li><a href="https://intl.cloud.tencent.com/document/product/457/33871">创建托管集群外网访问端口（CreateClusterEndpointVip）</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/33868">删除托管集群外网访问端口（DeleteClusterEndpointVip）</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/33866">查询托管集群开启外网端口流程状态（ DescribeClusterEndpointVipStatus）</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/33864">修改托管集群外网端口的安全策略（ModifyClusterEndpointSP）</a></li></ul></td>
	</tr>
	<tr>
		<td>驱逐集群节点（ DrainClusterNode）</td>
		<td>驱逐节点（DrainClusterNode）</td>
	</tr>
	<tr>
		<td>设置集群节点为是否可调度（ModifyClusterNodeSchedulable）</td>
		<td>Kubernetes API</a></td>
	</tr>
	<tr>
		<td>添加第三方私有镜像仓库（AddHubInfo）</td>
		<td rowspan=2>功能下线</td>
	</tr>
	<tr>
		<td>查询集群第三方镜像仓库（DescribeHubInfo）</td>
	</tr>
	<tr>
		<td rowspan=9  colspan=2>集群自动扩缩容相关</td>
		<td>创建集群伸缩组（CreateClusterAsg）</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/33852">创建集群的伸缩组（CreateClusterAsGroup）</a></td>
	</tr>
	<tr>
		<td>启用集群伸缩组（EnableClusterAsg）</td>
		<td>修改集群伸缩组属性（ModifyClusterAsGroupAttribute）</td>
	</tr>
	<tr>
		<td>查询集群伸缩组列表（DescribeClusterAsg）</td>
	 <td>集群关联的伸缩组列表（DescribeClusterAsGroups）</td>
	</tr>
	<tr>
		<td>修改集群伸缩组是否启用缩容（ModifyClusterAsgScaleDown）</td>
	 <td>修改集群弹性伸缩属性（ModifyClusterAsGroupOptionAttribute）</td>
	</tr>
	<tr>
		<td>修改集群伸缩组 label（ModifyClusterAsgLabel）</td>
	 <td rowspan=3>功能下线</td>
	</tr>
	<tr>
		<td>重置集群伸缩组 label（ResetClusterAsgLabel）</td>
	<tr>
		<td>删除集群伸缩组 label（DeleteClusterAsgLabel）</td>
	</tr>
	</tr>
	<tr>
		<td>停用集群伸缩组（DisableClusterAsg）</td>
		<td>修改集群伸缩组属性（ModifyClusterAsGroupAttribute）</td>
	</tr>
	<tr>
		<td>删除集群伸缩组（DeleteClusterAsg）</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/457/33851">删除集群伸缩组（DeleteClusterAsGroups）</a></td>
	</tr>
	<tr>
		<td rowspan=14  colspan=2>服务相关</td>
		<td>创建服务（CreateClusterService）</td>
		<td rowspan=25>Kubernetes API</td>
	</tr>
	<tr>
		<td>查询服务列表（DescribeClusterService）</td>
	</tr>
	<tr>
		<td>查询服务详情（DescribeClusterServiceInfo）</td>
	</tr>
	<tr>
		<td>获取服务事件列表（DescribeServiceEvent）</td>
	</tr>
	<tr>
		<td>获取服务的 yaml 文本信息（DescribeClusterServiceText）</td>
	</tr>
	<tr>
		<td>修改服务（ModifyClusterService）</td>
	</tr>
	<tr>
		<td>修改服务描述（ModifyServiceDescription）</td>
	</tr>
	<tr>
		<td>修改服务镜像（ModifyClusterServiceImage）</td>
	</tr>
	<tr>
		<td>修改服务的标签（Label）信息（ModifyServiceLabels）</td>
	</tr>
	<tr>
		<td>回滚服务（RollBackClusterService）</td>
	</tr>
	<tr>
		<td>服务重部署（RedeployClusterService）</td>
	</tr>
	<tr>
		<td>暂停服务更新（PauseClusterService）</td>
	</tr>
	<tr>
		<td>继续服务更新（ResumeClusterService）</td>
	</tr>
	<tr>
		<td>删除服务（DeleteClusterService）</td>
	</tr>
	<tr>
        <td rowspan=4  colspan=2>服务实例相关</td>
        <td>查询服务实例列表（DescribeServiceInstance）</td>
	</tr>
	<tr>
		<td>修改服务实例副本数（ModifyServiceReplicas）</td>
	</tr>
	<tr>
		<td>获取服务实例日志（DescribeInstanceLog）</td>
	</tr>
	<tr>
		<td>删除服务实例（DeleteInstances）</td>
	</tr>
	<tr>
        <td rowspan=3  colspan=2>命名空间相关</td>
        <td>查询集群命名空间（DescribeClusterNameSpaces）</td>
	</tr>
	<tr>
		<td>创建集群命名空间（CreateClusterNamespace）</td>
	</tr>
	<tr>
		<td>删除集群命名空间（DeleteClusterNamespace）</td>
	</tr>
	<tr>
        <td rowspan=4  colspan=2>Ingress 相关</td>
        <td>创建 Ingress（CreateIngress）</td>
	</tr>
	<tr>
		<td>查询 Ingress 列表（DescribeIngress）</td>
	</tr>
	<tr>
		<td>修改 Ingress（MosifyIngress）</td>
	</tr>
	<tr>
		<td>删除 Ingress（DeleteIngress）</td>
	</tr>
	<tr>
        <td rowspan=8  colspan=2>日志相关</td>
        <td>启用集群日志收集服务（GetLogDaemonStatus）</td>
        <td rowspan=8>功能下线</td>
	</tr>
	<tr>
		<td>创建集群日志收集规则（CreateLogCollector）</td>
	</tr>
	<tr>
		<td>列出日志收集规则（ListLogCollector）</td>
	</tr>
	<tr>
		<td>更新日志收集规则（UpdateLogCollector）</td>
	</tr>
	<tr>
		<td>获取日志收集器信息（GetLogCollector）</td>
	</tr>
	<tr>
		<td>获取日志收集器状态信息（GetLogDaemonStatus）</td>
	</tr>
	<tr>
		<td>检查日志收集器名称（CheckIfLogCollectorName）</td>
	</tr>
	<tr>
		<td>删除日志收集规则（DeleteLogCollector）</td>
	</tr>
	<tr>
        <td  colspan=2 >监控相关</td>
        <td>查询容器服务监控信息（GetMonitorData）</td>
        <td><ul class="params"><li><a href="https://intl.cloud.tencent.com/document/product/248/11016">容器服务-实例维度监控接口（GetMonitorData）</a></li><li><a href="https://intl.cloud.tencent.com/document/product/248/11017">容器服务-容器维度监控接口（GetMonitorData）</a></li><li><a href="https://intl.cloud.tencent.com/document/product/248/11018">容器服务-服务维度监控接口（GetMonitorData）</a></li></ul></td>
	</tr>
    <tr>       
        <td rowspan=28 >镜像仓库相关</td>
        <td rowspan=3>用户及密码管理</td>
        <td>用户注册（无需指定 Namespace）（RegisterRepositoryAccountNew）</td>
        <td >创建个人用户（CreateUserPersonal）</td>
    </tr>
    <tr>
        <td>查询用户配额（GetLimit）</td>
        <td >查询个人用户配额（DescribeUserQuotaPersonal）</td>
    </tr>
    <tr>
        <td>修改密码（ChangePassword）</td>
        <td >修改个人用户登录密码（ ModifyUserPasswordPersonal）</td>
    </tr>
    <tr>
    	<td rowspan=4>命名空间</td>
        <td>创建命名空间（CreateCCRNamespace）</td>
        <td >创建命名空间（CreateNamespacePersonal）</td>
    </tr>
    <tr>
        <td>查询命名空间（GetNamespaceInfo）</td>
        <td >查询命名空间（DescribeNamespacePersonal）</td>
    </tr>
    <tr>
        <td>查询命名空间是否存在（NamespaceIsExists）</td>
        <td >检查命名空间是否存在（ValidateNamespaceExistPersonal）</td>
    </tr>
    <tr>
        <td>删除命名空间（DeleteUserNamespace）</td>
        <td >删除命名空间（DeleteNamespacePersonal）</td>
    </tr>
    <tr>
    	<td rowspan=9>镜像仓库</td>
        <td>创建镜像仓库（CreateRepository）</td>
        <td >创建镜像仓库（CreateRepositoryPersonal）</td>
    </tr>
    <tr>
        <td>查询镜像仓库信息（GetRepositoryInfo）</td>
        <td >查询镜像仓库（DescribeRepositoryPersonal）</td>
    </tr>
    <tr>
        <td>-</td>
        <td >删除镜像仓库（DeleteRepositoryPersonal）</td>
    </tr>
    <tr>
        <td>批量删除仓库（BatchDeleteRepository）</td>
        <td >批量删除镜像仓库（BatchDeleteRepositoryPersonal）</td>
    </tr>
    <tr>
        <td>镜像仓库是否存在（RepositoryisExists）</td>
        <td >检查镜像仓库是否存在（ValidateRepositoryExistPersonal）</td>
    </tr>
    <tr>
        <td>获取用户自身的所有仓库列表（GetUserRepositoryList）</td>
        <td >查询用户创建的镜像仓库（DescribeRepositoryOwnerPersonal）</td>
    </tr>
    <tr>
        <td>查询用户仓库列表（SearchUserRepository）</td>
        <td >查询指定条件的镜像仓库（DescribeRepositoryFilterPersonal）</td>
    </tr>
    <tr>
        <td>更新镜像仓库访问属性（UpdateRepositoryPublic）</td>
        <td >修改镜像仓库公开属性（ModifyRepositoryAccessPersonal）</td>
    </tr>
    <tr>
        <td>更改镜像仓库描述内容（UpdateRepositoryDesc）</td>
        <td >修改镜像仓库描述信息（ModifyRepositoryInfoPersonal）</td>
    </tr>
    <tr>
    	<td rowspan=8>镜像仓库</td>
        <td>获取 tag 列表（GetTagList）</td>
        <td >查询镜像版本（DescribeImagePersonal）</td>
    </tr>
    <tr>
        <td>-</td>
        <td >查询指定条件的镜像版本（DescribeImageFilterPersonal）</td>
    </tr>
    <tr>
        <td>-</td>
        <td >删除镜像版本（DeleteImagePersonal）</td>
    </tr>
    <tr>
        <td>批量删除  tag（BatchDeleteTag）</td>
        <td >批量删除镜像版本（BatchDeleteImagePersonal）</td>
    </tr>
    <tr>
        <td>复制镜像版本（DuplicateImage）</td>
        <td >复制镜像版本（DuplicateImagePersonal）</td>
    </tr>
    <tr>
        <td>设置仓库 tag 超额保留策略（SetAutoDelStrategy）</td>
        <td >创建镜像版本生命周期配置（CreateImageLifecyclePersonal）</td>
    </tr>
    <tr>
        <td>获取仓库 tag 超额保留策略（GetAutoDelStrategy）</td>
        <td >查询镜像版本生命周期配置（DescribeImageLifecyclePersonal）</td>
    </tr>
    <tr>
        <td>关闭仓库 tag 超额保留策略（CloseAutoDelStrategy）</td>
        <td >删除镜像版本生命周期配置（DeleteImageLifecyclePersonal）</td>
    </tr>
    <tr>
    	<td rowspan=4>触发器</td>
        <td>添加触发器（AddUpdateWorkloadTrigger）</td>
        <td >创建应用更新触发器（CreateApplicationTriggerPersonal）</td>
    </tr>
    <tr>
        <td>修改服务更新触发器（ModifyUpdateServiceTrigger）</td>
        <td >修改应用更新触发器（ModifyApplicationTriggerPersonal）</td>
    </tr>
    <tr>
        <td>获取触发器（ListTrigger）</td>
        <td >查询应用更新触发器（DescribeApplicationTriggerPersonal）</td>
    </tr>
    <tr>
        <td>获取触发记录（ListTriggerLog）</td>
        <td >查询应用更新触发器触发日志（DescribeApplicationTriggerLogPersonal ）</td>
    </tr>
</table>


<style>
	.params{margin-bottom:0px !important;}
</style>






