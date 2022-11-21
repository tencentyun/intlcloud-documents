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

## コンポーネントの説明

TUICallKitはTencent Cloudがリリースするオーディオビデオ通話UIコンポーネントです。このコンポーネントを統合することにより、数行のコードを書くだけでAppにオーディオビデオ通話機能を追加することができ、さらにオフライン通知機能もサポートします。TUICallKitはAndroid、iOS、Webなどの複数の開発プラットフォームでサポートしています。基本機能は下図のとおりです。

![](https://qcloudimg.tencent-cloud.cn/raw/af697557d2746585a0d9f4b894dc42d5.png)

>! 開発者からのフィードバックと市場ニーズのリサーチを基に、2022年8月、TUICallingはTUICallKitへとアップグレードしました。新しいコンポーネントはグループ内の多人数通話やオフライン通知などの機能をサポートします。また、より割引率の高いオーディオビデオ通話SDKパッケージおよび60日間の無料トライアル期間をご用意しています。この機会にぜひご利用ください。

#### 機能のメリット
- 便利なアクセス：UI付きのオープンソースコンポーネントを提供することで、開発時間を90%節約でき、オーディオビデオ通話アプリケーションをスピーディーにリリースできます。
- プラットフォーム相互運用性：各プラットフォームのTUICallKitコンポーネントは通話の発信、応答、終了などを相互にサポートし、相互運用が可能です。
- 多人数通話：1対1のビデオ通話だけでなく、グループ内で多人数ビデオ通話を開始することもできます。
- オフラインプッシュ：Android&iOSのオフラインプッシュをサポートしています。着呼側ユーザーのAppはオフラインのときでも新しい着信通知を受け取ることができます。

#### 適用ケース

2人または複数人のオーディオビデオ通話が行えます。ゲームSNS、オンラインカスタマーサービス、ビデオカスタマーサービス、オンライン問診、保険相談などのシーンに適します。

## TUICallKitのダウンロード

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
	<div class="card-container">
			<div class="card">
					 <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
					<p class="titlename">Android TUICallKit</p>
					<p style="color:#586376;">「WeChat」のようなUIで、1V1通話、グループ通話、フローティングウィンドウ、オフラインプッシュなどの強力な機能をサポートします。</p>
					<a style="margin-left: 10px;" href="https://github.com/tencentyun/TUICalling"><b>Github </b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/50991"><b>クイックアクセス</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51004"><b>API参照</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51022"><b>よくあるご質問</b></a>
			</div>
	</div>
	<div class="card-container">
			<div class="card">
					 <img src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
					<p class="titlename">iOS TUICallKit</p>
					<p style="color:#586376;">「WeChat」のようなUIで、1V1通話、グループ通話、フローティングウィンドウ、オフラインプッシュなどの強力な機能をサポートします。</p>
					<a style="margin-left: 10px;" href="https://github.com/tencentyun/TUICalling"><b>Github </b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/50992"><b>クイックアクセス</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51010"><b>API参照</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51023"><b>よくあるご質問</b></a>
			</div>
	</div>
	<div class="card-container">
			<div class="card">
					 <img src="https://main.qcloudimg.com/raw/7e2651085e3e3c6e32190e401a6dfd32.svg" data-nonescope="true">
					<p class="titlename">Web TUICallKit</p>
					<p style="color:#586376;">「WeChat」のようなUIで、1V1通話、グループ通話、フローティングウィンドウ、オフラインプッシュなどの強力な機能をサポートします。</p>
					<a style="margin-left: 10px;" href="https://github.com/tencentyun/TUICalling"><b>Github </b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/50993"><b>クイックアクセス</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51014"><b>API参照</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51024"><b>よくあるご質問</b></a>
			</div>
	</div>
</div>

## オープンソース構築

アップグレード前のTUICallingオープンソースプロジェクトは[**ここ**](https://github.com/tencentyun/TUICalling/tree/open)で見つけることができます。