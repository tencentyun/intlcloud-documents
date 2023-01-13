## 소개

DragonDisk는 Windows 탐색기와 유사한 그래픽 인터페이스를 제공하며, 백업, 데이터 공유 및 기타 기능을 지원하는 무료 파일 관리 툴입니다. 사용자는 DragonDisk 툴을 통해 COS(Cloud Object Storage) 파일을 쉽고 빠르게 관리할 수 있습니다.

## 지원 시스템

Windows, Mac OS X 및 다양한 Linux 릴리스 버전에서 사용할 수 있습니다.

## 다운로드 주소

[DragonDisk 공식 다운로드](http://download.dragondisk.com/download-s3-compatible-cloud-client.html)로 이동하십시오.


## 설치 및 구성

>! 아래의 설정 단계는 DragonDisk Windows v1.05를 예로 들어 설명합니다. 다른 버전의 설정 과정과 약간의 차이가 있을 수 있습니다.
>

1. 설치 패키지를 더블클릭하고 프롬프트에 따라 설치를 완료합니다.
2. 툴을 열고 **File > Accounts**를 선택한 다음 팝업 창에서 **New**를 클릭하여 계정 설정 정보를 추가합니다.
3. 팝업 창에서 다음 정보를 설정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a8d83b57beafd32f916e7d530dd46416.png)
다음은 설정 항목에 관한 설명입니다.
 -  Provider: Other S3 compatible service를 선택합니다.
 - Service Endpoint: 형식은 `cos.<Region>.myqcloud.com`이며, 예를 들어 청두 리전의 버킷에 액세스하려면 `cos.ap-chengdu.myqcloud.com`을 입력하십시오. 리전 약칭(region)은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오.
 -  Account name: 사용자 정의 사용자 이름을 입력합니다.
 - Access key: 액세스 키 정보 SecretId를 입력합니다. [Tencent Cloud API 키](https://console.cloud.tencent.com/capi)로 이동하여 생성 및 획득할 수 있습니다.
 - Secret key: 액세스 키 정보 Secretkey를 입력합니다. [Tencent Cloud API 키](https://console.cloud.tencent.com/capi)로 이동하여 생성 및 획득할 수 있습니다.
4. 계정 정보 추가 완료 후 Root에서 이전에 설정한 사용자 이름을 선택하면 해당 사용자 이름 아래에 있는 버킷 리스트를 볼 수 있습니다. 이는 구성이 완료되었음을 의미합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/aa2cf3f681233d692d58ddcc7f16a833.png)

## COS 파일 관리

### 버킷 리스트 조회

Root에서 이전에 설정한 사용자 이름을 선택하여 사용자 이름 아래의 버킷 리스트를 볼 수 있습니다.

>! 이 작업은 Service Endpoint에서 설정한 리전에 해당하는 버킷만 볼 수 있습니다. 다른 리전의 버킷을 보려면 **File > Accounts**를 클릭하고 사용자 이름을 선택한 다음 Service Endpoint 매개변수를 다른 리전으로 수정합니다.
>



### 버킷 생성

1. 사용자 이름을 우클릭하여 **Create bucket**을 선택하고 팝업 창에 examplebucket-1250000000과 같이 전체 버킷 이름을 입력합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/46fd8b1296908a39b2949b7895dd1a60.png)
2. 입력이 완료되면 **OK**를 클릭하여 생성을 완료합니다.
버킷의 이름 생성 규칙은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오.

### 버킷 삭제

버킷 리스트에서 삭제할 버킷을 마우스 우클릭하여 컨텍스트 메뉴에서 **Delete bucket**을 선택합니다.


### 객체 업로드

버킷 리스트에서 업로드할 객체의 버킷 또는 경로를 선택한 후 로컬 컴퓨터에 업로드할 객체를 선택하고 해당 버킷 또는 경로로 드래그하여 업로드 작업을 완료합니다.


### 객체 다운로드

버킷 리스트에서 객체가 위치한 버킷을 찾아 우측 로컬 컴퓨터의 폴더로 드래그하면 다운로드가 완료됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/45fcab5119da7ab87d958853e8b6100a.png)


### 객체 복사

왼쪽 창에서 복사할 객체를 선택하고 **Copy**를 우클릭한 후 객체가 복사된 후 타깃 경로에서 **Paste**를 우클릭하면 객체 복사 작업이 완료됩니다.


### 객체 이름 변경

버킷에서 이름을 변경할 객체를 찾아 **Rename**을 우클릭하고 새 이름을 입력합니다.


### 객체 삭제

버킷에서 삭제하려는 객체를 찾아 **Delete**를 우클릭하여 객체를 삭제합니다.

### 객체 이동

왼쪽 창에서 이동할 객체를 선택하고 **Cut**을 우클릭한 다음, 객체가 이동된 타깃 경로 아래의 **Paste**를 우클릭하면 객체 이동 작업이 완료됩니다.


### 기타 기능

상기 기능 외에도 DragonDisk는 객체 ACL 설정, 객체 메타데이터 보기, Headers 사용자 지정, 객체 URL 가져오기 등과 같은 다른 기능도 지원합니다. 사용자는 실제 필요에 따라 작업할 수 있습니다.







