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


## 1단계: 제품 이해 
실시간 오디오 및 비디오(TRTC)는 Tencent Cloud에서 제공하는 저지연 고품질 오디오/비디오 통신 서비스 세트입니다. 안정적인 오디오/비디오 전송 기능을 저렴한 비용으로 제공합니다. 이를 사용하여 화상 통화, 온라인 교육, 대화형 라이브 스트리밍, 온라인 회의 등 저지연 오디오/비디오 통신 애플리케이션을 빠르게 구축할 수 있습니다.
<div class="doc-video-mod"><iframe src="https://cloudcache.intl.tencent-cloud.com/cms/backend-cms/Qv57087_%E3%80%8A%E5%AE%9E%E6%97%B6%E9%9F%B3%E8%A7%86%E9%A2%91%20TRTC%E3%80%8B%E8%8B%B1-%E8%85%BE%E8%AE%AF%E4%BA%91_0117.mp4"></iframe></div>

## 2단계: 제품 체험
TRTC 서비스를 사용해 볼 수 있는 Demo 앱을 제공합니다. 설치 후 다음 기능이 포함되어있습니다.
<div style="position: relative; box-sizing: border-box;  overflow:hidden">
    <a href="https://intl.cloud.tencent.com/document/product/647/35076" target="view_window">
            <div class="image_card">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/bb2facb7474a5c065b14d2996ead8d48.png"/>
            </div>
    </a>
</div>

- **영상 통화**: WeChat과 유사한 통화 기능. 뷰 스위치, 뷰티 필터 및 네트워크 연결 모니터링을 지원합니다.
- **그룹 회의**: 같은 방에 있는 여러 사람 간의 통신을 지원하므로 온라인 회의 및 교육 시나리오에 이상적입니다.
- **쇼룸 스트리밍**: 뷰티 필터, 노래 반주, 좋아요, 화면 댓글 및 공동 앵커링을 지원합니다.
- **듀엣**: 두 앵커가 짧은 대기 시간으로 노래를 부를 수 있습니다.
- **온라인 노래방**: 만 명 이상의 청중을 수용합니다. 오디오 인터랙션, 노래 반주 및 가사 동기화를 지원합니다.


## 3단계: 기능 통합
TRTC 기능을 애플리케이션에 신속하게 통합할 수 있는 두 가지 솔루션을 제공합니다.

### 솔루션1: UI 포함
표준 UI 컴포넌트 집합에 대한 소스 코드를 제공합니다. 필요한 컴포넌트를 프로젝트에 통합하고 필요할 때 로드할 수 있습니다. 일반적으로 이 솔루션을 사용하면 약 1시간 안에 통합을 완료할 수 있습니다.

<div style="position: relative; box-sizing: border-box; padding-bottom: 10px; margin-bottom: 10px; overflow:hidden;">
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/4f6e018388bce36b0f5b7807ed76c82a.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">음성/영상 통화</h3>
                <p style="color:#586376" ;>WeChat과 유사한 화상 통화 애플리케이션을 빠르게 구현하는 데 도움이 되는 컴포넌트 기반 UI 디자인</p>
                <a href="https://github.com/tencentyun/TUICalling">GitHub 소스 코드</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/36065">통합 가이드</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/129edf43d9adf4df6f022dec79ba6db0.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">화상 회의</h3>
                <p style="color:#586376" ;>화상 회의, 온라인 데이트 및 원격 인터뷰 애플리케이션을 빠르게 구현하는 데 도움이 되는 컴포넌트 기반 UI 디자인의 로우 코드 솔루션</p>
                <a href="https://github.com/tencentyun/TUIMeeting">GitHub 소스 코드</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/37284">통합 가이드</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/ab32f135f2847eaf22733e9a9ad1636a.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">인터랙티브 오디오 스트리밍</h3>
                <p style="color:#586376;" ;>오디오 채팅방 애플리케이션을 신속하게 구현하는 데 도움이 되는 컴포넌트 기반 UI 디자인의 로우 코드 솔루션</p>
                <a href="https://github.com/tencentyun/TUIVoiceRoom">GitHub 소스 코드</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/37287">통합 가이드</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/ab32f135f2847eaf22733e9a9ad1636a.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">인터랙티브 비디오 스트리밍</h3>
                <p style="color:#586376" ;>라이브 스트리밍 및 동일/크로스 룸 통신을 빠르게 구현하는 데 도움이 되는 컴포넌트 기반 UI 디자인의 로우 코드 솔루션</p>
                <a href="https://github.com/tencentyun/TUILiveRoom">GitHub 소스 코드</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/36060">통합 가이드</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/7a7b51c1536587f0fea130d375661552.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">온라인 노래방</h3>
                <p style="color:#586376;" ;>온라인 노래방 애플리케이션을 빠르게 구현하는 데 도움이 되는 컴포넌트 기반 UI 디자인의 로우 코드 솔루션</p>
                <a href="https://github.com/tencentyun/TUIKaraoke">GitHub 소스 코드</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/41940">통합 가이드</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/7a7b51c1536587f0fea130d375661552.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">듀엣</h3>
                <p style="color:#586376;" ;>실시간 듀엣 애플리케이션을 빠르게 활성화하는 데 도움이 되는 컴포넌트 기반 UI 디자인의 로우 코드 솔루션</p>
                <a href="https://github.com/tencentyun/TUIChorus">GitHub 소스 코드</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/42689">통합 가이드</a>
            </div>
        </div>
    </div>
</div>

### 솔루션2: UI 없음
또한 TRTC SDK를 프로젝트에 직접 통합하고 SDK API를 사용하여 필요한 기능을 구현할 수도 있습니다. 이 솔루션은 더 큰 유연성을 제공합니다. 하지만 UI와 인터랙션을 직접 디자인해야 하기 때문에 통합에 시간이 더 오래 걸릴 수 있습니다.

SDK의 API를 사용하는 방법을 빠르게 배울 수 있도록 다양한 플랫폼에 대한 API 예시를 제공합니다. SDK 소스 코드 패키지의 Basic 폴더에서 기본 TRTC 기능에 대한 API 예시를 찾을 수 있고 Advanced 폴더에서 고급 기능(예시: 해상도 설정, 배경 음악, 네트워크 속도 테스트)을 찾을 수 있습니다.

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
    <a href="https://github.com/LiteAVSDK/TRTC_iOS/tree/main/TRTC-API-Example-OC" target="view_window">
        <div class="card-container">
            <div class="card">
                <img class="icon" src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                <h3>iOS API 예시</h3>
                <p>RTC iOS API를 사용한 <br>오디오/비디오 App 구축 방법 예시</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/TRTC_Android/tree/main/TRTC-API-Example" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                <h3>Android API 예시</h3>
                <p>RTC Android API를 사용한 <br>오디오/비디오 App 구축 방법 예시</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/tencentyun/TRTCSDK/tree/master/Windows/QTDemo" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/104e3aadbd4515f61c3f2f5378948cfb.svg" data-nonescope="true">
                <h3>Windows API 예시</h3>
                <p>RTC Windows API를 사용한 <br>오디오/비디오 App 구축 방법 예시</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/Live_Mac/tree/main/QTDemo" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/98394fa5d669de7fb7a187565d138cdb.svg" data-nonescope="true">
                <h3>Mac OS API 예시</h3>
                <p>RTC Mac OS API를 사용한 <br>오디오/비디오 App 구축 방법 예시</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/TRTC_Web/tree/main/base-react-next" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/7e2651085e3e3c6e32190e401a6dfd32.svg" data-nonescope="true">
                <h3>Web API 예시</h3>
                <p>RTC Web API를 사용한 <br>오디오/비디오 App 구축 방법 예시</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/LiteAVSDK/TRTC_Electron/tree/main/TRTC-API-Example" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/559e93ed3c05c3916300b04b0b09e7aa.svg" data-nonescope="true">
                <h3>Electron API 예시</h3>
                <p>RTC Electron API를 사용한 <br>오디오/비디오 App 구축 방법 예시</p>
            </div>
        </div>
    </a>
</div>

