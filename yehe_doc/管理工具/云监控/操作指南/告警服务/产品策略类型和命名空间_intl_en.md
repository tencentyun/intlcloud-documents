This document lists the policy types and namespaces of Tencent Cloud services.


  <table>
   <thead>
	   <tr>
     <th style="width:10%;">Tencent Cloud Service</th>
     <th style="width:15%;">Policy Type (Namespaces.N)</th>
     <th style="width:75%;">Dimension Information (Dimensions)</th>
    </tr>
   </thead>
   <tbody>
    <tr>
     <td><span>CVM - <b>basic monitoring</b></span></td>
     <td><span>cvm_device</span></td>
     <td ><code>{&quot;unInstanceId&quot;:&quot;ins-ot3cq4bi&quot;}</code></td>
    </tr>
    <tr>
     <td><span>CVM - <b>storage monitoring</b></span></td>
     <td><span>BS</span></td>
     <td><code>{&quot;diskid&quot;:&quot;disk-1yukg09l&quot;}</code></td>
    </tr>
    <tr>
     <td><span>TencentDB for MySQL</span></td>
     <td><span>cdb_detail</span></td>
     <td><code>{&quot;unInstanceId&quot;:&quot;cdb-emzu6ysk&quot;}</code></td>
    </tr>
    <tr>
     <td  ><span>TencentDB for Redis (5-second) - <b>Proxy node</b></span></td>
		 <td><span>redis_mem_proxy</span></td>
     <td><span></span><code>{&quot;appid&quot;: &quot;1252068037&quot;,&quot;instanceid&quot;:&quot;crs-1amp2583&quot;,<br/> &quot;pnodeid&quot;:&quot;0f2ce0f969c4f43bc338bc1d6f60597d654bb3e4&quot;}</code>
		 <tr>
		   <td ><span>TencentDB for Redis (5-second) - <b>Redis node</b></span></td>
		 <td><span>redis_mem_node</td></span>
		 <td><span><code>{&quot;appid&quot;: &quot;1252068000&quot;,&quot;instanceid&quot;:&quot;crs-1amp2588&quot;,<br/>&quot;rnodeid&quot;:&quot;0f2ce0f969c4f43bc338bc1d6f60597d654bb3e4&quot;}</code></td>
		 </tr>
		 <tr>
		  <td ><span>TencentDB for Redis (5-second) - <b>instance summary</b></span></td>
		 <td><span>redis_mem_edition</td></span>
		 <td><span> <code>{&quot;AppId&quot;: &quot;1252068000&quot;, &quot;InstanceId&quot;:&quot;crs-1amp2588&quot;}</span></code></td>
		 </tr>
    <tr>
		<td><span>CLB - <b>layer-7 protocol</b></span></td>
     <td><span>LB-SEVEN-LAYER-<br>MONITOR</span></td>
     <td><code>{&quot;protocol&quot;:&quot;https&quot;,&quot;vip&quot;:&quot;14.22.4.26&quot;,&quot;port&quot;:&quot;443&quot;}</code></td>
    </tr>
    <tr>
     <td><span>CLB - <b>public network listener</b></span></td>
     <td><span>CLB_LISTENER_<br/>PUBLIC</span></td>
     <td><code>{&quot;protocol&quot;:&quot;https&quot;,&quot;vip&quot;:&quot;118.25.31.161&quot;,&quot;vport&quot;:443}</code></td>
    </tr>
    <tr>
     <td><span>CLB - <b>private network listener</b></span></td>
     <td><span>CLB_LISTENER_<br/>PUBLIC</span></td>
     <td><code>{&quot;protocol&quot;:&quot;https&quot;,&quot;vip&quot;:&quot;14.22.4.26&quot;,<br/>&quot;vpcId&quot;:vpc-1ywqac83,&quot;vport&quot;:&quot;443&quot;}</code></td>
    </tr>
    <tr>
     <td><span>CLB - <b>server port (classic private network)</b></span></td>
     <td><span>CLB_PORT_PRIVATE</span></td>
     <td><code>{&quot;protocol&quot;:&quot;https&quot;,&quot;lanIp&quot;:&quot;111.222.111.22&quot;,<br/>&quot;port&quot;:&quot;440&quot;,&quot;vip&quot;:&quot;14.12.13.25&quot;, &quot;vpcId&quot;:vpc-1ywqac83,<br/>&quot;loadBalancerPort&quot;:&quot;443&quot;}</code></td>
    </tr>
    <tr>
     <td><span>TencentDB for SQL Server</span></td>
     <td><span>sqlserver_instance</span></td>
     <td><code>{&quot;uid&quot;:&quot;gamedb.gz18114.cdb.db&quot;}</code></td>
    </tr>
    <tr>
     <td><span>TencentDB for MongoDB - <b>instance</b></span></td>
		 <td>cmongo_instance</td>
		 <td>{&quot;target&quot;:&quot;cmgo-ajc6okuy&quot;}</td>
		 </tr>
		   <tr>
			 <td><span>TencentDB for MongoDB - <b>node</b></span></td>
		 <td>CMONGO_NODE</td>
		 <td>{&quot;target&quot;:&quot;cmgo-ajc6okuy&quot;}</td>
		 </tr>
		 <tr>
     <td><span>TencentDB for MongoDB - <b>replica set</b></span></td>
		 <td>CMONGO_REPLICA</td>
		 <td>{&quot;target&quot;:&quot;cmgo-ajc6okuy&quot;}</td>
		 </tr>
    <tr>
     <td><span>TencentDB for PostgreSQL</span></td>
     <td><span>POSTGRESQL</span></td>
     <td><code>{&quot;uid&quot;:&quot;2123&quot;}</code></td>
    </tr>
    <tr>
     <td><span>TDSQL-C MySQL</span></td>
     <td><span>CYNOSDB_MYSQL</span></td>
     <td><code>{&quot;appid&quot;:&quot;1256754779&quot;,&quot;clusterid&quot;:&quot;cynosdbmysql-p7ahy11x&quot;,&quot;instanceid&quot;:&quot;cynosdbmysql-inscyi56ruc&quot;,<br/>&quot;insttype&quot;:&quot;ro&quot;}</code></td>
    </tr>
    <tr>
     <td><span>TcaplusDB</span></td>
     <td><span>tcaplusdb</span></td>
     <td><code>{&quot;ClusterId&quot;:&quot;xxx&quot;,&quot;TableInstanceId&quot;:&quot;xxx&quot;}</code></td>
    </tr>
    <tr>
     <td><span>TDSQL for MySQL</span></td>
     <td><span>DCDB</span></td>
     <td><code>{&quot;cluster_name&quot;:&quot;xxx&quot;,&quot;is_master&quot;:&quot;xxx&quot;, &quot;set_name&quot;:&quot;xxx&quot;,&quot;type&quot;:&quot;xxx&quot;,&quot;zk_name&quot;:&quot;xxx&quot;}</code></td>
    </tr>
    <tr>
     <td><span>SCF</span></td>
     <td><span>SCF</span></td>
     <td><code>{&quot;appid&quot;:&quot;1251316163&quot;,&quot;function_name&quot;:&quot;insert-tapd-task-result&quot;,&quot;namespace&quot;:&quot;qmap-insight-core&quot;,&quot;version&quot;:&quot;$latest&quot;}</code></td>
    </tr>
    <tr>
     <td><span>COS</span></td>
     <td><span>COS</span></td>
     <td><code>{&quot;bucket&quot;:&quot;fms-1255817900&quot;}</code></td>
    </tr>
    <tr>
     <td><span>VPC - <b>NAT gateway</span></td>
     <td><span>nat_tc_stat</span></td>
     <td><code>{&quot;uniq_nat_id&quot;:&quot;nat-4d545d&quot;}</code></td>
    </tr>
    <tr>
     <td><span>VPC - <b>VPN gateway</span></td>
     <td><span>VPN_GW</span></td>
     <td><code>{&quot;appid&quot;:&quot;12345&quot;,&quot;vip&quot;: &quot;10.0.0.0&quot;}</code></td>
    </tr>
    <tr>
     <td><span>VPC - <b>VPN tunnel</span></td>
     <td><span>vpn_tunnel</span></td>
     <td><code>{&quot;vpnconnid&quot;:&quot;vpnx-lr6cpqp6&quot;}</code></td>
    </tr>
    <tr>
     <td><span>VPC - <b>Direct Connect gateway</span></td>
     <td><span>DC_GW</span></td>
     <td><code>{&quot;directconnectgatewayid&quot;:&quot;dcg-8wo1p2ve&quot;}</code></td>
    </tr>
    <tr>
     <td><span>VPC - <b>peering connection</span></td>
     <td><span>vpc_region_conn</span></td>
     <td><code>{&quot;peeringconnectionid&quot;:&quot;pcx-6gw5wy11&quot;}</code></td>
    </tr>
    <tr>
     <td><span>VPC - <b>network detection</span></td>
     <td><span>NET_DETECT</span></td>
     <td><code>{&quot;appid&quot;:&quot;1258859999&quot;,&quot;netdetectid&quot;:&quot;netd-591p3g99&quot;,<br/>&quot;vpcid&quot;:&quot;vpc-mzfi69pi&quot;}</code></td>
    </tr>
    <tr>
     <td><span>VPC - <b>BWP</span></td>
     <td><span>BANDWIDTH<br/>PACKAGE</span></td>
     <td><code>{&quot;_regio_&quot;: &quot;xxx&quot;,&quot;appid&quot;: 12345,&quot;netgroup&quot;: &quot;xxx&quot;}</code></td>
    </tr>
 <tr>
<td><span>CDN - <b>project in the Chinese mainland</span></td>
<td>cdn_project</td>
<td><code>{&quot;appid&quot;:&quot;1257137149&quot;,&quot;projectid&quot;:&quot;1174789&quot;}</code></td>
</tr>
<tr>
<td><span>CDN - <b>project outside the Chinese mainland<span></td>
<td>qce/ov_cdn</td>
<td><code>{&quot;appid&quot;:&quot;1257137149&quot;,&quot;projectid&quot;:&quot;1174789&quot;}</code></td>
</tr>
<tr>
<td><span>CDN - <b>domain name in the Chinese mainland<span></td>
<td>cdn_domain</td>
<td><code>{"appid":"1257137149","domain":"cloud.tencent.com",<br/>"projectid":"1174789"}</code></td>
</tr>
<tr>
<td><span>CDN - <b>domain name outside the Chinese mainland<span></td>
<td>ov_cdn_domain</td>
<td><code>{"appid":"1257137149","domain":"cloud.tencent.com",<br/>"projectid":"1174789"}</code></td>
</tr>
<tr>
<td><span>CDN - <b>ISP by province in the Chinese mainland<span></td>
<td>ov_cdn_domain</td>
<td><code>{"appid":"1257137149","domain":"cloud.tencent.com",<br/>"projectid":"1174789","isp":"China Telecom","province":"Guangdong"}</code></td>
</tr>
 <tr>
 <td>CKafka - <b>ConsumerGroup - partition</td>
 <td>CKAFKA_CONSUM<br>ERGROUP</td>
 <td><code>{"appid":"1258344866",<br/>"consumer_group":"eslog-group22",<br/>"instance_id":"ckafka-65eago11",<br/>"topicid":"topic-4q9jjy11",<br/>"topicname":"eslog","partition":"123456"}</code></td>
 </tr>
 <tr>
 <td>CKafka - <b>ConsumerGroup - topic</td>
 <td>CONSUMERGROUP-TOPIC</td>
 <td><code>{"appid":"1258344866",<br/>"consumer_group":"eslog-group22", "instance_id":"ckafka-65eago11",<br/>"topicid":"topic-4q9jjy11", "topicname":"eslog"}</code></td>
 </tr>
  <tr>
 <td>CKafka - <b>instance</td>
 <td>CKAFKA_INSTANCE</td>
 <td><code>{"appid":"1255817890","instance_id":"ckafka-mdkk0kkk"}</code></td>
 </tr>
 <tr>
 <td>CKafka - <b>topic</td>
 <td>CKAFKA_TOPIC</td>
 <td><code>{"appid":"1258399706",<br/> "instance_id":"ckafka-r7f1rrhh",<br/>"topicid":"topic-cprg5vpp",<br/>"topicname":"topic-cluebaseserver-qb"}
</code></td>
 </tr>
    <tr>
		<td><span>CFS</span></td>
     <td><span>cfs_monitor</span></td>
     <td><code>{&quot;AppId&quot;:&quot;1258638990&quot;,&quot;FileSystemId&quot;:&quot;cfs-3e225da4p&quot;}</code></td>
    </tr>
    <tr>
     <td><span>Direct Connect - <b>connection</span></td>
     <td><span>dcline</span></td>
     <td><code>{&quot;directconnectid&quot;:&quot;dc-e1h9wqp8&quot;}</code></td>
    </tr>
    <tr>
     <td><span>Direct Connect - <b>dedicated tunnel</span></td>
     <td><span>dcchannel</span></td>
     <td><code>{&quot;directconnectconnid&quot;: &quot;dcx-jizf8hrr&quot;}</code></td>
    </tr>
   </tbody>
  </table>
