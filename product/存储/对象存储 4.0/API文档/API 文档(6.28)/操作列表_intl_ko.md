Tencent Cloud COS 관련 API 및 설명은 다음과 같습니다.

## Service 작업 관련
| API                                      | 작업 이름   | 작업 설명            |
| ---------------------------------------- | ----- | --------------- |
| [GET Service](https://cloud.tencent.com/document/product/436/8291) | 버킷 리스트 획득 | 지정 계정의 모든 Bucket List 획득 |

## Bucket 작업 관련

| API                                      | 작업 이름       | 작업 설명                        |
| ---------------------------------------- | --------- | --------------------------- |
| [DELETE Bucket](https://cloud.tencent.com/document/product/436/7732) | 버킷 삭제     | 지정 계정의 비어 있는 Bucket 삭제             |
| [DELETE Bucket cors](https://cloud.tencent.com/document/product/436/8283) | CORS 구성 삭제    | 버킷의 CORS 구성 정보 삭제         |
| [DELETE Bucket lifecycle](https://cloud.tencent.com/document/product/436/8284) | 수명 주기 삭제    | Bucket 수명 주기가 관리한 구성 삭제                 |
|[DELETE Bucket policy](https://cloud.tencent.com/document/product/436/8285)  |  버킷 정책 삭제 |지정 버킷의 권한 정책 삭제|
| [GET Bucket(List Object)](https://cloud.tencent.com/document/product/436/7734) | 개체 리스트 획득      | Bucket의 일부 또는 전체 Object 획득 |
| [GET Bucket acl](https://cloud.tencent.com/document/product/436/7733) | 버킷 ACL 획득 | Bucket의 ACL 획득           |
| [GET Bucket cors](https://cloud.tencent.com/document/product/436/8274) | CORS 구성 획득    | 버킷의 CORS 구성 정보 획득         |
| [GET Bucket lifecycle](https://cloud.tencent.com/document/product/436/8278) | 수명 주기 조회    | Bucket 수명 주기가 관리한 구성 조회                 |
|  [GET Bucket policy](https://cloud.tencent.com/document/product/436/8276)  | 버킷 정책 조회 | 지정 버킷의 권한 정책 조회
| [HEAD Bucket](https://cloud.tencent.com/document/product/436/7735) | 버킷 및 그 권한 인덱스   | Bucket 존재 여부 및 접근 권한 존재 여부 확인        |
| [List Multipart Uploads](https://cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 조회   | 진행 중인 멀티파트 업로드 정보 조회              |
| [PUT Bucket](https://cloud.tencent.com/document/product/436/7738) | 버킷 생성     | 지정 계정에 Bucket 1개 생성           |
| [PUT Bucket acl](https://cloud.tencent.com/document/product/436/7737) | 버킷 ACL 설정 | Bucket의 ACL 설정           |
| [PUT Bucket cors](https://cloud.tencent.com/document/product/436/8279) | CORS 구성 설정    | 버킷의 CORS 권한 설정           |
| [PUT Bucket lifecycle](https://cloud.tencent.com/document/product/436/8280) | 수명 주기 설정   |  Bucket 수명 주기가 관리한 구성 설정                 |
| [ PUT Bucket policy](https://cloud.tencent.com/document/product/436/8282) | 버킷 정책 설정 | 지정 버킷의 권한 정책 설정 |

## Object 작업 관련

| API                                      | 작업 이름      | 작업 설명                                 |
| ---------------------------------------- | -------- | ------------------------------------ |
| [Abort Multipart Upload](https://cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지   | 멀티파트 업로드 작업 1개 중지 및 업로드된 파트 삭제                 |
| [Complete Multipart Upload](https://cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료  | 전체 파일의 멀티파트 업로드 완료                          |
| [DELETE Multiple Object](https://cloud.tencent.com/document/product/436/8289) | 여러 개의 개체 삭제   | Bucket에서 Object(파일/개체) 배치 삭제        |
| [DELETE Object](https://cloud.tencent.com/document/product/436/7743) | 단일 개체 삭제   | 버킷에서 지정된 객체를 삭제합니다       |
| [GET Object](https://cloud.tencent.com/document/product/436/7753) | 개체 획득     | Object(파일/개체)를 로컬에 다운로드                |
| [GET Object acl](https://cloud.tencent.com/document/product/436/7744) | 개체 ACL 획득 | Object(파일/개체)의 ACL 획득              |
| [HEAD Object](https://cloud.tencent.com/document/product/436/7745) | 개체 메타데이터 획득  | Object의 Meta 정보 획득                  |
| [Initiate Multipart Upload](https://cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화  | Multipart Upload 업로드 작업 초기화            |
| [List Parts](https://cloud.tencent.com/document/product/436/7747) | 업로드된 파트 조회     | 특정 멀티파트 업로드 작업 중 업로드된 파트 조회                    |
| [Options Object](https://cloud.tencent.com/document/product/436/8288) | 사전 요청(Preflight)으로 CORS 구성   | 사전 요청을 이용하여 CORS 요청 발송 가능 여부 확인                    |
|[POST Object](https://cloud.tencent.com/document/product/436/14690) |  표 업로드 개체 | 표 요청을 사용하여 개체 업로드 |
|[POST Object restore](https://cloud.tencent.com/document/product/436/12633) | 보관 개체 복구 | 보관 유형의 개체를 되찾고 접근 |
| [PUT Object](https://cloud.tencent.com/document/product/436/7749) | 개체 업로드     | Object(파일/개체)를 Bucket에 업로드         |
| [PUT Object acl](https://cloud.tencent.com/document/product/436/7748) | 개체 ACL 설정 | Bucket 중 어느 Object (파일/개체)의 ACL 설정             |
| [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881) | 개체 복사 설정     | 파일을 대상 경로에 복사                   |
| [Upload Part](https://cloud.tencent.com/document/product/436/7750) | 파트 업로드     | 파일 멀티파트 업로드                               |
| [Upload Part - Copy](https://cloud.tencent.com/document/product/436/8287) | 멀티파트 복사 |  기타 개체를 하나의 멀티파트로 복사|

