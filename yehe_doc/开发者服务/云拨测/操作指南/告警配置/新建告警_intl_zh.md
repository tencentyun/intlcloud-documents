﻿本文将为您介绍如何为各拨测类型关键指标设置告警，在指标发生异常时及时通知您。

## 操作步骤

1. 登录 [云监控控制台](https://console.cloud.tencent.com/monitor)。
2. 单击**告警配置** > **告警策略**，进入告警策略配置页面。
3. 单击**新增**，配置告警策略，配置说明如下：
<table>
  <tr>
    <th>配置类型</th>
    <th width="18%">配置项</th>
    <th>说明</th>
  </tr>
  <tr>
    <td  rowspan="4"> 基本信息</td>
    <td>策略名称</td>
    <td>自定义策略名称</td>
  </tr>
  <tr>
    <td>备注</td>
    <td>自定义策略备注</td>
  </tr>
  <tr>
    <td>监控类型</td>
    <td>选择云拨测监控类型</td>
  </tr>
  <tr>
    <td>策略类型</td>
    <td>支持网络质量、页面性能、端口性能、文件传输、音视频体验</td>
  </tr>
  <tr>
    <td rowspan="3">配置告警规则</td>
    <td>筛选条件（与）</td>
    <td>筛选出符合条件的对象进行告警检测，各筛选条件之间为 AND 关系。筛选条件仅展示有上报数据的对象。<ul>
		<li>域名（必选）：支持按域名设置告警，目前只支持选择单个域名</li>
		<li>地区：支持筛选某域名下某区域的拨测数据做告警检测</li>
		<li>城市：支持筛选某域名下某城市的拨测数据做告警检测</li>
		<li>运营商：支持筛选某域名下运营商的拨测数据做告警检测</li></ul>
		假设您在筛选了 <code>https://www.tencentcloud.com/</code> 域名和 “广东” 地区，则表示满足域名 <code>=https://www.tencentcloud.com/</code> 且地区=广东做告警检测	</td>
	<tr>
    <td>告警对象维度</td>
    <td>支持自定义告警通知内容中的告警对象，假设您选择了域名和运营商，则告警对象显示 <code>域名=xxx  运营商=xxx</code>，若不设置则默认只显示域名信息。</td>
   </tr>
		<tr>
    <td>触发条件</td>
    <td>支持满足任意条件或满足所有条件
</td>
  </tr>
		<tr>
      <td>配置告警通知</td>
      <td >通知模板</td>
            <td>系统为您默认配置通知模板，如需创建通知模板请参见 <a href="https://intl.cloud.tencent.com/document/product/248/38922">新建通知模板</a></td>
     </tr>
		<tr>
      <td>高级配置</td>
      <td >弹性伸缩</td>
      <td>启用并配置成功后，达到告警条件可触发弹性伸缩策略并进行缩容或扩容</td>
     </tr>
</table>
4. 配置完以上信息后单击**保存**，即成功创建告警策略。在指标发生异常时，将会通过您配置的告警渠道发送告警通知。
>?如需了解各指标含义，请参见 [告警指标说明](https://www.tencentcloud.com/document/product/1169/52005)。