## 功能介绍
全站加速网络（ECDN）提供基础缓存配置能力，可根据指定业务类型、目录、具体 URL 等各类规则设置缓存过期时间，来达到定期清理节点缓存资源，回源站重新拉取最新资源重新缓存的目的。

>? 若您的业务已迁移至 CDN 控制台，请参考 [CDN 产品文档](https://intl.cloud.tencent.com/document/product/228)，前往 CDN 控制台进行操作。


除此之外，ECDN 提供了缓存刷新的能力，可批量指定 URL 或目录进行刷新操作：
- 刷新 URL：删除 ECDN 所有节点上对应资源的缓存。
- 刷新目录：选择【刷新变更资源】模式，当用户访问匹配目录下资源时，会回源获取资源 Last-Modify 信息，若与当前缓存资源一致，则直接返回已缓存资源，若不一致，回源拉取资源并重新缓存。选择【刷新全部资源】时，当用户访问匹配目录下资源时，直接回源拉取新资源返回给用户，并重新缓存新资源。

刷新成功执行后，节点上对应资源无有效缓存，当用户再次发起访问时，节点回源站拉取所需资源，并重新缓存在节点上。因此提交大量的刷新任务，会清空较多缓存，从而导致回源请求突增，源站会产生较大压力。

## 适用场景
### 新资源发布
在源站点将新资源覆盖至同名旧资源后，为避免全网用户受节点缓存影响仍访问到旧的资源上，可通过提交对应资源的 URL / 目录 进行刷新，清空全网缓存后，全网用户可直接访问到最新资源。

### 违规资源清理
当站点上存在违规资源（如涉黄、涉毒、涉赌）被发现时，删除源站资源后，由于节点缓存资源仍可被访问到，为维护网络环境，可通过 URL 刷新删除缓存资源，保证及时清理。

## 操作指南
### 使用方式
1. 登录 [ECDN 控制台](https://console.cloud.tencent.com/dsa)，单击左侧目录的【缓存刷新】，进入后可按需提交【URL 刷新】或【目录刷新】：
![](https://main.qcloudimg.com/raw/a3442259ffa50bccb60dabf002ea6dfb.png)
![](https://main.qcloudimg.com/raw/d4b01354bab726ea890e8167ccdbaffe.png)
2. 在【操作记录】模块，可指定时间周期、查询关键字、类型对已提交的刷新操作进行状态查看：
![](https://main.qcloudimg.com/raw/86e00c9652a635cf0a0007172119be92.png)


### 注意事项
#### URL 刷新：
- 每一个账号每日 URL 刷新限额为10000条，每次可提交的 URL 刷新限额为1000条。
- 刷新任务提交时需要携带`http:/`或 `https://`协议标识。
- 不支持刷新`http://*.test.com/` 格式 URL ，即使接入的是泛域名做加速服务，在刷新时也需要提交对应的子域名进行刷新。
- 刷新提交时 URL 中域名需要接入加速服务，否则会导致提交失败。
- 不支持路径中携带中文的 URL 刷新。

#### 目录刷新：
- 每一个账号每日目录刷新限额为100条，每次可提交的目录刷新限额为20条。
- 刷新任务提交时需要携带`http://`或`https://`协议标识。
- 不支持刷新`http://*.test.com/`格式目录，即使接入的是泛域名做加速服务，在刷新时也需要提交对应的子域名进行刷新。
- 刷新提交时 URL 中域名需要接入加速服务，否则会导致提交失败。
- 不支持路径中携带中文的 URL 目录刷新。

#### 子用户权限配置：
- 刷新目录、刷新 URL、查询刷新记录目前已经接入最新的权限系统，支持资源（域名）维度权限配置。
- 分配方式可查看 [权限配置](https://intl.cloud.tencent.com/document/product/228/35229) 文档说明。

## 使用案例
### 目录刷新-刷新变更资源
加速域名为：purge-test-1251991073.file.myqcloud.com，源站为腾讯云对象存储（COS），源站资源如下：
![](https://main.qcloudimg.com/raw/ed694acc98a8d3114c8a9922f7374a1b.png)
1. 分别发起请求访问资源 1.txt 与 2.txt，根据 X-Cache-Lookup: Hit From Disktank3 与 Server: NWS_SPMid 可以判定命中节点， 由节点直接返回资源：
![](https://main.qcloudimg.com/raw/ac358d3cca6618836113ca7e8e03475b.png)
![](https://main.qcloudimg.com/raw/fa4ad405deef4278e1a15baea0ac43de.png)
2. 在源站替换掉同名文件 1.txt，文件修改时间发生改变，2.txt 保持不变：
![](https://main.qcloudimg.com/raw/798fd6a984813aa3a16eaf43856ff7c2.png)
![](https://main.qcloudimg.com/raw/bc0d40200fbc744ed34d8552a95c5671.png)
3. 此时再发起请求，由于缓存尚未过期，访问资源 1.txt 仍为旧的内容：
![](https://main.qcloudimg.com/raw/28e772fbed23411bdf40529d80173de0.png)
4. 提交目录刷新，选择【刷新变更资源】，等待刷新完成：
![](https://main.qcloudimg.com/raw/31346a963f189187852dde17a4bf0309.png)
5. 刷新完成后，由于文件 1.txt Last-Modified 发生变更，请求直接回源，而文件 2.txt 由于未做变更，即时提交目录刷新，仍被节点命中返回：
![](https://main.qcloudimg.com/raw/cf11384db9bbd96aa4526cf64420ee98.png)
![](https://main.qcloudimg.com/raw/eb1458ed2f2e1c301cf5b45b9b891fec.png)
