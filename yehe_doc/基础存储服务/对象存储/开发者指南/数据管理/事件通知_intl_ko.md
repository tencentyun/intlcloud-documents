## 개요

COS 리소스에 변동이 생긴 경우 (예를 들어 새 파일 업로드, 파일 삭제) 곧바로 공지 메세지를 받을 수 있습니다. 이벤트 공지는 [SCF](https://intl.cloud.tencent.com/product/scf)(Serverless Cloud Function)와 결합하여 더욱 많은 응용 시나리오를 만들어 냅니다.

- **제품간 연동**: 새 파일을 COS에 업로드하면 CDN 캐시가 자동으로 새로 고침됩니다. 새 파일을 COS에 업로드하면 자동으로 데이터베이스가 갱신됩니다.
- **시스템 통합**: COS 상의 파일에 변경(새로 만들기, 삭제, 덮어쓰기)이 생긴 경우 자동으로 서비스 인터페이스를 호출합니다. UGC(User Generated Content) 시나리오에서 이벤트 공지 기능을 기반으로 모바일과 서버가 연동됩니다.
- **데이터 프로세스**: COS 파일은 자동으로 프로세스됩니다. 자동 압축 해제, AI 인식 등을 예로 들 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/4a32cb2d7739e6d183cbb94523689e1c.png)

COS 이벤트 공지는 다음과 같은 특징을 가집니다.

- 비동기화 프로세스: 공지 발송은 COS의 정상 작업에 영향을 주지 않습니다.
- 공지 타깃: 리전 내 SCF 함수로의 공지만 발송합니다.

현재 다음 COS 이벤트를 지원합니다.

| 이벤트 유형                                  | 설명                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| cos:ObjectCreated:*                       | 아래 언급한 모든 업로드 이벤트는 SCF를 트리거할 수 있습니다.                         |
| cos:ObjectCreated:Put                     | PUT Object 인터페이스를 사용해 파일을 생성할 때 SCF를 트리거합니다.                     |
| cos:ObjectCreated:Post                    | POST Object 인터페이스를 사용해 파일을 생성할 때 SCF를 트리거합니다.                    |
| cos:ObjectCreated:Copy                    | PUT Object - Copy 인터페이스를 사용해 파일을 생성할 때 SCF를 트리거합니다.              |
| cos:ObjectCreated:CompleteMultipartUpload | Complete Multipart Upload 인터페이스를 사용해 파일을 생성할 때 SCF를 트리거합니다.    |
| cos:ObjectCreated:Origin                  | 이미지 Origin-pull이 발생한 경우 SCF를 트리거합니다.                                    |
| cos:ObjectCreated:Replication             | 리전 간 복제로 객체를 생성할 경우 SCF를 트리거합니다.                           |
| cos:ObjectRemove:*                        | 아래 언급한 모든 삭제 이벤트는 SCF를 트리거할 수 있습니다.                         |
| cos:ObjectRemove:Delete                   | 버전 제어 버킷을 활성화하지 않고 DELETE Object 인터페이스로 객체를 삭제하거나 versionid를 사용해 지정된 버전의 객체를 삭제할 경우 SCF를 트리거합니다. |
| cos:ObjectRemove:DeleteMarkerCreated      | 활성화되어 있거나 잠시 중지된 버전이 제어하는 버킷에서 DELETE Object 인터페이스로 객체를 삭제할 경우 SCF를 트리거 합니다. |
| cos:ObjectRestore:Post                    | 보관 복구 작업이 생성될 때 SCF를 트리거합니다.                             |
| cos:ObjectRestore:Completed               | 보관 복구 작업이 완료되었을 때 SCF를 트리거합니다.                                 |

## COS 이벤트 공지 사용 방법

다음은 COS 이벤트 공지 사용 절차입니다.

1. SCF 함수 생성
   - [SCF 콘솔](https://console.cloud.tencent.com/scf?rid=1)이나 CLI를 통해 함수를 생성할 수 있습니다. 함수 생성을 위해 실행 환경 선택(함수 편집을 할 때 사용할 언어 선택), 함수 코드(온라인 편집이나 로컬 업로드 코드 패키지 지원) 제출이 필요합니다.
   - 미리 설정된 SCF 템플릿으로 생성 절차를 간소화시킬 수 있습니다. 자세한 내용은 [함수 생성](https://intl.cloud.tencent.com/document/product/583/19806)을 참조하십시오. 함수 작성 방법은 프로그래밍 언어에 따라 다릅니다. 자세한 내용은 [SCF](https://intl.cloud.tencent.com/document/product/583) 문서를 참조하십시오.
2. 함수 테스트
   함수 생성 완료 후 테스트 템플릿 기능을 사용해 테스트를 진행할 수 있습니다. 테스트 템플릿은 COS 이벤트를 시뮬레이션하며 함수 실행을 트리거 합니다. 자세한 내용은 [함수 테스트](https://intl.cloud.tencent.com/document/product/583/14572)를 참조하십시오.
3. 트리거 추가
   테스트 완료 후 COS 트리거 생성을 통해 SCF 함수와 버킷을 바인딩할 수 있으며 콘솔이나 명령 라인으로 트리거를 추가할 수 있습니다. 자세한 내용은 [트리거 생성](https://intl.cloud.tencent.com/document/product/583/31441) 문서를 참조하십시오.
4. 실제 인증
   위 절차를 완료한 후 COS 버킷을 조작하여 전체 프로세스가 정상인지 인증할 수 있습니다. 예를 들어 콘솔, COS Browser 등의 툴을 통해 파일을 업로드 및 삭제하며 **[SCF 콘솔](https://console.cloud.tencent.com/scf?rid=1)** > **함수 세부 사항** > **일치하는 함수 명** > **실행 로그** 순서로 정상 작동하는지 인증할 수 있습니다.

SCF COS 트리거에 대한 자세한 내용은 [COS 트리거](https://intl.cloud.tencent.com/document/product/583/9707) 문서를 참조하십시오.
