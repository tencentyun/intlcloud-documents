루트 계정의 비디오 라이브 방송 리소스에 액세스할 때 인증 규칙을 준수해야 합니다. 본 문서는 비디오 라이브 방송 API 인증 규칙을 소개합니다.

## 인증 규칙

서브 계정으로 라이브 방송 서비스 API를 통해 루트 계정의 라이브 방송 리소스에 액세스하면, 라이브 방송 서비스 백그라운드는 서브 계정에 대해 권한 검사를 진행하여 리소스 소유자가 관련 리소스 권한을 부여한 게 맞는지 확인합니다. 

모든 라이브 방송 서비스 API는 관련 리소스 및 API 의미에 따라 어떤 리소스의 권한을 검사할지 확인합니다. 구체적인 API 인증 규칙은 다음 표를 참고하십시오. 

## 리소스 권한 부여를 지원하는 API

| 인터페이스 이름                        | 인터페이스 기능                          | 리소스(Resource)                                      |
| ------------------------------- | --------------------------------- | ----------------------------------------------------- |
| DescribeLiveDomainReferer       | 라이브 방송 도메인 Referer 블랙리스트/화이트리스트 쿼리 설정| qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLivePlayAuthKey         | 재생 인증 key 쿼리                  | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLivePushAuthKey         | 푸시 스트림 인증 key 쿼리                  | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ModifyLiveDomainReferer         | 라이브 방송 도메인 Referer 블랙리스트/화이트리스트 설정    | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ModifyLivePlayAuthKey           | 재생 인증 key 수정                  | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ModifyLivePushAuthKey           | 푸시 스트림 인증 key 수정                  | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLiveStreamEventList     | 스트림 중단 이벤트 쿼리                    | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLiveStreamOnlineList    | 라이브 방송 중인 스트림 쿼리                    | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLiveStreamPublishedList | 이전 스트림 리스트 쿼리                    | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLiveStreamState         | 스트림 상태 쿼리                        | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DropLiveStream                  | 라이브 방송 스트림 중지                        | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ForbidLiveStream                | 라이브 방송 푸시 스트림 금지                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ResumeLiveStream                | 라이브 방송 푸시 스트림 복구                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| CreateLiveWatermarkRule         | 워터마크 규칙 생성                     | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DeleteLiveWatermarkRule         | 워터마크 규칙 삭제                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| CreateLiveTranscodeRule         | 트랜스 코딩 규칙 생성                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DeleteLiveTranscodeRule         | 트랜스 코딩 규칙 삭제                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| AddLiveDomain                   | 도메인 추가                          | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DeleteLiveDomain                | 도메인 삭제                          | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLiveDomain              | 도메인 정보 쿼리                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| EnableLiveDomain                | 도메인 활성화                          | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ForbidLiveDomain                | 도메인 비활성화                          | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ModifyLivePlayDomain            | 도메인 재생 정보 수정                  | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| CreateLiveSnapshotRule          | 화면 캡처 규칙 생성                       | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DeleteLiveSnapshotRule          | 화면 캡처 규칙 삭제                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| AddDelayLiveStream              | 딜레이 재생                          | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ResumeDelayLiveStream           | 딜레이 재생 복구                          | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLiveStreamPushInfoList  | 온라인 스트림의 푸시 스트림 데이터 획득              | qcs::${ApiModule}:${Region}:uin/:domain/${PushDomain} |
| DescribeLiveTranscodeDetailInfo | 라이브 방송 트랜스 코딩 통계 정보 쿼리              | qcs::${ApiModule}:${Region}:uin/:domain/${PushDomain} |
| DescribeStreamDayPlayInfoList   | 모든 스트림의 트래픽 데이터 쿼리              | qcs::${ApiModule}:${Region}:uin/:domain/${PlayDomain} |
| DescribeStreamPlayInfoList      | 스트림 재생 정보 리스트 쿼리              | qcs::${ApiModule}:${Region}:uin/:domain/${PlayDomain} |
| CreateLiveCallbackRule          | 콜백 규칙 생성                       | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DeleteLiveCallbackRule          | 콜백 규칙 삭제                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| BindLiveDomainCert              | 도메인 바인딩 인증서                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeLiveDomainCert          | 도메인 인증서 정보 획득                  | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| ModifyLiveDomainCert            | 도메인 및 인증서 바인딩 정보 수정            | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| UnBindLiveDomainCert            | 도메인 인증서 바인딩 해제                     | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| CreateLiveRecordRule            | 녹화 규칙 생성                       | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| CreateRecordTask                | 녹화 작업 생성(New)                | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DeleteLiveRecordRule            | 녹화 규칙 삭제                      | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DeleteRecordTask                | 녹화 작업 삭제(New)                 | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| DescribeRecordTask              | 녹화 작업 리스트 쿼리(New)             | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |
| StopRecordTask                  | 녹화 작업 중지(New)                 | qcs::${ApiModule}:${Region}:uin/:domain/${DomainName} |

