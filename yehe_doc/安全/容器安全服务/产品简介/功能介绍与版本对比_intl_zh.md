不同版本提供的主要功能对比如下表所示：

<table>
<thead>
<tr>
<th>分类</th>
<th colspan=2>类别</th>
<th>详细描述</th>
<th>专业版</th>
<th>增值功能</th>
</tr>
</thead>
<tbody><tr>
<td>安全概览</td>
<td colspan=2>安全概览</td>
<td>以可视化的图形、图表等方式实时展示资产信息（容器、镜像、主机）、待处理安全事件数量、运行时安全事件新增趋势、本地镜像新增风险趋势及详情。</td>
<td>支持</td>
<td>-</td>
</tr>
<tr>
<td>资产中心</td>
<td colspan=2>资产管理</td>
<td>支持自动化统计容器、镜像、主机、进程端口、应用 Web 资产、运行应用、数据库应用等资产基本信息。</td>
<td>支持</td>
<td>-</td>
</tr>
<tr>
<td rowspan=6>安全加固</td>
<td colspan=2>漏洞管理</td>
<td>漏洞管理模块支持对容器环境中的漏洞开展一键检测，为漏洞应急响应及漏洞运营场景提供更好体验。根据实际处理及漏洞响应类型，将漏洞划分为两类，分别是：系统漏洞、Web 应用漏洞。<br>支持按影响资产紧急度和关注紧急度快速筛选漏洞，例如仅展示影响容器的漏洞、仅展示影响最新版本的镜像、重点关注、高危及严重、远程 EXP 等。同时关联漏洞影响的本地镜像、仓库镜像、容器等资产数据。</td>
<td>支持</td>
<td>-</td>
</tr>
<tr>
<td rowspan=2>镜像风险管理</td>
<td>本地镜像</td>
<td><li>支持定时扫描、一键扫描本地镜像获取镜像资产基本信息及镜像安全风险详情。</li><li>支持对业务环境存在风险的镜像总数、安全漏洞、木马病毒、敏感信息进行汇总。</li></td>
<td>-</td>
<td>支持</td>
</tr>
<tr>
<td>仓库镜像</td>
<td><li>支持定时扫描、一键扫描仓库镜像获取镜像资产基本信息及镜像安全风险详情。</li><li>支持对业务环境存在风险的镜像总数、安全漏洞、木马病毒、敏感信息进行汇总。</li></td>
<td>-</td>
<td>支持</td>
</tr>
<tr>
<td rowspan=2>集群风险管理</td>
<td>集群检查</td>
<td>支持自动检查、手动检查获取集群资产基本信息及其存在的配置和漏洞风险，并对业务环境中存在风险的集群及每个集群存在的风险数据进行汇总；集群检查模式包括正常模式和主动模式。<li>正常模式为默认模式，该模式不会改变和影响集群状态，是一种常规检查方式。</li><li>主动模式会主动利用已知漏洞进行渗透或执行利用，<strong>可能改变集群状态，请在特定场景下谨慎开启使用。</strong></li></td>
<td>支持</td>
<td>-</td>
</tr>
<tr>
<td>风险分析</td>
<td>支持按严重、高危、中危、低危对存在风险的集群节点进行统计，并按检查项对受影响的集群数、受影响的节点数进行统计。</td>
<td>支持</td>
<td>-</td>
</tr>
<tr>
<td colspan=2>基线管理</td>
<td><li>支持 CIS  Benchmark 基线检查标准，检测 Docker 及 kubernetes  安全基线，并对业务环境中合规容器占比、严重检查项、高危检查项、中危检查项、低危检查项进行统计。</li><li>基线检测结果包括基线检测项、类型、基线标准、威胁等级、检测结果、检测项详情等，检测对象包括容器、镜像、主机和 kubernetes。</li></td>
<td>支持</td>
<td>-</td>
</tr>
<tr>
<td rowspan=6>入侵防御</td>
<td rowspan=3>运行时安全</td>
<td>容器逃逸</td>
<td><li>支持实时检测容器内存在的敏感路径挂载、特权容器、提权事件、逃逸漏洞利用、访问 Docker  API 接口逃逸、篡改敏感文件逃逸、利用 cgroup 机制逃逸等行为，并自定义开启/关闭检测规则。</li><li>支持按风险容器、程序提权、容器逃逸等对告警事件进行分类，明确区分存在风险的容器和容器逃逸行为。</li><li>告警信息包括：逃逸事件类型、首次生成时间、最近生成时间、事件数量、容器名称/ID、镜像名称/ID、节点名称、POD 名称等，同时告警详情提供事件描述、解决方案、进程信息、父进程信息、祖先进程信息等详情。</li></td>
<td>支持</td>
<td>-</td>
</tr>
<tr>
 <td>反弹Shell</td>
<td><li>支持实时检测容器内存在的反弹 Shell 行为并产生告警，告警信息包括：进程名称、父进程名称、目标地址、进程路径、首次生成时间、最近生成时间、事件数量、容器名称/ID、镜像名称/ID 等，同时告警详情提供风险描述、解决方案、进程、父进程和祖先进程详细信息。</li><li>支持用户对告警事件加白处理，或按目标地址（IP、端口）、连接进程和生效镜像范围自定义新增白名单。</li></td>
<td>支持</td>
<td>-</td>
</tr>
<tr>
<td>文件查杀</td>
<td><li>支持实时检测容器运行时存在的木马病毒并产生告警，告警信息包括文件名称、文件路径、病毒名称、首次生成时间、最近生成时间、容器名称/ID、镜像名称/ID、容器状态等；同时告警详情提供恶意文件详情、事件详情、解决方案、进程、父进程、祖先进程等详细信息</li><li>支持实时监控、一键扫描和定时扫描容器内恶意文件；同时支持客户自定义开启自动隔离恶意文件开关。</li></td>
<td>支持</td>
<td>-</td>
</tr>
<tr>
<td rowspan=3>高级防御</td>
<td>异常进程</td>
<td><li>支持实时检测容器内存在的进程异常启动行为并告警通知或拦截异常进程。告警信息包括：进程路径、命中规则、威胁等级、首次生成时间、最近生成时间、事件数量、容器名称/ID、镜像名称/ID、动作执行结果等，同时告警详情提供风险描述、解决方案、进程、父进程和祖先进程详细信息。</li><li>异常进程检测系统策略至少包括代理软件、横向渗透、恶意命令、反弹 Shell、无文件程序执行、高危命令、敏感服务异常子进程启动等。</li><li>支持用户对告警事件加白处理，或按进程路径和生效镜像范围自定义新增进程放行规则。</li><li> 支持用户自定义新增进程检测规则，配置内容包括规则名称、进程路径、执行动作（拦截、告警、放行）和生效镜像范围。</li></td>
<td>支持</td>
<td>-</td>
</tr>
<tr>
 <td>文件篡改</td>
<td><li>支持实时检测容器内存在的文件异常访问行为并告警通知或拦截异常访问。告警信息包括：文件名称、进程路径、命中规则、首次生成时间、最近生成时间、事件数量、容器名称/ID、镜像名称/ID、动作执行结果等。同时告警详情提供风险描述、解决方案、进程、父进程和祖先进程详细信息。</li><li> 文件篡改系统策略至少包括篡改计划任务、篡改系统程序、篡改用户配置等规则。</li><li>支持用户对告警事件加白处理，或按进程路径、被访问文件路径和生效镜像范围自定义新增放行规则。     </li><li>支持用户自定义新增访问控制规则，配置内容包括规则名称、进程路径、被访问文件路径、执行动作（拦截、告警、放行）和生效镜像范围。</li></td>
<td>支持</td>
<td>-</td>
</tr>
<tr>
<td>高危系统调用</td>
<td><li>支持实时检测容器内存在的高危系统调用行为并产生告警，告警信息包括：进程路径、系统调用名称、首次生成时间、最近生成时间、事件数量、容器名称/ID、镜像名称/ID、节点名称、POD 名称等，同时告警详情提供风险描述、解决方案、进程、父进程和祖先进程详细信息。</li><li>支持用户对告警事件加白处理，或按进程路径、系统调用名称和生效镜像范围自定义新增白名单。</li></td>
<td>支持</td>
<td>-</td>
</tr>
<tr>
<td>安全运营</td>
<td colspan=2>日志分析</td>
<td><li>支持按时间、日志类型、日志内容等自定义检索容器 bash 日志、容器启动审计日志、kubernetes  API 审计日志，并按检索结果展示日志趋势图。支持自定义日志的展示字段和隐藏字段，查看 json 格式日志，并支持导出日志。</li><li>日志配置：支持自定义配置容器 bash 日志、容器启动审计日志和 kubernetes  API 审计日志是否开启日志审计，以及按照日志类型自定义节点是否开启审计。支持按百分比和存储天数清理日志。</li><li>日志投递：支持自定义配置 CKAFKA 和 CLS 日志投递功能。CKAFKA 日志投递支持按公网域名接入，客户可自定义选择投递的消息队列实例、接入的公网域名、每类日志投递的 Topic  ID 和名称，以及是否开启投递；CLS 日志投递支持自定义日志投递的日志集和日志主题，以及是否开启投递。</li></td>
<td>支持</td>
<td>-</td>
</tr>
<tr>
<td>设置中心</td>
<td colspan=2>告警设置</td>
<td>支持自定义对本地镜像（安全漏洞、木马病毒、敏感信息）、仓库镜像（安全漏洞、木马病毒、敏感信息）、运行时安全&amp;高级防御（容器逃逸、反弹 Shell、文件查杀、异常进程、文件篡改）等告警进行通知，可配置内容包括告警状态、告警时间和告警项，接收渠道包括站内信、邮件、短信等。</td>
<td>支持</td>
<td>-</td>
</tr>
</tbody></table>