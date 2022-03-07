본문에서 안내하는 로컬 파일 시스템에서 VOD로 비디오를 빠르게 업로드하고 VOD 기능으로 처리하는 방법을 통해 **Web 페이지에서 가속화되고 워터마크가 표시된 출력 비디오를 직접 볼 수 있습니다**. 본문은 로컬 비디오 파일 ‘Tencent Cloud.mp4’를 예시로 사용합니다.


## 1단계: VOD 활성화
1. [Tencent Cloud 계정](https://intl.cloud.tencent.com/document/product/378/17985) 등록 및 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)을 완료합니다.
2. VOD 서비스를 구매합니다. 자세한 내용은 [과금 개요](https://intl.cloud.tencent.com/document/product/266/2838)를 참고하십시오.
3. [제품]>[비디오 서비스]>[[VOD]](https://console.cloud.tencent.com/vod)를 선택하여 VOD 콘솔로 이동합니다.

>?VOD 서비스가 이미 활성화된 경우 이 단계를 건너뜁니다.



## 2단계: 비디오 업로드
1. 왼쪽 사이드바에서 [[미디어 자산 관리]](https://console.cloud.tencent.com/vod/media)를 클릭합니다.
2. [비디오 업로드]를 클릭하고 [업로드 방법]은 [로컬 업로드]를 선택합니다.
![](https://main.qcloudimg.com/raw/1d54bda88e541f56d8c2fdec162761f0.png)
3. [비디오 선택]을 클릭하고 로컬 비디오 파일 ‘Tencent Cloud.mp4’를 선택합니다.
4. [비디오 처리]에서 [업로드 후 처리 안 함]을 선택하고 왼쪽 하단 모서리에서 [업로드]를 클릭합니다.

## 3단계: 워터마크 템플릿 생성
1. 왼쪽 사이드바에서 [비디오 처리 설정]>[[템플릿 설정]](https://console.cloud.tencent.com/vod/video-process/template)을 선택합니다.
2. [워터마크 템플릿] 탭을 선택합니다.
3. [워터마크 템플릿 생성]을 클릭하고 다음과 같이 설정한 후 [생성]을 클릭합니다.<br>
<img src="https://main.qcloudimg.com/raw/423f29236a2e12bb8546682db5eb97fc.png" width="450">

## 4단계: 비디오 처리
1. [미디어 자산 관리](https://console.cloud.tencent.com/vod/media) 탭에서 [업로드됨]을 선택합니다.
2. ‘Tencent Cloud.mp4’ 앞의 체크박스를 클릭하고 [비디오 처리]를 클릭합니다.
![](https://main.qcloudimg.com/raw/246099e6f6c37bca0f3b4901b4125412.png)
3. ‘비디오 처리’ 팝업 창에서 [처리 유형] 항목 중 [트랜스코딩]을 선택합니다.
4. [트랜스코딩 템플릿]을 클릭한 다음 하나 이상의 [트랜스코딩 템플릿]을 선택합니다.
5. [워터마크 템플릿]의 드롭다운 목록을 클릭한 다음 [워터마크 선택]에서 [p001]을 선택합니다.
6. [썸네일]을 클릭하고 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/31ecab7ef88cc80f103a16a7dee3deb8.png)

## 5단계: 재생 URL 가져오기
1. ‘Tencent Cloud.mp4’ 작업 열에서 [관리]를 클릭합니다.
2. [표준 트랜스코딩 목록] 섹션의 [MP4-SD-SD]의 작업 열에서 [URL 복사]를 클릭합니다.
<img src="https://main.qcloudimg.com/raw/18a5e92a1200dfcd67dc5d5d0567159c.png" width="1100">
3. 복사한 URL 주소를 Web 브라우저에 입력하고 Enter 키를 누르면 동영상이 재생됩니다.

## 관련 작업
- [모범 사례 - Web을 통해 비디오를 업로드하는 방법](https://intl.cloud.tencent.com/document/product/266/39106)
- [모범 사례 - 비디오 트랜스코딩 방법](https://intl.cloud.tencent.com/document/product/266/37546)
- [모범 사례 - Key 링크 도용 방지를 사용하는 방법](https://intl.cloud.tencent.com/document/product/266/37544)
- [모범 사례 - 이벤트 알림 수신 방법](https://intl.cloud.tencent.com/document/product/266/37542)



## FAQ

- [VOD 과금 방식을 변경하는 방법은 무엇입니까?](https://intl.cloud.tencent.com/document/product/266/18941)
- [VOD 업로드가 지원되는 미디어 파일 형식은 무엇입니까?](https://intl.cloud.tencent.com/document/product/266/2846)
- [VOD 파일 업로드 방식은 무엇이 있습니까? 체크포인트 재시작이 지원됩니까?](https://intl.cloud.tencent.com/document/product/266/2846)

