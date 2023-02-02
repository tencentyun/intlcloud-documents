Prometheus 监控服务对常用的开发语言/中间件/大数据/基础设施数据库进行了集成，支持一键安装和自定义安装方式，用户只需根据指引即可对相应的组件进行监控，同时提供了开箱即用的 Grafana 监控大盘。集成中心涵盖了基础服务监控，应用层监控、Kubernetes 容器监控三大监控场景，方便您快速接入并使用。


 ## 支持服务列表

 <table>
	<tr>
	<th>服务类型</th>
	<th>服务名称</th>
	<th>监控项</th>
	<th>是否支持一键安装</th>
	<th>接入文档</th>
	</tr>
	<tr>
		<td rowspan="2">大数据</td>
		<td>ElasticSearch</td>
	<td>包括集群/索引/节点等监控</td>
<td>支持</td>
			<td><a href="https://intl.cloud.tencent.com/document/product/1116/43223">ElasticSearch Exporter 接入</a></td>
	</tr>
    <tr>
	    <td>Flink</td>
		<td>包括集群/Job/Task 等监控</td>
		<td>不支持</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/1116/43217">Flink 接入</a></td>
	</tr>
	<tr>
		<td rowspan="4">开发</td>
		<td>CVM 云服务器</td>
		<td>使用扩展的 cvm_sd_config 配置 CVM 抓取任务，采集 node-exporter 或业务自定义指标</td>
		<td>支持</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/1116/49141">CVM node_expoter</a></td>
	</tr>
		<tr>
		<td>Golang</td>
		<td>包括 GC/Heap/Thread/Goroutine 等监控</td>
		<td>不支持</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/1116/43221">Golang 应用接入</a></td>
	</tr>
	<tr>
		<td>JVM</td>
		<td>包括 Heap/Thread/GC/CPU/File 等监控</td>
		<td>不支持</td>
			<td><a href="https://intl.cloud.tencent.com/document/product/1116/43220">JVM 接入</a></td>
	</tr>
	<tr>
		<td>Spring MVC</td>
		<td>包括 HTTP接口/异常/JVM 等监控</td>
			<td>不支持</td>
			<td><a href="https://intl.cloud.tencent.com/document/product/1116/43219">Spring Boot 接入</a></td>
	</tr>
	<tr>
		<td rowspan="4">中间件</td>
		<td>Kafka</td>
		<td>包括 Broker/Topic/Consumer Group 等监控</td>
		<td>支持</td>
				<td><a href="https://intl.cloud.tencent.com/document/product/1116/43224">Kafka Exporter 接入</a></td>
	</tr>
		<tr>
		<td>Consul</td>
		<td>Consul 监控</td>
		<td>支持</td>
				<td><a href="https://intl.cloud.tencent.com/document/product/1116/43230">Consul Exporter 接入</a></td>
	</tr>
			<tr>
		<td>Etcd</td>
		<td>Etcd 监控</td>
		<td>不支持</td>
				<td>-</td>
	</tr>
			<tr>
		<td>Istio</td>
		<td>Istio 监控</td>
		<td>不支持</td>
				<td>-</td>
	</tr>
	<tr>
		<td>基础设施</td>
		<td>Kubernetes</td>
		<td>包括 API Server/DNS/Workload/Network 等监控</td>
		<td>支持</td>
						<td><a href="https://intl.cloud.tencent.com/document/product/1116/43183">安装 Agent 接入 Kubernete</a></td>
</tr>
	<tr>
		<td rowspan="5">数据库</td>
		<td>云数据库 MongoDB</td>
		<td>包括文档数/读写性能/网络流量等</td>
		<td>支持</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1116/43225">MongoDB Exporter 接入</a></td>
</tr>
<tr>
		<td>云数据库 MySQL</td>
		<td>包括网络/连接数/慢查询等</td>
		<td>支持</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/1116/43229">MySQL Exporter 接入</a></td>
</tr>
<tr>
		<td>云数据库 PostgreSQL</td>
		<td>包括 CPU/Memory/事务/Lock/读写等监控</td>
			<td>支持</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/1116/43226">PostgreSQL Exporter 接入</a></td>
</tr>
<tr>
		<td>云数据库 Redis</td>
		<td>包括内存使用率/连接数/命令执行情况等监控</td>
		<td>支持</td>
				<td><a href="https://intl.cloud.tencent.com/document/product/1116/43228">Redis Exporter 接入</a></td>
</tr>
<tr>
		<td>云数据库 Memcached</td>
	<td>Memcached 监控</td>
	<td>支持</td>
				<td><a href="https://intl.cloud.tencent.com/document/product/1116/43231">Memcached Exporter 接入</a></td>
</tr>
<tr>
		<td>巡检</td>
		<td>健康巡检</td>
		<td>通过 Blackbox 定期对目标服务进行连通性测试，帮助您掌握服务的健康状况，及时发现异常</td>
			<td>支持</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1116/43233">健康巡检</a></td>
</tr>
<tr>
		<td >云监控</td>
		<td>云监控</td>
		<td>云产品监控</td>
			<td>支持</td>
<td>-</td>
</tr>
<tr>
		<td rowspan="2">自定义</td>
		<td>抓取任务</td>
		<td>使用原生 static_config 配置抓取任务</td>
			<td>支持</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1116/43214"> 抓取配置说明</a></td>
</tr>
<tr>
		<td>CVM 抓取任务</td>
		<td>使用扩展的 cvm_sd_config 配置 CVM 抓取任务</td>
			<td>支持</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1116/43214"> 抓取配置说明</a></td>
</tr>
</table>




## 操作步骤
### 一键安装
部分服务支持一键安装 Agent ，详情请参见 [支持服务列表](https://intl.cloud.tencent.com/document/product/1116/43163)。
1. 登录 [云监控 Prometheus 控制台](https://console.cloud.tencent.com/monitor/prometheus)。
2. 在实例列表中，选择对应的 Prometheus 实例。
3. 进入实例详情页，单击 **集成中心**。
4. 在集成中心选择支持一键安装的服务，单击模块左下角的 **安装**。
![](https://qcloudimg.tencent-cloud.cn/raw/270a1592ff70e8cdfc2d446d4ec02222.png)
5. 在集成列表页，填写指标采集名称和地址等信息，并单击保存即可。如下图以 Kafka 为例：
![](https://qcloudimg.tencent-cloud.cn/raw/98888f5b23e80e6b7279084e64247994.png)

### 自定义安装
1. 登录 [云监控 Prometheus 控制台](https://console.cloud.tencent.com/monitor/prometheus)。
2. 在实例列表中，选择对应的 Prometheus 实例。
3. 进入实例详情页，单击 **集成中心**。
4. 在集成中心选择对应的服务。您可以单击 **接入指南** 查看接入指引，接入成功后即可实时监控对应的服务。您还可以单击  **Dashboard 安装/升级** 安装或升级该服务的 Grafana Dashboard。
![](https://qcloudimg.tencent-cloud.cn/raw/9f2ad0a579a4677f7f2fe1da1af970fb.png)
