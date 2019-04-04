## 개요 정보

Batc Compute에서 로그 실행(StdOut, StdErr)과 원격 저장 매핑은 모두 COS/CFS 경로 입력과 관련이 있습니다. http 방식으로 COS 버킷 또는 파일에 접근하는 방식과 비교하였을 때와 차이가 있습니다. 세부 내용은 다음과 같습니다.

## 1. COS 경로 설명

### COS XML API 접근 도메인 이름만 지원합니다.

![1](https://main.qcloudimg.com/raw/ffdc93298f0715949baa7c47cc161c07.png)

COS는 지원하는 접근 도메인 이름은 XML API와 JSON API에 적용할 수 있는 두 가지가 있습니다. Batch에 입력할 때는 XML API 형식의 도메인 이름만 지원합니다. 위 그림 빨간색 프레임 부분과 같습니다.

### 접두사는 cos://로 시작해야 합니다

![2](https://main.qcloudimg.com/raw/260fbee4e1bfddf4bd92f60ff3d68510.png)

예를 들어 위 그림의 주소를 Batch 경로에 입력할 때에는 cos://를 반드시 추가해야 합니다. 구체적인 형식은 아래와 같습니다.

``` 
cos://testbatch-1252462967.cos.ap-beijing-1.myqcloud.com/ 
```

``주의: /로 마무리해야 함``

### 하위 디렉터리 탑재

![3](https://main.qcloudimg.com/raw/051f08ee7dd0665a5ced29b1c41affac.png)

하위 디렉터리에 일잔벅인 파일 디렉터리의 방식으로 버킷의 도메인 이름 뒷부분에 추가하면 됩니다. 예를 들어, 위 그림 버킷의 폴더에 디렉터리 탑재 시 COS 경로 입력 방식은 다음과 같습니다.

``` 
cos://testbatch-1252462967.cos.ap-beijing-1.myqcloud.com/testdir/ 
```

### 동일 지역 버킷 지원

COS는 지역 속성을 지니며 Batch 작업과 COS 버킷이 동일 지역에 있어야 하고 데이터를 고효율적으로 저장과 CVM 사이에서 전송할 수 있습니다.

## 2. CFS 경로 설명

원격 저장 매핑에서 CFS/NAS 경로를 로컬 경로에 자동 탑재를 구성할 수 있습니다.

![4](https://mc.qcloudimg.com/static/img/7721d8b14f775055615d430528008cb9/3.png)

### 접두사는 cfs:// 또는 nfs://로 시작해야 합니다

예를 들어 위 그림의 주소를 Batch 경로에 입력할 때에는 cfs:// 또는 nfs://를 반드시 추가해야 합니다. 구체적인 형식은 아래와 같습니다.

``` 
cfs://10.66.140.208/ 
```

``주의: /로 마무리해야 하며, CFS/NAS와 Batch 작업을 동일 네트워크에 구성해야 합니다.``








