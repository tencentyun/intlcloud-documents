ECDN 状态码统计为您提供状态码监控数据查询功能。您可以登录 [ECDN 控制台](https://console.cloud.tencent.com/dsa)，在左侧菜单中，单击【统计分析】，进入 [状态码统计](https://console.cloud.tencent.com/dsa/statistics/status) 页面体验该功能。

## 查询条件说明
+ 时间选择：支持查询历史12个自然月的数据，查询跨度最大为31天。
+ 项目：支持按照项目维度查询使用量。
+ 域名：支持指定域名查询使用量。
+ 时间间隔：指查询数据展示的时间间隔，与所选时间跨度有关：
	1. 所选时间跨度为1天，您可以查询每5分钟、15分钟、30分钟、1小时、2小时、4小时、24小时时间间隔的数据。
	2. 所选时间跨度为2 - 3天，您可以查询每15分钟、30分钟、1小时、2小时、4小时时间间隔的数据。
	3. 所选时间跨度为4 - 7天，您可以查询每30分钟、1小时、2小时、4小时时间间隔的数据。
	4. 所选时间跨度为8 - 30天，您可以查询每1小时、2小时、4小时、24小时时间间隔的数据。
	

![](https://main.qcloudimg.com/raw/58dccdea420d816b3be6bcc4a4502920.png)

## 状态码数据展示说明
状态码数据使用状态码分布饼图和状态码趋势曲线两种展示方式，所有数据均可支持导出。
- 30天内接入的域名，都会纳入【全部域名】下拉框中，包括已删除的域名。
- 当日实时监控数据延迟在5分钟左右，即如果执行查询操作的时刻为14:26:00，则查询结果一般统计的是当日00:00:00至14:21:00的数据。
- 监控数据统计时，以查询间隔为时间段，向前划归统计。例如当查询时间间隔为5分钟时，10:00:00 - 10:04:59之间的统计数据，会划归到10:00:00这个统计点上。
- 当指定查询时间区间大于域名接入时间区间时，仅统计域名接入时间段的数据，未接入或已删除时间段不纳入统计。
- 当需要查询多个域名、多个指标的监控数据时，您还可以使用监控数据查询 API查询。

![](https://main.qcloudimg.com/raw/745bd6a24240811422187aa3433b1438.png)



## 状态码及状态码含义说明
<table>
   <tr>
      <th style="text-align: center">类别</th>
      <th style="text-align: center">状态码</th>
      <th style="text-align: center">状态码含义</th>
      <th style="text-align: center">处理建议</th>
   </tr>
   <tr>
      <td rowspan="2">2XX</td>
      <td>200</td>
      <td>访问成功。</td>
      <td rowspan="2">2XX 类别状态码一般表示访问正常状态。</td>
   </tr>
   <tr>
      <td>206</td>
      <td>访问成功。</td>
   </tr>
   <tr>
      <td rowspan="3">3XX</td>
      <td>301</td>
      <td>访问内容已永久迁移。</td>
      <td rowspan="3">3XX 类别状态码一般表示访问正常状态。</td>
   </tr>
    <tr>
      <td>302</td>
      <td>访问重定向。</td>
   </tr>
   <tr>
      <td>304</td>
      <td>访问内容未发生改变。</td>
   </tr>
   <tr>
      <td rowspan="6">4XX</td>
      <td>400</td>
      <td>请求参数有误。</td>
      <td rowspan="6">4XX 类别状态码一般表示客户端请求错误，或域名已停止加速服务。</td>
   </tr>
   <tr>
       <td>401</td>
       <td>访问请求验证失败。</td>
   </tr>
   <tr>
      <td>403</td>
      <td>内容禁止访问。</td>
   </tr>
   <tr>
      <td>404</td>
      <td>请求内容未发现。</td>
   </tr>
   <tr>
      <td>405</td>
      <td>请求方法不支持。</td>
   </tr>
   <tr>
      <td>416</td>
      <td>Range 范围不合法。</td>
   </tr>
   <tr>
      <td rowspan="10">5XX</td>
      <td>500</td>
      <td>服务器内部错误。</td>
      <td rowspan="2">请先确认源站服务是否异常，若源站服务无异常，请<a href='https://console.cloud.tencent.com/workorder/category'> 提交工单 </a>处理。</td>
   </tr>
   <tr>
      <td>502</td>
      <td>服务器当前无法服务。</td>
   </tr>
    <tr>
      <td>501</td>
      <td>此请求方法不被服务器支持且无法被处理。</td>
      <td>请确认请求方法。</td>
   </tr>
    <tr>
      <td>513</td>
      <td>ECDN 边缘过载，通常是客户请求数突发或被 cc 攻击。</td>
      <td>请确认域名业务是否正常突发。</td>
   </tr>
    <tr>
      <td>522</td>
      <td>针对 HTTP 的 ECDN 内部建连失败或 ECDN 回源建连接失败。</td>
      <td>请先确认源站80端口是否开放。</td>
   </tr>
   <tr>
      <td rowspan="2">529</td>
			<td >新增域名，路由配置还未生效</td>
      <td>平台配置部署时间约5 - 10分钟，请您确认配置生效后再切换 CNAME 解析。</td>
   </tr>
	 <tr>
     <td >源站禁 ping，无法探测到回源路由信息。</td>
      <td>需要您为 ECDN 回源节点开放 ping 权限，您可以 <a href='https://console.cloud.tencent.com/workorder/category'> 提交工单 </a> 获取 ECDN 回源节点 IP 列表。</td>
   </tr>
   </tr>
    <tr>
      <td>533</td>
      <td>ECDN 边缘与 ECDN 中转传输失败，读取超时或建连失败。</td>
      <td>请<a href='https://console.cloud.tencent.com/workorder/category'> 提交工单 </a>联系我们处理。</td>
   </tr>
    <tr>
      <td>538</td>
      <td>针对 HTTPS 的 SSL 握手失败，ECDN 内部传输失败或 ECDN 回源 SSL 握手失败。</td>
      <td>请先确认源站443端口是否开放，是否能正常 SSL 握手。</td>
   </tr>
    <tr>
      <td>564</td>
      <td>ECDN 回源超时。</td>
      <td>请先查看源站出口网络是否波动。</td>
   </tr>
   <tr>
      <td>其它</td>
      <td>0</td>
      <td>响应内容时，客户端主动关闭连接。</td>
      <td>一般为客户端网络问题或客户主动中止访问导致。</td>
   </tr>
</table>
