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


## Getting to know MLVB SDK 
The MLVB SDK is a quick integration tool that provides devices with stream push and playback capabilities and is often used in large-scale high-concurrency live streaming scenarios, including live shows, ecommerce live streaming, sports events, new product launches, roadshows, and online auctions. It offers the RTMP-based stream push method, a demo for you to try out features, and a non-UI integration solution and supports multi-terminal access, so you can integrate it more quickly and efficiently.


## Tryout
### Trying the demo
`MLVB API-Example Demo` is provided to help you better understand MLVB SDK APIs to quickly implement the basic features of some live streaming scenarios. You can quickly run this demo as instructed in the following documents:

| Platform | Source Code Address | How to Run the Demo |
|:--|--|--|
| Android | [MLVB API-Example](https://github.com/LiteAVSDK/Live_Android/tree/main/MLVB-API-Example) | [Android](https://www.tencentcloud.com/document/product/1071/50600) |
| iOS | [MLVB-API-Example-OC](https://github.com/LiteAVSDK/Live_iOS/tree/main/MLVB-API-Example-OC) | [iOS](https://www.tencentcloud.com/document/product/1071/50601) |

![](https://qcloudimg.tencent-cloud.cn/raw/9e2a0d37adc782d7c36db1d05cfdbfea.png) 


## Integration
The MLVB SDK provides a non-UI component integration solution for you to integrate the SDK features into your application more quickly:

You can also integrate the MLVB SDK directly into your project and use the SDK APIs to implement the features you need. This solution offers greater flexibility, but you have to design the UI and interactions by yourself.

We offer API examples for different platforms to help you quickly learn how to use the APIs of the SDK. You can find the API examples for basic TRTC features in the `Basic` folder of the SDK source code package and advanced features (such as resolution setting, background music, and network speed testing) in the `Advanced` folder.


<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
    <a href="https://www.tencentcloud.com/document/product/1071/38155" target="view_window">
        <div class="card-container">
            <div class="card">
                <img class="icon" src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                <h3>Integration Guide for iOS</h3>
                <p>Describes how to integrate the MLVB SDK into your iOS application.</p>
            </div>
        </div>
    </a>
    <a href="https://www.tencentcloud.com/document/product/1071/38156" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                <h3>Integration Guide for Android</h3>
                <p>Describes how to integrate the MLVB SDK to your Android application.</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/TRTC_Electron/tree/main/TRTC-API-Example" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/3b6929f89ce1113bc2005873f2338de9.png" data-nonescope="true">
                <h3>SDK Integration Guide for Flutter</h3>
                <p>Describes how to integrate the MLVB SDK into your Flutter application.</p>
            </div>
        </div>
    </a>
</div>
