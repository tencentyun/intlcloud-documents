## 소개
COS 콘솔의 버킷 리스트 페이지에서 버킷을 생성할 수 있습니다. 버킷에 대한 자세한 내용은 [버킷 개요](https://intl.cloud.tencent.com/document/product/436/13312)를 참고하십시오.

>! 각 계정은 리전에 관계없이 최대 200개의 버킷을 생성할 수 있습니다.
>

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 메뉴에서 **버킷 리스트**를 클릭하여 버킷 리스트 페이지로 이동합니다.
3. **버킷 생성**을 클릭합니다.
4. 팝업되는 버킷 생성 대화 상자에서 다음 정보를 설정합니다.


 1. 기본 정보
![](https://qcloudimg.tencent-cloud.cn/raw/3cd1360bc4c2fe796ee2f2d97975727d.png)
	 - **리전**: 비즈니스 또는 사용자가 분포된 물리적 위치에 해당하는 COS 리전입니다. 이 매개변수는 일단 구성되면 수정할 수 없습니다. 리전에 대한 자세한 내용은 [리전 및 액세스 엔드포인트](https://intl.cloud.tencent.com/document/product/436/6224)를 참고하십시오.
	 - **이름**: 사용자 지정 버킷 이름으로 구성된 후에는 수정할 수 없습니다. 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312#.E5.AD.98.E5.82.A8.E6.A1.B6.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83)을 참고하십시오.
	 - **액세스 권한**: 버킷에 대해 기본적으로 비공개 읽기/쓰기, 공개 읽기/비공개 쓰기, 공개 읽기/쓰기의 세 가지 액세스 권한을 사용할 수 있습니다. 필요한 경우 수정할 수 있습니다. 자세한 내용은 [액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13315)을 참고하십시오.
	 - **엔드포인트**: 값이 자동으로 생성됩니다. 버킷을 생성한 후 이 엔드포인트를 사용하여 버킷에 액세스할 수 있습니다.
 2. 고급 옵션 설정
>? 이 설정 항목은 선택 사항으로, 필요에 따라 설정할 수 있습니다.
>
![](https://qcloudimg.tencent-cloud.cn/raw/f8acbd14ecadbbdf0445f567f5853898.png)
    - **버전 제어**: 이 필드가 활성화되어 있고 이름이 이미 존재하는 객체를 업로드하면 이전 버전이 보존됩니다.
    - **MAZ(다중 AZ) 구성**: 버킷 플래그입니다. 활성화하면 리전 내 재해 복구를 위해 데이터가 동일한 리전의 다른 데이터 센터에 저장됩니다. 현재 이 기능은 베이징, 상하이, 광저우, 싱가포르와 같은 특정 리전에서만 사용할 수 있습니다. 자세한 내용은 [Overview of Multi-AZ Feature](https://intl.cloud.tencent.com/document/product/436/35208)를 참고하십시오.
>!
>- 버킷에 대한 MAZ 구성을 활성화하면 버전 관리도 활성화됩니다. MAZ 구성이 활성화된 후에는 수정할 수 없으며 데이터는 MAZ_STANDARD 및 MAZ_STANDARD_IA와 같은 MAZ 스토리지 클래스의 버킷에 저장됩니다. 주의하여 구성하십시오.
>- 기존 버킷에 대해 다중 AZ를 활성화할 수 없습니다. 생성 중에 새 버킷에 대해서만 활성화할 수 있습니다.
>
	  - **로그 저장**: 버킷 작업과 관련된 각종 요청 로그를 기록합니다.
  	- **버킷 태그**: 버킷을 관리하기 위한 식별자로 사용되는 태그입니다. 자세한 내용은 [버킷 태그 설정](https://intl.cloud.tencent.com/document/product/436/30928)을 참고하십시오.
  	- **서버측 암호화**: 현재 유일하게 지원되는 버킷 암호화 방법은 SSE-COS 암호화(즉, 관리 키를 사용한 서버 암호화)입니다. 서버 암호화에 대한 자세한 내용은 [서버측 암호화 개요](https://intl.cloud.tencent.com/document/product/436/18145)를 참고하십시오.
 3. 설정 확인
  ![](https://qcloudimg.tencent-cloud.cn/raw/20e65888c7a948dfe5ce67402df5167b.png)
  버킷의 설정 정보를 확인합니다. 수정이 필요한 경우 **이전 단계**를 클릭합니다.

  

 4. 정보가 정확한지 확인한 후 **생성**을 클릭하면 버킷이 생성됩니다. 버킷 리스트 페이지에서 방금 생성한 버킷을 확인할 수 있습니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/7d7f83ffab77e7892d7d2dd8f5ca633d.png)

