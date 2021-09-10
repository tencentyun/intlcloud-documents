본문은 TRTC 부가 서비스 및 기본 서비스의 후불 결제 활성화 방법에 대한 설명입니다.

## 기본 서비스
기본 서비스는 응용 시나리오에 따라 [음성 ILVB](https://intl.cloud.tencent.com/document/product/647/39785), [비디오 ILVB](https://intl.cloud.tencent.com/document/product/647/39786), [음성 통화](https://intl.cloud.tencent.com/document/product/647/39787) 및 [영상 통화](https://intl.cloud.tencent.com/document/product/647/39788)로 나뉘어지며, 필요에 따라 후불 결제를 활성화할 수 있습니다.

[](id:case1)
### 방법1: 콘솔으로 이동하여 후불 결제를 활성화합니다

#### 애플리케이션 최초 생성 시 후불 결제 활성화를 선택합니다

1. [TRTC](https://console.cloud.tencent.com/trtc) 서비스 최초 개통인 경우 **개발 지원** > [**Demo 빠른 실행**](https://console.cloud.tencent.com/trtc/quickstart)을 선택하여 신규 TRTC 애플리케이션을 생성합니다.
2. 애플리케이션 이름(예: ‘TestTRTC’)을 입력합니다.
3. 업무 상 필요에 따라 태그를 편집 또는 추가하고, **생성**을 클릭합니다.
![](https://main.qcloudimg.com/raw/db5d85f5352ebbe6af38db655798750f.png)
4. 증정 패키지 팝업창에서 ‘**서비스 정지하지 않음, 후불 결제 방식 선택, 정가 기준으로 과금’**을 선택할 수 있습니다.

[](id:case2)
#### 애플리케이션 정보 리스트에서 후불 결제를 활성화합니다

1. 애플리케이션 최초 생성 시 후불 결제를 활성화하지 않았으나, 서비스 패키지 사용량 소진 혹은 기간 만료 후 필요에 따라 서비스 유지를 원하는 경우, TRTC 콘솔로 이동하여 **[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)**에서 **애플리케이션 정보**를 선택하여 애플리케이션 리스트를 확인하십시오.
2. 오른쪽 작업 열에서 **애플리케이션 정보**를 클릭합니다.
![](https://main.qcloudimg.com/raw/ece9dfbcf3c6a7555a9e4b6d2221700d.png)
3. 애플리케이션 상세 페이지로 이동하여 **애플리케이션 정보** 탭의 ‘애플리케이션 정보’ 모듈에서 기존 적용된 애플리케이션 기본 정보를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/a95103ce8e184e48987938e91a71ba7f.png)
4. ‘TRTC 서비스 상태’를 확인하고 **후불 결제 활성화**를 클릭합니다.
![](https://main.qcloudimg.com/raw/74d800a5d2c5dad39214c7ea2e432d59.png)

[](id:case3)
### 방법2: 시스템을 통해 후불 결제를 자동 활성화합니다
범용 패기지를 구매한 경우, 패키지 사용량 소진 혹은 기간 만료 후 시스템에서 후불 결제를 **자동으로 활성화**하고, 패키지 초과 사용분은 **후불** 결제 방식이 적용됩니다.

>! TRTC 기본 사용량을 공제할 패키지가 없거나, 사용량이 패키지 잔여량을 초과한 경우, 후불 결제 방식이 적용되어 **정가** 기준 과금됩니다. **후불 결제 방식은 활성화 후 비활성화할 수 없습니다.**


## 부가 서비스
부가 서비스는 네 가지 기본 서비스 기초 위에 추가로 제공되는 부가 기능으로, 기본 서비스와 별도로 사용할 수 없으며, 부가 서비스 비용이 별도로 발생합니다. TRTC는 [클라우드 녹화](https://intl.cloud.tencent.com/document/product/647/38385) 및 [클라우드 혼합 스트림 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/38929) 두 가지 부가 서비스를 제공합니다. TRTC 부가 서비스는 **일 결산 후불** 결제 방식만 지원하므로, 후불 결제 방식을 활성화할 필요가 없습니다.





