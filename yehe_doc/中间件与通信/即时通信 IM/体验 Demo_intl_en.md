<style>
    .card-container {
         width: 350px;
        display: block;
        float: left;
        padding-left: 15px;
        padding-right: 15px;
        box-sizing: border-box;
    }

    .card {
        height: 190px; 
        border-radius: 10px;
        padding-top: 20px;
        padding-left: 10px;
        padding-right: 10px;
        padding-bottom: 10px;
        margin-top: 10px;
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
<style>
.markdown-text-box table th,.markdown-text-box table td{text-align: center;}
.inbuttom{height: 30px;width: 150px;min-width: 24px;padding: 0 20px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;vertical-align: middle;white-space: nowrap;}
.preview-demo-section .preview-demo-item {
    display: inline-block;
    width: 280px;
    height: 220px;
    background: #fff;
    box-shadow: 0 1px 8px 0 rgba(156,175,204,0.25);
    border-radius: 1px;
    text-align: center;
    padding: 0 15px;
    margin: 10px 10px 10px 0;
    vertical-align: top;
}

.preview-demo-section .preview-demo-item .demo-item-header {
    margin-top: 30px;
}
.preview-demo-section .preview-demo-item .demo-item-desc {
    font-size: 12px;
}

.preview-demo-section .preview-demo-item .demo-item-platform {
    font-size: 20px;
    font-weight: bold;
}
.preview-demo-section .preview-demo-item .demo-logo-wrapper {
    line-height: 1;
}
.preview-demo-section .preview-demo-item .demo-item-header img {
    box-shadow: none;
    width: 40px;
    height: 40px;
}
.preview-demo-section .preview-demo-item.style-qrcode .demo-item-download {
    margin-top: 15px;
}
.preview-demo-section .preview-demo-item.style-web .demo-item-download {
    margin-top: 46px;
}
.preview-demo-section .preview-demo-item.style-single-download-btn .demo-item-download {
    margin-top: 50px;
}
.preview-demo-section .preview-demo-item.style-flutter .demo-item-download {
    margin-top: 55px;
}
.preview-demo-section .preview-demo-item.style-electron .demo-item-download {
    margin-top: 25px;
}
.preview-demo-section .preview-demo-item.style-electron .demo-item-download-btn:first-child {
    margin-bottom: 10px;
}
.preview-demo-section .preview-demo-item .demo-item-download img {
    box-shadow: none;
    width: 110px;
    height: 110px;
}
.preview-demo-section .preview-demo-item .demo-item-download .demo-item-download-btn {
    background-color: #00a4ff;
    border-radius: 20px;
    color: #fff;
    font-size: 14px;
    width: 135px;
    height: 35px;
    line-height: 35px;
    margin: 0 auto;
}
.preview-demo-section .preview-demo-item.style-web .demo-item-download .demo-item-download-btn {
    color: #fff;
    background-color: #00a4ff;
    height: 24px;
    line-height: 24px;
    margin-bottom: 6px;
}
.preview-demo-section .preview-demo-item .demo-item-download .demo-item-download-btn:hover {
    cursor: pointer;
}
.markdown-text-box img {
        box-shadow: none;
        background:0;
}
.support-platform{
    width: 56px;
    height: 24px;
    font-family: PingFangSC-Regular;
    font-weight: 400;
    font-size: 14px;
    color: #333333;
    letter-spacing: 0;
    line-height: 24px;
}
.tab-bottom{
    width: 100%;
    height: 172px;
    background: #EDF1F5;
    display:flex;
    justify-content: center;
    align-items: center;
}
.tab-bottom .platform-icon{
    text-align:center;
}
.tab-support{
    height:24px;
    text-align:center;
    padding: 24px 0 0 0;
}
.platform-img{
    width: 18px;
    height: 18px;
    box-shadow: 0 0 0 0 #FFFFFF;
    vertical-align:-4px;
    padding:0 8px;
}
.try-icon{
    width: 16px;
    height: 16px !important;
    margin-left: 5px !important;
    vertical-align: -3px !important;
}
.tab-experience{
    width: 150px;
    height: 40px;
    background: #FFFFFF;
    box-shadow: 0 2px 4px 0 rgba(215,226,236,0.40);
    border-radius: 20px;
    border:0;
    color:#06A4FF;
    line-height:40px;
}
.tab-img {
    width: 100%;
    background-color: #F4F7FA;
    padding: 0 0 18px 0;
}
.tab-experience-button{
    height: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
    
}
.rno-tabs-operation-bd {
    padding: 18px 0 0 0;
    background-color: #F4F7FA;
}
ul.rno-tabs-operation {
    padding-top: 4px;
    border-bottom: #E5E8ED 1px solid;
    position: relative;
    padding-left: 0;
    font-size: 0;
    margin-bottom: 0;
    height: 56px;
    background-color: #F4F7FA;
}
.rno-tabs-operation-item.active {
    border-bottom-color: #06A4FF;
}
.rno-tabs-operation-item {
    display: inline-block;
    text-align: center;
    position: relative;
    cursor: pointer;
    padding-bottom: 4px;
    overflow: hidden;
    vertical-align: bottom;
    margin-bottom: -1px;
    margin-right: 20px;
    border-bottom: 2px solid transparent;
    height: 36px;
    margin-top: 19px;
}
.rno-tabs-operation-item.active>a {
    color: #00a4ff;
}
</style>


### Free demo
<div class="preview-demo-section" id="demo-card">
   <div class="preview-demo-item style-web">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/ff4dc34a1c72fdb26fc41c1268898025.svg" alt="">
            </div>
            <div class="demo-item-platform">Web</div>
        </div>
        <div class="demo-item-desc">
           Try now
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://web.sdk.qcloud.com/im/demo/intl/index.html');reportEvent({name: 'demo-click-web', ext1: 'api-sample'});">In-App Chat</div>
        </div>
    </div>
    </div>





## Demo Features

<dx-tabs>
::: In-App Chat
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/4562be8179a1534efb17d33428239c82.png"/>
</div>
<div class="tab-bottom">
    <div>
    <div class="platform-icon">
        <span class="support-platform">Supported platforms</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/7adfb7daedcc48ead500f1ddf6bdb237.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
       <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/864f8562e1b7780e6f23e1f2987f9ff9.svg" class="platform-img">Flutter</span>
        <span class="support-platform"><img src="" class="platform-img"></span>
    </div>
    <div class="tab-experience-button"><a href="#demo-.E5.8F.8A.E8.A7.A3.E5.86.B3.E6.96.B9.E6.A1.88.E4.B8.8B.E8.BD.BD"><button class="tab-experience">Source Code Download</button></a></div>
    <div style="text-align:center;">You can click <a href="https://www.tencentcloud.com/document/product/1047/45914" style="color:#06A4FF;">Get Started</a> to learn how to quickly run the demo. You can also click <a href="https://intl.cloud.tencent.com/document/product/1047/50055" style="color:#06A4FF;">Integration Solution</a> to learn more about the features.</div>
    </div>
</div>
:::
::: Conversation
<div class="tab-img">
    <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/C7Qm895_%E4%BC%9A%E8%AF%9D%E7%AE%A1%E7%90%86%402x.png"/>
</div>
<div class="tab-bottom">
    <div>
    <div class="platform-icon">
        <span class="support-platform">Supported platforms</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/7adfb7daedcc48ead500f1ddf6bdb237.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
       <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/864f8562e1b7780e6f23e1f2987f9ff9.svg" class="platform-img">Flutter</span>
        <span class="support-platform"><img src="" class="platform-img"></span>
    </div>
    <div class="tab-experience-button"><a href="#demo-.E5.8F.8A.E8.A7.A3.E5.86.B3.E6.96.B9.E6.A1.88.E4.B8.8B.E8.BD.BD"><button class="tab-experience">Source Code Download<class="try-icon"></button></a></div>
    <div style="text-align:center;">You can click <a href="https://www.tencentcloud.com/document/product/1047/45914" style="color:#06A4FF;">Get Started</a> to learn how to quickly run the demo. You can also click <a href="https://intl.cloud.tencent.com/document/product/1047/34320" style="color:#06A4FF;">Integration Solution</a> to learn more about the features.</div>
    </div>
</div>
:::
::: Group Management
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/583ddd04d57be2129c6005165828033c.png"/>
</div>
<div class="tab-bottom">
    <div>
    <div class="platform-icon">
        <span class="support-platform">Supported platforms</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/7adfb7daedcc48ead500f1ddf6bdb237.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/864f8562e1b7780e6f23e1f2987f9ff9.svg" class="platform-img">Flutter</span>
        <span class="support-platform"><img src="" class="platform-img"></span>
    </div>
    <div class="tab-experience-button"><a href="#demo-.E5.8F.8A.E8.A7.A3.E5.86.B3.E6.96.B9.E6.A1.88.E4.B8.8B.E8.BD.BD"><button class="tab-experience">Source Code Download<class="try-icon"></button></a></div>
    <div style="text-align:center;">You can click <a href="https://www.tencentcloud.com/document/product/1047/45914" style="color:#06A4FF;">Get Started</a> to learn how to quickly run the demo. You can also click <a href="https://intl.cloud.tencent.com/document/product/1047/34328" style="color:#06A4FF;">Integration Solution</a> to learn more about the features.</div>
    </div>
</div>
:::
</dx-tabs>
</dx-tabs>
</dx-tabs>  

<dx-tabs>
::: User Profile and Relationship Chain
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/7cabab98274e99291cc0186f2fd34f14.png"/>
</div>
<div class="tab-bottom">
    <div>
    <div class="platform-icon">
        <span class="support-platform">Supported platforms</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/7adfb7daedcc48ead500f1ddf6bdb237.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
       <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/864f8562e1b7780e6f23e1f2987f9ff9.svg" class="platform-img">Flutter</span>
        <span class="support-platform"><img src="" class="platform-img"></span>
    </div>
    <div class="tab-experience-button"><a href="#demo-.E5.8F.8A.E8.A7.A3.E5.86.B3.E6.96.B9.E6.A1.88.E4.B8.8B.E8.BD.BD"><button class="tab-experience">Source Code Download<class="try-icon"></button></a></div>
    <div style="text-align:center;">You can click <a href="https://www.tencentcloud.com/document/product/1047/45914" style="color:#06A4FF;">Get Started</a> to learn how to quickly run the demo. You can also click <a href="https://intl.cloud.tencent.com/document/product/1047/34332" style="color:#06A4FF;">Integration Solution</a> to learn more about the features.</div>
    </div>
</div>
:::
::: Offline push
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/03ec8c8db4a2431ad835dac757be6af6.jpg"/>
</div>
<div class="tab-bottom">
    <div>
    <div class="platform-icon">
        <span class="support-platform">Supported platforms</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/7adfb7daedcc48ead500f1ddf6bdb237.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
       <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/864f8562e1b7780e6f23e1f2987f9ff9.svg" class="platform-img">Flutter</span>
        <span class="support-platform"><img src="" class="platform-img"></span>
    </div>
    <div class="tab-experience-button"><a href="#demo-.E5.8F.8A.E8.A7.A3.E5.86.B3.E6.96.B9.E6.A1.88.E4.B8.8B.E8.BD.BD"><button class="tab-experience">Source Code Download<class="try-icon"></button></a></div>
    <div style="text-align:center;">You can click <a href="https://www.tencentcloud.com/document/product/1047/45914" style="color:#06A4FF;">Get Started</a> to learn how to quickly run the demo. You can also click <a href="https://intl.cloud.tencent.com/document/product/1047/39156" style="color:#06A4FF;">Integration Solution</a> to learn more about the features.</div>
    </div>
</div>
:::
::: Local Search
<div class="tab_list">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/1f2595db3599daad32316d0fd037f62e.png"/>
</div>
<div class="tab-bottom">
    <div>
    <div class="platform-icon">
        <span class="support-platform">Supported platforms</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/7adfb7daedcc48ead500f1ddf6bdb237.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
       <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/864f8562e1b7780e6f23e1f2987f9ff9.svg" class="platform-img">Flutter</span>
        <span class="support-platform"><img src="" class="platform-img"></span>
    </div>
    <div class="tab-experience-button"><a href="#demo-.E5.8F.8A.E8.A7.A3.E5.86.B3.E6.96.B9.E6.A1.88.E4.B8.8B.E8.BD.BD"><button class="tab-experience">Source Code Download<class="try-icon"></button></a></div>
    <div style="text-align:center;">You can click <a href="https://www.tencentcloud.com/document/product/1047/45914" style="color:#06A4FF;">Get Started</a> to learn how to quickly run the demo. You can also click <a href="https://intl.cloud.tencent.com/document/product/1047/41795" style="color:#06A4FF;">Integration Solution</a> to learn more about the features.</div>
    </div>
</div>
:::
</dx-tabs>
</dx-tabs>
</dx-tabs>



## Demo and Solution Download

<div>
<div style="margin-top: 15px;">
<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden;">
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                                <p class="titlename"> Chat Demo (Android)</p>
                <p style="color:#586376;">Includes all Chat features and the capability to co-anchor in a live stream in a group</p>
                    <div style="margin-top: 13px;" >
                    <a href="https://github.com/tencentyun/TIMSDK/tree/master/Android">Download via GitHub</a>
                                <a style="margin-left: 10px;" href="https://im.sdk.qcloud.com/download/github/TIMSDK.zip">Download via ZIP</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/1047/45914">Integration Guide</a>
                    </div>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                                <p class="titlename"> Chat Demo (iOS)</p>
                <p style="color:#586376;">Includes all Chat features and the capability to co-anchor in a live stream in a group</p>
                    <div style="margin-top: 13px;" >
                    <a  href="https://github.com/tencentyun/TIMSDK/tree/master/iOS">Download via GitHub</a>
                          <a style="margin-left: 10px;" href="https://im.sdk.qcloud.com/download/github/TIMSDK.zip">Download via ZIP</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/1047/45913">Integration Guide</a>
                    </div>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/98394fa5d669de7fb7a187565d138cdb.svg" data-nonescope="true">
                                <p class="titlename"> Chat Demo (Web)</p>
                <p style="color:#586376;">Includes all Chat features and the capability to co-anchor in a live stream in a group</p>
                    <div style="margin-top: 13px;" >
                    <a " href="https://github.com/TencentCloud/chat-uikit-react">Download via GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/1047/45912">Integration Guide</a>
                    </div>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/98394fa5d669de7fb7a187565d138cdb.svg" data-nonescope="true">
                                <p class="titlename"> Chat Demo (Flutter)</p>
                <p style="color:#586376;">Includes the main features of Chat</p>
                     <div style="margin-top: 13px; " >
                    <a href="https://github.com/tencentyun/TIMSDK/tree/master/Flutter/Demo/im-flutter-uikit">Download via GitHub</a>
                     <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/1047/45907">Integration Guide</a></div>
         </div>
            </div>
        </div>
    </div>
</div>
<div>






