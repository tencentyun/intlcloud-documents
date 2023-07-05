## 작업 시나리오
본문은 CVM 콘솔과 클라우드 API를 통해 종료 상태의 인스턴스를 실행하는 방법을 설명합니다.

## 작업 단계
<dx-tabs>
::: 콘솔을 통한 인스턴스 시작

#### 단일 인스턴스 시작
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
2. 인스턴스의 관리 페이지에서 실제로 사용된 뷰 모드에 따라 작업합니다.
   - **리스트 뷰**: 아래 그림과 같이 실행할 인스턴스를 선택하고 오른쪽 작업 열에서 **더보기** > **인스턴스 상태** > **시작**을 선택합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/900a2d8fb4a48ef1e9746922d6447666.png)
   - **탭 뷰**: 아래 그림과 같이 실행할 인스턴스 페이지 우측 상단에서 **시작**을 선택합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/c62f67a3415635ddf535442b4b73343c.png)


#### 다중 인스턴스 시작
아래 이미지와 같이 시작할 모든 인스턴스를 선택하고 리스트 상단의 **시작**을 클릭하여 인스턴스를 일괄 시작합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/dd734cf2e58b3e9d1ee1114bb94fe41a.png)

:::
::: \sAPI\s를 통한 인스턴스 시작
[StartInstances](https://intl.cloud.tencent.com/document/product/213/33236) 인터페이스를 참고하십시오.

:::
</dx-tabs>

## 후속 작업
다음 작업은 인스턴스 시작 상태에서만 실행할 수 있습니다.
- **인스턴스 로그인**: 인스턴스 운영 체제에 따라. [Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5436)과 [Windows 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5435)을 참고하십시오.
- **[CBS 초기화](https://intl.cloud.tencent.com/document/product/362/31596)**: 마운트된 CBS에 포맷, 파티션 및 파일 시스템 생성 등 초기화 작업을 실행합니다.
