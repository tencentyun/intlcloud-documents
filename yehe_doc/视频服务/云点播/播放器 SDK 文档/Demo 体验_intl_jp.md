Tencent Cloud View Cube·Player+ Demoは完全な製品レベルのインタラクティブインターフェースとビジネスソースコードを提供します。開発者は必要に応じて取得することができます。

### Demo体験
<style>
.markdown-text-box table th,.markdown-text-box table td{
    text-align: center;
}
/*カード*/
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
/*上部のiconからカード上方のサイズ*/
.preview-demo-section .preview-demo-item .demo-item-header {
    margin-top: 30px;
}
/*カード文字説明のフォントサイズです。例えばweb：機能デモ·サンプルコード*/
.preview-demo-section .preview-demo-item .demo-item-desc {
    font-size: 12px;
}
/*web下部リンク*/
.preview-demo-section .preview-demo-item .demo-item-link-web {
    font-size: 14px;
	 margin-top: 53px;
}
/*iOS/Android下部リンク*/
.preview-demo-section .preview-demo-item .demo-item-link {
    font-size: 14px;
	 margin-top: 5px;
}
/*カードタイトル*/
.preview-demo-section .preview-demo-item .demo-item-platform {
    font-size: 20px;
    font-weight: bold;
}
/*カード上部のiconとタイトルの距離
.preview-demo-section .preview-demo-item .demo-logo-wrapper {
    line-height: 1;
}
/*上部iconのアイコンサイズ*/
.preview-demo-section .preview-demo-item .demo-item-header img {
    box-shadow: none;
    width: 40px;
    height: 40px;
}
/*下部の2次元コードの上方からの位置*/
.preview-demo-section .preview-demo-item.style-qrcode .demo-item-download {
    margin-top: 5px;
}
/*webボタンの上方からの位置*/
.preview-demo-section .preview-demo-item.style-web .demo-item-download {
    margin-top: 40px;
}
/*下部の2次元コードのサイズ*/
.preview-demo-section .preview-demo-item .demo-item-download img {
    box-shadow: none;
    width: 110px;
    height: 110px;
}
/*web内部ボタン*/
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
/*内部ボタンのマウスオーバー表示カーソル*/
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
           機能デモ · サンプルコード
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://tcplayer.vcube.tencent.com/');reportEvent({name: 'demo-click-web', ext1: 'api-sample'});">今すぐ体験する</div>
        </div>
				<div class="demo-item-link-web">
				<a href="https://intl.cloud.tencent.com/document/product/266/33977">統合ガイド</a>
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
           ドラマ· ショートビデオ· Feedストリーム
        </div>
        <div class="demo-item-download">
            <img src="https://qcloudimg.tencent-cloud.cn/raw/728d7f5fb63e5790ea3555e5940ef446.png">
        </div>
								<div class="demo-item-link">
				<a href="https://github.com/LiteAVSDK/Player_iOS">Demoソースコード</a>
				 <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/266/42005">統合ガイド</a>
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
           ドラマ· ショートビデオ· Feedストリーム
        </div>
        <div class="demo-item-download">
            <img src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png">
        </div>
					<div class="demo-item-link">
				<a href="https://github.com/LiteAVSDK/Player_Android">Demoソースコード</a>
				 <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/266/41755">統合ガイド</a>
        </div>
				 </div>		
    </div>
    </div>
</div> 

## Demoデモンストレーション
### Web端末（TCPlayer）
WebプレーヤーはPC端末およびモバイル端末のブラウザのビデオ再生をサポートしています。Web端末はビデオ再生機能の効果およびそれに付随するコードを確認し、比較することができるDemo体験ページを提供しています。サンプルコードを修正することによって、すぐに再生エリア内で修正した機能の効果を確認することができます。

![](https://qcloudimg.tencent-cloud.cn/raw/6aef8503bffdc07df4d01117d66b6e2a.jpg)

### モバイル端末
Tencent Cloud View Cube AppはTencentオーディオビデオが開発した複数の製品および機能を一つに統合した最適な体験ソリューションです。コードをスキャンしてTencent Cloud View Cubeをダウンロードします。**Tencent Cloud View Cube** > **プレーヤー** では多くのシナリオ化されたDemoを提供し、必要に応じて対応する機能を選択し、体験することができます。
* **Super Player**では、一般的な長編ビデオの再生シーンのスタイル、およびビデオのプレビュー、ビデオリスト、カスタムカバーなど一般的なビデオ機能を体験することができます。
* **UGSV再生**では、「TencentWesee」に類似した没入型UGSV再生シナリオを体験することができます。
* **Feedストリーム再生**では、「Tencentニュース」に類似したFeedストリームの再生シナリオを体験することができます。

![](https://qcloudimg.tencent-cloud.cn/raw/c3123138f894795a237e3fc65a74ad95.png)
