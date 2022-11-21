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

## Overview

`TUICallKit` is a UI component for audio/video calling. After integrating it and writing a few simple lines of code, your application will be able to support audio/video calls and offline call push so users can receive calls even when the application is offline. It supports Android, iOS, and web platforms, and provides the following basic features:

![](https://qcloudimg.tencent-cloud.cn/raw/af697557d2746585a0d9f4b894dc42d5.png)

>! Based on feedback from developers and market research, `TUICalling` was officially upgraded to `TUICallKit` in August 2022. The new component version upgrades features such as group call and offline call push and offers audio/video call SDK plans at higher discounts and a 60-day free trial.

#### Strengths
- Easy integration: `TUICallKit` provides open-source components with UIs to help you save 90% of the development time and quickly release audio/video call applications.
- Platform interconnection: The `TUICallKit` component for various platforms can call, answer, hang up, and interconnect with each other.
- Group call: In addition to one-to-one video calls, `TUICallKit` also supports group video calls with multiple group members.
- Offline push: `TUICallKit` supports offline push on Android and iOS, so that callees can receive new incoming call notifications even when their application is offline.

#### Use cases

`TUICallKit` is ideal for audio/video calls between two or more people in various scenarios such as in-game communication, online customer service, online medical consultation, and insurance consultation.

## `TUICallKit` Download

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
	<div class="card-container">
			<div class="card">
					 <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
					<p class="titlename">TUICallKit for Android</p>
					<p style="color:#586376;">With UI similar to WeChat, it supports various powerful features, including one-to-one calls, group calls, floating window, and offline push.</p>
					<a style="margin-left: 10px;" href="https://github.com/tencentyun/TUICalling"><b>tencentyun/TUICallKit</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/50991"><b>Quick Integration</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51004"><b>API Documentation</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51022"><b>FAQs</b></a>
			</div>
	</div>
	<div class="card-container">
			<div class="card">
					 <img src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
					<p class="titlename">TUICallKit for iOS</p>
					<p style="color:#586376;">With UI similar to WeChat, it supports various powerful features, including one-to-one calls, group calls, floating window, and offline push.</p>
					<a style="margin-left: 10px;" href="https://github.com/tencentyun/TUICalling"><b>tencentyun/TUICallKit</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/50992"><b>Quick Integration</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51010"><b>API Documentation</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51023"><b>FAQs</b></a>
			</div>
	</div>
	<div class="card-container">
			<div class="card">
					 <img src="https://main.qcloudimg.com/raw/7e2651085e3e3c6e32190e401a6dfd32.svg" data-nonescope="true">
					<p class="titlename">TUICallKit for web</p>
					<p style="color:#586376;">With UI similar to WeChat, it supports various powerful features, including one-to-one calls, group calls, floating window, and offline push.</p>
					<a style="margin-left: 10px;" href="https://github.com/tencentyun/TUICalling"><b>tencentyun/TUICallKit</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/50993"><b>Quick Integration</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51014"><b>API Documentation</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51024"><b>FAQs</b></a>
			</div>
	</div>
</div>

## Open Source Construction

You can find the pre-upgrade TUICalling open source project [**here**](https://github.com/tencentyun/TUICalling/tree/open).