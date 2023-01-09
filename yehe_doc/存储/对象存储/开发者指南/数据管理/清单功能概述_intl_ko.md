## 인벤토리가 무엇인가요?

인벤토리는 사용자가 버킷의 객체를 관리하도록 도와주는 기능입니다. COS를 대신해 List API 동기화 작업을 주기적으로 할 수 있습니다. Cloud Object Storage(COS)는 사용자의 인벤토리 작업 설정에 따라 매일 혹은 매주 제 시간에 사용자 버킷 내의 지정된 객체나 똑같은 접두사를 가진 객체를 스캐닝하고 인벤토리 보고서를 CSV 형식 파일로 출력하여 사용자가 지정한 버킷에 저장합니다. 파일에서 저장한 객체와 이에 대응되는 메타데이터 목록을 만들 수 있으며 사용자의 설정 정보에 따라 사용자가 필요한 객체 속성 정보를 기록합니다.

인벤토리 기능의 용도는 다음을 포함하며 이에 국한되지 않습니다.

- 객체 복사 및 암호화 상태를 심의하고 보고합니다.
- 비즈니스 작업 흐름 및 빅 데이터 작업을 간소화하고 가속화합니다.

>!
>- 사용자는 버킷에서 여러 개의 인벤토리 작업을 설정할 수 있으며 인벤토리 작업을 실행하는 동안 객체의 메타데이터 등의 속성 정보는 스캐닝할 수 있지만 객체 콘텐츠를 읽어 들일 수는 없습니다.
>

## 인벤토리 매개변수

사용자가 인벤토리 작업을 설정한 후 COS는 설정에 따라 정기적으로 사용자 버킷 내에 지정된 객체를 스캐닝하며 CSV 형식 파일로 인벤토리 보고서를 출력합니다. 현재 COS 인벤토리 보고서는 다음 정보를 기록할 수 있습니다.

| 인벤토리 정보            | 설명                                                         |
| ------------------- | ------------------------------------------------------------ |
| AppID               | 계정 ID                                                |
| Bucket              | 인벤토리 작업을 실행할 버킷 이름                                 |
| fileFormat       |  파일 형식  |
| listObjectCount | 나열된 객체 수량. 이 항목에 따라 요금이 부과되며, 자세한 사항은 <a href="https://intl.cloud.tencent.com/document/product /436/40098">관리 기능 요금</a>의 인벤토리 기능 요금 부분을 참고하십시오. |
| listStorageSize | 나열된 객체 크기 |
|filterObjectCount  |선별된 객체 수|
|filterStorageSize  |  선별된 객체 크기|
| Key                 | 버킷의 객체 파일 이름. CSV 파일 형식을 사용할 때 객체 파일 이름은 URL 코드 형식으로 복호화한 후 사용할 수 있습니다.|
| VersionId           | 객체 버전 ID. 버킷에서 버전 제어를 활성화한 후 COS는 버킷에 추가된 객체에 버전 번호를 지정할 수 있습니다. 인벤토리가 객체의 현재 버전 전용인 경우 해당 필드는 포함하지 않습니다. |
| IsLatest            | 객체가 최신 버전이라면 True로 설정합니다. 인벤토리가 객체의 현재 버전 전용인 경우 해당 필드는 포함하지 않습니다. |
| IsDeleteMarker      | 객체가 삭제 마커라면 True로 설정합니다. 인벤토리가 객체의 현재 버전 전용인 경우 해당 필드는 포함하지 않습니다. |
| Size                | 객체 크기(바이트 단위)                                   |
| LastModifiedDate    | 객체의 최근 수정 일자(늦은 일자 기준)                     |
| ETag                | 실물 태그는 객체의 해시 값입니다. ETag는 객체 콘텐츠의 변경 내용만 반영되며 객체 메타데이터의 변경 내용은 반영되지 않습니다. ETag는 객체 데이터 MD5의 요약일 수도 있고 아닐 수도 있습니다. 이 여부는 객체의 생성 방식과 암호화 방식으로 결정되지 않습니다. |
| StorageClass        | 객체의 스토리지 분류. 자세한 내용은 [스토리지 유형](https://intl.cloud.tencent.com/document/product/436/30925)을 참고하십시오. |
| IsMultipartUploaded | 객체가 멀티파트 업로드의 형식으로 업로드되면 True로 설정합니다. 자세한 내용은 [멀티파트 업로드](https://intl.cloud.tencent.com/document/product/436/14112)를 참고하십시오. |
| Replicationstatus   | 객체 복제에서 소스 및 복제본 파일의 상태입니다. 소스 파일 상태: PENDING`(복제 예정), COMPLETED(복제됨) 또는 FAILED(복제 실패); 복제 파일 상태: REPLICA(생성된 복제 파일로 복제됨). 자세한 내용은 [복사 작용 설명](https://intl.cloud.tencent.com/document/product/436/19923)을 참고하십시오.  |
| Tag | 객체 태그 |

## 인벤토리 설정 방법

인벤토리를 설정하기 전 두 가지 개념을 알아야 합니다.

- 소스 버킷: 인벤토리 기능을 활성화하고 싶은 버킷.
  - 인벤토리가 나열한 객체를 포함합니다.
  - 인벤토리 설정을 포함합니다.
- 타깃 버킷: 스토리지 인벤토리의 버킷.
  - 인벤토리 목록 파일을 포함합니다.
  - Manifest 파일을 포함하며 인벤토리 목록 파일 위치를 설명합니다.

다음은 인벤토리 설정 절차입니다.

<span id="step1"></span>

#### 소스 버킷에서 분석할 객체 정보 지정

COS에 어떤 객체 정보 분석이 필요한지 보고해야 합니다. 따라서 인벤토리 기능을 설정할 때 소스 버킷에서 아래 정보를 설정해야 합니다.

- 객체 버전 선택: 모든 객체 버전을 나열하거나 현재 버전만 나열합니다. 모든 객체 버전 나열을 선택했다면 COS는 동일 이름을 가진 객체의 지난 모든 버전을 인벤토리 보고서에 나열합니다. 현재 버전만 나열하도록 선택했다면 COS는 최신 버전 객체만 기록합니다.
- 분석이 필요한 객체 속성 설정: 객체 속성 중 어떤 정보가 인벤토리 보고서에 어떤 정보가 기록되는지 COS에 알려야 하며 현재 지원하는 객체 속성은 계정 ID, 소스 버킷 이름, 객체 파일 이름, 객체 버전 ID, 최신 버전 여부, 삭제 마커 여부, 객체 크기, 객체 최신 수정 일자, ETag, 객체 스토리지 종류, 리전 간 복제 표시, 멀티파트 업로드 파일에 속하는지의 여부가 포함됩니다.

<span id="step2"></span>
#### 인벤토리 보고서의 스토리지 정보 설정

COS는 어느 주파수에 따라 인벤토리 보고서를 내보낼지 공지하며 어느 버킷에 인벤토리 보고서가 저장되고 암호화 여부가 필요한지 결정합니다. 설정이 필요한 정보는 다음과 같습니다.

- 인벤토리 내보내기 빈도수 선택: 매일 혹은 매주. 이 설정을 통해 COS에 어떤 빈도수에 따라 인벤토리 기능을 실행할지 알릴 수 있습니다.
- 인벤토리 암호화 선택: 비암호화 혹은 SSE-COS. SSE-COS 암호화를 선택했다면 생성한 인벤토리 보고서에 대해 암호화를 진행합니다.
- 인벤토리를 내보낼 위치 설정: 버킷 저장이 필요한 인벤토리 보고서를 지정해야 합니다.

>! 타깃 버킷은 반드시 소스 버킷과 동일 리전에 위치해야 하며 양자는 동일 버킷일 수 있습니다.
>


## 사용 방법

#### 콘솔로 인벤토리 설정

[인벤토리 기능 활성화](https://intl.cloud.tencent.com/document/product/436/30624) 콘솔 문서를 참고하여 콘솔을 통한 인벤토리 기능 설정 방법을 알 수 있습니다.

#### API로 인벤토리 설정

API를 사용해 지정 버킷에 인벤토리 기능을 활성화하려면 다음 단계를 참고하십시오.

1. COS 역할을 생성합니다.
2. COS 역할 권한을 바인딩합니다.
3. 인벤토리 기능을 활성화합니다.

#### 1. COS 역할 생성
COS 역할 생성과 구체적인 인터페이스 정보는 [CreateRole](https://intl.cloud.tencent.com/document/product/598/33561)을 참고하십시오.
roleName은 반드시 COS_QcsRole이어야 합니다.
policyDocument:
```
{
	"version": "2.0",
	"statement": [{
		"action": "name/sts:AssumeRole",
		"effect": "allow",
		"principal":{
			"service": "cos.cloud.tencent.com"
		}
	}]
}
```

#### 2. COS 역할 권한 바인딩
역할 권한 바인딩 권한과 구체적인 인터페이스 정보는 [AttachRolePolicy](https://intl.cloud.tencent.com/document/product/598/33562)를 참고하십시오.
policyName은 QcloudCOSFullAccess, roleName은 1단계의 COS_QcsRole입니다. roleName 생성 시 반환된 roleID를 사용할 수 있습니다.

#### 3. 인벤토리 기능 활성화
인터페이스 호출, 인벤토리 기능 활성화 및 구체적인 인터페이스 정보는 [PUT Bucket inventory](https://www.tencentcloud.com/document/product/436/30625)를 참고하십시오. 매니페스트 파일에 저장할 타깃 버킷과 소스 버킷은 같은 리전에 있어야 합니다.


## 인벤토리 보고서 스토리지 경로

인벤토리 보고서와 Manifest 관련 파일은 타깃 버킷에 배포될 수 있으며 그 중 인벤토리 보고서는 다음 경로로 배포될 수 있습니다.

```shell
destination-prefix/appid/source-bucket/config-ID/
```

Manifest 관련 파일은 다음 경로로 타깃 버킷에 배포됩니다.

```shell
destination-prefix/appid/source-bucket/config-ID/YYYYMMDD/manifest.json
destination-prefix/appid/source-bucket/config-ID/YYYYMMDD/manifest.checksum
```

경로에서 나타내는 의미는 다음과 같습니다.

- **desitination-prefix**: 사용자가 인벤토리를 설정할 때 설치하는 ‘타깃 접두사’입니다. 타깃 버킷에서 공용 위치에 있는 모든 인벤토리 보고서를 그룹화하는데 사용할 수 있습니다.
- **source-bucket**: 인벤토리 보고서와 일치하는 소스 버킷 이름입니다. 이 폴더는 각각의 인벤토리 보고서를 여러 소스 버킷에서 동일한 타깃 버킷에 발송할 때 발생하는 충돌을 방지하기 위함입니다.
- **config-ID**: 사용자가 인벤토리를 설정할 때 설치된 ‘인벤토리 이름’으로 동일한 소스 버킷이 여러 인벤토리 보고서를 설치하고 이를 동일한 타깃 버킷에 발송할 때 config-ID로 상이한 인벤토리 보고서를 구분할 수 있습니다.
- **YYYYMMDD**: 타임스탬프. 인벤토리 보고서를 생성할 때 버킷이 스캐닝하기 시작하는 시간과 일자를 포함합니다.
- **manifest.json**: Manifest 파일을 가리킵니다.
- **manifest.checksum**: manifest.json 파일 콘텐츠의 MD5를 가리킵니다.

그 중 Manifest와 관련된 파일은 총 2개의 파일로 manifest.json과 manifest.checksum 입니다.

>?
> Mainfest 관련 파일 소개는 다음과 같습니다.
> - manifest.json과 manifest.chenksum은 모두 Manifest 파일입니다. manifest.json은 인벤토리 보고서의 위치를 설명하고 manifest.checksum은 manifest.json 파일 콘텐츠의 MD5입니다. 새로운 인벤토리 보고서를 딜리버리할 때마다 새로운 Manifest 파일이 따라 나올 수 있습니다.
> - manifest.json이 포함하는 모든 Manifest는 인벤토리의 메타데이터와 관련된 기타 기본 정보를 제공하며 그 정보는 아래와 같습니다.
>   - 소스 버킷 이름.
>   - 타깃 버킷 이름.
>   - 인벤토리 버전.
>   - 타임스탬프. 인벤토리 보고서 생성 시 버킷 일자와 시간을 스캐닝하기 시작합니다.
>   - 매니페스트 파일의 형식과 구성.
>   - 타깃 버킷 인벤토리가 보고하는 객체 키, 크기, md5Checksum.
>   

다음은 CSV 형식 인벤토리의 manifest.json 파일에 있는 Manifest 예시입니다.

```
{
 "sourceAppid": "1250000000",
 "sourceBucket": "example-source-bucket",
 "destinationAppid": "1250000000",
 "destinationBucket": "example-inventory-destination-bucket",
 "fileFormat": "CSV",
 "listObjectCount": "13",
 "listStorageSize": "7212835",
 "filterObjectCount": "13",
 "filterStorageSize": "7212835",
 "fileSchema": "Appid, Bucket, Key, Size, LastModifiedDate, ETag, StorageClass, IsMultipartUploaded, ReplicationStatus",
 "files": [
  {
   "key": "cos_bucket_inventory/1250000000/examplebucket/inventory01/04d73d9debc73d9f0bf85af461abde6c.csv.gz",
   "size": "502",
   "md5Checksum": "7d40288a09c25b302ad6cb5fced54f35"
  }
 ]
}
```

#### 인벤토리의 일치성

COS 인벤토리 보고서는 새 객체와 덮어쓴 PUT 그리고 삭제의 최종 일관성을 제공합니다. 따라서 인벤토리 보고서에는 최근 추가되거나 삭제한 객체가 포함되지 않을 수 있습니다. 예시로 COS가 사용자 설정의 인벤토리 업무 과정을 실행할 때 사용자가 객체를 업로드하거나 삭제할 경우 이 작업 결과는 인벤토리 보고서에 반영되지 않을 수 있습니다.

객체가 작업을 실행하기 전 객체의 상태를 확인하려면 [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) API를 사용하여 객체 메타데이터를 인덱스하거나 COS 콘솔에서 객체 속성을 조회하시기 바랍니다.
