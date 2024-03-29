## 작업 시나리오
Cloud Access Management(CAM)의 역할은 한 세트의 권한을 보유한 가상 신분으로, 역할 엔터티에 Tencent Cloud의 서비스, 작업 및 리소스에 대한 액세스 권한을 부여하는 데 사용합니다. 사용자는 CAM 역할을 CVM 인스턴스에 연결한 뒤, 인스턴스 내부에서 Tencent Cloud 보안 증명 서비스 STS의 임시 보안키를 사용해 다른 클라우드 서비스 API(임시 보안키는 주기적 갱신됨)에 액세스할 수 있습니다. 이는 직접 SecretKey를 사용하는 권한 제어보다 계정의 SecretKey 보안을 더욱 강화할 수 있으며, CAM의 성능으로 권한을 더 세밀하게 제어 및 관리할 수 있습니다.

본 문서에서는 인스턴스 역할의 바인딩, 수정 및 삭제 등 관리 방법에 관해 소개합니다.

## 기능 및 장점
인스턴스에 CAM 역할을 바인딩하면 아래의 기능 및 장점을 보유하게 됩니다.
- STS 임시 키를 사용하여 Tencent Cloud의 다른 클라우드 서비스에 액세스할 수 있습니다.
- 각각 다른 정책 권한이 포함된 역할을 각 인스턴스에 부여할 수 있습니다. 여러 클라우드 리소스에 대해 다른 액세스 권한을 가진 인스턴스로 더욱 정밀하게 권한을 제어할 수 있습니다.
- 인스턴스 안에 SecretKey를 직접 저장할 필요 없이, 역할의 권한 수정만으로도 즉시 변경할 수 있어 손쉽게 인스턴스의 액세스 권한을 점검할 수 있습니다.




## 사용 설명
- 인스턴스는 `cvm.qcloud.com` 등을 포함한 역할 엔터티만 바인딩하도록 지원합니다. 자세한 내용은 [역할 기본 개념](https://intl.cloud.tencent.com/document/product/598/19421)을 참고하십시오.
- 인스턴스의 네트워크 유형은 전용 네트워크인 VPC여야 합니다.
- 각 인스턴스에는 한 번에 한 CAM 역할만 부여할 수 있습니다.
- 인스턴스 역할의 바인딩, 수정 및 삭제는 추가 요금이 발생하지 않습니다.


## 작업 단계

### 인스턴스의 역할 바인딩/수정
<dx-tabs>
::: 단일 인스턴스의 역할 바인딩/수정
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm)에 로그인한 뒤, 왼쪽 사이드바의 **인스턴스**를 선택합니다.
2. 인스턴스의 관리 페이지에서 사용된 실제 뷰 모드에 따라 작업합니다.
  - **리스트 뷰**: 역할을 바인딩 또는 수정할 CVM의 행 오른쪽의 **더보기** > **인스턴스 설정** > **역할 바인딩/수정**을 선택합니다. 아래 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/34d5a9866aa28fdb8a3363884918e3bb.png)
  - **탭 뷰**: CVM 페이지 오른쪽 상단의 **더보기** > **인스턴스 설정** > **역할 바인딩/수정**을 선택합니다. 
3. 팝업된 ‘역할 바인딩/수정’ 창에서 바인딩할 역할을 선택하고 **확인**을 클릭합니다.

:::
::: 여러 인스턴스의 역할 바인딩/수정

1. ‘인스턴스’ 리스트 페이지에서 역할을 바인딩 또는 수정할 CVM을 체크하고, 상단의 **더 많은 작업** > **인스턴스 설정** > **역할/바인딩 수정**을 클릭합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/4093443ee4f5b484860f8c8eae3b3b3e.png)
2. 팝업된 ‘역할 바인딩/수정’ 창에서 바인딩할 역할을 선택하고 **확인**을 클릭합니다.
<dx-alert infotype="explain" title="">
이 방식을 통하여 수정된 여러 대의 인스턴스는 역할이 모두 동일합니다.
</dx-alert>


:::
</dx-tabs>


### 인스턴스의 역할 삭제
<dx-tabs>
::: 단일 인스턴스의 역할 삭제
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm)에 로그인한 뒤, 왼쪽 사이드바의 **인스턴스**를 선택합니다.
2. 인스턴스의 관리 페이지에서 사용된 실제 뷰 모드에 따라 작업합니다.
   - **리스트 뷰**: 역할을 삭제할 CVM의 행 오른쪽의 **더보기** > **인스턴스 설정** > **역할 삭제**를 선택합니다. 아래 이미지와 같습니다.
   ![](https://main.qcloudimg.com/raw/8b44772763ab60fa69c404360db1ebbf.png)
   - **탭 뷰**: CVM 페이지 오른쪽 상단의 **더 많은 작업** > **인스턴스 설정** > **역할 삭제**를 선택합니다. 
2. 팝업된 ‘역할 삭제’ 창에서 **확인**을 클릭합니다.

:::
::: 여러 인스턴스의 역할 삭제
1. ‘인스턴스’ 리스트 페이지에서 역할을 삭제할 CVM을 체크하고, 상단의 **더 많은 작업** > **인스턴스 설정** > **역할 삭제**를 클릭합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/72669a0d3bbdde1491c24b5acc0eadbf.png)
3. 팝업된 ‘역할 삭제’ 창에서 **확인**을 클릭합니다.
:::
</dx-tabs>

