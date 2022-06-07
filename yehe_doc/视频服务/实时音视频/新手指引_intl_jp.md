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


## 手順1：製品についての理解 
Tencent Real-Time Communication (TRTC)は、Tencent Cloudが提供する低遅延、高品質のオーディオおよびビデオ通信サービスのセットであり、Tencent Cloudのお客様に安定した、高信頼で低コストのオーディオおよびビデオ転送機能を提供することを目的としています。このサービスを使用して、「ビデオ通話」、「オンライン教育」、「ライブブロードキャストのマイク接続」、「オンライン会議」など、通信遅延が厳しく要求されたオーディオおよびビデオアプリケーションをすばやく構築できます。
<div class="doc-video-mod"><iframe src="https://cloudcache.intl.tencent-cloud.com/cms/backend-cms/Qv57087_%E3%80%8A%E5%AE%9E%E6%97%B6%E9%9F%B3%E8%A7%86%E9%A2%91%20TRTC%E3%80%8B%E8%8B%B1-%E8%85%BE%E8%AE%AF%E4%BA%91_0117.mp4"></iframe></div>

## 手順2：製品の体験
当社の製品を迅速に理解できるように、TRTCサービスを統合した機能デモ(Demo)を提供しています。インストール後、次のようなTRTCのさまざまな機能を体験できます：
<div style="position: relative; box-sizing: border-box;  overflow:hidden">
    <a href="https://intl.cloud.tencent.com/document/product/647/35076" target="view_window">
            <div class="image_card">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/bb2facb7474a5c065b14d2996ead8d48.png"/>
            </div>
    </a>
</div>

- **ビデオ通話**：WeChatの通話機能と類似しており、ウィンドウの切り替え、美顔、ネットワーク信号の提示などの機能をサポートしています。
- **マルチプレイヤー会議**：複数のユーザーが同じ部屋でコミュニケーションと対話を行えるようにサポートしています。オンライン会議やオンライン教育などのシーンで使用できます。
- **ショーのライブブロードキャスト**：キャスターはオンラインで才能を展示します。美顔、伴奏、いいね、弾幕インタラクティブおよびオンラインマイク接続をサポートします。
- **オンラインコーラス**：2名のキャスターがオンラインで一緒に歌を歌い、TRTCが提供する低遅延の通信機能を感じることができます。
- **オンラインカラオケ**：何万人もの人々が同時に聞くことをサポートするとともに、音声対話、音楽伴奏および歌詞同期などの機能をサポートするオンライン音楽のライブブロードキャストスキームです。


## 手順3：機能の統合
TRTC機能をアプリケーションにすばやく統合できるようにするために、2つの異なる統合スキームが用意されています。必要に応じて、そのうちの1つを選択して統合できます。

### スキーム1：UIコンポーネントが統合されたスキーム
標準化されたUIコンポーネントのセットを開発し、ソースコードを提供しました。適切なUIコンポーネントをプロジェクトに直接インポートし、必要に応じてロードできます。この統合スキームは非常に高速で、通常は1時間で完了できます。

<div style="position: relative; box-sizing: border-box; padding-bottom: 10px; margin-bottom: 10px; overflow:hidden;">
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/4f6e018388bce36b0f5b7807ed76c82a.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">オーディオおよびビデオ通話</h3>
                <p style="color:#586376" ;>コンポーネント化されたUIによって、「WeChatのような」ビデオ通話シーンなどをすばやく実現</p>
                <a href="https://github.com/tencentyun/TUICalling">GitHubソースコード</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/36065">ドキュメントにアクセス</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/129edf43d9adf4df6f022dec79ba6db0.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">多人数ビデオミーティング</h3>
                <p style="color:#586376" ;>コンポーネント化されたUIによって、ミーティング、ブラインドデート、面接シーンをローコードですばやく実現</p>
                <a href="https://github.com/tencentyun/TUIMeeting">GitHubソースコード</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/37284">ドキュメントにアクセス</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/ab32f135f2847eaf22733e9a9ad1636a.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">音声によるInteractive Live Video Broadcasting</h3>
                <p style="color:#586376;" ;>コンポーネント化されたUIによって、ボイスチャットルームシーンをローコードですばやく実現</p>
                <a href="https://github.com/tencentyun/TUIVoiceRoom">GitHubソースコード</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/37287">ドキュメントにアクセス</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/ab32f135f2847eaf22733e9a9ad1636a.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">画面によるInteractive Live Video Broadcasting</h3>
                <p style="color:#586376;" ;>コンポーネント化されたUIによって、ライブブロードキャスト、マイク接続、PKシーンをローコードですばやく実現</p>
                <a href="https://github.com/tencentyun/TUILiveRoom">GitHubソースコード</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/36060">ドキュメントにアクセス</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/7a7b51c1536587f0fea130d375661552.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">オンラインカラオケ</h3>
                <p style="color:#586376;" ;>コンポーネント化されたUIによって、オンラインKTVシーンをローコードですばやく実現</p>
                <a href="https://github.com/tencentyun/TUIKaraoke">GitHubソースコード</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/41940">ドキュメントにアクセス</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/7a7b51c1536587f0fea130d375661552.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">リアルタイムコーラス</h3>
                <p style="color:#586376;" ;>コンポーネント化されたUIによって、リアルタイムコーラスシーンをローコードですばやく実現</p>
                <a href="https://github.com/tencentyun/TUIChorus">GitHubソースコード</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/42689">ドキュメントにアクセス</a>
            </div>
        </div>
    </div>
</div>

### スキーム2：UIコンポーネントが統合されていないスキーム
プロジェクトにTRTC SDKを直接インポートし、SDK APIを介して目的の業務形態を構築できます。この統合スキームは自由度が高いですが、UIインターフェースとインタラクションロジックを自分で構築する必要があるため、統合速度はスキーム1よりもわずかに遅くなります。

SDK APIの使用スキームをすばやく理解できるように、各プラットフォームSDKのAPIサンプルのソースコードを提供しました。ソースコードフォルダーのBasicディレクトリには基本機能のサンプルコードが含まれ、Advancedディレクトリには高度機能（解像度、背景音、ネットワーク速度の測定など）のサンプルコードが含まれています。

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
    <a href="https://github.com/LiteAVSDK/TRTC_iOS/tree/main/TRTC-API-Example-OC" target="view_window">
        <div class="card-container">
            <div class="card">
                <img class="icon" src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                <h3>iOS APIサンプル</h3>
                <p>RTC iOS API使用方法のデモンストレーション <br>オーディオビデオアプリケーションをゼロから構築する</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/TRTC_Android/tree/main/TRTC-API-Example" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                <h3>Android APIサンプル</h3>
                <p>RTC Android API使用方法のデモンストレーション <br>オーディオビデオアプリケーションをゼロから構築する</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/tencentyun/TRTCSDK/tree/master/Windows/QTDemo" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/104e3aadbd4515f61c3f2f5378948cfb.svg" data-nonescope="true">
                <h3>Windows APIサンプル</h3>
                <p>RTC Windows API使用方法のデモンストレーション <br>オーディオビデオアプリケーションをゼロから構築する</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/Live_Mac/tree/main/QTDemo" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/98394fa5d669de7fb7a187565d138cdb.svg" data-nonescope="true">
                <h3>Mac OS APIサンプル</h3>
                <p>RTC Mac OS API使用方法のデモンストレーション <br>オーディオビデオアプリケーションをゼロから構築する</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/TRTC_Web/tree/main/base-react-next" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/7e2651085e3e3c6e32190e401a6dfd32.svg" data-nonescope="true">
                <h3>Web APIサンプル</h3>
                <p>RTC Web API使用方法のデモンストレーション <br>オーディオビデオアプリケーションをゼロから構築する</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/TRTC_Electron/tree/main/TRTC-API-Example" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/559e93ed3c05c3916300b04b0b09e7aa.svg" data-nonescope="true">
                <h3>Electron APIサンプル</h3>
                <p>RTC Electron API使用方法のデモンストレーション <br>オーディオビデオアプリケーションをゼロから構築する</p>
            </div>
        </div>
    </a>
</div>

