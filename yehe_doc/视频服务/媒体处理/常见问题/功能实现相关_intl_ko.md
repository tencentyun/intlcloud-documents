[](id:que1)

### 미디어 메타 정보를 얻는 방법은 무엇입니까?
자세한 내용은 [미디어 메타 정보 가져오기](https://intl.cloud.tencent.com/document/product/1041/37461)를 참고하십시오.

[](id:que2)

### 시간대별 스크린샷을 설정하는 방법은 무엇입니까?

#### 호출 API 생성

자세한 내용은 [지정된 시간대별 스크린샷 템플릿 생성](https://intl.cloud.tencent.com/document/product/1041/33672)을 참고하십시오.

#### 콘솔을 통해 생성

1. [MPS 콘솔](https://console.cloud.tencent.com/mps/workflows/add)에 로그인한 후, 왼쪽 메뉴에서 **워크플로 관리**를 클릭해 ‘워크플로 관리’ 인터페이스로 이동합니다.
2. **워크플로 생성**을 클릭해 '워크플로 생성' 페이지로 이동합니다. 워크플로 생성 시 워크플로 이름, 트리거 Bucket, 트리거 디렉터리, 출력 Bucket, 출력 디렉터리, 이벤트 공지와 같은 항목을 설정해야 합니다.
3. 스크린샷 유형에서 시간대별 스크린샷을 선택합니다. 스크린샷 시점은 워크플로 관리에서 설정해야 합니다. 템플릿은 템플릿 이름과 이미지 크기만 설정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/751f3dd9ea1c03ed9dce47a83d13008b.png)
 - 스크린샷 템플릿: 시간대별 스크린샷, 샘플링 화면 캡처, 스프라이트 스크린샷을 포함합니다. 각 스크린샷 방법은 해당 모드에서 구성된 템플릿만 선택할 수 있습니다. 시간대별 스크린샷은 시점 선택이 필요합니다. 기존 템플릿이 사용 요구 사항을 충족하지 않는 경우 [템플릿 설정 - 스크린샷 템플릿](https://console.cloud.tencent.com/mps/templates?tab=snapshot)에서 새 템플릿을 생성할 수 있습니다.
 - 워터마크 템플릿: 각 트랜스코딩 템플릿은 최대 4개의 워터마크를 지원합니다. 기존 워터마크가 사용 요구 사항을 충족하지 못하는 경우 [템플릿 설정 - 워터마크 템플릿](https://console.cloud.tencent.com/mps/templates?tab=watermark)에서 새 템플릿을 생성할 수 있습니다.

[](id:que3)
### 비디오 콘텐츠 분석 템플릿은 어떻게 생성합니까?
MPS는 [사전 설정 비디오 콘텐츠 분석 템플릿](https://intl.cloud.tencent.com/document/product/1041/33476)을 제공합니다. 또한 [서버 API](https://intl.cloud.tencent.com/document/product/1041/37470)를 호출하여 사용자 정의 비디오 콘텐츠 분석 템플릿을 생성하고 관리할 수 있습니다.

[](id:que4)
### 비디오 콘텐츠 분석 템플릿은 어떻게 사용합니까?
1. 비디오 콘텐츠 분석 작업은 **API를 통한 수동 시작 **및** 업로드를 통한 자동 트리거**의 두 가지 방법을 지원합니다.
2. 비디오 콘텐츠 분석 작업이 시작된 후, 비디오 콘텐츠 분석 작업의 실행 결과는 쿼리 작업을 동기적으로 수행하는 것과 비동기적으로 결과 알림을 기다리는 두 가지 방법으로 얻을 수 있습니다.

[](id:que5)
### scrollToken 쿼리를 사용하여 새로 완료된 작업을 찾을 수 있습니까?
MPS에서 scrollToken을 이용하여 작업 리스트를 쿼리하면 작업 리스트가 생성 시간별로 정렬되어 있기 때문에 새로 완료된 작업을 찾지 못할 수 있습니다.
>? scrollToken은 분할 가져오기에 사용됩니다. 단일 요청으로 모든 데이터를 가져올 수 없는 경우, 인터페이스는 ScrollToken을 반환합니다. 다음 요청은 해당 Token을 수반하고 다음 기록에서 가져옵니다.

[](id:que6)
### 작업 리스트는 어떻게 가져옵니까?
자세한 방법은 [작업 리스트 가져오기](https://intl.cloud.tencent.com/document/product/1041/33643) 인터페이스를 참고하십시오.

[](id:que7)
### 작업 리스트는 어떻게 정렬합니까?
MPS로 얻은 작업 리스트는 **생성 시간** 순으로 정렬되어 있으며, 자세한 내용은 [작업 리스트 가져오기](https://intl.cloud.tencent.com/document/product/1041/33643)를 참고하십시오.

[](id:que8)
### 동적 워터마크를 추가하는 방법은 무엇입니까?
동적 이미지는 APNG 형식으로 설정한 다음 편집 워크플로에서 워터마크로 추가해야 합니다.

[](id:que9)
### 워터마크 템플릿은 어떻게 수정합니까?
구체적인 수정 방법은 [워터마크 템플릿 수정](https://intl.cloud.tencent.com/document/product/1041/33646) 인터페이스를 참고하십시오.

[](id:que10)
### COS bucket을 MPS 서비스와 연결하는 방법은 무엇입니까?
워크플로를 설정하기 위해서는 bucket을 선택해야 하며, 지정 Bucket과 디렉터리에 업로드된 비디오가 자동으로 MPS를 트리거하게됩니다. 자세한 내용은 [워크플로 관리](https://intl.cloud.tencent.com/document/product/1041/33485)를 참고하십시오.

[](id:que11)

### 콘텐츠 처리 서비스 이용 시 특정 프레임의 이미지를 처리하여 OCR의 콘텐츠를 얻는데, 프레임의 이미지는 어떻게 가져옵니까?
MPS의 ‘MPS 인터페이스 시작’을 사용하여 시간대별 스크린샷을 찍습니다.
1. OCR 인식 시점을 기록합니다.
2. 획득한 시점을 MPS 인터페이스 ProcessMedia의 스크린샷 작업 전달 매개변수 [MediaProcessTaskInput](https://intl.cloud.tencent.com/document/product/1041/33640)>[SnapshotByTimeOffsetTaskInput](https://intl.cloud.tencent.com/document/product/1041/33690)에 전달합니다.

[](id:que12)

### COS에 작업 권한을 어떻게 부여합니까?

MPS는 COS 버킷에 업로드된 파일에 다운로드, 트랜스 코딩, 업로드 등의 읽기 및 쓰기 작업을 수행해야 하므로, 서비스 역할을 생성하고 MPS에 COS 관련 작업 권한을 부여해야 합니다.
작업 순서:
1. [MPS 콘솔](https://console.cloud.tencent.com/mps)에 접속한 후, 왼쪽 메뉴바의 **인증 관리**를 클릭하여 ‘인증 관리’ 페이지로 이동합니다. 권한이 없는 경우 **CAM으로 이동**을 클릭하여 통합 권한 관리 페이지로 이동하여 권한을 부여합니다. MPS 권한 부여에 동의하면 서비스 사전 설정 역할이 생성되고 MPS 관련 권한이 부여됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/acd667fb5514bc01da3deaf0f84fbcc8.png)

> ! 권한 부여가 완료되지 않은 경우, MPS 콘솔에서 다른 작업을 수행할 수 없습니다.
2. 권한 부여 후 ‘인증 관리’ 페이지에서 권한 부여가 완료되었음을 확인할 수 있습니다. **권한 부여 취소**을 클릭하면 **CAM**으로 리디렉션되고, [서비스 역할](https://intl.cloud.tencent.com/document/product/598/19388)을 삭제하면 COS에 대한 MPS에 대한 작업 권한을 해제할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f880511bc91dfbda8bde68990c93adcc.png)
