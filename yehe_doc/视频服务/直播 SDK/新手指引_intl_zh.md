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


## 步骤一：了解产品 
直播 SDK 是提供终端推流播放能力的快速集成工具。常用于秀场直播、电商直播、赛事直播、新品发布会、路演、在线拍卖等各类高并发大规模直播场景。直播 SDK 提供 RTMP 推流方式。直播 SDK 提供 Demo 体验，支持多终端接入，无 UI 集成方案，方便开发者更快速、高效的接入直播 SDK。


## 步骤二：体验产品
### 体验 Demo
为了帮助开发者可以更好的理解直播 SDK 的 API，从而快速实现一些直播场景的基本功能，我们提供了 MLVB API-Example Demo，您可以参考下面的链接快速跑通此 Demo。

|平台 |源码地址 |跑通 Demo |
|:--|--|--|
|Android |[Github](https://github.com/LiteAVSDK/Live_Android/tree/main/MLVB-API-Example) |[跑通 Demo](https://www.tencentcloud.com/document/product/1071/50600)|
|iOS |[Github](https://github.com/LiteAVSDK/Live_iOS/tree/main/MLVB-API-Example-OC) |[跑通 Demo](https://www.tencentcloud.com/document/product/1071/50601)|

![](https://qcloudimg.tencent-cloud.cn/raw/9e2a0d37adc782d7c36db1d05cfdbfea.png) 


## 步骤三：功能集成
为了能让您更快速地将直播SDK功能集成到您的应用中，直播SDK提供了无 UI 组件集成方案：

您可以在项目中直接导入 直播 SDK，并通过 SDK API 以构建自己期望的业务形态。该集成方案的自由度很高，不过需要您自行构建 UI 界面和交互逻辑。

为了让您快速了解 SDK API 的使用方案，我们为您提供了各个平台 SDK 的 API 示例源码，源码文件夹中的 Basic 目录包含了基础功能的示例代码，Advanced 目录则包含了高级功能（比如设置分辨率、背景音效、网络测速等）的示例代码。


<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
    <a href="https://www.tencentcloud.com/document/product/1071/38155" target="view_window">
        <div class="card-container">
            <div class="card">
                <img class="icon" src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                <h3>iOS 集成指引</h3>
                <p>教您如何将直播 SDK 集成到您的 iOS 应用中</p>
            </div>
        </div>
    </a>
    <a href="https://www.tencentcloud.com/document/product/1071/38156" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                <h3>Android 集成指引</h3>
                <p>教您如何将直播 SDK 集成到您的 Android 应用中</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/TRTC_Electron/tree/main/TRTC-API-Example" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/3b6929f89ce1113bc2005873f2338de9.png" data-nonescope="true">
                <h3>Flutter SDK 集成指引</h3>
                <p>教您如何将直播 SDK 集成到您的 Flutter 应用中</p>
            </div>
        </div>
    </a>
</div>
