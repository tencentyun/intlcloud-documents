<style>
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

## API 예시
<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
    <a href="https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTC-API-Example-OC" target="view_window">
        <div class="card-container">
            <div class="card">
                <img class="icon" src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                <h3>iOS API 예시</h3>
                <p>RTC iOS API를 사용한 <br>오디오/비디오 App 구축 방법 예시</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTC-API-Example" target="view_window">
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
    <a href="https://github.com/tencentyun/TRTCSDK/tree/master/Mac/QTDemo" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/98394fa5d669de7fb7a187565d138cdb.svg" data-nonescope="true">
                <h3>Mac OS API 예시</h3>
                <p>RTC Mac OS API를 사용한 <br>오디오/비디오 App 구축 방법 예시</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/tencentyun/TRTCSDK/tree/master/Web/base-react-next" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/7e2651085e3e3c6e32190e401a6dfd32.svg" data-nonescope="true">
                <h3>Web API 예시</h3>
                <p>RTC Web API를 사용한 <br>오디오/비디오 App 구축 방법 예시</p>
            </div>
        </div>
    </a>
    <a href="https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTC-API-Example" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/559e93ed3c05c3916300b04b0b09e7aa.svg" data-nonescope="true">
                <h3>Electron API 예시</h3>
                <p>RTC Electron API를 사용한 <br>오디오/비디오 App 구축 방법 예시</p>
            </div>
        </div>
    </a>
    <a href="https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/index.html" target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/7e2651085e3e3c6e32190e401a6dfd32.svg" data-nonescope="true">
                <h3>Web 온라인 API Examples</h3>
                <p>Web API를 통한 빠르고 편리한 오디오/비디오 기능 구현 온라인 체험하기</p>
            </div>
        </div>
    </a>
    <span target="view_window">
        <div class="card-container">
            <div class="card">
                <img src="https://main.qcloudimg.com/raw/559e93ed3c05c3916300b04b0b09e7aa.svg" data-nonescope="true">
                <h3>Electron API 간편 체험</h3>
                <p style="color:#586376;">
                    설치 패키지 다운로드. App 내 코드 편집 지원:
                    <a href="https://web.sdk.qcloud.com/trtc/electron/download/api-example/TRTC-Electron-API-Examples-windows.zip" download>Windows 버전</a> &nbsp;&nbsp;&nbsp;
                    <a href="https://web.sdk.qcloud.com/trtc/electron/download/api-example/TRTC-Electron-API-Examples-mac.zip" download>Mac 버전</a>
                </p>
            </div>
        </div>
    </span>
</div>

## 솔루션 시나리오
### 소셜 엔터테인먼트
<div style="position: relative; box-sizing: border-box; padding-bottom: 10px; margin-bottom: 10px; overflow:hidden;">
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/82cfd639a13f1f65cf18c0415bfb37c4.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">Interactive Live Video Broadcasting(ILVB)</h3>
                <p style="color:#586376;" ;>로우 코드로 쇼, 이커머스, 경기과 같은 비디오 인터랙티브 라이브 방송 시나리오를 빠르게 구현합니다.</p>
                <a href="https://github.com/tencentyun/TUILiveRoom">GitHub 소스 코드</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/36060">문서 바로가기</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/bee791cf7cdccf175b70918f83115c7f.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">음성 살롱</h3>
                <p style="color:#586376" ;>컴포넌트화된 UI를 통해 로우 코드로 음성 살롱 시나리오를 빠르게 구현하도록 지원합니다.</p>
                <a href="https://github.com/tencentyun/TUIChatSalon">GitHub 소스 코드</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/39803">문서 바로가기</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/80a7a3e917e4e65908bf2fb1736f7121.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">음성 채팅방</h3>
                <p style="color:#586376;" ;>컴포넌트화된 UI를 통해 로우 코드로 음성 채팅방 시나리오를 빠르게 구현하도록 지원합니다.</p>
                <a href="https://github.com/tencentyun/TUIVoiceRoom">GitHub 소스 코드</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/37287">문서 바로가기</a>
            </div>
        </div>
    </div>
		<div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/4651627d75d0e712d8032fb5f6149a3d.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">온라인 노래방</h3>
                <p style="color:#586376;" ;>컴포넌트화된 UI를 통해 로우 코드로 온라인 KTV 시나리오를 빠르게 구현하도록 지원합니다.</p>
                <a href="https://github.com/tencentyun/TUIKaraoke">GitHub 소스 코드</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/41940">문서 바로가기</a>
            </div>
        </div>
    </div>
</div>

### 교육
<div style="position: relative; box-sizing: border-box; padding-bottom: 10px; margin-bottom: 10px; overflow:hidden;">
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://main.qcloudimg.com/raw/1b60d290134f2a93e04dcb453c3dd51f.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">인터랙션 클래스</h3>
                <p style="color:#586376" ;>Electron 크로스 플랫폼 컴포넌트는 클래스를 신속하게 구축하도록 지원합니다.</p>
                <a
                    href="https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTCScenesDemo/TRTCEducation">GitHub 소스 코드</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/37278">문서 바로가기</a>
            </div>
        </div>
    </div>
</div>

### 커뮤니케이션
<div style="position: relative; box-sizing: border-box; padding-bottom: 10px; margin-bottom: 10px; overflow:hidden;">
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/c8b92d2457467e3c349cb56e83b37ef4.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">다중 사용자 화상 회의</h3>
                <p style="color:#586376" ;>컴포넌트화된 UI를 통해 로우 코드로 회의 시나리오를 빠르게 구현하도록 지원합니다.</p>
                <a href="https://github.com/tencentyun/TUIMeeting">GitHub 소스 코드</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/37284">문서 바로가기</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/2dffabbe27521eb08c95dc5e72101886.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">음성 통화</h3>
                <p style="color:#586376" ;>컴포넌트화된 UI를 통해 ‘WeChat과 유사한’ 음성 통화 시나리오를 빠르게 구현하도록 지원합니다.</p>
                <a href="https://github.com/tencentyun/TUICalling">GitHub 소스 코드</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/36067">문서 바로가기</a>
            </div>
        </div>
    </div>
    <div class="scene-card-container">
        <div class="scene-card">
            <div style="float: left; margin-top: 20px;">
                <img src="https://qcloudimg.tencent-cloud.cn/raw/96f08d55e04928ddd1d731192a3dc8a4.png" width="160" data-nonescope="true">
            </div>
            <div style="float: left; width: 200px; margin-left: 30px; margin-top: 20px; ">
                <h3 style="color:191919;">영상 통화</h3>
                <p style="color:#586376" ;>컴포넌트화된 UI를 통해 ‘WeChat과 유사한’ 영상 통화 시나리오를 빠르게 구현하도록 지원합니다.</p>
                <a href="https://github.com/tencentyun/TUICalling">GitHub 소스 코드</a>
                <a style="margin-left: 30px;" href="https://intl.cloud.tencent.com/document/product/647/36065">문서 바로가기</a>
            </div>
        </div>
    </div>
</div>
</div>
