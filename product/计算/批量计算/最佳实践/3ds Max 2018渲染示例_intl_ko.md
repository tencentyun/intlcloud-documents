## 퀵 스타트
이 문서는 Batch Compute 콘솔로 작업을 제출하여 3ds Max 2018 이미지 렌더링을 완료하고 렌더링 이미지를 내보내는 방법을 소개합니다. 구체적인 절차는 다음과 같습니다.
### A. 사용자 지정 이미지 생성
1. 사용자 지정 Windows 이미지를 생성합니다.
2. 3ds Max 2018 설치 프로세스는 [공식 홈페이지](https://www.autodesk.com/products/3ds-max/overview)를 참조하십시오.

>주의:
- 소프트웨어 다운로드 중단을 막기 위해, 잠시 Windows 방화벽을 끄십시오.
- 그래픽 카드 초기화에 실패하지 않도록 [그래픽 카드 모델 선택 가이드](https://knowledge.autodesk.com/zh-hans/support/3ds-max/learn-explore/caas/CloudHelp/cloudhelp/2015/CHS/3DSMax/files/GUID-3D6B4C8E-8C0D-4A9C-BFB0-2463803268CE-htm.html)를 참조하여 적합한 유형을 선택합니다. 특별한 이유가 없는 경우, “Nitrous Software”를 선택하길 권장합니다.

### B. 렌더링 파일 준비
렌더링 소재의 주류 저장 방식은 [COS](https://intl.cloud.tencent.com/document/product/436)과 [파일 저장](https://intl.cloud.tencent.com/document/product/582)이 있습니다. 탑재 매개변수를 구성하여 Batch는 렌더링 작업 실행 전 개체 저장 또는 파일 저장을 로컬에 탑재합니다. 렌더러는 로컬 파일에 접근하듯이 개체 저장 또는 파일 저장에 접근할 수 있습니다.

- 렌더링 소재가 작을 경우, 전체 소재를 gzip 패킷으로 압축하여 COS에 업로드하길 권장합니다. [개체 업로드](https://intl.cloud.tencent.com/document/product/436/6233)를 참조할 수 있습니다.
- 렌더링 소재가 클 경우, 파일 저장에 저장하길 권장합니다.

### C. 태스크 템플릿 생성
1. [Batch Compute 콘솔]()에 로그인하고 왼쪽 탐색 모음 [태스크 템플릿] 옵션을 클릭하여 대상 지역을 선택한 뒤, [생성] 버튼을 클릭합니다.

2. 기본 정보를 구성합니다. 예제는 다음과 같습니다.

![1](https://main.qcloudimg.com/raw/2d1fc5db083681fb89227c4477059b0a.png)

   - 이름: rendering
   - 설명: 3ds Max 2018 Demo
   - 리소스 구성: S1.LARGE8(4코어 8G)
   - 리소스 수량: 동시 발생 렌더링 수, 예: 1대
   - 초과 시간: 기본값
   - 다시 시도 횟수: 기본값
   - 이미지: 사용자 지정 이미지 식별자, 예: img-i64lx84h


3. 프로그램 정보 구성 예제는 다음과 같습니다.

   ![2](https://main.qcloudimg.com/raw/54a957780f1aab9a9c5377a0909997d4.png)

  - 실행 방식: PACKAGE
  - 프로그램 패키지 주소: COS로 예롤 들면, `cos://barrygz-1251783334.cos.ap-guangzhou.myqcloud.com/render/max.tar.gz`
  - Stdout로그: 형식은 [COS, CFS 경로 입력](https://cloud.tencent.com/document/product/599/13996)을 참조하십시오.
  - Stderr 로그: Stdout 로그와 같음
  - 명령행: `3dsmaxcmd Demo.max -outputName:c:\\render\\image.jpg`

4. 저장 매핑 구성
![3](https://main.qcloudimg.com/raw/72ae500ef3427774e6dcae08eed55e46.png)

  * 출력 경로 매핑 - 로컬 경로: `C:\\render\\`
  * 출력 경로 매핑 - COS CFS 경로: 형식은 [COS, CFS 경로 입력](https://cloud.tencent.com/document/product/599/13996)을 참조하십시오.

5. 태스크 JSON 파일을 미리보고, 정확한지 확인 후, [저장] 버튼을 클릭합니다.

### D. 작업 제출
1. 왼쪽 탐색 모음 [작업] 옵션을 클릭하고 대상 지역을 선택한 뒤 [생성] 버튼을 클릭합니다.

2. 작업 기본 정보를 구성합니다. 예제는 다음과 같습니다.

   ![4](https://main.qcloudimg.com/raw/3092bd4e78b584afa1fc635255594456.png)
  
  - 작업 이름: max
  - 우선 순위: 기본값
  - 설명: 3ds Max 2018 Demo

3. 작업 흐름 페이지 왼쪽 **rendering** 작업을 선택하고 마우스를 움직여 오른쪽 캔버스에 배치하십시오.

4. 작업 흐름 오른쪽 **태스크 세부 정보**를 열어 구성이 확실한지 확인한 뒤, [완료] 버튼을 클릭합니다.
![5](https://main.qcloudimg.com/raw/a1c1c8c70978b41081713fe3559f9d56.png)

5. 작업 실행 정보 조회, [정보 조회](https://cloud.tencent.com/document/product/599/14567)를 참조하십시오.

6. 렌더링 과정이 프리젠테이션됩니다.
![6](https://main.qcloudimg.com/raw/50b13ce08378e4a8fca7d8ac064ebf0b.png)

7. 렌더링 결과 조회, [개체 정보 조회](https://cloud.tencent.com/document/product/436/13326)를 참조하십시오.
![7](https://main.qcloudimg.com/raw/c85df5470620cac4bdd2c118da7dab36.png)

## 다음 단계에서는 무엇을 할 수 있을까요?
이 문서에는 단일 인스턴스 작업인 쉬운 렌더링 인스턴스를 나열하고.기본적인 기능만 보여줍니다. 사용자는 콘솔 사용 가이드에 따라 Batch Compute에 대한 고차형 능력을 지속적으로 테스트할 수 있습니다.
- **다양한 CVM 구성**: Batch는 다양한 CVM 구성 항목을 제공하기 때문에 비즈니스 시나리오에 따라 CVM 구성을 사용자 지정할 수 있습니다.
- **원격 저장 매핑**: Batch는 저장소 접근을 최적화하여 원격 저장 서비스 접근을 로컬 파일 시스템 작업으로 간소화합니다.
- **여러 장 이미지 동시 렌더링**: Batch는 렌더링 수를 지정 및 동시 발생을 지원하기 때문에 [환경 변수](https://intl.cloud.tencent.com/document/product/599/11752)를 통해 다른 렌더링 인스턴스를 구분하며 모든 렌더링 인스턴스는 다른 렌더링 소개를 읽어 동시 렌더링을 실현합니다.

