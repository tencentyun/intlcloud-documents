COS Select 기능은 구조화된 쿼리 명령(SQL)을 통해 Cloud Object Storage(COS)에 저장된 객체를 선별하여 객체나 사용자가 필요한 데이터를 인덱스하기 쉽도록 합니다. COS Select 기능으로 객체 데이터를 선별하여 COS에 전송된 데이터 양을 줄이면 데이터 검색에 필요한 비용과 딜레이 현상을 줄일 수 있습니다.

현재 COS Select 기능은 CSV, JSON, Parquet 포맷 형태의 버킷 객체와 GZIP이나 BZIP2로 압축된 객체(CSV, JSON 포맷의 객체) 인덱스를 지원합니다. 또한 COS Select 기능으로 결과물을 CSV나 JSON 포맷으로 지정할 수 있으며 결과 기록을 어떻게 구분할지 지정할 수 있습니다.

요청을 통해 SQL 표현식을 COS에 전송할 수 있습니다. 현재 COS Select는 일부 SQL 표현식만 지원합니다. COS Select가 지원하는 SQL 표현식에 대한 자세한 정보는 [SQL 함수](https://intl.cloud.tencent.com/document/product/436/32474) 문서를 참고하십시오.

COS 콘솔, API, SDK, COSCMD 등의 방식으로 SQL쿼리를 실행할 수 있습니다. COS 콘솔을 사용하여 파일 검색을 진행할 때는 일부 제한 사항이 있음을 주의하십시오. 최대 128M 파일 검색을 지원하며 데이터양은 40MB까지 반환됩니다. 더 많은 데이터를 인덱스 하려면 다른 방식을 사용해 주십시오.

>?
>- COS Select가 지원하는 데이터 유형과 현재 예약된 필드는 [데이터 유형](https://intl.cloud.tencent.com/document/product/436/32476)과 [보관 필드](https://intl.cloud.tencent.com/document/product/436/32475)에서 자세히 볼 수 있습니다.
>- 현재 인덱스 기능은 중국대륙 공유 클라우드 리전에서만 지원됩니다. 기타 리전에서는 이 기능을 지원하지 않습니다.
>

## 사용 제한

COS Select을 사용할 때 다음과 같은 제한 사항이 있습니다.

- 조회 대상의 `cos:GetObject` 권한을 가지고 있어야 합니다. 루트 계정은 기본적으로 이 권한을 가지고 있습니다.
- 표준 스토리지 유형의 객체만 인덱스할 수 있습니다.
- SQL 표현식의 최대 길이는 256KB입니다.
- 인덱스 결과에서 단일 기록의 최대 길이는 1MB입니다.

COS Select 기능이 지원하는 SQL 절은 다음과 같습니다.

- SELECT 명령
- FROM 절
- WHERE 절
- LIMIT 절

>?SQL 절에 대한 세부 정보는 [Select 명령어](https://intl.cloud.tencent.com/document/product/436/32473)를 참고하십시오.

현재 COS Select가 지원하는 함수는 다음 예시와 같습니다.

- 집계 함수: AVG 함수, COUNT 함수, MAX 함수, MIN 함수, SUM 함수
- 조건부 함수: COALESCE 함수, NULLIF 함수
- 변환 함수: CAST 함수
- 날짜 함수: DATE_ADD 함수, DATE_DIFF 함수, EXTRACT 함수, TO_STRING 함수, TO_TIMESTAMP 함수, UTCNOW 함수
- 문자열 함수: CHAR_LENGTH 함수, CHARACTER_LENGTH 함수, LOWER 함수,  SUBSTRING 함수, TRIM 함수, UPPER 함수

>?SQL 함수에 대한 세부 정보는 [SQL 함수](https://intl.cloud.tencent.com/document/product/436/32474)를 참고하십시오.

현재 COS Select가 지원하는 오퍼레이터는 다음과 같습니다.

- 논리 오퍼레이터: `AND, NOT, OR`
- 비교 오퍼레이터: `<, >, <=, >=, =, <>, !=, BETWEEN, IN`
- 패턴 매칭 오퍼레이터: `LIKE`
- 수학 오퍼레이터: `+, -, *, %`

>? 오퍼레이터에 관한 자세한 정보는 [오퍼레이터](https://intl.cloud.tencent.com/document/product/436/32477)를 참고하십시오.
>



## 인덱스 요청 보내기

콘솔, API, SDK등 여러 방식을 사용해 인덱스 요청을 할 수 있습니다.

- 콘솔을 사용하려면 [인덱스 데이터](https://intl.cloud.tencent.com/document/product/436/32538) 문서를 참고하여 작업할 수 있습니다.
- API를 사용하려면 [SELECT Object Content](https://intl.cloud.tencent.com/document/product/436/32360) API 문서를 참고하십시오.
- SDK를 사용하려면 [SDK 개요](https://intl.cloud.tencent.com/document/product/436/6474)에서 필요한 SDK 인터페이스를 선택하십시오.


## FAQ

조회할 때 오류가 생기면 COS Select는 오류 코드와 관련 오류 메시지를 반환합니다. 관련 오류 코드와 설명 리스트는 [Special error codes](https://intl.cloud.tencent.com/document/product/436/32360#errorcode)를 참고하십시오.                      


