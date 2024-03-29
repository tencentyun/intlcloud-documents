云顾问的巡检项包含安全、可靠、服务限制、成本及性能五个维度。

## 安全[](id:Safety)
通过建议您启用腾讯云安全功能以及检查权限，提高系统和业务的安全性。

<table>
   <tr>
      <th>产品</th>
      <th>巡检项</th>
      <th>巡检说明</th>
   </tr>
   <tr>
      <td> 网络 ACL</td>
      <td> 网络 ACL 开放公网可访问权限</td>
      <td> 检查网络 ACL 是否放通全量、或者放通除 80、443 以外端口的源 IP 入站访问限制。若放通，容易产生如非法访问、拒绝服务攻击等安全风险。</td>
   </tr>
   <tr>
      <td rowspan="2"> 访问管理（CAM）</td>
      <td> 访问管理（CAM）账号是否绑定 MFA 设备</td>
      <td> 判断账号是否绑定 MFA 设备。如未绑定，登录账号无需 MFA 动态验证码二次验证，安全系数低。</td>
   </tr>
   <tr>
      <td> 访问管理（CAM）是否开启账号保护功能</td>
      <td> 判断登录操作保护、敏感操作保护、异地登录保护等功能是否开启。如未开启，那么相应操作无需二次验证，安全系数低。</td>
   </tr>
   <tr>
      <td> 内容分发网络（CDN）</td>
      <td> 内容分发网络（CDN）IP 访问限频</td>
      <td> 如果不开通，无法通过对单 IP 单节点在每一秒钟的访问次数进行限制，可能受到高频 CC 攻击、恶意用户盗刷等。 </td>
   </tr>
   <tr>
      <td> 云防火墙（CFW）</td>
      <td> 云防火墙（CFW）资源防护检查</td>
      <td> 检查云防火墙防护策略，若资源类型为 CVM/NAT/VPN/CLB 的实例未开启，则提示风险。</td>
   </tr>
   <tr>
      <td> 负载均衡（CLB）</td>
      <td> 负载均衡（CLB）实例绑定证书到期</td>
      <td> 检查负载均衡（CLB）实例绑定证书到期情况。</td>
   </tr>
   <tr>
      <td rowspan="4"> 对象存储（COS）</td>
      <td> 对象存储（COS）子账号访问不受限制</td>
      <td> 检查 COS 存储桶子账号权限范围，若子账号具有完全控制存储桶的权限，则存储桶可能存在安全风险。</td>
   </tr>
   <tr>
      <td> 对象存储（COS）存储桶公有读写</td>
      <td> 检查 COS 存储桶公有读写权限，若设置了公有读写权限，匿名用户组可直接读、写存储桶，存储桶存在非常大的安全风险，不建议在存储桶赋予此权限。</td>
   </tr>
   <tr>
      <td> 对象存储（COS）存储桶 CORS 配置</td>
      <td> 检查存储桶 CORS 配置， 若已存在 CORS 规则且未配置 CORS Allow-Headers/Expose-Headers 头部，可能导致跨域访问请求失败。</td>
   </tr>
   <tr>
      <td> 对象存储（COS）存储桶防盗链（Referer）配置</td>
      <td> 检查 COS 存储桶权限 和 Referer 配置，当存储桶权限为允许匿名用户访问，且未配置或者配置了空 Referer 访问规则，可能受到恶意用户盗刷等。 </td>
   </tr>
   <tr>
      <td rowspan="2"> 主机安全（CWP）</td>
      <td> 主机安全（CWP）漏洞未修复</td>
      <td> 检查是否有主机存在漏洞未修复，若存在漏洞未修复，将大幅增加主机失陷、数据丢失风险。</td>
   </tr>
   <tr>
      <td> 主机安全（CWP）客户端离线</td>
      <td> 检查主机安全客户端是否离线，若安全客户端离线，主机将失去安全防护能力。</td>
   </tr>
   <tr>
      <td> 云原生数据库 TDSQL-C </td>
      <td> 云原生数据库 TDSQL-C MySQL 版 root 账号安全</td>
      <td> 检查账号配置，若只存在 root 账号，没有其他应用账号，说明权限过大，存在误操作或恶意操作影响数据安全的风险。</td>
   </tr>
   <tr>
      <td rowspan="2"> DDoS 防护（Anti-DDoS）</td>
      <td> DDoS 防护（Anti-DDoS）可用 IP 黑洞解封次数检查</td>
      <td> 检查黑洞解封次数使用占比是否过大。 </td>
   </tr>
   <tr>
      <td> DDoS 防护（Anti-DDoS）被封堵的公网 IP 检查 </td>
      <td> 检查是否有公网 IP（EIP）因 DDoS 攻击被封堵。</td>
   </tr>
   <tr>
      <td rowspan="2"> TDSQL MySQL 版</td>
      <td> TDSQL MySQL 版账号高危命令限制</td>
      <td> 检查账号配置，若所有账号都拥有全局命令权限 DROP 和 DELETE，容易出现数据误删除或恶意删除风险。</td>
   </tr>
   <tr>
      <td> TDSQL MySQL 版公网安全策略检查</td>
      <td> 检查公网安全策略，若开放公网访问且没有配置安全组规则，有受到外网攻击导致应用异常或数据安全风险。</td>
   </tr>
   <tr>
      <td rowspan="2"> Elasticsearch Service </td>
      <td> Elasticsearch 集群公网访问策略</td>
      <td> 检查 Elasticsearch 集群公网访问策略，若未配置任何限制，则提示集群可能存在访问风险，且外网访问有带宽限制。</td>
   </tr>
   <tr>
      <td> Elasticsearch 集群的 Kibana 组件公网访问策略</td>
      <td> 检查 Elasticsearch 集群的 Kibana 组件公网访问策略，若未配置任何限制，则提示 Kibana 可能存在访问风险。</td>
   </tr>
   <tr>
      <td rowspan="3"> 云数据库（MySQL）</td>
      <td> 云数据库（MySQL）root 账号安全</td>
      <td> 检查 MySQL 账号配置，若只存在 root 账号，没有其他应用账号，说明权限过大，存在误操作或恶意操作影响数据安全的风险。</td>
   </tr>
   <tr>
      <td> 云数据库（MySQL）非 root 账号高危命令限制</td>
      <td> 检查 MySQL 非 root 账号权限范围，若应用账号拥有高危命令权限，如 DROP，DELETE 等，容易出现数据误删除或恶意删除风险。</td>
   </tr>
   <tr>
      <td> 云数据库（MySQL）公网安全策略检查</td>
      <td> 检查 MySQL 公网安全策略，若开放公网访问且没有配置安全组规则，有受到外网攻击，导致应用异常或数据安全风险。</td>
   </tr>
   <tr>
      <td> 云数据库（Redis）</td>
      <td> 云数据库（Redis）高危命令检查</td>
      <td> 检查 Redis 实例禁用命令配置，若高危命令未禁用，容易出现应用阻塞，数据误删等风险。</td>
   </tr>
   <tr>
      <td> 安全组（SG）</td>
      <td> 安全组（SG）开放公网可访问权限</td>
      <td> 检查安全组是否放通全量，或者放通除 80、443 以外端口的源 IP 入站访问限制。若放通，容易产生如非法访问、拒绝服务攻击等安全风险。</td>
   </tr>
   <tr>
      <td rowspan="2"> 云数据库（MariaDB）          </td>
      <td> 云数据库（MariaDB）账号高危命令限制</td>
      <td> 检查账号配置，若所有账号都拥有全局命令权限 DROP 和 DELETE，容易出现数据误删除或恶意删除风险。</td>
   </tr>
   <tr>
      <td> 云数据库（MariaDB）公网安全策略检查</td>
      <td> 检查公网安全策略，若开放公网访问且没有配置安全组规则，有受到外网攻击导致应用异常或数据安全风险。</td>
   </tr>
</table>

## 可靠[](id:reliable)

通过多方位监控，维护实例的运行稳定性。

<table>
   <tr>
      <th>产品</th>
      <th>巡检项</th>
      <th>巡检说明</th>
   </tr>
   <tr>
      <td rowspan="2"> 云硬盘（CBS）</td>
      <td> 云硬盘（CBS）存储容量</td>
      <td> 检查云硬盘（CBS）的存储容量使用情况，若已使用容量占总容量比率过高，会导致云硬盘读写受到影响。</td>
   </tr>
   <tr>
      <td> 云硬盘（CBS）未创建快照</td>
      <td> 检查 CBS 是否有创建快照或定期快照策略，若均无，服务器或云硬盘出现问题时数据找回非常困难，易造成较大损失。</td>
   </tr>
   <tr>
      <td> 消息队列（CKafka）</td>
      <td> 消息队列（CKafka）跨可用区部署</td>
      <td> 如果没有跨可用区部署，单可用区集群出现严重故障的情况下，可能会导致 CKafka 集群不可用。</td>
   </tr>
   <tr>
      <td rowspan="10"> 负载均衡（CLB）</td>
      <td> 负载均衡（CLB）及其绑定的 CVM 跨区</td>
      <td> 检查 CLB 及其绑定的 CVM 实例是否在同一个可用区，如果不是，跨区转发可能影响服务可靠性，如降低部分转发请求的速度。</td>
   </tr>
   <tr>
      <td> 负载均衡（CLB）后端服务单点 </td>
      <td> 检查 CLB 监听器或转发规则绑定的如 CVM、EVM 等类型的后端服务实例，如果只有一个，存在单点隐患。</td>
   </tr>
   <tr>
      <td> 负载均衡（CLB）转发规则绑定 CVM 多个端口</td>
      <td> 检查 CLB 同一转发规则是否绑定同一台 CVM 的多个端口。若是，随着业务量的增长，进程间的资源争抢会增加排障难度，同时多个端口可能会降低系统对流量波峰的抵御能力。</td>
   </tr>
   <tr>
      <td> 负载均衡（CLB）下的 CVM 跨子网</td>
      <td> 检查 CLB 同一监听器或转发规则绑定的多个 CVM 实例是否跨 VPC 子网。若是，在异常发生情况不利于快速排障。</td>
   </tr>
   <tr>
      <td> 负载均衡（CLB）下的 CVM 权重</td>
      <td> 检查 CLB 同一监听器或转发规则关联的 CVM 权重，如果出现相同配置不同权重，或相同权重不同配置的情况，则可能在业务高峰时暴露性能短板的风险，影响业务稳定 。</td>
   </tr>
   <tr>
      <td> 负载均衡（CLB）健康检查配置</td>
      <td> 检查 CLB 是否配置健康检查，若未配置健康检查，CLB 将向所有后端服务器转发流量（包括异常的后端服务器）。</td>
   </tr>
   <tr>
      <td> 负载均衡（CLB）转发规则配置</td>
      <td> 检查 CLB 监听器配置， 若未配置转发规则，则无法正常使用 CLB 功能，产生额外成本。</td>
   </tr>
   <tr>
      <td> 负载均衡（CLB）健康检查存在跳变情况 </td>
      <td> 检查 CLB 监听器的健康检查是否有跳变情况，即是否存在服务器端口状态异常。</td>
   </tr>
   <tr>
      <td> 负载均衡（CLB）实例类型</td>
      <td> 检查 CLB 实例类型为传统型还是应用型，应用型功能更加丰富，如每个四层监听器可以配置不同的后端服务、支持七层监听器、支持 CLS 日志、SNI、绑定弹性网卡等多种特性。</td>
   </tr>
   <tr>
      <td> 负载均衡（CLB）带宽上限为 1Mbps</td>
      <td> 为避免购买时未选择 CLB 带宽（默认1Mbps），对账号下 1Mbps 限速的 CLB 进行扫描，如果出现大流量业务使用该类限速 CLB 的情况，可能会导致严重丢包现象。</td>
   </tr>
   <tr>
      <td rowspan="2"> 对象存储（COS）</td>
      <td> 对象存储（COS）存储桶版本控制</td>
      <td> 检查 COS 存储桶的版本控制配置，若未处于启用版本控制状态，则有可能存在数据丢失的风险。</td>
   </tr>
   <tr>
      <td> 对象存储（COS）存储桶日志管理配置</td>
      <td> 检查 COS 存储桶日志管理功能，若目标存储桶与源存储桶的所有者不同，则会导致存储桶日志投递失败。</td>
   </tr>
   <tr>
      <td rowspan="4"> 云服务器（CVM）</td>
      <td> 云服务器（CVM）系统盘快照</td>
      <td> 检查 CVM 系统盘快照，若未创建快照，服务器或云硬盘出现问题时数据找回非常困难，易造成较大损失。 </td>
   </tr>
   <tr>
      <td> 云服务器（CVM）实例磁盘空间使用率过高</td>
      <td> 检查 CVM 实例磁盘使用情况，若使用率过高，则磁盘读写会受到影响 。</td>
   </tr>
   <tr>
      <td> 云服务器（CVM）实例本地盘类型检查</td>
      <td> 检查 CVM 实例使用本地盘的情况，若实例为非 IO 或大数据类型，且使用了本地盘，则磁盘数据无法通过快照备份，存在容灾风险。</td>
   </tr>
   <tr>
      <td> 云服务器（CVM）带宽利用率过高</td>
      <td> 检查 CVM 实例带宽利用率情况，若带宽利用率过高，则网络性能可能会受到影响。</td>
   </tr>
   <tr>
      <td> DDoS 防护（Anti-DDoS）</td>
      <td> DDoS 防护（Anti-DDoS）L7 转发规则健康检查</td>
      <td> 检查当前7层转发规则健康检查是否存在异常。</td>
   </tr>
   <tr>
      <td> TDSQL MySQL 版</td>
      <td> TDSQL MySQL 版容灾情况 </td>
      <td> 检查灾备实例的配置，若未配置，当实例出现严重故障时，业务访问可能受影响。</td>
   </tr>
   <tr>
      <td> 弹性公网 IP（EIP）</td>
      <td> 弹性公网 IP（EIP）带宽限速 1Mbps</td>
      <td> 为避免购买时未选择 EIP 带宽（默认1Mbps），对账号下 1Mbps 限速的 EIP 进行扫描，如果出现大流量业务使用该类 EIP 的情况，可能会导致严重丢包现象。</td>
   </tr>
   <tr>
      <td> Elasticsearch Service </td>
      <td> Elasticsearch 集群自动快照备份</td>
      <td> 检查 Elasticsearch 集群自动快照备份配置，若未配置，则提示风险。</td>
   </tr>
   <tr>
      <td rowspan="7"> 云直播（CSS）</td>
      <td> 云直播（CSS）是否使用直播码模式</td>
      <td> 检查业务时候有使用直播码模式，当业务使用非直播码模式时，则提示风险。</td>
   </tr>
   <tr>
      <td> 云直播（CSS）域名 CNAME 解析到专有域名</td>
      <td> 域名 CNAME 配置错误会影响云直播的正常推流和播放，如未 CNAME 到正确的值，则提示风险。 </td>
   </tr>
   <tr>
      <td> 云直播（CSS）推流域名包含父子域名</td>
      <td> 子级域名是父级域名的下级域名，云直播的域名是 CNAME 到泛域名的，必要时会对域名进行实例化，若父级域名实例化但子级域名未实例化，则会影响子级域名的正常解析。 </td>
   </tr>
   <tr>
      <td> 云直播（CSS）播放域名包含父子域名</td>
      <td> 子级域名是父级域名的下级域名，云直播的域名是 CNAME 到泛域名的，必要时会对域名进行实例化，若父级域名实例化但子级域名未实例化，则会影响子级域名的正常解析。</td>
   </tr>
   <tr>
      <td> 云直播（CSS）推流开启鉴权</td>
      <td> 检查是否开启推流鉴权且是否配置了直播回调，均未开启则提示风险。</td>
   </tr>
   <tr>
      <td> 云直播（CSS）SSL 证书有效期</td>
      <td> 如果证书过期，影响 HTTPS 访问有效性，HTTPS 访问会出现无法访问的情况。</td>
   </tr>
   <tr>
      <td> 云直播（CSS）带宽超过封顶配置值</td>
      <td> 检查带宽封顶是否开启，若开启则检查当前带宽是否即将到顶，带宽触顶后将限制新增用户的访问。</td>
   </tr>
   <tr>
      <td rowspan="3"> 云数据库（MongoDB）</td>
      <td> 云数据库（MongoDB）oplog 保存时间</td>
      <td> 检查 MongoDB oplog 保存时间，若保存时间过短，会导致回档失败或影响问题排查。</td>
   </tr>
   <tr>
      <td> 云数据库（MongoDB）备份是否成功</td>
      <td> 检查 MongoDB 备份是否成功，如果备份任务失败，可能导致无法恢复数据。</td>
   </tr>
   <tr>
      <td> 云数据库（MongoDB）使用基础网络</td>
      <td> 检查 MongoDB 是否使用基础网络。</td>
   </tr>
   <tr>
      <td rowspan="5"> 云数据库（MySQL）    </td>
      <td> 云数据库（MySQL）容灾情况</td>
      <td> 检查 MySQL 灾备实例的配置，若未配置，当实例出现严重故障时，业务访问可能受影响。</td>
   </tr>
   <tr>
      <td> 云数据库（MySQL）主从延迟</td>
      <td> 检查 MySQL 主从延迟情况，若延迟过高，可能会导致数据库 RO 实例被剔除，主从 HA 切换时间过长等风险。</td>
   </tr>
   <tr>
      <td> 云数据库（MySQL）跨可用区部署</td>
      <td> 检查 MySQL 是否跨可用区部署，如果实例没有跨可用区部署，当实例所在可用区出现严重故障时，数据库会出现无法访问的风险。</td>
   </tr>
   <tr>
      <td> 云数据库（MySQL）RO 组单点</td>
      <td> 检查 MySQL RO 组是否单点，当 RO 组 中只有一个实例时，该实例故障会导致只读业务不可用。</td>
   </tr>
   <tr>
      <td> 云数据库（MySQL）使用基础网络 </td>
      <td> 检查 MySQL 是否使用基础网络。 </td>
   </tr>
   <tr>
      <td rowspan="2"> 云数据库（Redis）</td>
      <td> 云数据库（Redis）跨可用区部署 </td>
      <td> 检查 Redis 实例是否跨可用区部署，如果实例未跨可用区部署，当实例出现可用区级别的灾难故障时，可能造成实例无法访问风险。</td>
   </tr>
   <tr>
      <td> 云数据库（Redis）使用基础网络</td>
      <td> 检查 Redis 是否使用基础网络。</td>
   </tr>
   <tr>
      <td> 安全组（SG）</td>
      <td> 安全组（SG）存在冗余规则 。</td>
      <td> 检查没有生效的安全组规则，无效规则容易占用有限额度，可能导致无法新建规则，对业务使用产生限制。无效规则可以是重复的、端口有包含关系的规则 。</td>
   </tr>
   <tr>
      <td rowspan="3"> 消息队列（TDMQ）</td>
      <td> 消息队列（TDMQ）集群健康状态检查</td>
      <td> 非健康状态下，集群使用可能面临一定风险。</td>
   </tr>
   <tr>
   <td> 消息队列（TDMQ）备份消费者检查</td>
      <td> 检查是否只有一个消费者，如果采用单个消费者消费，单点挂了会影响消费业务。 </td>
   </tr>
   <tr>
   <td> 消息队列（TDMQ）死信队列检查</td>
      <td> 如果没有死信队列，消费者可能无法处理一些特殊情况的消息。</td>
   </tr>
   <tr>
      <td rowspan="2"> 云数据库（MariaDB）</td>
      <td> 云数据库（MariaDB）主从延迟</td>
      <td> 当主从延迟持续过大时，主从数据一致性将得不到保障，此时如果实例发生了 HA 主从切换，极端情况下数据可能出现丢失。</td>
   </tr>
   <tr>
      <td> 云数据库（MariaDB）容灾情况</td>
      <td> 检查 MariaDB 灾备实例的配置，若未配置，当实例出现严重故障时，业务访问可能受影响 。</td>
   </tr>
   <tr>
      <td> 容器服务（TKE）</td>
      <td> 容器服务（TKE）集群节点跨可用区 </td>
      <td> 集群节点是否都在单一可用区，单一可用区不可用时影响业务，集群无法调度到其他可用区。</td>
   </tr>
   <tr>
      <td rowspan="10"> 实时音视频（TRTC）</td>
      <td> 实时音视频（TRTC）Native SDK 终端版本分布情况</td>
      <td> 检查 Native SDK 终端版本情况，若版本较低，可能会导致质量上的不稳定。</td>
   </tr>
   <tr>
      <td> 实时音视频（TRTC）Web SDK 终端版本分布情况</td>
      <td> 检查 Web SDK 终端版本情况，若版本较低，可能会导致质量上的不稳定。</td>
   </tr>
   <tr>
      <td> 实时音视频（TRTC）Native SDK 视频码率设置是否合理</td>
      <td> 检查 Native SDK 视频码率，视频参数需要考虑画质和流畅的平衡，配置合理的视频参数将带来更好的用户体验。</td>
   </tr>
   <tr>
      <td> 实时音视频（TRTC）Native SDK 场景选择是否一致</td>
      <td> 检查同一房间号中是否出现多个通话场景，若通话场景不统一可能出现预期外的结果。</td>
   </tr>
   <tr>
      <td> 实时音视频（TRTC）Native SDK 拉流时序是否正确</td>
      <td> 检查 Native SDK 拉流时序, 在对面视频流还未到达时拉流会导致概率性的黑屏。</td>
   </tr>
   <tr>
      <td> 实时音视频（TRTC）Native SDK 退房逻辑是否正确</td>
      <td> 检查 Native SDK 退房逻辑，若退房时机不当，会导致 SDK 内部状态混乱，容易引起异常。</td>
   </tr>
   <tr>
      <td> 实时音视频（TRTC）是否开启后付费</td>
      <td> 检查是否开启后付费，如果未开启，套餐包用完将停服。</td>
   </tr>
   <tr>
      <td> 实时音视频（TRTC）Native SDK 视频辅路流码率设置是否合理</td>
      <td> 检查 Native SDK 辅路视频码率，视频参数需要考虑画质和流畅的平衡，码率配置过低会导致画面不清晰，过高弱网络情况下可能会导致卡顿。</td>
   </tr>
   <tr>
      <td> 实时音视频（TRTC）Native SDK 进房场景和角色是否一致</td>
      <td> 检查 Native SDK 应用场景选择与角色配置是否一致，例如视频通话场景和语音通话场景无需设置观众角色，若不一致可能会导致画面卡顿、黑屏等问题。</td>
   </tr>
   <tr>
      <td> 实时音视频（TRTC）Native SDK 同一个 userId 互踢</td>
      <td> 检查 Native SDK 是否存在同一个 userId 进到同一个房间造成的互踢问题，此情况可能会导致黑屏、卡顿等问题。</td>
   </tr>
   <tr>
      <td> 私有网络（VPC）</td>
      <td> 私有网络（VPC）子网规划</td>
      <td> 检查子网网段与 VPC 网段是否一致，如果完全一致，导致不能规划更多子网使用，不利于跨区拓展等长期规划实施。</td>
   </tr>
   <tr>
      <td> 私有网络 VPN 网关（VPNGW）</td>
      <td> 私有网络 VPN 网关（VPNGW）到期时间不足 1 个月</td>
      <td> 检查 VPNGW 付费类型，若类型为手动续费或到期不续费，且临近过期，容易导致 VPNGW 服务不可用，影响业务。</td>
   </tr>
   <tr>
      <td> 私有网络 VPN</td>
      <td> 私有网络 VPN 通道状态</td>
      <td> 检查是否存在未联通状态的 VPN 通道，如果执行备用通道切换，可能导致切换失败。</td>
   </tr>
</table>



## 服务限制[](id:ServiceRestrictions)


通过监控可提供的服务资源的最大数量，提醒您按照建议删除资源或请求增加配额。

<table>
   <tr>
      <th>产品</th>
      <th>巡检项</th>
      <th>巡检说明</th>
   </tr>
   <tr>
      <td> 云防火墙（CFW）</td>
      <td> 云防火墙（CFW）规则配额检查</td>
      <td> 检查云防火墙规则列表配额，若配额不足，则提示风险。</td>
   </tr>
   <tr>
      <td> 云服务器（CVM）</td>
      <td> 云服务器（CVM）实例到期</td>
      <td> 检查 CVM 到期情况，若付费类型为包年包月的实例即将到期，且未配置自动续费，则在到期后存在实例被销毁的风险。</td>
   </tr>
   <tr>
      <td> 云原生数据库 TDSQL-C </td>
      <td> 云原生数据库 TDSQL-C MySQL 版到期</td>
      <td> 检查集群的到期情况，若类型为包年包月的集群即将到期，且未配置自动续费，过期后可能会导致业务访问受损。</td>
   </tr>
   <tr>
      <td> TDSQL MySQL 版</td>
      <td> TDSQL MySQL 版实例到期</td>
      <td> 检查实例的到期情况，若类型为包年包月的实例即将到期且未配置自动续费，过期后可能会导致业务访问受损。</td>
   </tr>
   <tr>
      <td> DNS 解析 DNSPod</td>
      <td> DNS 解析 DNSPod 付费套餐两月内到期且未设置自动续费</td>
      <td> 检查付费套餐是否两月内到期且未设置自动续费，如果未设置，套餐用完将立即停服。</td>
   </tr>
   <tr>
      <td> 域名（Domain）</td>
      <td> 域名（Domain）到期</td>
      <td> 检查域名的到期情况，未配置自动续费的域名过期后可能会导致业务访问受损。</td>
   </tr>
   <tr>
      <td> 弹性公网 IP（EIP）</td>
      <td> 弹性公网 IP（EIP）使用量</td>
      <td> 检查 EIP 在各个地域的使用量，若临近配额或超过配额，容易导致无法申请 EIP 使用。</td>
   </tr>
   <tr>
      <td rowspan="2"> 云数据库（MongoDB）</td>
      <td> 云数据库（MongoDB）实例到期 </td>
      <td> 检查 MongoDB 实例的到期情况，若类型为包年包月的实例即将到期，且未配置自动续费，过期后可能会导致业务访问受损。</td>
   </tr>
   <tr>
      <td> 云数据库（MongoDB）存储容量 </td>
      <td> 检查 MongoDB 存储容量的使用情况，当容量使用率达到 100% 时，将会导致写入失败。</td>
   </tr>
   <tr>
      <td rowspan="4"> 云数据库（MySQL）</td>
      <td> 云数据库（MySQL）实例到期</td>
      <td> 检查 MySQL 实例的到期情况，若类型为包年包月的实例即将到期，且未配置自动续费，过期后可能会导致业务访问受损。</td>
   </tr>
   <tr>
      <td> 云数据库（MySQL）连接使用率</td>
      <td> 检查 MySQL 实例连接使用率情况，当连接使用率达到100%，业务将出现连接数据库失败的风险。</td>
   </tr>
   <tr>
      <td> 云数据库（MySQL）磁盘使用率</td>
      <td> 检查 MySQL 实例磁盘使用率情况，若磁盘使用率过高，有可能会出现数据无法写入风险。</td>
   </tr>
   <tr>
      <td> 云数据库（MySQL）磁盘空间接近 6T 上限</td>
      <td> 检查 MySQL 磁盘空间是否接近 6T 上限。</td>
   </tr>
   <tr>
      <td> NAT 网关</td>
      <td> NAT 网关配置 DNAT 的使用量</td>
      <td> 检查 NAT 网关 DNAT 的使用情况，若使用量接近上限，可能会影响后续新业务部署。</td>
   </tr>
   <tr>
      <td rowspan="3"> 云数据库（Redis）</td>
      <td> 云数据库（Redis）实例到期 </td>
      <td> 检查 Redis 实例的到期情况，若类型为包年包月的实例即将到期，且未配置自动续费，如果业务继续使用，可能有访问失败风险。</td>
   </tr>
   <tr>
      <td> 云数据库（Redis）内存接近 4T 上限</td>
      <td> 检查 Redis 实例内存是否接近 4T 上限。</td>
   </tr>
   <tr>
      <td> 云数据库（Redis）副本数达到上限 5 个</td>
      <td> 检查 Redis 实例副本数是否达到上限 5 个。</td>
   </tr>
   <tr>
      <td rowspan="3"> 云数据库（MariaDB）</td>
      <td> 云数据库（MariaDB）连接使用率</td>
      <td> 当连接数使用率 100% 的时候，新增请求将无法建立连接，访问失败。</td>
   </tr>
   <tr>
      <td> 云数据库（MariaDB）数据盘使用率</td>
      <td> 当磁盘使用率达到 100% 时，写入将会失败。</td>
   </tr>
   <tr>
      <td> 云数据库（MariaDB）实例到期</td>
      <td> 检查 MariaDB 实例的到期情况，若类型为包年包月的实例即将到期且未配置自动续费，过期后可能会导致业务访问受损。 </td>
   </tr>
   <tr>
      <td> 私有网络（VPC）</td>
      <td> 私有网络（VPC）路由表使用数量</td>
      <td> 检查 VPC 路由表的数量，若接近或超过上限值，容易导致无法及时建立新的路由表。</td>
   </tr>
</table>

## 成本[](id:cost)

根据运行情况，给出性价比更高的配置建议，降低您的成本花费。

<table>
   <tr>
      <th>产品</th>
      <th>巡检项</th>
      <th>巡检说明</th>
   </tr>
   <tr>
      <td> 云硬盘（CBS）</td>
      <td> 云硬盘（CBS）未充分利用</td>
      <td> 检查 CBS 的挂载状态及 IO 读写情况，若 CBS 在近 5 天一直处于未挂载状态或近 7 天每天的 IOPS 不超过 1 次，则发出警报。长期闲置的云硬盘会带来不必要的开销。</td>
   </tr>
   <tr>
      <td rowspan="2"> 负载均衡（CLB）</td>
      <td> 负载均衡（CLB）实例被闲置</td>
      <td> 检查 CLB 后端云资源绑定情况，若未绑定云资源（CVM 实例、弹性网卡），则会判定为实例被闲置，产生额外成本。</td>
   </tr>
   <tr>
      <td> 负载均衡（CLB）低利用率 </td>
      <td> 检查 CLB 低利用率情况，如果连接数小于配额的 10%，可能存在冗余成本。</td>
   </tr>
   <tr>
      <td rowspan="2"> 对象存储（COS）</td>
      <td> 对象存储（COS）存储桶生命周期配置</td>
      <td> 检查 COS 存储桶生命周期规则，若未配置，则存储桶中的访问热度较低的对象会产生不必要的开销。</td>
   </tr>
   <tr>
      <td> 对象存储（COS）存储桶碎片检查</td>
      <td> 检查 COS 存储桶生命周期碎片规则，若未配置碎片的清理规则，则可能产生不必要的开销。</td>
   </tr>
   <tr>
      <td rowspan="2"> 云服务器（CVM） </td>
      <td> 云服务器（CVM）实例低使用率</td>
      <td> 检查 CVM 实例 CPU、网络 I/O 使用情况，若长期低使用率，则提示风险。</td>
   </tr>
   <tr>
      <td> 云服务器（CVM）计费模式检查</td>
      <td> 检查 CVM 实例是否长期（超过2个月）处于按量计费模式，按量计费单价较高，会造成较多不必要的开销。</td>
   </tr>
   <tr>
      <td> 云原生数据库 TDSQL-C </td>
      <td> 云原生数据库 TDSQL-C MySQL 版利用率不足</td>
      <td> 检查集群是否闲置，如果业务生命周期已经稳定，长时间的闲置资源对业务成本会造成较多浪费。</td>
   </tr>
   <tr>
      <td> 云数据库（MongoDB）</td>
      <td> 云数据库（MongoDB）利用率不足</td>
      <td> 检查实例是否闲置，如果业务生命周期已经稳定，长时间的闲置资源对业务成本会造成较多浪费。</td>
   </tr>
   <tr>
      <td> 云数据库（MySQL）    </td>
      <td> 云数据库（MySQL）利用率不足</td>
      <td> 检查实例是否闲置，如果业务生命周期已经稳定，长时间的闲置资源对业务成本会造成较多浪费。</td>
   </tr>
   <tr>
      <td> NAT 网关</td>
      <td> 私有网络 NAT 闲置情况</td>
      <td> 检查 NAT 实例是否配置到路由表中，如未配置，则造成 NAT 实例闲置，容易耗费成本。</td>
   </tr>
   <tr>
      <td> 云数据库（Redis）</td>
      <td> 云数据库（Redis）利用率不足</td>
      <td> 检查实例是否闲置，如果业务生命周期已经稳定，长时间的闲置资源对业务成本会造成较多浪费。</td>
   </tr>
   <tr>
      <td> 云数据库（MariaDB）</td>
      <td> 云数据库（MariaDB）利用率不足</td>
      <td> 检查实例是否闲置，如果业务生命周期已经稳定，长时间的闲置资源对业务成本会造成较多浪费。</td>
   </tr>
   <tr>
      <td> 私有网络 VPN 网关（VPNGW）</td>
      <td> 私有网络 VPN 网关（VPNGW）被闲置</td>
      <td> 检查 VPN 网关是否关联 VPN 通道，若未关联，可能产生额外费用消耗。</td>
   </tr>
</table>

## 性能[](id:performance)

根据监控实例运行中的资源使用情况和最佳实践，为您提供改善性能的建议。

<table>
   <tr>
      <th>产品</th>
      <th>巡检项</th>
      <th>巡检说明</th>
   </tr>
   <tr>
      <td rowspan="3"> 云硬盘（CBS）</td>
      <td> 云硬盘（CBS）IO 高负载  </td>
      <td> 检查云硬盘（CBS）IO 负载情况，若 IO 负载过高，则发出警告。</td>
   </tr>
   <tr>
      <td> 云硬盘（CBS）IOPS 超限</td>
      <td> 检查 CBS 的 IOPS 峰值是否达到该类型 CBS 的配置上限，若已达到会有受到限流的风险。</td>
   </tr>
   <tr>
      <td> 云硬盘（CBS）吞吐量超限</td>
      <td> 检查 CBS 的吞吐量峰值是否达到该类型 CBS 的配置上限，若已达到会有受到限流的风险。</td>
   </tr>
   <tr>
      <td> 云联网（CCN）</td>
      <td> 云联网（CCN）出带宽使用情况</td>
      <td> 检查跨地域的云联网在各个地域的出带宽使用情况，若使用量接近阈值，有限速丢包风险，影响业务。</td>
   </tr>
   <tr>
      <td rowspan="6"> 内容分发网络（CDN）</td>
      <td> 内容分发网络（CDN）单链接下行限速配置</td>
      <td> 不处理则默认不进行单链接限速，可能在活动期间产生较大的峰值带宽 。</td>
   </tr>
   <tr>
      <td> 内容分发网络（CDN）带宽封顶配置</td>
      <td> 如果不关闭，触发带宽封顶以后将关闭 CDN 服务，请求转到源站或者返回 404，该功能可一定程度降低带宽费用，后续需要重新设置域名上线才能使用 CDN 服务。</td>
   </tr>
   <tr>
      <td> 内容分发网络（CDN）域名绑定证书到期</td>
      <td> 如果证书过期，影响 HTTPS 访问有效性，HTTPS 访问会出现无法访问的情况。</td>
   </tr>
   <tr>
      <td> 内容分发网络（CDN）缓存命中率</td>
      <td> 如果命中率比较低，不能有效减少源站压力，提升用户访问速度体验不能达到很好的优化效果。</td>
   </tr>
   <tr>
      <td> 内容分发网络（CDN）错误状态码占比</td>
      <td> 如果异常状态码较高，可能存在对业务有影响的事件发生或潜在的故障问题。</td>
   </tr>
   <tr>
      <td> 内容分发网络（CDN）备用源站</td>
      <td> 如果主源站无法服务，则没有备源可用容灾。</td>
   </tr>
   <tr>
      <td> 负载均衡（CLB）</td>
      <td> 负载均衡（CLB）后端服务器返回 404 或 502 状态码</td>
      <td> 检查 CLB 后端服务器是否出现返回 404 或 502 状态码，即无法找到对应资源或网关错误的情况，该类情况容易影响业务质量。</td>
   </tr>
   <tr>
      <td> 对象存储（COS）</td>
      <td> 对象存储（COS）5XX 错误率</td>
      <td> 检查 COS 状态码， 若 5XX 状态码出现次数过多、且出现频率占比过大，则可能影响存储桶的正常访问。</td>
   </tr>
   <tr>
      <td rowspan="2"> 云服务器（CVM）</td>
      <td> 云服务器（CVM）实例内存高负载</td>
      <td> 检查 CVM 实例内存使用率情况，若负载过高，则提示风险。</td>
   </tr>
   <tr>
      <td> 云服务器（CVM）实例 CPU 高负载 </td>
      <td> 检查 CVM 实例 CPU 使用率情况，若负载过高，则提示风险。</td>
   </tr>
   <tr>
      <td rowspan="2"> 云原生数据库 TDSQL-C </td>
      <td> 云原生数据库 TDSQL-C MySQL 版 CPU 使用率</td>
      <td> 检查 CPU 使用率情况，若使用率过高，可能会出现业务请求延迟增加，甚至无响应等风险。</td>
   </tr>
   <tr>
      <td> 云原生数据库 TDSQL-C MySQL 版全表扫描数量</td>
      <td> 检查实例每秒执行全表扫描的次数。</td>
   </tr>
   <tr>
      <td rowspan="2"> 云数据库（MongoDB）</td>
      <td> 云数据库（MongoDB）Cache 脏数据</td>
      <td> 检查 MongoDB Cache 脏数据情况，若 Cache 脏数据百分比大于20%，用户线程将参与刷盘，阻塞业务。</td>
   </tr>
   <tr>
      <td> 云数据库（MongoDB）CPU 使用率 </td>
      <td> 检查 MongoDB 实例 CPU 使用率情况，若使用率过高，可能会出现业务请求延迟增加、等待等风险。</td>
   </tr>
   <tr>
      <td rowspan="2"> 云数据库（MySQL）    </td>
      <td> 云数据库（MySQL）CPU 使用率</td>
      <td> 检查 MySQL 实例 CPU 使用率情况，若使用率过高，可能会出现业务请求延迟增加，甚至无响应等风险。</td>
   </tr>
   <tr>
      <td> 云数据库（MySQL）运行线程数</td>
      <td> 检查 MySQL 实例运行线程数，如果运行线程数大量超过实例 CPU 核心数，会导致请求等待，延迟增加的风险。</td>
   </tr>
   <tr>
      <td rowspan="3"> 云数据库（Redis）</td>
      <td> 云数据库（Redis）Proxy 节点出流量限流触发情况</td>
      <td> 检查 Redis 实例 Proxy 节点出流量限流触发次数，出现限流说明业务峰值访问期间可能已经受损，若限流次数过高，说明业务流量到达上限，业务访问会有延迟增加或失败风险。</td>
   </tr>
   <tr>
      <td> 云数据库（Redis）CPU 使用率</td>
      <td> 检查 Redis 实例 CPU 使用率，CPU 使用率长期过高可能导致请求延迟上升，阻塞等现象。</td>
   </tr>
   <tr>
      <td> 云数据库（Redis）Redis 节点请求数超限</td>
      <td> 检查 Redis 节点请求数是否接近上限。</td>
   </tr>
   <tr>
      <td rowspan="2"> 云数据库（MariaDB）</td>
      <td> 云数据库（MariaDB）CPU 使用率</td>
      <td> 当 CPU 使用率较高时，说明当前实例处理繁忙，容易导致查询变慢、堵塞的问题。</td>
   </tr>
   <tr>
      <td> 云数据库（MariaDB）活跃连接数</td>
      <td> 当活跃连接数过多时，表明实例目前已经处于较高的压力状态，容易出现请求阻塞的情况。</td>
   </tr>
</table>
