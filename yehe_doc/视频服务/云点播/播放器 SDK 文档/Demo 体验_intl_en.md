The Tencent Cloud RT-Cube Player SDK demo provides complete product-grade interactive UIs and business source code for you to use on demand.

### Demo
<style>
.markdown-text-box table th,.markdown-text-box table td{
    text-align: center;
}
/*A card*/
.preview-demo-section .preview-demo-item {
    display: inline-block;
    width: 226px;
    height: 300px;
    background: #fff;
    box-shadow: 0 1px 8px 0 rgb(156 175 204 / 25%);
    border-radius: 1px;
    text-align: center;
    padding: 0 15px;
    margin: 10px 13px 10px 7px;
    vertical-align: top;
}
/*The top margin between the top icon and the card*/
.preview-demo-section .preview-demo-item .demo-item-header {
    margin-top: 30px;
}
/*The font size of the card text such as "Web: Feature Demo - Code Sample"*/
.preview-demo-section .preview-demo-item .demo-item-desc {
    font-size: 12px;
}
/*The bottom link for web*/
.preview-demo-section .preview-demo-item .demo-item-link-web {
    font-size: 14px;
	 margin-top: 53px;
}
/*The bottom link for iOS/Android*/
.preview-demo-section .preview-demo-item .demo-item-link {
    font-size: 14px;
	 margin-top: 5px;
}
/*The card title*/
.preview-demo-section .preview-demo-item .demo-item-platform {
    font-size: 20px;
    font-weight: bold;
}
/*The distance between the top icon and title in the card
.preview-demo-section .preview-demo-item .demo-logo-wrapper {
    line-height: 1;
}
/*The size of the top icon*/
.preview-demo-section .preview-demo-item .demo-item-header img {
    box-shadow: none;
    width: 40px;
    height: 40px;
}
/*The top margin of the bottom QR code*/
.preview-demo-section .preview-demo-item.style-qrcode .demo-item-download {
    margin-top: 5px;
}
/*The top margin of the web button*/
.preview-demo-section .preview-demo-item.style-web .demo-item-download {
    margin-top: 40px;
}
/*The size of the bottom QR code*/
.preview-demo-section .preview-demo-item .demo-item-download img {
    box-shadow: none;
    width: 110px;
    height: 110px;
}
/*The internal web button*/
.preview-demo-section .preview-demo-item.style-web .demo-item-download .demo-item-download-btn {
    color: #fff;
		border-radius: 20px;
    background-color: #00a4ff;
    height: 35px;
		width: 170px;
    line-height: 35px;
    margin-bottom: 6px;
		margin: auto;
}
/*Display a hand icon when the user hovers over the internal button.*/
.preview-demo-section .preview-demo-item .demo-item-download .demo-item-download-btn:hover {
    cursor: pointer;
}

</style>

<div class="preview-demo-section" id="demo-card">
 <div class="preview-demo-item style-web">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/ff4dc34a1c72fdb26fc41c1268898025.svg" data-nonescope="true">
            </div>
            <div class="demo-item-platform">Web</div>
        </div>
        <div class="demo-item-desc">
           Feature Demo  Code Sample
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://tcplayer.vcube.tencent.com/intl/index.html');reportEvent({name: 'demo-click-web', ext1: 'api-sample'});">Try Now</div>
        </div>
				<div class="demo-item-link-web">
				<a href="https://intl.cloud.tencent.com/document/product/266/33977">Integration Guide</a>
        </div>
	 </div>
	 <div class="preview-demo-item style-qrcode">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/36154dc8bb7c93826dbdc6fdcec4e194.svg" data-nonescope="true">
            </div>
            <div class="demo-item-platform">iOS</div>
        </div>
        <div class="demo-item-desc">
           TV Series   Short Video   Feed Stream
        </div>
        <div class="demo-item-download">
            <img src="https://qcloudimg.tencent-cloud.cn/raw/728d7f5fb63e5790ea3555e5940ef446.png">
        </div>
								<div class="demo-item-link">
				<a href="https://github.com/LiteAVSDK/Player_iOS">Demo source code</a>
				 <a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/266/49669">Integration Guide</a>
        </div>
    </div>
    <div class="preview-demo-item style-qrcode" style="margin-left:0">
        <div class="demo-item-header">
            <div class="demo-logo-wrapper">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/53be7f245c4d11d3aefcb6dc53918757.svg" data-nonescope="true">
            </div>
            <div class="demo-item-platform">Android</div>
        </div>
        <div class="demo-item-desc">
           TV Series   Short Video   Feed Stream
        </div>
        <div class="demo-item-download">
            <img src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png">
        </div>
					<div class="demo-item-link">
				<a href="https://github.com/LiteAVSDK/Player_Android">Demo source code</a>
				 <a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/266/49670">Integration Guide</a>
        </div>
				 </div>		
    </div>
    </div>
</div> 

## Demos
### Player for web (TCPlayer)
TCPlayer supports video playback in a browser on a PC or mobile device. It provides demo pages for you to compare and view the video playback features and code. You can modify the code samples to view the effect of modified features in the playback area in real time.

![](https://qcloudimg.tencent-cloud.cn/raw/6aef8503bffdc07df4d01117d66b6e2a.jpg)

### Mobile client
Tencent Cloud RT-Cube app is the best trial solution that integrates multiple products and features developed by the Tencent Cloud Audio/Video team. You can scan the QR code to download the app and try out features as needed by using scenario-specific demos in **Tencent Cloud RT-Cube** > **Player**.
* In **Superplayer**, you can experience common styles of long video playback as well as common video features such as video preview, video list, and custom thumbnails.
* In **Short Video Playback**, you can experience an immersive short video playback scenario similar to WeSee.
* In **Feed Stream Playback**, you can experience a feed stream playback scenario similar to Tencent News.

![](https://qcloudimg.tencent-cloud.cn/raw/c3123138f894795a237e3fc65a74ad95.png)
