﻿本文为您介绍云数据库 SQL Server 支持的常见监控指标。

## 监控指标
云数据库 SQL Server 监控支持 SQL Server 常见的38种参数，您可以通过配置 SSMS 的计数器，额外统计其他参数。
>?系统维度监控指标，如需查看，可通过 [在线支持](https://cloud.tencent.com/online-service?from=connect-us) 咨询。 

<table>
<thead>
<tr><th>分类</th><th>指标名</th><th>单位</th><th>指标说明</th></tr></thead>
<tbody><tr>
<td>CPU</td>
<td>CPU 利用率</td><td>%</td><td>实际 CPU 消耗的百分比</td></tr>
<tr>
<td rowspan=5>内存</td>
<td>内存使用</td><td>MB</td><td>总内存的占用大小</td></tr>
<tr>
<td>最大内存</td><td>KB</td><td>最大内存</td></tr>
<tr>
<td>内存使用率</td><td>%</td><td>内存的使用率</td></tr>
<tr>
<td>内部系统锁定内存</td><td>KBytes</td><td>内部系统的锁定内存<dx-alert infotype="notice" title="">
仅2014及以上版本支持查看此项监控指标。
</dx-alert></td></tr>
<tr>
<td>内部系统消耗内存</td><td>KBytes</td><td>内部系统的消耗内存<dx-alert infotype="notice" title="">
仅2014及以上版本支持查看此项监控指标。
</dx-alert></td></tr>
<tr>
<td rowspan=12>存储</td>
<td>磁盘 IOPS</td><td>次/秒</td><td>磁盘读写次数</td></tr>
<tr>
<td>读取磁盘次数</td><td>次/秒</td><td>每秒读取磁盘次数</td></tr>
<tr>
<td>写入磁盘次数</td><td>次/秒</td><td>每秒写入磁盘次数</td></tr>
<tr>
<td>已用存储空间</td><td>GB</td><td>实例数据库文件和日志文件占用的空间总和</td></tr>
<tr>
<td>剩余存储空间</td><td>%</td><td>硬盘剩余容量百分比，计算方式为：(购买磁盘 - 已用存储空间) / 购买磁盘</td></tr>
<tr>
<td>读 IO 平均响应时间</td><td>ms</td><td>每个读 IO 的平均响应时间（系统维度监控）</td></tr>
<tr>
<td>写 IO 平均响应时间</td><td>ms</td><td>每个写 IO 的平均响应时间（系统维度监控）</td></tr>
<tr>
<td>IO  请求平均响应时间</td><td>ms</td><td>每个 IO 请求的平均响应时间（系统维度监控）</td></tr>
<tr>
<td>磁盘每秒读 IO 数量</td><td>次/秒</td><td>磁盘每秒的读 IO 数量（系统维度监控）</td></tr>
<tr>
<td>磁盘每秒写 IO 数量</td><td>次/秒</td><td>磁盘每秒的写 IO 数量（系统维度监控）</td></tr>
<tr>
<td>磁盘 IOPS 总数</td><td>次/秒</td><td>磁盘上的 IOPS 总数（系统维度监控）</td></tr>
<tr>
<td>磁盘队列长度</td><td>个</td><td>磁盘队列长度  （系统维度监控）</td></tr>
<tr>
<td rowspan=4>网络</td>
<td>输入流量</td><td>KB/s</td><td>所有连接输入包大小总和</td></tr>
<tr>
<td>输出流量</td><td>KB/s</td><td>所有连接输出包大小总和</td></tr>
<tr>
<td>平均网络 IO 延迟</td><td>ms</td><td>平均网络 IO 延迟时间</td></tr>
<tr>
<td>RO 同步延迟时间</td><td>秒</td><td>主实例和只读实例间的数据同步延迟时间</td></tr>
<tr>
<td rowspan=3>连接</td>
<td>连接数</td><td>个</td><td>平均每秒用户连接数据库的个数</td></tr>
<tr>
<td>每秒登录次数</td><td>次/秒</td><td>每秒登录次数</td></tr>
<tr>
<td>每秒登出次数</td><td>次/秒</td><td>每秒登出次数</td></tr>
<tr>
<td rowspan=9>访问</td>
<td>慢查询</td><td>个</td><td>运行时间超过一秒的查询数量</td></tr>
<tr>
<td>请求数</td><td>次/秒</td><td>平均每秒的请求数</td></tr>
<tr>
<td>SQL  编译数</td><td>次/秒</td><td>平均每秒 SQL 编译次数</td></tr>
<tr>
<td>SQL  重编译数</td><td>次/秒</td><td>平均每秒 SQL 重编译次数</td></tr>
<tr>
<td>每秒钟 SQL 做全表扫描数目</td><td>次/秒</td><td>每秒钟 SQL 做全表扫描数目</td></tr>
<tr>
<td>事务数</td><td>次/秒</td><td>平均每秒的事务数</td></tr>
<tr>
<td>阻塞数</td><td>个</td><td>当前阻塞数量</td></tr>
<tr>
<td>执行缓存缓存命中率</td><td>%</td><td>每个 SQL 有一个执行计划，执行计划的命中率</td></tr>
<tr>
<td>缓冲区缓存命中率</td><td>%</td><td>数据缓存（内存）命中率</td></tr>
<tr>
<td rowspan=5>锁</td>
<td>锁请求次数</td><td>次/秒</td><td>平均每秒锁请求的次数</td></tr>
<tr>
<td>每秒闩锁等待数量</td><td>次/秒</td><td>每秒闩锁等待数量</td></tr>
<tr>
<td>平均锁等待延迟</td><td>Ms</td><td>每个导致等待的锁请求的平均等待时间</td></tr>
<tr>
<td>死锁数</td><td>个/秒</td><td>每秒导致死锁的锁请求数</td></tr>
<tr>
<td>阻塞报告生成阈值</td><td>秒</td>
<td>所指定的生成阻塞报告的阈值，超过该阈值将生成阻塞的进程报告，默认情况下，不生成阻塞的进程报告</td></tr>
<tr>
<td>其他</td>
<td>用户错误数</td><td>次/秒</td><td>平均每秒错误数</td></tr>
</tbody></table>
