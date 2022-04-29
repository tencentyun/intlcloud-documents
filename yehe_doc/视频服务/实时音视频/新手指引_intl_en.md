<style>

.tp-grid__row.tp-grid--gutter-5n {
    margin-right: -10px;
    margin-bottom: -20px;
    margin-left: -10px;
}

.tp-grid__row {
    display: -webkit-box;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
    -webkit-flex-flow: row wrap;
    -ms-flex-flow: row wrap;
    flex-flow: row wrap;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    margin-right: 0;
    margin-left: 0;
    -webkit-box-orient: horizontal;
    -webkit-box-direction: normal;
}

.tp-grid__row.tp-grid--gutter-5n .tp-grid__col {
    margin-bottom: 20px;
    padding-right: 10px;
    padding-left: 10px;
}
.tp-grid__col--6 {
    display: block;
    -webkit-flex: 0 0 auto;
    -ms-flex: 0 0 auto;
    flex: 0 0 auto;
    width: 25%;
    -webkit-box-flex: 0;
}

.tp-grid__col {
    display: block;
    -webkit-flex: 1 1 auto;
    -ms-flex: 1 1 auto;
    flex: 1 1 auto;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    padding-right: 0;
    padding-left: 0;
    font-size: 14px;
    -webkit-box-flex: 1;
}

	.tpm-experience__item {
	display: flex;
	height: 100%;
	background-image: linear-gradient(0deg,#fff,#f3f5f8);
	border: 2px solid #fff;
	box-shadow: 8px 8px 20px 0 rgb(55 99 170 / 10%), -8px -8px 20px 0 #fff;
	border-radius: 4px;
	padding: 20px 28px;
	justify-content: space-between;
		}
		
	.tpm-experience__item-cnt {
	flex: 1;
	max-width: 192px;
   }

 .tpm-experience__item-hd {
    padding-top: 8px; 
  }
	
	.tpm-experience__item-title {
	font-size: 18px;
	color: #000;
	line-height: 26px;
	font-weight: 500;
	display: inline-block;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
	vertical-align: top;
}
	
	.tpm-experience__item-qr {
	width: 100px;
	height: 100px;
	background: #fff;
	border-radius: 4px;
	padding: 4px;
	margin-left: 12px;
	}


element.style {
}
.tpm-experience__item-btns {
    margin-left: 12px;
    display: flex;
    flex-direction: column;
    justify-content: center;
}

 .tpm-btn {
    display: inline-block;
    box-sizing: border-box;
    min-width: 104px;
    height: 36px;
    padding: 0 24px;
    color: #fff;
    font-size: 14px;
    line-height: 34px;
    white-space: nowrap;
    text-align: center;
    text-decoration: none;
    vertical-align: middle;
    background-color: #0052d9;
    border: 1px solid transparent;
    outline: 0 none;
    cursor: pointer;
    box-shadow: 8px 8px 20px 0 rgb(55 99 170 / 10%);
}

.tpm-experience__item .tpm-btn {
    min-width: 120px;
    margin-bottom: 12px;
    box-shadow: 8px 8px 20px 0 rgb(55 99 170 / 10%);
    -webkit-font-smoothing: auto;
}

.tpm-btn.size-s {
    min-width: 104px;
    height: 32px;
    padding: 0 24px;
    line-height: 30px;
}

    .card-container {
        width: 293px;
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
    
    .scene-card-container {
        width: 450px;
        display: block;
        float: left;
        padding-left: 15px;
        padding-right: 15px;
        box-sizing: border-box;
    }
    
    .scene-card {
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
    }
    
    .image_card {
        margin-top: 10px;
        border: 1px solid #ebeef5;
        box-shadow: 0 2px 1px 0 rgb(0 0 0 / 10%);
    }
    .markdown-text-box img {
        box-shadow: none;
    }


    h3 {
        position: relative;
        top: -2px;
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


## Getting to Know TRTC 
TRTC is a set of low-latency and high-quality audio/video communication services provided by Tencent Cloud. It offers stable and reliable audio/video transmission capabilities at a low cost. You can use it to quickly build video call, online education, interactive live streaming, online conferencing, and other audio/video communication applications that require low latency.
<div class="doc-video-mod"><iframe src="https://cloudcache.intl.tencent-cloud.com/cms/backend-cms/Qv57087_%E3%80%8A%E5%AE%9E%E6%97%B6%E9%9F%B3%E8%A7%86%E9%A2%91%20TRTC%E3%80%8B%E8%8B%B1-%E8%85%BE%E8%AE%AF%E4%BA%91_0117.mp4"></iframe></div>

## Try it out
We offer a demo app for you to try out TRTC services. It integrates the following features:
<div style="position: relative; box-sizing: border-box;  overflow:hidden">
    <a href="https://intl.cloud.tencent.com/document/product/647/35076" target="view_window">
            <div class="image_card">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/bb2facb7474a5c065b14d2996ead8d48.png"/>
            </div>
    </a>
</div>

- **Video call**: Call features similar to those in WeChat; supports view switch, beauty filters, and network connection monitoring.
- **Group conference**: Supports communication among multiple people in the same room, ideal for online conferencing and education applications.
- **Showroom streaming**: Supports beauty filters, song accompaniments, likes, on-screen commenting, and co-anchoring.
- **Duet**: Allows two anchors to sing a song together with low latency.
- **Online karaoke**: Allows over 10,000 audience members; supports audio interaction, song accompaniments, and lyric syncing.


## Integration
We offer two solutions for you to quickly integrate TRTC features into your application.

### Solution 1 (UI included)
We offer source code for a set of standard UI components. You can integrate the components you need into your project and load them when necessary. Normally, you can complete the integration in about an hour using this solution.

<div style="position: relative; box-sizing: border-box; padding-bottom: 10px; margin-bottom: 10px; overflow:hidden;">
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/4f6e018388bce36b0f5b7807ed76c82a.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">Audio/Video Call</h3>
                <p style="color:#586376" ;>Component-based UI design to help you quickly implement WeChat-like video call applications</p>
                <a href="https://github.com/tencentyun/TUICalling">GitHub source code</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/36065">Integration guide</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/129edf43d9adf4df6f022dec79ba6db0.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">Video Conferencing</h3>
                <p style="color:#586376" ;>Low-code solution with component-based UI design to help you quickly implement video conferencing, online dating, and remote interviewing applications</p>
                <a href="https://github.com/tencentyun/TUIMeeting">GitHub source code</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/37284">Integration guide</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/ab32f135f2847eaf22733e9a9ad1636a.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">Interactive Audio Streaming</h3>
                <p style="color:#586376;" ;>Low-code solution with component-based UI design to help you quickly implement audio chat room applications</p>
                <a href="https://github.com/tencentyun/TUIVoiceRoom">GitHub source code</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/37287">Integration guide</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/ab32f135f2847eaf22733e9a9ad1636a.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">Interactive Video Streaming</h3>
                <p style="color:#586376;" ;>Low-code solution with component-based UI design to help you quickly implement live streaming and same/cross-room communication.</p>
                <a href="https://github.com/tencentyun/TUILiveRoom">GitHub source code</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/36060">Integration guide</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/7a7b51c1536587f0fea130d375661552.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">Online Karaoke</h3>
                <p style="color:#586376;" ;>Low-code solution with component-based UI design to help you quickly implement online karaoke applications</p>
                <a href="https://github.com/tencentyun/TUIKaraoke">GitHub source code</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/41940">Integration guide</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/7a7b51c1536587f0fea130d375661552.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">Duet</h3>
                <p style="color:#586376;" ;>Low-code solution with component-based UI design to help you quickly enable real-time duet applications</p>
                <a href="https://github.com/tencentyun/TUIChorus">GitHub source code</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/42689">Integration guide</a>
            </div>
        </div>
    </div>
</div>

### Solution 2 (No UI)
You can also integrate the TRTC SDK directly into your project and use the SDK APIs to implement the features you need. This solution offers greater flexibility. However, because you have to design the UI and interactions by yourself, the integration may take a longer time.

We offer API examples for different platforms to help you quickly learn how to use the APIs of the SDK. You can find the API examples for basic TRTC features in the `Basic` folder of the SDK source code package and advanced features (such as resolution setting, background music, and network speed testing) in the `Advanced` folder.

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
    <a href="https://github.com/LiteAVSDK/TRTC_iOS/tree/main/TRTC-API-Example-OC" target="view_window">
        <div class="card-container">
            <div class="card">
                <img class="icon" src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                <h3>iOS API Examples</h3>
                <p>Demonstrates how to use RTC iOS APIs<br>Build an RTC application from scratch</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/TRTC_Android/tree/main/TRTC-API-Example" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                <h3>Android API Examples</h3>
                <p>Demonstrates how to use RTC Android APIs<br>Build an RTC application from scratch</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/tencentyun/TRTCSDK/tree/master/Windows/QTDemo" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/104e3aadbd4515f61c3f2f5378948cfb.svg" data-nonescope="true">
                <h3>Windows API Examples</h3>
                <p>Demonstrates how to use RTC Windows APIs<br>Build an RTC application from scratch</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/Live_Mac/tree/main/QTDemo" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/98394fa5d669de7fb7a187565d138cdb.svg" data-nonescope="true">
                <h3>macOS API Examples</h3>
                <p>Demonstrates how to use RTC macOS APIs<br>Build an RTC application from scratch</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/TRTC_Web/tree/main/base-react-next" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/7e2651085e3e3c6e32190e401a6dfd32.svg" data-nonescope="true">
                <h3>Web API Examples</h3>
                <p>Demonstrates how to use RTC web APIs<br>Build an RTC application from scratch</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/TRTC_Electron/tree/main/TRTC-API-Example" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/559e93ed3c05c3916300b04b0b09e7aa.svg" data-nonescope="true">
                <h3>Electron API Examples</h3>
                <p>Demonstrates how to use RTC Electron APIs<br>Build an RTC application from scratch</p>
            </div>
        </div>
    </a>
</div>

