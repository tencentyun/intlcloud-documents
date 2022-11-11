<style>
.markdown-text-box table th,.markdown-text-box table td{text-align: center;}
.inbuttom{height: 30px;width: 150px;min-width: 24px;padding: 0 20px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;vertical-align: middle;white-space: nowrap;}
.preview-demo-section .preview-demo-item {
    display: inline-block;
    width: 186px;
    height: 300px;
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
    display: flex;
    justify-content: center;
    align-items: center;
}
.tab-bottom .platform-icon{
    text-align: center;
}
.tab-support{
    height:24px;
    text-align: center;
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

<div class="preview-demo-section" id="demo-card">
    <div class="preview-demo-item style-web">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/ff4dc34a1c72fdb26fc41c1268898025.svg" alt="">
            </div>
            <div class="demo-item-platform">Web</div>
        </div>
        <div class="demo-item-desc">
           オーディオおよびビデオ通話、多人数での会議<br/>インタラクティブブロードキャストなど
        </div>
        <div class="demo-item-download">
           <div class="demo-item-download-btn" onclick="window.open('https://tcms-demo.tencentcloud.com/exp-center/index.html#/home?s_url=https%3A%2F%2Ftrtc.tencentcloud.com%2F');reportEvent({name: 'demo-click-web', ext1: 'api-sample'});">今すぐ体験</div>
        </div>
    </div>
    <div class="preview-demo-item style-qrcode">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/53be7f245c4d11d3aefcb6dc53918757.svg" alt="">
            </div>
            <div class="demo-item-platform">Android</div>
        </div>
        <div class="demo-item-desc">
            オーディオビデオ通話<br>インタラクティブストリーミング
        </div>
        <div class="demo-item-download">
            <img src="https://main.qcloudimg.com/raw/8a603ced0a61983018c794df842f7029.png" data-nonescope="true">
        </div>
    </div>
    <div class="preview-demo-item style-qrcode">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/36154dc8bb7c93826dbdc6fdcec4e194.svg" alt="">
            </div>
            <div class="demo-item-platform">iOS</div>
        </div>
        <div class="demo-item-desc">
            オーディオビデオ通話<br>インタラクティブストリーミング
        </div>
        <div class="demo-item-download">
            <img src="https://qcloudimg.tencent-cloud.cn/raw/eebba4153838ac9252eeab3275215c2f.png" data-nonescope="true">
        </div>
    </div>
    <div class="preview-demo-item style-single-download-btn">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/7622934bfd307936181d3a57ed69706d.svg" alt="">
            </div>
            <div class="demo-item-platform">Windows</div>
        </div>
        <div class="demo-item-desc">
            オーディオビデオ通話、複数参加者会議<br>ボイスチャットルーム
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Win_Demo.exe');reportEvent({name: 'demo-click-native', ext1: 'windows'});">今すぐダウンロード</div>
        </div>
    </div>
    <div class="preview-demo-item style-single-download-btn">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/2f867a868913c590fbb2929b8b240f45.svg" alt="">
            </div>
            <div class="demo-item-platform">Mac OS</div>
        </div>
        <div class="demo-item-desc">
            オーディオビデオ通話、複数参加者会議<br>ボイスチャットルーム
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Mac_Demo.tar.bz2');reportEvent({name: 'demo-click-native', ext1: 'windows'});">今すぐダウンロード</div>
        </div>
    </div>
    <div class="preview-demo-item style-flutter">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/0fae0aca728ba2ce98e66d1b9641aa56.svg" alt="">
            </div>
            <div class="demo-item-platform">Flutter</div>
        </div>
        <div class="demo-item-desc">
            オーディオビデオ通話 複数参加者会議など
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://comm.qq.com/im_demo_download/trtc_flutter_demo.apk');reportEvent({name: 'demo-click-flutter', ext1: 'android'});">今すぐダウンロード</div>
        </div>
    </div>
    <div class="preview-demo-item style-electron">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/96a6b7e86eb8d7a93f830d3686d3164c.svg" alt="">
            </div>
            <div class="demo-item-platform">Electron</div>
        </div>
        <div class="demo-item-desc">
            オーディオビデオ通話、複数参加者会議<br>画面共有など
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/TUIRoom-Electron/TUIRoom-Electron-windows-latest.zip');reportEvent({name: 'demo-click-electron', ext1: 'windows'});">Windows</div>
            <div class="demo-item-download-btn" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/TUIRoom-Electron/TUIRoom-Electron-mac-latest.zip');reportEvent({name: 'demo-click-electron', ext1: 'mac'});">Mac OS</div>
        </div>
    </div>
</div> 


## オーディオビデオ通話シーン

<dx-tabs>
::: iOS&Android
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/990efb74019c885eccc47468afba9363.png"/>
</div>
<div class="tab-bottom">
    <div>
    <div class="platform-icon">
        <span class="support-platform">Demoの対応プラットフォーム</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/7adfb7daedcc48ead500f1ddf6bdb237.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
        <span class="support-platform"><img src="" class="platform-img"></span>
    </div>
    <div class="tab-experience-button"><a href="#demo-card"><button class="tab-experience">今すぐトライアル<img src="https://qcloudimg.tencent-cloud.cn/raw/8b41f1a6d19d184c029c6e92e6a01544.svg" class="try-icon"></button></a></div>
    <div style="text-align:center;"><a href="https://intl.cloud.tencent.com/document/product/647/46660" style="color:#06A4FF;">「導入ガイド」</a>をクリックして、速やかに導入する方法を学ぶことができます。または、<a href="https://github.com/tencentyun/TUICalling" style="color:#06A4FF;">「ソースコードをダウンロード」</a>をクリックして、Githubから最新のソースコードをダウンロードします</div>
    </div>
</div>
:::
::: Web
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/00ebeb4ac808df2b9366351ac7f46648.png"/>
</div>
<div class="tab-bottom">
    <div>
    <div class="platform-icon">
        <span class="support-platform">Demoの対応プラットフォーム</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/7adfb7daedcc48ead500f1ddf6bdb237.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
        <span class="support-platform"><img src="" class="platform-img"></span>
    </div>
    <div class="tab-experience-button"><a href="#demo-card"><button class="tab-experience">今すぐトライアル<img src="https://qcloudimg.tencent-cloud.cn/raw/8b41f1a6d19d184c029c6e92e6a01544.svg" class="try-icon"></button></a></div>
    <div style="text-align:center;"><a href="https://intl.cloud.tencent.com/document/product/647/46660" style="color:#06A4FF;">「導入ガイド」</a>をクリックして、速やかに導入する方法を学ぶことができます。または、<a href="https://github.com/tencentyun/TUICalling" style="color:#06A4FF;">「ソースコードをダウンロード」</a>をクリックして、Githubから最新のソースコードをダウンロードします</div>
    </div>
</div>
:::
</dx-tabs>

</dx-tabs>  

## ビデオ・インタラクティブストリーミングシーン
<dx-tabs>
::: iOS&Android
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/86a3d489c0ea7c9897cf63a67a97ad0f.png"/>
</div>
<div class="tab-bottom">
    <div>
    <div class="platform-icon">
        <span class="support-platform">Demoの対応プラットフォーム</span>
         <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/7adfb7daedcc48ead500f1ddf6bdb237.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
        <span class="support-platform"><img src="" class="platform-img"></span>
    </div>
    <div class="tab-experience-button"><a href="#demo-card"><button class="tab-experience">今すぐトライアル<img src="https://qcloudimg.tencent-cloud.cn/raw/8b41f1a6d19d184c029c6e92e6a01544.svg" class="try-icon"></button></a></div>
    <div style="text-align:center;"><a href="https://intl.cloud.tencent.com/zh/document/product/647/46666" style="color:#06A4FF;">「導入ガイド」</a>をクリックして、速やかに導入する方法を学ぶことができます。または、<a href="https://github.com/tencentyun/TUILiveRoom" style="color:#06A4FF;">「ソースコードをダウンロード」</a>をクリックして、Githubから最新のソースコードをダウンロードします</div>
    </div>
</div>
:::
::: Web
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/fd41c8627d4e6911e9fae1a0309a82c2.png"/>
</div>
<div class="tab-bottom">
    <div>
    <div class="platform-icon">
        <span class="support-platform">Demoの対応プラットフォーム</span>
         <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/7adfb7daedcc48ead500f1ddf6bdb237.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
        <span class="support-platform"><img src="" class="platform-img"></span>
    </div>
    <div class="tab-experience-button"><a href="#demo-card"><button class="tab-experience">今すぐトライアル<img src="https://qcloudimg.tencent-cloud.cn/raw/8b41f1a6d19d184c029c6e92e6a01544.svg" class="try-icon"></button></a></div>
    <div style="text-align:center;"><a href="https://intl.cloud.tencent.com/zh/document/product/647/46666" style="color:#06A4FF;">「導入ガイド」</a>をクリックして、速やかに導入する方法を学ぶことができます。または、<a href="https://github.com/tencentyun/TUILiveRoom" style="color:#06A4FF;">「ソースコードをダウンロード」</a>をクリックして、Githubから最新のソースコードをダウンロードします</div>
    </div>
</div>
:::
</dx-tabs>

</dx-tabs>

## ボイス・インタラクティブストリーミングシーン
<dx-tabs>
::: iOS&Android
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/b1dabc803a241dd26b89e4b5ef60cf27.png"/>
</div>
<div class="tab-bottom">
    <div>
    <div class="platform-icon">
        <span class="support-platform">Demoの対応プラットフォーム</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
    </div>
    <div class="tab-experience-button"><a href="#demo-card"><button class="tab-experience">今すぐトライアル<img src="https://qcloudimg.tencent-cloud.cn/raw/8b41f1a6d19d184c029c6e92e6a01544.svg" class="try-icon"></button></a></div>
    <div style="text-align:center;"><a href="https://intl.cloud.tencent.com/zh/document/product/647/46664" style="color:#06A4FF;">「導入ガイド」</a>をクリックして、速やかに導入する方法を学ぶことができます。または、<a href="https://github.com/tencentyun/TUIVoiceRoom" style="color:#06A4FF;">「ソースコードをダウンロード」</a>をクリックして、Githubから最新のソースコードをダウンロードします</div>
    </div>
</div>
:::
</dx-tabs>

</dx-tabs>
## ビデオミーティングシーン
<dx-tabs>
::: iOS&Android
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/86285a62460edd04313d97e06bd369d5.png"/>
</div>
<div class="tab-bottom">
    <div>
    <div class="platform-icon">
        <span class="support-platform">Demoの対応プラットフォーム</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/cf4c9ee1645ee381b7fec591223b8f75.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/864f8562e1b7780e6f23e1f2987f9ff9.svg" class="platform-img">Flutter</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/71cd4ae02a39a0a8345dee11737e717a.svg" class="platform-img">Windows</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/5300d0170d592174fc94411d162a09a1.svg" class="platform-img">Mac OS</span>
    </div>
    <div class="tab-experience-button"><a href="#demo-card"><button class="tab-experience">今すぐトライアル<img src="https://qcloudimg.tencent-cloud.cn/raw/8b41f1a6d19d184c029c6e92e6a01544.svg" class="try-icon"></button></a></div>
    <div style="text-align:center;"><a href="https://intl.cloud.tencent.com/zh/document/product/647/46662" style="color:#06A4FF;">「導入ガイド」</a>をクリックして、速やかに導入する方法を学ぶことができます。または、<a href="https://github.com/tencentyun/TUIRoom" style="color:#06A4FF;">「ソースコードをダウンロード」</a>をクリックして、Githubから最新のソースコードをダウンロードします</div>
    </div>
</div>
:::
::: Web
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/a34feae74aaa845cab05626eae52ac9f.png"/>
</div>
<div class="tab-bottom">
    <div>
    <div class="platform-icon">
        <span class="support-platform">Demoの対応プラットフォーム</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/cf4c9ee1645ee381b7fec591223b8f75.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/864f8562e1b7780e6f23e1f2987f9ff9.svg" class="platform-img">Flutter</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/71cd4ae02a39a0a8345dee11737e717a.svg" class="platform-img">Windows</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/5300d0170d592174fc94411d162a09a1.svg" class="platform-img">Mac OS</span>
    </div>
    <div class="tab-experience-button"><a href="#demo-card"><button class="tab-experience">今すぐトライアル<img src="https://qcloudimg.tencent-cloud.cn/raw/8b41f1a6d19d184c029c6e92e6a01544.svg" class="try-icon"></button></a></div>
    <div style="text-align:center;"><a href="https://intl.cloud.tencent.com/zh/document/product/647/46662" style="color:#06A4FF;">「導入ガイド」</a>をクリックして、速やかに導入する方法を学ぶことができます。または、<a href="https://github.com/tencentyun/TUIRoom" style="color:#06A4FF;">「ソースコードをダウンロード」</a>をクリックして、Githubから最新のソースコードをダウンロードします</div>
    </div>
</div>
:::
::: Windows & Mac
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/bd486997590c2c60326b04d997a9bd0c.png"/>
</div>
<div class="tab-bottom">
    <div>
    <div class="platform-icon">
        <span class="support-platform">Demoの対応プラットフォーム</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/cf4c9ee1645ee381b7fec591223b8f75.svg" class="platform-img">Web</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/864f8562e1b7780e6f23e1f2987f9ff9.svg" class="platform-img">Flutter</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/71cd4ae02a39a0a8345dee11737e717a.svg" class="platform-img">Windows</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/5300d0170d592174fc94411d162a09a1.svg" class="platform-img">Mac OS</span>
    </div>
    <div class="tab-experience-button"><a href="#demo-card"><button class="tab-experience">今すぐトライアル<img src="https://qcloudimg.tencent-cloud.cn/raw/8b41f1a6d19d184c029c6e92e6a01544.svg" class="try-icon"></button></a></div>
    <div style="text-align:center;"><a href="https://intl.cloud.tencent.com/document/product/647/46662" style="color:#06A4FF;">「導入ガイド」</a>をクリックして、速やかに導入する方法を学ぶことができます。または、<a href="https://github.com/tencentyun/TUIRoom" style="color:#06A4FF;">「ソースコードをダウンロード」</a>をクリックして、Githubから最新のソースコードをダウンロードします</div>
    </div>
</div>
:::
</dx-tabs>

</dx-tabs>

## オンラインカラオケシーン
<dx-tabs>
::: iOS&Android
<div class="tab-img">
    <img src="https://qcloudimg.tencent-cloud.cn/raw/e71e6aaf11de33e132819493be699c19.png"/>
</div>
<div class="tab-bottom">
    <div>
    <div class="platform-icon">
        <span class="support-platform">Demoの対応OS</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/901d05fdb42e3ac74f4a1521c119b320.svg" class="platform-img">Android</span>
        <span class="support-platform"><img src="https://qcloudimg.tencent-cloud.cn/raw/8aef65529388017d7f9a46a24085d15a.svg" class="platform-img">iOS</span>
    </div>
    <div class="tab-experience-button"><a href="#demo-card"><button class="tab-experience">今すぐ体験<img src="https://qcloudimg.tencent-cloud.cn/raw/8b41f1a6d19d184c029c6e92e6a01544.svg" class="try-icon"></button></a></div>
    <div style="text-align:center;"><a href="https://intl.cloud.tencent.com/document/product/647/46668" style="color:#06A4FF;">「導入ガイド」</a>をクリックして、速やかに導入する方法を学ぶことができます。または、<a href="https://github.com/tencentyun/TUIKaraoke" style="color:#06A4FF;">「ソースコードをダウンロード」</a>をクリックして、Githubから最新のソースコードをダウンロードします</div>
    </div>
</div>

:::
</dx-tabs>
</dx-tabs>

<script src="https://cdn-go.cn/aegis/aegis-sdk/latest/aegis.min.js"></script>
<script>
let aegis;
if(Aegis) {
    aegis = new Aegis({
        id: 'iHWefAYqlXjjlfAkpx',
        uin: document.cookie.replace(/(?:(?:^|.*;\s*)uin\s*\=\s*([^;]*).*$)|^.*$/, "$1")|| '',
        reportApiSpeed: false,
        reportAssetSpeed: false
    });
}
function reportEvent(options){ aegis && aegis.reportEvent(options); }
</script>

## 問い合わせとフィードバック
アクセスと利用中に何か不明点などがありましたら、Telegram Groupに参加し、エンジニアに連絡してください。[リンクをクリック](https://t.me/+EPk6TMZEZMM5OGY1)して、または、QRコードをスキャンしてください。
![](https://qcloudimg.tencent-cloud.cn/raw/acf42c4f1a472f9f77da9412a045995a.jpg)
