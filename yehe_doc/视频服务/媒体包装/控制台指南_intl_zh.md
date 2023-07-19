## 概览 

腾讯云StreamPackage是腾讯云新发布的的高质量视频封装及源站平台。致力于为全球用户提供专业、稳定、安全的视频封装及交付服务，降低视频包装分发难度，增加源弹性（origin resiliency），允许视频供应商能够大规模安全稳定地分配视频流媒体。

StreamPackage控制台基于channel维度进行管理，通过对视频内容进行重塑，将已经编码压缩好的视频轨和音频轨按照一定的格式放到直播源站中，使视频供应商能够大规模、安全、稳定地分配视频流媒体。

## 控制台概览

StreamPackage控制台提供丰富、有用的功能以及简单灵活的访问体验。StreamPackage控制台基于channel维度进行管理，整体可分为Channel、Input、Endpoint、CDN配置四个模块。

![img](https://main.qcloudimg.com/raw/2d70be467d74639158d0be4ea94692d2.png)

## 前提条件

- 用于CDN播放的域名（若需使用腾讯云直播CDN进行分发）。
- 已经[开通腾讯云直播服务](https://console.cloud.tencent.com/live)。
- 登录[腾讯云StreamPackage控制台](https://console.cloud.tencent.com/mdp/channel)。


## 操作步骤

### 一、选择可用区

目前腾讯云StreamPackage已提供印度孟买、泰国曼谷、韩国首尔、日本东京、德国法兰克福、新加坡这几个可用区，您可在此选择您所在的地域。如果您有其它可用区的加速部署诉求请[联系我们](https://intl.cloud.tencent.com/contact-sales)。

![](https://qcloudimg.tencent-cloud.cn/raw/14e4406387923306e201024a529f3d2b.png)

### 二、创建Channel

Channel是StreamPackage输入流及输出流的基础配置，用户基于创建完成Channel可以输入既定协议的直播流，也可以创建相应的回源节点（Endpoint）供直播流输出分发。

1. 单击【Create Channel】创建新Channel。
2. 输入Channel Name，选择Channel输入协议（支持HLS/DASH）。

![img](https://main.qcloudimg.com/raw/f545e69458ff80b55c6775219d574374.png)

3. 填写所选择的HLS/DASH协议相关参数。

- **Max Segment Duration**表示您朝此Channel推送HLS/DASH格式的流的ts/m4s切片的最大分片时长，该配置参数默认值为15s。
- **Max Playlist Duration**表示您朝此Channel推送HLS/DASH格式的流的m3u8/mpd列表的最大总时长，该配置参数的默认值为600s。您可根据您推流的m3u8/mpd列表的实际情况进行修改。

>? 如果您创建的此Channel会同时推送主备通道两路流，以便于主流异常时实现快速切换备流，建议您将这个配置参数设置略大于分片的实际最大时长，从而实现更好地快速切换。


4. 点击【Create】，完成创建。

### 三、查看Channel

#### 查看Channel信息

创建完毕后即跳转至Channel的详情页（点击Channel名字或右侧【Info】也可进入Channel详情页）。详情页会显示Channel的Name、ID（由后台自动生成）、指定的输入协议及相关配置参数。同时会基于指定的协议自动生成两个输入点（Input）。

![img](https://main.qcloudimg.com/raw/d962c942d07f8303832d070c7d0d2a26.png)

#### 查看Input

Input是Channel输入的基本单位，后台会基于创建完成的Channel自动生成两个Input节点以及对应的输入URL，用户可将直播流推到节点的URL中。

![img](https://main.qcloudimg.com/raw/9fc040a6cb575be7411327476f0fe7a1.png)

Input模块支持Authentication操作，用户可对每个输入点独立做Authentication配置。用户点击操作栏的【Authentication】进入弹框，打开Authentication配置后，后台会对该输入节点自动生成Username和Password，通过http认证模式进行鉴权。点击【Rotate credentials】完成Authentication配置。

![img](https://main.qcloudimg.com/raw/6927ebe8232a26cb341aa1b69f008e45.png)

>! 一旦用户Rotate credentials，现有的Channel credential将失效。

#### 创建Endpoints

用户可对每个Channel创建回源拉流Endpoint节点。

1. 单击【Create Endpoint】创建节点。

![img](https://main.qcloudimg.com/raw/ce143b55735dee33f7e708c5ea19f89a.png)

2. 输入Endpoint Name，Endpoint Type 默认与Channel的输入协议相同。 另外，如果你的输入协议为HLS，则额外可选Type为CMAF，StreamPackage支持将HLS转封装为CMAF（DASH格式）。

![](https://qcloudimg.tencent-cloud.cn/raw/9ccec5cbe3db2e1ce1ef76baa3fb39b7.png)

如果你需要修改Manifest Name, 请在Manifest Name中输入，默认值是main。

![](https://qcloudimg.tencent-cloud.cn/raw/bdf95344c0310ded0d5e05f3293d4558.png)


3. 用户可根据需要选择是否开启IP黑白名单、Authkey等功能。

- IP 黑白名单：固定合法IP段进行推流，或者拒绝异常IP端推流。

- 支持配置Authkey：支持http-header通过 X-TENCENT-PACKAGE进行鉴权。

![](https://qcloudimg.tencent-cloud.cn/raw/6f0ea51524e8fc074c92f0ece1848d2e.png)


4. 如果你需要时移功能，可以开启【Time-shifted Viewing】，以开启时移功能。
![](https://qcloudimg.tencent-cloud.cn/raw/e947b5903dec1e71f29ef4f15c3b30a0.png)
Startover Windows：在多长时间内可以对直播进行时移回看。默认1天，还支持选择3天、7天、15天和30天。 

开启时移后，直播切片将会被保存在云端，可以通过Endpoint的URL增加参数进行时移观看，具体参数如下
- timeshift=1,表示观看时移
- start=xxx,表示时移开始时间，支持ISO 8601 dates格式或者POSIX (or Epoch) time格式。
- end=xxx,表示时移结束时间，支持ISO 8601 dates格式或者POSIX (or Epoch) time格式。

注意：
- 如果同时指定start和end，那么end必须大于start，否则会返回400错误。
- start必须在StartoverWindows范围内，否则会返回400错误。
- 最多只能返回24小时的时移内容，也就是end和start的时间差不能超过24小时，否则会返回400错误。

时移URL示例:
- 请求2023-07-01T00:00:00Z ~ 2023-07-01T23:59:59Z这段时间的时移内容
```
http://domain/v1/path/subpath/playlist.m3u8?timeshift=1&start=2023-07-01T00:00:00Z&end=2023-07-01T23:59:59Z
或者
http://domain/v1/path/subpath/playlist.m3u8?timeshift=1&start=1688169600&end=1688255999
```

- 请求2023-07-01T00:00:00Z开始的直播内容,直到直播结束
```
http://domain/v1/path/subpath/playlist.m3u8?timeshift=1&start=2023-07-01T00:00:00Z
或者
http://domain/v1/path/subpath/playlist.m3u8?timeshift=1&start=1688169600
```

5. 单击【Create】保存设置，创建完毕。创建完毕的Endpoint支持编辑及删除操作。用户可基于生成的Endpoint URL进行回源拉流操作，从而对直播流进行Distribution。

![img](https://main.qcloudimg.com/raw/219346607e144822c43173ba1e055905.png)

#### 配置CDN分发

StreamPackage支持在Channel中配置直播CDN，配置完成后您可将StreamPackage Channel中的直播流直接通过直播CDN来进行分发。这需要您先开通云直播，并对StreamPackage与云直播完成**双向授权**操作。

在阅读以下内容前，解释相关名词：

- 直播CDN：标准直播（LVB）中的CDN，StreamPackage整合复用了该项能力，让您StreamPackage的Channel中的直播流可以快速通过LVB的CDN进行分发播放。
- CDN域名/CDN播放域名：LVB CDN中的播放域名，用于直播流分发。


1. 开通LVB服务

在进行腾讯云CDN配置前，请先确保您已经[开通腾讯云直播服务](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)。

2. 授权StreamPackage访问LVB

回到StreamPackage控制台，打开您需要配置CDN分发的Channel详情页，选择CDN选项，点击下方【Authorization】开始授权StreamPackage访问LVB服务流程。

>? 完成StreamPackage访问LVB的授权后，StreamPackage可为Channel创建一个直播播放域名。

![img](https://main.qcloudimg.com/raw/d0f1bc546937e0fbbb111bd6d97f2557.png)

**点击【Click here】授权StreamPackage使用LVB CDN。**若要使用StreamPackage功能，需允许StreamPackage访问您的部分资源，他们将通过服务角色访问这些授权资源，以实现当前的功能。点击【Authorization Now】跳转至【角色管理】，单击【Grant】将访问相关服务API的权限授予**StreamPackage**。

![img](https://main.qcloudimg.com/raw/c2e6a9006094003091539f31d1d4c63c.png)![img](https://main.qcloudimg.com/raw/a6476145b574ebbfe7f828dbbbfce984.png)

![img](https://main.qcloudimg.com/raw/b18b2fbb7440d557ee82093d44660258.png)

自动跳转回StreamPackage控制台，点击【Authorize completed】，提示已授权StreamPackage使用LVB CDN。

![img](https://main.qcloudimg.com/raw/2e7a6e29600485b593323658cf738b7d.png)

![img](https://main.qcloudimg.com/raw/3374604fff9c19ec580eb6a43af7f86e.png) 

点击【Next】进入下一步。

3. 授权LVB访问StreamPackage

**单击【Click here】转到CDN控制台，并授权LVB CDN使用StreamPackage。LVB控制台授权状态已变为【Activated】。**

![img](https://main.qcloudimg.com/raw/3be8efcd4c8302b15df46be54daebed4.png)

![img](https://main.qcloudimg.com/raw/c63def0152b6d95901929b7abc093d59.png)

回到StreamPackage控制台界面，点击【Completed】

![img](https://main.qcloudimg.com/raw/2616575aa0b6d56323eafcfac0aec9f8.png)


此时显示已授权LVB CDN使用StreamPackage。点击下方【Authorization Completed】，**至此，您已经完成了StreamPackage与LVB的双向授权（即可通过StreamPackage的Channel快速创建一个CDN播放域名，LVB也可以回源到Channel进行拉流分发）**

![img](https://main.qcloudimg.com/raw/5e3084a78e0ce61a0a9eabd5a61c9a90.png)


4. 快速配置CDN播放域名

完成上述双向授权后，打开CDN选项栏，点击【Edit Configuration】即可快速进行CDN配置。

![img](https://main.qcloudimg.com/raw/4d2031b1fe8c42a1a05c7b619291e1dd.png)

输入您用于CDN播放的域名，点击【Confirm】即配置完成。

![img](https://main.qcloudimg.com/raw/ee8a3bf7ab68b655bba010df76bac910.png)

![img](https://main.qcloudimg.com/raw/1fd6d414ef8fb41cee52c0a489c79395.png)

>?
>- 新创建的播放域名添加成功后，系统会为您自动分配一个 CNAME 域名（以.liveplay.myqcloud.com为后缀）。CNAME 域名不能直接访问，您需要在域名服务提供商处完成 CNAME 配置，配置生效后才可享受云直播服务。CNAME相关操作详见：[CNAME 配置](https://intl.cloud.tencent.com/document/product/267/31057)
>- 在StreamPackage配置的CDN播放域名的播放区域默认为中国大陆之外的海外区域（含中国香港、中国台湾、中国澳门）。若您需要在中国大陆地区进行直播分发，根据中国大陆的相关法律规定，需要对播放域名进行备案，请点击【Go to LVB CDN console】前往直播控制台做更多操作。

#### 通过配置的播放域名进行播放

StreamPackage的Channel配置绑定CDN播放域名后，将Endpoint的播放地址中的域名替换为CDN播放域名即可正常播放。

例如：

您某个Channel的Endpoint拉流地址为：

http://123456789.ap-seoul.streampackage.srclivepull.myqcloud.com/v1/017697a3513109df73abda3c4b26/017697a918bf09dfabc033b04d43/main.m3u8

则您的CDN播放地址为：

http://CDN播放域名/v1/017697a3513109df73abda3c4b26/017697a918bf09dfabc033b04d43/main.m3u8

配置完成后请联系我们对你的配置进行优化，以确保您的使用体验更佳。

>? 使用直播CDN进行分发播放会产生直播流量费用，详见[云直播费用](https://intl.cloud.tencent.com/zh/document/product/267/2818?lang=zh&pg=)。

### 四、编辑和删除Channel

在Channel列表页，用户可对创建完成的所有Channel进行管理。在操作栏右侧点击【Info】/【Edit】/【Delete】，可查看Channel的详情、重新编辑和删除Channel操作。当Channel已有endpoint节点时不支持删除，若需要删除Channel需先删除包含的所有Endpoint节点。

![img](https://main.qcloudimg.com/raw/bd7b3e8c0033d6591f5b61b2974dc12a.png)