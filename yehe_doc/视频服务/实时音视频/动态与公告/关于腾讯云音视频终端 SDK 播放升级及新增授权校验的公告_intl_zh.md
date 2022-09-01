<style>.markdown-text-box table td, .markdown-text-box table th {text-align: center;}</style>

腾讯云音视频终端 SDK 移动端（Android & iOS & Flutter）已发布 10.1 版本，新版本 SDK 采用“腾讯视频”同款播放内核打造，视频播放能力获得全面优化升级，详见 [升级特性](#up)。

同时从该版本开始将增加对**视频播放**功能模块的授权校验。

若您需使用新版本 SDK 中的**直播播放或点播播放功能，则需免费开通指定 License 获得授权**，详情参见 [免费授权方式](#warrant)。若您无需使用视频播放功能或未升级至 10.1 及更高版本的 SDK，则不受到此次变更的影响。

>! **如果您的 App 已经拥有直播 License 或短视频 License 授权，当您升级至 10.1 版本后仍可继续正常使用**，不受到此次变更影响。您可以登录 [云直播控制台](https://console.intl.cloud.tencent.com/live) 查看您当前的 直播 License 信息，登录 [云点播控制台](https://console.intl.cloud.tencent.com/vod) 查看您当前的 点播 License 信息。

[](id:warrant)

## 免费授权方式

10.1 版本后，若您需要使用**视频播放**功能模块，则需授权视频播放 License，该 License 为免费授权。具体授权方式如下：

第一步，注册/登录腾讯云账号，进入[实时音视频控制台](https://console.tencentcloud.com/trtc)。

第二步，点击左侧导航栏中的”**相关云服务**“，在 ”**License 签发**“ 一栏中，点击**新建正式 License**。按提示填写内容后，点击”**确定**“，则为成功授权。


[](id:up)

## 升级特性

升级后的腾讯云音视频终端 SDK 视频播放内核由腾讯内部完全自研，且经过长期优化和海量服务验证，对比系统播放器，性能提升 30% ~ 50%。 同时针对控制带宽成本、辅助运营增长、降低接入门槛等方面为企业用户进行了专门的优化升级，新增终端极速高清、版权保护、全链路数据洞察和场景化低代码等多种方案，打造业界独家、行业领先的企业级视频播放解决方案，全面满足企业级需求。

<table>
<thead>
<tr>
<th width=16% style="text-align: left;">特性</th>
<th style="text-align: left;">说明</th>
</tr>
</thead>
<tbody><tr>
<td style="text-align: left;">“腾讯视频”同款</td>
<td style="text-align: left;">首次将“腾讯视频”播放能力以 SDK 的形式开放给广大开发者，在具备“臻彩视听”、精准 Seek、清晰度切换、小窗播放、离线缓存等多项“腾讯视频”同款播放功能的同时，具备同等水平的视频播放稳定性和机型适配性。</td>
</tr><tr>
<td style="text-align: left;">新增格式支持</td>
<td style="text-align: left;">新增支持 QUIC、AV1、H.266 等格式，相比 H.264/H.265节省带宽 20%～55%，满足多样化的业务场景同时降低客户成本。</td>
</tr><tr>
<td style="text-align: left;">版权保护升级</td>
<td style="text-align: left;">在支持私有协议加密、本地加密、防盗链等方案前提下，新增支持商业 DRM 加密方案，具备完整视频安全方案矩阵，全方位保护视频版权。</td>
</tr><tr>
<td style="text-align: left;">画质提升解决方案</td>
<td style="text-align: left;">新增支持“腾讯视频-臻彩视听” HDR 10 视频播放能力；并提供终端极速高清方案，能够在几乎不降低视频主观画质的情况下，为企业节省传输带宽成本。</td>
</tr><tr>
<td style="text-align: left;">场景化低代码</td>
<td style="text-align: left;">提供类似腾讯视频号（沉浸式短视频）、腾讯新闻（Feed 流视频）的场景化方案，可以快速搭建相关场景 App；并新增视频封面、动态水印、列表轮播等多种功能组件，适配多样业务场景，降低开发成本。</td>
</tr>
</tbody></table>
