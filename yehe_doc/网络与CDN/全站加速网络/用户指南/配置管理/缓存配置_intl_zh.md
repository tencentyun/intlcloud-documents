## 功能介绍

ECDN 将根据您配置的规则自动识别动静态内容访问请求，智能地选择合适的加速方案，一站式满足动静内容混合站点的访问加速需求。

- 对于静态内容请求，优先采用边缘节点缓存内容响应，提升访问效果，降低回源流量。
- 对于动态内容请求，直接通过智能路由和优质资源快速回源，降低平均响应时延。

>? 若您的业务已迁移至 CDN 控制台，请参考 [CDN 产品文档](https://intl.cloud.tencent.com/document/product/228)，前往 CDN 控制台进行操作。
## 功能配置指导
1. 登录 [ECDN 控制台](https://console.cloud.tencent.com/dsa)，在左侧目录中，单击【域名管理】，进入管理页面。
2. 在列表中，找到需要配置的域名，在右侧操作栏下单击【管理】，进入域名配置管理页面。   
3. 在“缓存配置”页面下，进行内容缓存规则配置管理。   
   - 过滤参数缓存配置：
     开启过滤参数缓存开关，可在缓存时对用户请求 URL 中 “?” 之后的参数进行过滤。例如，URL 为：` http://www.example.com/1.jpg?version=1.1`的资源，节点存储资源时，对应的 cache_key 为` www.example.com/1.jpg`，忽略了 "?" 之后的参数。当用户请求时 ，也将忽略"?"后参数，按照cache_key为`www.example.com/1.jpg`查找资源，可直接命中。
	![](https://main.qcloudimg.com/raw/99d0e9fe096ed15b1ec3ed42cfa7c1d3.png)
   - 内容缓存配置：
   单击【编辑缓存规则】，可添加新的缓存规则或对现有规则进行修改，单击【保存】，规则生效。
     ![](https://main.qcloudimg.com/raw/2afa0aff85361ff74fe25912fe232328.png)

### 缓存规则类型  

<table style="display:table" width="100%">
	<tbody>
		<tr>
			<th colspan="1" style="text-align: center" width="15%"> 缓存类型 </th>
			<th colspan="1" style="text-align: center" width="30%"> 类型说明 </th>
			<th colspan="1" style="text-align: center" width="10%"> 设置举例 </th>
			<th width="45%">注意事项</th>
		</tr>
		<tr>
			<td style="text-align: center">文件类型</td>
			<td>根据文件后缀类型设置缓存时间</td>
			<td>.jpg;.png;.jsp</td>
			<td>1. 内容区分大小写，必须是以“.”开头的文件后缀。</br>2. 不同文件类型使用“;”隔开。</td>
		</tr>
		<tr>
			<td style="text-align: center">文件夹</td>
			<td>根据文件夹设置缓存时间</td>
			<td>/access;/pic</td>
			<td>1. 内容区分大小写，不同路径使用“;”隔开。</br>2. 必须是以“/”开头的文件夹。</br>3. 内容不能以“/”结尾。</td>
		</tr>
		<tr>
			<td style="text-align: center">全路径文件</td>
			<td>为指定的文件设置缓存时间</td>
			<td>/a.jpg;/b.png</td>
			<td>1. 内容区分大小写，不同路径文件使用“;”隔开。</br>2. 支持“*”正则匹配某一类型文件，如“/test/abc/*.jpg”。</br>3. 必须是以“/”开头的文件夹。</td>
		</tr>
		<tr>
			<td style="text-align: center">首页</td>
			<td>指定首页设置缓存时间</td>
			<td style="text-align: center">/</td>
			<td>首页缓存的内容默认为“/”，无需修改。</td>
		</tr>
	</tbody>
</table> 



### 缓存刷新时间  

<strong>缓存刷新时间说明</strong>  

- 缓存刷新时间支持按秒、分、小时、天设置，最长缓存刷新时间不超过365天。  
- 缓存刷新时间等于0时，表示为动态内容，所有请求直接透传回源，并且响应内容不作缓存处理。  
- 缓存刷新时间大于0时，表示为静态内容，开启边缘缓存功能：
  - 当用户访问的内容已经在边缘节点缓存，且缓存时间未过期，则本次请求无需回源，直接使用缓存内容响应，让用户就近获取访问内容。
  - 当用户访问的内容未在边缘节点缓存，或缓存内容已过期，则本次请求需回源获取内容响应给用户，并缓存在节点。


<strong>缓存刷新时间设置建议</strong>

<table style="display:table" width="100%">
	<tbody>
		<tr>
			<th colspan="1" style="text-align: center" width="40%"> 文件类型 </th>
			<th colspan="1" style="text-align: center" width="30%"> 场景示例 </th>
			<th colspan="1" style="text-align: center" width="30%"> 缓存时间建议 </th>
		</tr>
		<tr>
			<td>基本不更新的静态内容</td>
			<td>图片文件、音视频文件</td>
			<td>缓存刷新时间设置为30天。</td>
		</tr>
		<tr>
			<td>需要频繁更新的静态内容</td>
			<td>js、css 等类型文件</td>
			<td>按照更新周期设置缓存时间，一般可以按天或小时级别设置缓存时间。</td>
		</tr>
		<tr>
			<td>频繁更新的，且允许用户共享访问的动态内容</td>
			<td>天气查询、分地区门户内容</td>
			<td>设置分钟或秒级别缓存时间。</td>		
		</tr>
		<tr>
			<td>动态生成的，或不允许用户重复访问的内容</td>
			<td>用户注册、登录接口</td>
			<td>不缓存，缓存刷新时间设置成0秒。</td>		
		</tr>
	</tbody>
</table> 



### 缓存规则优先级

当您设置了多条缓存策略时，规则之间可能会有重复，导致同一请求可能符合多条设置规则，因此我们对缓存规则设置了优先等级。  

- 配置列表底部的优先级高于列表顶部优先级，新增的缓存规则默认设置最高优先等级。
- 用户请求按照规则优先等级从高到低匹配，首次命中的缓存规则决定了该次请求的缓存刷新时间。
- 您可以通过调整优先级设置调整不同规则的优先等级。

单击【编辑缓存规则】，通过<strong>鼠标拖拽小图标</strong>的方式调整缓存规则优先等级。

![](https://main.qcloudimg.com/raw/67575a5f1c292ac2074f51fe17e032f7.png)

## 缓存继承问题

当您设置静态内容使用边缘缓存功能时，ECDN 系统将默认以平台配置的缓存规则处理用户静态请求，源站 Response Header 中存在的 Cache-Control 字段节点默认不继承处理。但是如果源站 Cache-control 字段为 private、no-store 或 no-cache，此时 ECDN 节点对此资源不做缓存。
