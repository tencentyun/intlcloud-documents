## 소개

CloudBerry Explorer는 COS(Cloud Object Storage) 관리에 사용할 수 있는 클라이언트 툴입니다. COS는 CloudBerry Explorer를 통해 Windows 등 운영 체제에 마운트할 수 있어 사용자의 COS 파일 액세스, 이동 및 관리가 편리합니다.


## 지원 시스템

Windows, macOS 시스템을 지원합니다.

## 다운로드 주소

[CloudBerry 공식 다운로드](https://www.cloudberrylab.com/download-thanks.aspx?prod=cbes3free&src=ms)로 이동하십시오.

## 설치 및 구성

>! 하기 구성 단계는 CloudBerry Explorer Windows v6.3을 예로 들어 설명합니다. 다른 버전의 구성 과정과 약간의 차이가 있을 수 있습니다.
>

1. 설치 패키지를 더블클릭하고 프롬프트에 따라 설치를 완료합니다.
2. 툴을 열고 S3 Compatible을 선택하고 더블클릭합니다.
3. 팝업 창에서 다음 정보를 설정하고 Test Connection을 클릭하면 연결이 성공적으로 완료됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c7c351ac3c8fbabcf635ae7699fb3dba.png)
다음은 설정 항목에 관한 설명입니다.
 - Display name: 사용자 정의 사용자 이름을 입력합니다.
 - Service point: 형식은 `cos.<Region>.myqcloud.com`이며, 예를 들어 청두 리전의 버킷에 액세스하려면 `cos.ap-chengdu.myqcloud.com`을 입력하십시오. 리전 약칭(region)은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오.
 - Access key: 액세스 키 정보 SecretId를 입력합니다. [Tencent Cloud API 키](https://console.cloud.tencent.com/capi)로 이동하여 생성 및 획득할 수 있습니다.
 - Secret key: 액세스 키 정보 Secretkey를 입력합니다. [Tencent Cloud API 키](https://console.cloud.tencent.com/capi)로 이동하여 생성 및 획득할 수 있습니다.
4. 계정 정보 추가 완료 후 Source에서 이전에 설정한 사용자 이름을 선택하면 해당 사용자 이름 아래에 있는 버킷 리스트를 볼 수 있습니다. 이는 구성이 완료되었음을 의미합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5b001159dea9eada859a06014d1cbdfd.png)

## COS 파일 관리

### 버킷 리스트 조회

Source에서 이전에 설정한 사용자 이름을 선택하여 사용자 이름 아래의 버킷 리스트를 볼 수 있습니다.

>! Service point에서 구성한 리전에 해당하는 버킷만 볼 수 있습니다. 다른 리전의 버킷을 보려면 **File > Edit Accounts**를 클릭하고 사용자 이름을 선택한 다음 Service point 매개변수를 다른 리전으로 수정합니다.
>

### 버킷 생성

이미지의 아이콘을 클릭하고 팝업 창에 전체 버킷 이름을 입력합니다(예: examplebucket-1250000000). 입력이 정확하면 **OK**를 클릭하여 생성을 완료합니다.
버킷의 이름 생성 규칙은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/9192916f402017e27f8b233ac2c72c9e.png)

### 버킷 삭제

버킷 리스트에서 삭제할 버킷을 선택하고 **Delete**를 우클릭하여 삭제합니다.


### 객체 업로드

버킷 리스트에서 업로드할 객체의 버킷 또는 경로를 선택한 후 로컬 컴퓨터에 업로드할 객체를 선택하고 왼쪽 창으로 드래그하면 업로드 작업이 완료됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/92aea7e39697ab46bb29f430bc58206a.png)

### 객체 다운로드

왼쪽 창에서 다운로드할 객체를 선택한 후 오른쪽에 있는 로컬 컴퓨터의 폴더로 객체를 드래그하여 다운로드 작업을 완료합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1ed1432256fd44ac2f9739f6fda263b1.png)

### 객체 복사

툴의 오른쪽 창에서 복사된 객체 타깃 경로를 선택한 후 왼쪽 창에서 복사할 객체를 선택하고 **Copy**를 우클릭하여 팝업 정보를 확인하면 객체 복사 작업이 완료됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5d1801cd20fe1885ee6e16ddec1139c5.png)

### 객체 이름 변경

버킷에서 이름을 변경할 객체를 찾아 **Rename**을 우클릭하고 새 이름을 입력합니다.


### 객체 삭제

버킷에서 삭제하려는 객체를 찾아 **Delete**를 우클릭하여 객체를 삭제합니다.

### 객체 이동

툴 오른쪽 창에서 이동된 객체 타깃 경로를 선택한 후 왼쪽 창에서 이동할 객체를 선택하고 **Move**를 우클릭하여 팝업 창 정보를 확인하면 객체 이동 작업이 완료됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5b4f20a2f400bf24f70dde5b93ed8053.png)


### 기타 기능

상기 기능 외에도 CloudBerry Explorer는 객체 ACL 설정, 객체 메타데이터 조회, 사용자 정의 Headers, 객체 URL 가져오기 등과 같은 다른 기능도 지원합니다. 사용자는 실제 필요에 따라 작업할 수 있습니다.


