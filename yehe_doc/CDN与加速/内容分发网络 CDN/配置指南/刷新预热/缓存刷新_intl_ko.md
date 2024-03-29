## 기능 소개

CDN은 기본 캐시 설정 기능을 제공하여 지정된 서비스 유형, 디렉터리 및 특정 URL과 같은 다양한 규칙 설정에 따라 캐시 만료 시간을 설정하여 주기적으로 노드 캐시 리소스를 정리하고 원본 서버로 최신 리소스를 풀링 할 수 있습니다.

이외에도 CDN은 캐시 퍼지 기능을 제공하며 URL 및 디렉터리를 일괄 지정하여 퍼지 작업을 진행할 수 있습니다.

- URL 퍼지: CDN 모든 노드에서 해당 리소스의 캐시를 삭제합니다.
- 디렉터리 퍼지: ‘업데이트된 리소스 퍼지’를 선택하면 최종 사용자가 해당 디렉터리 아래의 리소스에 액세스할 때 해당 리소스의 Last-Modify 정보를 원본 서버에서 가져옵니다. 캐시된 리소스와 동일한 경우 캐시된 리소스가 직접 반환됩니다. 그렇지 않으면 업데이트된 리소스가 원본 서버에서 가져와 다시 캐시됩니다. ‘모든 리소스 퍼지’를 선택하면 사용자가 해당 디렉터리 아래의 리소스에 액세스할 때 최신 버전의 리소스를 원본 서버에서 직접 가져와서 다시 캐시합니다.

> ?퍼지가 성공적으로 실행된 후에는 노드의 해당 리소스는 유효하지 않은 캐시가 됩니다. 사용자가 다시 액세스하면 노드 원본 서버는 필요한 리소스를 불러오고 다시 노드에 캐시합니다. 따라서 대량의 퍼지 작업을 제출하면 더 많은 캐시가 삭제되어 원본 가져오기 요청이 갑자기 증가하여 원본 서버에 더 많은 부담이 가중됩니다.

## 적용 시나리오

### 새로운 리소스 배포

원본 서버의 새 리소스로 같은 이름의 이전 리소스를 덮어쓴 후, 전체 네트워크 사용자가 노드 캐시의 영향으로 이전 리소스에 액세스되는 것을 방지하기 위해 해당 리소스의 URL/디렉터리를 제출하여 퍼지할 수 있습니다. 전체 네트워크 캐시가 삭제된 후에는 전체 네트워크 사용자는 직접 최신 리소스에 액세스할 수 있습니다.

### 위반 리소스 정리

사이트에서 위반 리소스(음란물, 마약, 도박)가 발견된 경우 원본 서버 리소스를 삭제한 후에도 노드 캐시 리소스로 인해 계속 액세스할 수 있게 됩니다. 네트워크 환경 보호를 위해 URL 퍼지를 통해 캐시 리소스를 삭제하여 적절한 시기에 정리 작업을 진행할 수 있습니다.

## 운영 가이드



[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인한 후, 왼쪽 메뉴에서 **Purge and Prefetch**를 클릭한 다음 필요에 따라 **Purge URL** 또는 **Purge Directory**를 제출합니다.
- CDN 및 ECDN URL/디렉터리를 함께 퍼지할 수 있습니다.
- 콘텐츠 입력과 txt 파일 업로드의 두 가지 제출 방법을 지원합니다.

![]()


### 콘텐츠 사양
우선 제출한 내용이 규칙에 부합하는지 확인하십시오:
- `http://www.test.com/test.html`과 같이 URL에 http:// 또는 https:// 프로토콜 식별자를 포함해야 하며, 한 줄에 하나씩 입력합니다.
- 비활성화/잠긴/현재 계정에 액세스되지 않은 도메인은 제출하지 마십시오.
- 파일 업로드를 선택한 경우 파일 형식이 txt이고 크기가 10M을 초과하지 않는지 확인하십시오.
- `http://*.test.com/` 형식의 URL 제출은 지원하지 않습니다.  - 액세스 가속 도메인이 와일드카드 서브도메인이더라도 해당 서브 도메인을 제출해야 합니다.
- URL 퍼지는 와일드카드가 포함된 URL 제출을 지원하지 않습니다.
- URL에 중국어가 포함된 경우 URL Encode 스위치를 활성화하여 중국어 인코딩을 변환하십시오.

### 제출 한도
- **Purge URL**:
각 계정의 하루 URL 퍼지 한도는 10000개입니다. 중국 본토 외 가속을 활성화한 경우 중국 본토 외 하루 URL 퍼지 한도는 10000개 이며, 중국 내 한도와 별개입니다.
	- 콘텐츠 직접 입력 제출 방식을 선택하는 경우, 한 번에 제출할 수 있는 URL 퍼지 한도는 1000개입니다.
	- 파일 업로드 방식을 선택하면 단일 제출 제한이 없으며, 제출 수량은 잔여 한도에서 차감됩니다.
>? URL 퍼지량이 많아 URL 퍼지의 일일 잔여 제한이 낮을 경우 (예: 1000 이하) Tencent Cloud CDN은 콘솔에서 일일 잔여 한도 원클릭 향상을 지원합니다(예: 50000개 이상으로 향상).
>- 한도 확대 후 바로 적용되니 한도 확대 버튼을 반복해서 누르지 말고 페이지를 새로고침하여 확인하십시오.
>- 한도 향상은 한 번만 지원됩니다. 일일 제한을 50000으로 향상한 후 다시 50000이상으로 향상할 수 없습니다.
>- 각 리전의 한도 향상은 상호 독립적입니다.
- **Purge Directory**:
	각 계정의 일일 디렉터리 퍼지 한도는 100개입니다. 중국 본토 외 가속을 활성화한 경우 중국 본토 외 일일 디렉터리 퍼지 한도는 100개이며 이는 중국 내 지역 한도와 별개입니다.
	- 콘텐츠 직접 입력 제출 방식을 선택하는 경우, 한 번에 제출할 수 있는 디렉터리 퍼지 한도는 20개입니다.
	- 파일 업로드 방식을 선택하면 단일 제출 제한이 없으며, 제출 수량은 잔여 한도에서 차감됩니다.
	

퍼지 작업을 제출할 때 기본적으로 URL의 도메인이 위치한 가속 리전에 따라 리전 전체를 퍼지합니다. 도메인 가속 영역이 글로벌인 경우 중국 내/외의 한도가 동시에 차감됩니다.
<span ID = "notes"></span>
작업 기록 쿼리는 [작업 기록](https://intl.cloud.tencent.com/document/product/228/42176)을 참고하십시오.


### 서브 계정 권한 설정

URL 퍼지, 디렉터리 퍼지 및 쿼리 기록 퍼지는 권한 시스템에 연결되었습니다. 리소스(도메인) 차원 권한 구성 설정을 지원합니다. 자세한 내용은 [콘솔 권한 설명](https://intl.cloud.tencent.com/document/product/228/35229)을 참고하십시오.


## 사용 사례

### 디렉터리 퍼지 - 리소스 변경 퍼지

가속 도메인이 purge-test-1251991073.file.myqcloud.com이고 원본 서버가 Tencent Cloud Object Storage(COS)일 때 원본 서버 리소스는 다음과 같습니다.
![]()

1. 리소스 1.txt 및 2.txt에 각각 액세스를 요청합니다. X-Cache-Lookup: Hit From Distank3 및 Server: NWS_SPMid에 따라 히트 노드를 판별하고, 노드가 직접 리소스를 반환합니다.
   ![](https://main.qcloudimg.com/raw/9b307b80e7d1c759bb073eb9f2cf4b6c.png)
   ![](https://main.qcloudimg.com/raw/5fed8bff43d699f47235e5d0db1f2447.png)
2. 동일한 이름의 파일 1.txt가 원본 서버에서 대체될 때 파일 수정 시간이 변경되고 2.txt는 변경되지 않습니다.
   ![](https://main.qcloudimg.com/raw/798fd6a984813aa3a16eaf43856ff7c2.png)
   ![](https://main.qcloudimg.com/raw/bc0d40200fbc744ed34d8552a95c5671.png)
3. 이때 요청이 다시 시작됩니다. 캐시가 만료되지 않았으므로 액세스 리소스 1.txt는 여전히 이전 내용입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/394a84d8f9974ed72cb629b11aac7206.png)
4. 디렉터리 퍼지를 제출하고 [리소스 변경 퍼지]를 선택한 후, 퍼지가 완료될 때까지 기다립니다.
   ![]()
5. 퍼지가 완료되면 1.txt Last-Modified 파일이 변경되므로 직접 원본 가져오기 요청이 진행되며, 2.txt 파일은 변경사항이 없어 디렉터리 퍼지가 제출되어도 노드 히트에 의해 반환됩니다.
   ![](https://main.qcloudimg.com/raw/0ea8c1e0e7caac970b3875d4b3987687.png)
   ![](https://main.qcloudimg.com/raw/84e599b1c9c655e62497fb4bdc8e7918.png)
