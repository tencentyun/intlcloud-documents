直播播放默认通过源码率输出，若需要对播放码率进行限制或者设定，可对播放域名进行转码模板关联。本文将向您介绍如何在播放域名下进行转码模板关联与解绑。

## 注意事项
- 模板配置完后约5分钟 - 10分钟生效。
- 指定转码模板后，后台将生成对应码率的不同播放地址，方便用户选择调用。推流原始分辨率尽可能接近原比率以避免画面拉伸变形。
- 由于 H.265 兼容性不及 H.264，若遇到播放器不支持 H.265 编码，出现播放失败的情况，可配置 [转码模板](https://intl.cloud.tencent.com/document/product/267/31071) 转成 H.264 编码进行播放。
- 第一次访问新的码率地址时，首位触发链接的访问用户会感到加载时间稍长，属正常现象。
- 一个域名可关联多个转码模板，关联后，播放码率将会按照设置的对应转码模板进行转码。
- 转码模板设置数量上限为**50个**。



## 前提条件
- 已登录 [云直播控制台](https://console.cloud.tencent.com/live)，并成功添加 [播放域名](https://intl.cloud.tencent.com/document/product/267/35970)。
- 已 [创建转码模板](https://intl.cloud.tencent.com/document/product/267/31071)。

[](id:conect)
## 关联转码模板
1. 进入[【域名管理】](https://console.cloud.tencent.com/live/domainmanage)，单击需配置的**播放域名**或右侧的【管理】进入域名详情页。
2. 选择【模板配置】页签，单击【转码配置】标签右上角的【编辑】。
3. 选择不同的转码配置模板，为该域名下播放地址指定模板设置的编译方式和码率。
4. 单击【保存】即可。

![](https://main.qcloudimg.com/raw/8ab50571f4260ba070cf3270f8487e30.png)

[](id:descript)
## 转码播放地址说明
配置转码模板后，播放 URL 需增加转码模板名称，拼接方式为：**播放地址_转码模板名称**。若未拼接转码模板名称，则播放的为原始直播流内容。更多播放地址相关内容，请参见  [播放配置](https://intl.cloud.tencent.com/document/product/267/31058)。

**例如：**播放域名关联的转码模板名称为 **hd**，原始播放地址为：
<pre>
http://domain/AppName/StreamName.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName</b>+hex(time))&txTime=hex(time) 
</pre>
若您需获取播放转码后的视频，则需重新生成的新的播放地址，如下：
<pre>
http://domain/AppName/<b style="color:yellow;">StreamName_hd</b>.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName_hd</b>+hex(time))&txTime=hex(time)
</pre>

[](id:Untie)
## 解绑转码模板
1. 进入[【域名管理】](https://console.cloud.tencent.com/live/domainmanage)，单击需配置的播放域名或右侧的【管理】，进入域名详情页。
2. 选择【模板配置】页签，选择【转码配置】。
3. 单击右侧的【编辑】，取消相应模板的勾选。
4. 然后单击【保存】，即可取消模板与域名的关联。
![](https://main.qcloudimg.com/raw/497478a836b8017c7e8be177b26af24d.png)

>? 若需删除模板，可在解绑模板后，进入【功能模板】>[【转码配置】](https://console.cloud.tencent.com/live/config/transcode)进行删除操作，具体请参见 [删除模板](https://intl.cloud.tencent.com/document/product/267/31071#delect)。
