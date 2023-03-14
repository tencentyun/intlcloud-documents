본문에서는 애플리케이션을 생성하고 서비스를 활성화하는 방법을 설명합니다.

## 애플리케이션 생성

[](id:test1)

1. [GME 콘솔](https://console.intl.cloud.tencent.com/gamegme)에 로그인하고 왼쪽 사이드바의 **서비스 관리**를 클릭하여 서비스 관리 페이지로 이동합니다.
2. 이 페이지에서 **애플리케이션 생성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f687244df3c633d9a873c58aec4bf864.png)
3. 애플리케이션 정보를 작성합니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/7fac1c705952f11b994e4769b964d803.png)
   - 애플리케이션 이름: 애플리케이션 목록에 표시될 애플리케이션 이름을 입력합니다.
   - 프로젝트: 기본값으로 ‘기본 프로젝트’가 선택됩니다. 프로젝트를 생성하여 선택할 수도 있습니다. 자세한 내용은 [Project Management - Creating Projects](https://www.tencentcloud.com/zh/document/product/378/34726#.E6.96.B0.E5.BB.BA.E9.A1.B9.E7.9B.AE)를 참고하십시오.
   - 태그: ‘+추가’를 클릭하여 태그를 추가합니다. 자세한 내용은 [태그 관리](#test)를 참고하십시오.
4. 필요에 따라 원하는 서비스를 활성화 또는 비활성화합니다.
   - **음성 채팅**을 활성화 또는 비활성화합니다.
    음성 채팅은 음성 사용 시간에 따라 청구됩니다. 필요에 따라 활성화할 수 있습니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/d8986ba5724ee54e2824d917e74a64d6.png)
   - **음성 메시지 서비스**를 활성화 또는 비활성화합니다.
   음성 메시지 서비스는 DAU에 따라 과금됩니다. 필요에 따라 활성화할 수 있습니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/54770276d70bdffaee0c5d9f19d5df83.png)
   - **음성-텍스트 변환 서비스**를 활성화 또는 비활성화합니다.
   음성-텍스트 변환 서비스는 시간에 따라 과금됩니다. 필요에 따라 활성화할 수 있습니다.
	![](https://qcloudimg.tencent-cloud.cn/raw/851315bafd172e1c830ead5fbe78a8a7.png)
5. ‘GME [Service Level Agreement](https://www.tencentcloud.com/zh/document/product/607/30455) 및 [개인 정보 보호 정책](https://www.tencentcloud.com/zh/document/product/607/37524)을 읽었으며 이에 동의합니다’.
6. **확인**을 클릭합니다.



## 애플리케이션 설정

생성된 애플리케이션은 서비스 관리 페이지의 ‘애플리케이션 목록’에 표시됩니다. **설정**을 클릭하여 애플리케이션 세부 정보 페이지로 이동합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5030bd1d74a6ee68fb414ca1644037fd.png)

### 애플리케이션 정보 수정

1. **수정**을 클릭하여 관련 정보를 수정합니다.
2. 수정을 완료한 후 **저장**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/4027bcb5db4cdf5c17b07bf305832e69.png)

### 서비스 상태 수정

1. **수정**을 클릭하여 원하는 서비스를 활성화/비활성화합니다.
2. 수정을 완료한 후 **저장**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e28d05b92ccda7aa011764800a5f3a50.png)

## 주요 매개변수

‘인증 정보’에서 SDK 음성 서비스에 필요한 AppID 및 권한 키를 얻을 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/667413c114bec5fc5f73cb0f08c3d472.png)

>?
>- 여기에서 권한 키는 SDK 연결 시 매개변수로 사용됩니다. 
>- 키 재설정 후 15분 - 1시간 이내에 적용됩니다. 자주 바꾸는 것은 권장하지 않습니다.
>- **키 재설정** 옵션은 게임 생성 계정, 루트 계정, 글로벌 협업 파트너만 가능합니다.
>- 인증에 대한 자세한 내용은 [Authentication Key](https://www.tencentcloud.com/zh/document/product/607/12218)를 참고하십시오.



[](id:test)

## 태그 관리

[애플리케이션 생성](#test1) 시 ‘+추가’를 클릭하여 애플리케이션에 기존 태그를 추가할 수 있습니다. 태그가 생성되지 않은 경우 아래 단계에 따라 태그를 생성할 수 있습니다.

1. 애플리케이션 생성 시 애플리케이션 정보 섹션의 **[태그 관리](https://console.intl.cloud.tencent.com/tag/taglist)**를 클릭하여 태그 목록 페이지로 이동할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2675330a883aefeeaa2c0ad6f374afb7.png)
2. **태그 생성**을 클릭하고 태그 정보를 입력합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/81a09412f346f0df5f3e5c94dd03f5b0.png)
3. **확인**을 클릭합니다.

## 서비스 비활성화

기존 애플리케이션은 삭제할 수 없습니다. 더 이상 사용하지 않으려면 그 아래의 모든 서비스를 비활성화하십시오. 그 후에는 애플리케이션에 대한 모든 요청이 실패합니다. 서비스를 비활성화하려면 [GME 콘솔](https://console.intl.cloud.tencent.com/gamegme)에 로그인한 후 원하는 애플리케이션의 **설정**을 클릭하여 애플리케이션 세부 정보 페이지로 이동하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/5030bd1d74a6ee68fb414ca1644037fd.png)
원하는 서비스에 대해 **수정** > **비활성화** > **저장**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/887c4e50e5f22b32bc08f9f4d712f80c.png)
