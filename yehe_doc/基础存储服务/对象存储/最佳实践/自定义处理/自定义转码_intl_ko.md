## 개요

정보 전파 트래픽의 가장 큰 부분을 차지하는 멀티미디어는 다양한 업계의 비즈니스에서 매우 중요한 위치를 차지하고 있습니다. 다양한 비즈니스 시나리오에서 멀티미디어 프로세싱 로직은 산업적 특성을 지니고 있습니다. 퍼블릭 클라우드는 사용자에게 많은 비디오 프로세싱 서비스 옵션을 제공하지만, 여전히 사용자의 특수한 프로세싱 및 커스터마이징 니즈를 완전히 커버하지 못하고 있습니다. Serverless Cloud Function(SCF)과 결합된 Cloud Object Storage(COS) 워크플로 프로세싱을 통한 로직 커스터마이징은 사용자가 자신의 요구에 맞는 다양한 멀티미디어 프로세싱 서비스를 빠르게 구축할 수 있는 최선의 선택입니다.

![](https://qcloudimg.tencent-cloud.cn/raw/ba4c5169a249015ca11d190c98b0f9c8.png)

## 응용 시나리오

- 사용자 자체 구축 트랜스 코딩 클러스터에 빠르게 액세스하고, 사용자의 기존 서비스와 호환해야 하는 시나리오.
- 영화업 및 보안업 등 업계 특수 형식 및 프로세스 로직 시나리오.
- 다양한 시나리오의 맞춤형 프로세스 니즈를 충족시키기 위해 사용자 정의 프로세싱 로직 지원.
- 워크플로 템플릿화 프로세싱을 트리거하여 비디오 사이트, 교육 및 소셜 등 멀티미디어 수요가 많은 시나리오 니즈 충족.

## 솔루션 장점

- 개발 가속화: 더 이상 리소스 운영 및 유지 관리 및 구성 요소 오버헤드에 주의를 기울일 필요가 없으므로 서비스 아키텍처 구축의 복잡성이 크게 줄어듭니다.
- 오버헤드 감소: 유휴 상태일 때 리소스가 실행되지 않고 함수가 실행될 때 컴퓨팅 리소스의 요청 수와 실행 시간에 따라 요금이 부과되므로, 비용이 절감됩니다.
- 높은 가용성 및 확장성: 요청에 따라 서비스 리소스를 자동 평행 조정하며, 무제한에 가까운 스케일업 기능을 보유하고 있습니다. 단일 가용존 운영의 장애 리스크를 제거합니다.


## 작업 순서

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하여 워크플로, 사용자 정의 필터링 규칙 및 사용자 정의 함수 노드를 생성합니다.

2. 함수 노드 팝업 창에서 [함수 생성]을 클릭합니다.

3. SCF 생성 페이지에서 [COS 데이터 워크플로 멀티미디어 트랜스 코딩] 템플릿을 선택합니다.

4. 사용자 파일 크기에 따라 기본 설정 항목의 실행 타임 아웃 시간을 설정하고, 고급 설정 항목에서 충분한 메모리를 설정합니다.
5. [고급 설정]>[환경 설정]에서 환경 변수를 설정합니다. 이 기능 템플릿은 다음 환경 변수를 지원합니다.
 - targetBucket: 타깃 버킷. 필수 입력.
 - targetRegion: 타깃 버킷 리전. 필수 입력.
 - targetKeyTemplate: 타깃 경로 템플릿. 선택 입력. 기본값: `${InputPath}${InputName}_transcode.${ext}`.
 - ffmpegTemplate: 트랜스 코딩 명령어 템플릿. 필수 입력. 예시: `${ffmpeg} -loglevel error -i ${source} -r 10 -b:a 32k ${target}`.
 - localTmpPath: 임시 저장 경로. CFS 바인딩 시 임시 경로를 변경할 수 있습니다. 선택 입력. 기본값: `/tmp`.

6. 권한 설정을 활성화하고, 현재 버킷의 읽기 및 쓰기 권한이 포함된 역할을 바인딩합니다. 실행 역할 생성은 [역할 및 정책](https://intl.cloud.tencent.com/document/product/583/38176)을 참고하십시오.

7. [완료]를 클릭합니다.
8. 방금 생성한 워크플로 페이지로 돌아가 방금 생성한 사용자 정의 트랜스 코딩 함수를 선택하고 워크플로를 저장하고 워크플로 목록 페이지에서 워크플로를 실행합니다.

9. 파일을 업로드합니다. 워크플로가 성공적으로 처리되면 업로드된 비디오가 성공적으로 트랜스 코딩되어 새 파일에 저장되었음을 확인할 수 있습니다.



