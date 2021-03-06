> 缓存过期配置是指配置 CDN 加速节点在缓存您的业务内容时遵循的一套过期规则。CDN 节点上缓存的用户资源都面临“过期”问题。若资源处于未过期状态，当用户请求到达节点后，节点会将此资源直接返回给用户，提升获取速度；当资源处于过期状态（即超过了设置的有效时间），此时用户请求会由节点发送至源站，重新获取内容并缓存至节点，同时返回给用户。
>
> 腾讯云 CDN 支持各维度的内容缓存时间设置、支持自定义优先级调整。合理的配置缓存时间，能够有效的提升命中率，降低回源率，节省您的带宽。
>
> 腾讯云 CDN 支持403、404状态码缓存过期时间设置。

## 浏览器缓存过期配置

### 配置指引

登录 [CDN 控制台](https://console.cloud.tencent.com/cdn)，选择左侧菜单栏的【域名管理】，单击您所要编辑的域名右侧的【管理】。

单击【缓存配置】，您可以看到 **浏览器缓存过期配置** 模块。

在域名接入时，默认不配置浏览器缓存过期配置。

### 修改配置

单击【新增缓存配置】可以添加缓存配置，您可以根据自身业务需求，添加浏览器缓存过期时间配置，CDN 支持 4 种方式的浏览器缓存过期时间设置：

#### 1. 全部文件设置缓存过期时间

您可以选择对全部文件设置缓存过期时间，内容固定为 ```all``` 不可更改。

刷新时间设置为 0 时，不缓存；缓存时间设置最大值不能超过365天。

#### 2. 按文件类型设置缓存过期时间

您可以填充文件类型后缀，根据类型来设置缓存时间。

配置缓存时间时可填入多项，每项用 ```;``` 隔开，内容区分大小写，必须是以 ```.``` 开头的文件后缀，如 ```.png```。刷新时间设置为 0 时，不缓存；缓存时间设置最大值不能超过365天。

#### 3. 按文件夹设置缓存过期时间
您可以填充文件夹路径，根据文件夹来设置缓存时间。

配置缓存时间时可填入多项，每项用 ```;``` 隔开，内容区分大小写，必须是以 ```/ ``` 开头的文件夹。刷新时间设置为 0 时，不缓存；缓存时间设置最大值不能超过365天。

#### 4. 全路径文件设置缓存过期时间
您可以为某一具体文件设置缓存时间。

配置缓存时间时可填入多项，每项用 ```;``` 隔开，内容区分大小写，支持```*```匹配某一类型文件，如 ```/test/abc/*.jpg```：


### 优先级
当设置了多条缓存策略时，相互之间会有重复，配置项列表底部优先级高于顶部优先级。假设某域名配置了如下缓存配置：
> 全部文件 30天
> .php .jsp .aspx 0秒
> .jpg .png .gif 300秒
> /test/*.jpg 400秒
> /test/abc.jpg 200秒

假设域名为 ```www.test.com```，资源为 ```www.test.com/test/abc.jpg```，其匹配方式如下：
1. 匹配第一条全部文件，命中，此时缓存时间为 30 天。
2. 匹配第二条，未命中。
3. 匹配第三条，命中，此时缓存时间为 300 秒。
4. 匹配第四条，命中，此时缓存时间为 400 秒。
5. 匹配第五条，命中，此时缓存时间为 200 秒。

因此最终缓存时间为 200 秒，以最后一次匹配生效。

单击【调整优先级】可以添加缓存配置，您可以根据业务情况自定义调整已经添加的缓存过期配置顺序。

使用右侧上下箭头调整缓存过期时间配置的顺序，单击【保存】即可完成调整。

## 节点缓存过期配置

### 配置指引

在 **浏览器缓存过期配置** 模块下方，您可以看到 **节点缓存过期配置** 模块：


在域名接入时，您可以手动添加节点缓存过期配置，系统默认不添加配置。

节点缓存时间配置默认遵循源站回包头部 max-age 信息：

1. 当未设置任何 CDN 节点缓存规则，或请求未命中节点设置的缓存规则时，CDN 节点缓存时间将遵循源站的 max-age 信息；
2. 当源站回包头部无 max-age 信息时，CDN 节点默认不缓存该类型文件。

### 修改配置

单击【新增缓存配置】可以添加缓存配置，您可以根据自身业务需求，添加节点缓存时间配置，CDN 支持 5 种方式的节点缓存过期时间设置：

#### 1. 无 max-age 文件设置缓存过期时间

当用户请求某一业务资源时，若源站回包头部无 max-age 信息，您可以选择对这些无 max-age 的文件设置缓存过期时间，内容为所有无 max-age 文件，不可更改。

刷新时间设置为 0 时，不缓存，所有请求转发至用户源站；缓存时间设置最大值不能超过365天。	

#### 2. 全部文件设置缓存过期时间

您可以选择对全部文件设置缓存过期时间，内容固定为 ```all``` 不可更改。

刷新时间设置为 0 时，不缓存，所有请求转发至用户源站；缓存时间设置最大值不能超过365天。

#### 3. 按文件类型设置缓存过期时间

您可以填充文件类型后缀，根据类型来设置缓存时间。

配置缓存时间时可填入多项，每项用 ```;``` 隔开，内容区分大小写，必须是以 ```.``` 开头的文件后缀，如 ```.png```。刷新时间设置为 0 时，不缓存，所有请求转发至用户源站；缓存时间设置最大值不能超过365天。

#### 4. 按文件夹设置缓存过期时间

您可以填充文件夹路径，根据文件夹来设置缓存时间。

配置缓存时间时可填入多项，每项用 ```;``` 隔开，内容区分大小写，必须是以 ```/ ``` 开头的文件夹。刷新时间设置为 0 时，不缓存，所有请求转发至用户源站；缓存时间设置最大值不能超过365天。

#### 5. 全路径文件设置缓存过期时间

您可以为某一具体文件设置缓存时间。

配置缓存时间时可填入多项，每项用 ```;``` 隔开，内容区分大小写，支持```*```匹配某一类型文件，如```/test/abc/*.jpg```：


### 优先级

当设置了多条缓存策略时，相互之间会有重复，配置项列表底部优先级高于顶部优先级。假设某域名配置了如下缓存配置：

> 全部文件 30天
> 无 max-age 60秒
> .php .jsp .aspx 0秒
> .jpg .png .gif 300秒
> /test/*.jpg 400秒
> /test/abc.jpg 200秒

假设域名为 ```www.test.com```，资源为 ```www.test.com/test/abc.jpg```，源站回包头部 ```Cache-Control: max-age=600```，其匹配方式如下：

1. 匹配第一条全部文件，命中，此时缓存时间为 30 天。
2. 匹配第二条，未命中。
3. 匹配第三条，未命中。
4. 匹配第四条，命中，此时缓存时间为 300 秒。
5. 匹配第五条，命中，此时缓存时间为 400 秒。
6. 匹配第六条，命中，此时缓存时间为 200 秒。

因此最终缓存时间为 200 秒，以最后一次匹配生效。

单击【调整优先级】可以添加缓存配置，您可以根据业务情况自定义调整已经添加的缓存过期配置顺序。

使用右侧上下箭头调整缓存过期时间配置的顺序，单击【保存】即可完成调整。


## 头部缓存

当资源在节点命中缓存时，CDN 默认会缓存以下来自于源站头部，并返回给用户。

+ Access-Control-Allow-Origin
+ Timing-Allow-Origin
+ Content-Disposition
+ Accept-Ranges 



## 状态码缓存

CDN 节点请求源站资源时，除上述缓存策略外，还会在状态码为 403、404 时按照您所配置的缓存策略进行缓存：

您可以在【缓存配置】中【状态码缓存】模块调整 403、404 缓存时间。

403、404 状态码缓存时间可调整至 0 ~ 365 天。

**注意**：若文件对应的缓存过期时间为 0，产生 403 / 404 后，仍遵循不缓存原则，直接透传。
