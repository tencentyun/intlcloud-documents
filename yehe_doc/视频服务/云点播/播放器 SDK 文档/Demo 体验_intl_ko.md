Tencent Cloud RT-Cube Player SDK Demo는 완전한 제품 수준의 인터랙티브 UI 및 비즈니스 소스 코드를 제공합니다. 개발자는 필요에 따라 사용할 수 있습니다.

### Demo 체험
<style>
.markdown-text-box table th,.markdown-text-box table td{
    text-align: center;
}
/*카드*/
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
/*카드 위쪽 상단 icon의 크기*/
.preview-demo-section .preview-demo-item .demo-item-header {
    margin-top: 30px;
}
/*web과 같은 카드 텍스트 설명 글꼴 크기: 기능 데모 · 예시 코드*/
.preview-demo-section .preview-demo-item .demo-item-desc {
    font-size: 12px;
}
/*web 하단 링크*/
.preview-demo-section .preview-demo-item .demo-item-link-web {
    font-size: 14px;
	 margin-top: 53px;
}
/*iOS/Android 하단 링크*/
.preview-demo-section .preview-demo-item .demo-item-link {
    font-size: 14px;
	 margin-top: 5px;
}
/*카드 제목*/
.preview-demo-section .preview-demo-item .demo-item-platform {
    font-size: 20px;
    font-weight: bold;
}
/*카드 상단의 icon과 제목의 거리
.preview-demo-section .preview-demo-item .demo-logo-wrapper {
    line-height: 1;
}
/*상단 icon 크기*/
.preview-demo-section .preview-demo-item .demo-item-header img {
    box-shadow: none;
    width: 40px;
    height: 40px;
}
/*하단 QR코드에서 상단까지의 거리*/
.preview-demo-section .preview-demo-item.style-qrcode .demo-item-download {
    margin-top: 5px;
}
/* web 버튼에서 상단까지의 거리*/
.preview-demo-section .preview-demo-item.style-web .demo-item-download {
    margin-top: 40px;
}
/* 하단 QR 코드 크기 */
.preview-demo-section .preview-demo-item .demo-item-download img {
    box-shadow: none;
    width: 110px;
    height: 110px;
}
/*web 내부 버튼*/
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
/*내부 버튼을 가리키면 손 모양 아이콘이 표시됨*/
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
           기능 데모 · 예시 코드
        </div>
        <div class="demo-item-download">
            <div class="demo-item-download-btn" onclick="window.open('https://tcplayer.vcube.tencent.com/');reportEvent({name: 'demo-click-web', ext1: 'api-sample'});">체험하기</div>
        </div>
				<div class="demo-item-link-web">
				<a href="https://intl.cloud.tencent.com/document/product/266/33977">통합 가이드</a>
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
           TV 시리즈 · UGSV · Feed 스트림
        </div>
        <div class="demo-item-download">
            <img src="https://qcloudimg.tencent-cloud.cn/raw/728d7f5fb63e5790ea3555e5940ef446.png">
        </div>
								<div class="demo-item-link">
				<a href="https://github.com/LiteAVSDK/Player_iOS">Demo 소스 코드</a>
				 <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/266/42005">통합 가이드</a>
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
           TV 시리즈 · UGSV · Feed 스트림
        </div>
        <div class="demo-item-download">
            <img src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png">
        </div>
					<div class="demo-item-link">
				<a href="https://github.com/LiteAVSDK/Player_Android">Demo 소스 코드</a>
				 <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/266/41755">통합 가이드</a>
        </div>
				 </div>		
    </div>
    </div>
</div> 

## Demo
### Web(TCPlayer)
Web 플레이어는 PC와 모바일 브라우저의 비디오 재생을 지원합니다. Web은 비디오 재생 기능의 효과와 코드를 대조하여 볼 수 있는 Demo 체험 페이지를 제공합니다. 예시 코드를 수정하면 재생 영역에서 수정된 기능 효과를 즉시 볼 수 있습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/6aef8503bffdc07df4d01117d66b6e2a.jpg)

### 모바일
Tencent Cloud RT-Cube App은 Tencent Cloud 오디오/비디오가 개발한 다양한 제품과 기능을 통합한 최고의 경험 솔루션입니다. 코드를 스캔하여 Tencent Cloud RT-Cube를 다운로드하고 **Tencent Cloud RT-Cube** > **Player**에서 다양한 시나리오 기반 Demo를 제공합니다. 필요한 기능을 선택하여 체험해 볼 수 있습니다.
* **Superplayer**에서는 일반적인 긴 동영상 재생 시나리오 스타일과 동영상 미리보기, 동영상 목록, 사용자 지정 커버와 같은 일반적인 동영상 기능을 경험할 수 있습니다.
* **쇼트 비디오 재생**에서는 ‘Tencent WeSee’와 유사한 몰입형 짧은 동영상 재생 시나리오를 경험할 수 있습니다.
* **Feed 스트리밍**에서는 ‘Tencent 뉴스’와 유사한 Feed 스트리밍 시나리오를 경험할 수 있습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/c3123138f894795a237e3fc65a74ad95.png)
