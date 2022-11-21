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

## 컴포넌트 개요

TUICallKit은 음성/영상 통화를 위한 UI 컴포넌트입니다. 이를 통합하고 몇 줄의 간단한 코드를 작성하면 App이 오디오/비디오 통화 및 오프라인 푸시를 지원할 수 있으므로 애플리케이션이 오프라인일 때도 사용자가 전화를 받을 수 있습니다. Android, iOS 및 Web 플랫폼을 지원하며 다음과 같은 기본 기능을 제공합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/af697557d2746585a0d9f4b894dc42d5.png)

>! 2022년 8월 TUICalling은 개발자들의 피드백과 시장 조사를 바탕으로 TUICallKit으로 정식 업그레이드 되었습니다. 새로운 컴포넌트 버전에는 그룹 통화 및 오프라인 푸시와 같은 기능이 업그레이드 되었으며, 더 낮은 비용으로 음성/영상 통화 SDK 플랜을 제공하고, 60일 무료 평가판도 제공합니다.

#### 강점
- 손쉬운 통합: TUICallKit은 개발 시간의 90%를 절약하고 음성/영상 통화 응용 프로그램을 빠르게 출시할 수 있도록 UI와 함께 오픈 소스 컴포넌트를 제공합니다.
- 플랫폼 상호 연결: 다양한 플랫폼을 위한 TUICallKit 컴포넌트는 서로 전화를 걸고, 받고, 끊고, 연결할 수 있습니다.
- 그룹 통화: TUICallKit은 일대일 영상 통화 외에도 여러 그룹 구성원과의 그룹 영상 통화를 지원합니다.
- 오프라인 푸시: TUICallKit은 Android&iOS에서 오프라인 푸시를 지원하므로 수신자는 App이 오프라인일 때도 새로운 수신 전화 알림을 받을 수 있습니다.

#### 적용 시나리오

TUICallKit은 게임 내 커뮤니케이션, 온라인 고객 서비스, 온라인 의료 상담, 보험 상담 등 다양한 시나리오에서 2명 이상의 음성/영상 통화에 이상적입니다.

## TUICallKit  다운로드

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
	<div class="card-container">
			<div class="card">
					 <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
					<p class="titlename">Android TUICallKit</p>
					<p style="color:#586376;">’WeChat’과 유사한 UI로 1V1 통화, 그룹 통화, 플로팅 창, 오프라인 푸시 등 다양한 강력한 기능을 지원합니다.</p>
					<a style="margin-left: 10px;" href="https://github.com/tencentyun/TUICalling"><b>Github </b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/50991"><b>빠른 통합</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51004"><b>API 문서</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51022"><b>FAQ</b></a>
			</div>
	</div>
	<div class="card-container">
			<div class="card">
					 <img src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
					<p class="titlename">iOS TUICallKit</p>
					<p style="color:#586376;">’WeChat’과 유사한 UI로 1V1 통화, 그룹 통화, 플로팅 창, 오프라인 푸시 등 다양한 강력한 기능을 지원합니다.</p>
					<a style="margin-left: 10px;" href="https://github.com/tencentyun/TUICalling"><b>Github </b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/50992"><b>빠른 통합</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51010"><b>API 문서</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51023"><b>FAQ</b></a>
			</div>
	</div>
	<div class="card-container">
			<div class="card">
					 <img src="https://main.qcloudimg.com/raw/7e2651085e3e3c6e32190e401a6dfd32.svg" data-nonescope="true">
					<p class="titlename">Web TUICallKit</p>
					<p style="color:#586376;">’WeChat’과 유사한 UI로 1V1 통화, 그룹 통화, 플로팅 창, 오프라인 푸시 등 다양한 강력한 기능을 지원합니다.</p>
					<a style="margin-left: 10px;" href="https://github.com/tencentyun/TUICalling"><b>Github </b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/50993"><b>빠른 통합</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51014"><b>API 문서</b></a>
					<a style="margin-left: 10px;" href="https://www.tencentcloud.com/document/product/647/51024"><b>FAQ</b></a>
			</div>
	</div>
</div>

## 오픈 소스 구축

업그레이드 이전의 TUICalling 오픈 소스 프로젝트는 [**여기**](https://github.com/tencentyun/TUICalling/tree/open)에서 찾을 수 있습니다.