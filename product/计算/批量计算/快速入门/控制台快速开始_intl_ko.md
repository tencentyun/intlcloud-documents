## 퀵 스타트
이 문서는 Batch Compute 콘솔로 작업을 제출하는 방법을 소개합니다. 구체적인 작업 절차는 다음과 같습니다.
### 준비
[COS](https://intl.cloud.tencent.com/document/product/436) 버킷을 준비하십시오. 아직 버킷을 생성하지 않았다면 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/6232)을 참조하여 생성을 완료하십시오.

### [콘솔]() 로그인
아직 Batch Compute 서비스를 개통하지 않았다면 Batch Compute 콘솔 홈페이지 관련 알림을 참조하여 개통하십시오.

### 태스크 템플릿 생성

1. 왼쪽 탐색 모음 "태스크 템플릿" 옵션을 클릭하여 "광저우"와 같은 대상 지역을 선택하십시오. [생성] 버튼을 클릭하십시오.

2. 기본 정보를 구성합니다.
  * 이름: 예- hello
  * 설명: 예- hello demo
  * 리소스 구성: 기본값
  * 리소스 수량: 예를 들어, 1대
  * 초과 시간: 기본값
  * 다시 시도 횟수: 기본값
  * 이미지: img-m4q71qnf
  
![1](https://main.qcloudimg.com/raw/d41672fb4c479f0b0949255661ed8b37.png)

3. 프로그램 정보 구성
  * 실행 방식: Local
  * Stdout 로그: 형식은 [COS, CFS 경로 입력](https://cloud.tencent.com/document/product/599/13996)을 참조하십시오.
  * Stderr 로그: Stdout 로그와 같음
  * 명령행: echo 'hello, world'
  
![2](https://main.qcloudimg.com/raw/9f35c7e4f23bc24716bf169085aa55de.png)

4. 저장 매핑을 구성한 뒤 [다음] 버튼을 클릭하십시오.

   ![3](https://main.qcloudimg.com/raw/bdcf6c662556c52defa78ef4cb81412a.png)

5. 태스크 JSON 파일을 미리보고, 정확한지 확인 후, [저장] 버튼을 클릭합니다.

  ![4](https://main.qcloudimg.com/raw/13c0833df655ff7ad1d5b7e15dc938dd.png)

6. 태스크 템플릿을 확인하십시오.

  ![5](https://main.qcloudimg.com/raw/a7b5820d223ee50c04a5cd6e2e6b585c.png)

### 작업 제출
1. 왼쪽 탐색 모음 "작업" 옵션을 클릭하여 "광저우"와 같은 대상 지역을 선택하십시오. [생성] 버튼을 클릭하십시오.

2. 작업 기본 정보를 구성합니다.
  * 작업 이름: 예- hello
  * 우선 순위: 기본값
  * 설명: 예- hello job
  
  ![6](https://main.qcloudimg.com/raw/b61d5d12a4afdc0d2292f27ceacbc61b.png)

3. "태스크 흐름" 왼쪽 "hello" 태스크를 선택하고 마우스를 움직여 오른쪽 캔버스에 배치하십시오.

  ![7](https://main.qcloudimg.com/raw/05ebaae417f50aa2fd85057546b5cf69.png)

4. "태스크 흐름" 오른쪽 "태스크 세부 정보"를 열어 구성이 정확한지 확인한 뒤, "완료" 버튼을 클릭하십시오.

![8](https://main.qcloudimg.com/raw/0e446dca39ecc0c520f830ec15faa27d.png)

5. 결과를 확인하십시오. 작업 리스트 페이지에서 작업 실행 상태를 확인할 수 있습니다.

  ![9](https://main.qcloudimg.com/raw/7685866d2fc13f65c13b28d6c0eaf1e6.png)
 - 작업 ID를 클릭하면 "태스크 실행 상황"에서 각 태스크 인스턴스의 실행 상태를 확인할 수 있습니다.
 - "로그 조회" 버튼을 클릭하면 태스크 인스턴스의 표준 출력과 표준 오류를 확인할 수 있습니다.

  ![10](https://main.qcloudimg.com/raw/d55d8e331f3bc2637c5c73dc22ffc6b1.png)

## 다음 단계에서는 무엇을 할 수 있을까요?

이것은 가장 간단한 예이며, 단일 태스크를 가진 작업입니다. 원격 저장 매핑 능력을 사용하지 않고 사용자에게 가장 기본적인 기능만 보여줍니다. 사용자는 콘솔 사용 가이드에 따라 Batch Compute에 대한 고차형 능력을 지속적으로 테스트할 수 있습니다.
- **다양한 CVM 구성**: Batch는 다양한 CVM 구성 항목을 제공하기 때문에 비즈니스 시나리오에 따라 CVM 구성을 사용자 지정할 수 있습니다.
- **원격 코드 패킷 실행**: Batch Compute는 **사용자 지정 이미지 + 원격 코드 패킷 + 명령행** 방식을 제공하기 때문에 기술 측면에서 사용자의 수요를 전면적으로 만족시킬 수 있습니다.
- **원격 저장 매핑**: Batch는 저장소 접근을 최적화하여 원격 저장 서비스 접근을 로컬 파일 시스템 작업으로 간소화합니다.
