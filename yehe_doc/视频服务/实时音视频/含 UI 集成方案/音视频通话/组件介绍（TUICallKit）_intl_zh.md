<style>
    .card-container {
        width: 380px;
        display: block;
        float: left;
        padding-left: 15px;
        padding-right: 15px;
        box-sizing: border-box;
    }

    .card {
        border-radius: 10px;
        padding-top: 10px;
        padding-left: 10px;
        padding-right: 10px;
        padding-bottom: 10px;
        margin-top: 30px;
        border: 1px solid #ebeef5;
        background-color: #fff;
        overflow: hidden;
        box-shadow: 0 2px 12px 0 rgb(0 0 0 / 10%);
        text-align: center;
    }
    
    .markdown-text-box img {
        box-shadow: none;
    }


    .titlename {
                color:#191919;
        position: relative;
        top: -2px;
                font-weight: bolder;
                font-size: larger;
    }
        
        @media (max-width: 768px){
                .card-container,
                .scene-card-container{
                        width: 100%;
                }
                .scene-card > div{
                        width: 100%!important;
                        margin-left: 0!important;
                }
                img {
        box-shadow: none;
    }
        }
</style>

## 组件介绍

TUICallKit 是腾讯云推出一款音视频通话 UI 组件，通过集成该组件，您只需要编写几行代码就可以为您的 App 添加音视频通话功能，并且支持离线唤起能力。TUICallKit 支持 Android、iOS、Web 等多个开发平台，基本功能如下图所示：

![](https://qcloudimg.tencent-cloud.cn/raw/af697557d2746585a0d9f4b894dc42d5.png)

>! 基于开发者反馈和市场需求调研，2022年08月 TUICalling 正式升级为 TUICallKit，新的组件升级了群内多人通话和离线唤醒等功能，并且配备了更低折扣的音视频通话 SDK 套餐包以及60天的免费试用期，期待您的关注与使用！

#### 功能优势
- 接入方便：提供带 UI 的开源组件，节省90%开发时间，快速上线音视频通话应用。
- 平台互通：各平台的 TUICallKit 组件支持相互拨打、接听、挂断等，互联互通。
- 多人通话：不仅仅支持1对1视频通话，还支持在群组内发起多人视频通话。
- 离线推送：支持 Android&iOS 离线推送，被叫用户 App 不在线时也能收到新的来电消息。

#### 适用场景

两人或多人进行音视频通话，覆盖游戏社交、在线客服、视频客服、在线问诊、保险咨询等场景。

## TUICallKit  下载

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
	<div class="card-container">
			<div class="card">
					 <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
					<p class="titlename">Android TUICallKit</p>
					<p style="color:#586376;">类“微信” UI，支持 1V1 通话、群组通话、悬浮窗、离线推送等特性，功能强大。</p>
					<a style="margin-left: 10px;" href="https://github.com/tencentyun/TUICalling"><b>Github </b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/50991"><b>快速接入</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51004"><b>API 参考</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51022"><b>常见问题</b></a>
			</div>
	</div>
	<div class="card-container">
			<div class="card">
					 <img src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
					<p class="titlename">iOS TUICallKit</p>
					<p style="color:#586376;">类“微信” UI，支持 1V1 通话、群组通话、悬浮窗、离线推送等特性，功能强大。</p>
					<a style="margin-left: 10px;" href="https://github.com/tencentyun/TUICalling"><b>Github </b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/50992"><b>快速接入</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51010"><b>API 参考</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51023"><b>常见问题</b></a>
			</div>
	</div>
	<div class="card-container">
			<div class="card">
					 <img src="https://main.qcloudimg.com/raw/7e2651085e3e3c6e32190e401a6dfd32.svg" data-nonescope="true">
					<p class="titlename">Web TUICallKit</p>
					<p style="color:#586376;">类“微信” UI，支持 1V1 通话、群组通话、悬浮窗、离线推送等特性，功能强大。</p>
					<a style="margin-left: 10px;" href="https://github.com/tencentyun/TUICalling"><b>Github </b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/50993"><b>快速接入</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51014"><b>API 参考</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51024"><b>常见问题</b></a>
			</div>
	</div>
</div>

## 开源建设

您可以在 [**这里**](https://github.com/tencentyun/TUICalling/tree/open) 找到升级前的 TUICalling 开源项目。