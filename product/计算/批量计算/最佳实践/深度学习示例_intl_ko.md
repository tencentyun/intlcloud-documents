## 퀵 스타트
이 문서는 scikit-learn 서버 러닝 라이브러리에 기반하여 다층 인식(Multilayer Perceptron, MLP) BP 알고리즘에 대한 심도 있는 예제를 프로그래밍합니다. 역대 국제 축구 경기, 축구팀 랭킹, 축구 선수 스킬 메트릭 및 FIFA 2018 조 경기 결과를 모델링하여 두 팀의 승부 확률을 예측합니다. 구체적인 절차는 다음과 같습니다.
### A. 사용자 지정 이미지 생성
1. 제작 단계는 [사용자 지정 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942) 문서를 참조하십시오.
2. 의존 패킷을 설치합니다. Centos 7.2 64 bit이 예입니다.
```
yum -y install gcc
yum -y install python-devel
yum -y install tkinter
yum -y install python-pip
pip install --upgrade pip
pip install pandas
pip install numpy
pip install matplotlib
pip install seaborn
pip install sklearn
pip install --upgrade python-dateutil
```

### B. 프로그램 패키지 다운로드
[프로그램 압축 패킷 다운로드](https://main.qcloudimg.com/raw/40b6eb7103072ca549e398ca39783f21.gz)를 클릭합니다. 다운로드 완료 후 압축 패킷을 [COS](https://intl.cloud.tencent.com/document/product/436)에 업로드합니다. 지정한 프로그램 패키지의 COS 주소를 통해 Batch는 작업을 실행하기 전에 압축 패킷을 CVM에 다운로드하고 자동 압축 해제 이후 실행합니다.

### C. ‘Fifa-predict’ 태스크 템플릿 생성
1. [Batch Compute 콘솔]()에 로그인하고 왼쪽 탐색 모음 [태스크 템플릿] 옵션을 클릭하여 대상 지역을 선택한 뒤, [생성] 버튼을 클릭합니다.

2. 기본 정보를 구성합니다. 예제는 다음과 같습니다. 

  ![1](https://main.qcloudimg.com/raw/fa5136de41ab24c1a2c964280c71b7b3.png)
  * 이름: fifa-predict;
  * 설명: 데이터 훈련과 예측;
  * 리소스 구성: S2.SMALL1(1코어 1G), 공중망 대역폭은 사용량에 따라 계산합니다.
  * 리소스 수량: 동시 발생 렌더링 수량. 예: 3대, 3개의 신경망 모델 동시 발생 및 훈련합니다
  * 초과 시간: 기본값
  * 다시 시도 횟수: 기본값
  * 이미지: 사용자 지정 이미지 식별자, 예: img-i64lx84h

3. 프로그램 정보 구성 예제는 다음과 같습니다.

   ![2](https://main.qcloudimg.com/raw/d1fc62bb75b2741a9f839f8383e1e6f1.png)
  * 실행 방식: PACKAGE
  * 프로그램 패키지 주소: COS를 예로 들면, `cos://barrygz-1251783334.cosgz.myqcloud.com/fifa/fifa.2018.tar.gz`입니다.
  * Stdout 로그: 형식은 [COS, CFS 경로 입력](https://cloud.tencent.com/document/product/599/13996)을 참조하십시오.
  * Stderr 로그: Stdout 로그와 같음
  * 명령행: `python predict.py "Japan" "Senegal"`

4. 팀 목록: 'Russia', 'Saudi Arabia', 'Egypt', 'Uruguay', 'Portugal', 'Spain', 'Morocco', 'Iran', 'France', 'Australia', 'Peru', 'Denmark', 'Argentina', 'Iceland', 'Croatia', 'Nigeria', 'Brazil', 'Switzerland', 'Costa Rica', 'Serbia', 'Germany', 'Mexico', 'Sweden', 'Korea Republic', 'Belgium', 'Panama', 'Tunisia', 'England', 'Poland', 'Senegal', 'Colombia', 'Japan'

5. 저장 매핑 구성(생략).

6. 태스크 JSON 파일을 미리보고, 정확한지 확인 후, [저장] 버튼을 클릭합니다.

### D. ‘Fifa-merge’ 태스크 템플릿 생성
1. [Batch Compute 콘솔]()에 로그인하고 왼쪽 탐색 모음 [태스크 템플릿] 옵션을 클릭하여 대상 지역을 선택한 뒤, [생성] 버튼을 클릭합니다.

2. 기본 정보를 구성합니다. 예제는 다음과 같습니다.
![3](https://main.qcloudimg.com/raw/2e4ba7fcfc64fc47cc358cce95666b07.png)
  * 이름: fifa-merge;
  * 설명: 예측 데이터 합계;
  * 리소스 구성: S2.SMALL1(1코어 1G), 공중망 대역폭은 사용량에 따라 계산합니다.
  * 리소스 수량: 1대
  * 초과 시간: 기본값
  * 다시 시도 횟수: 기본값
  * 이미지: 사용자 지정 이미지 식별자, 예: img-i64lx84h

3. 프로그램 정보 구성 예제는 다음과 같습니다.
![4](https://main.qcloudimg.com/raw/a8366db12e50a7ec25d1f2222dfe7d89.png)
  * 실행 방식: PACKAGE
  * 프로그램 패키지 주소: COS를 예로 들면, `cos://barrygz-1251783334.cosgz.myqcloud.com/fifa/fifa.2018.tar.gz`입니다.
  * Stdout 로그: 형식은 [COS, CFS 경로 입력](https://intl.cloud.tencent.com/document/product/599/13996)을 참조하십시오.
  * Stderr 로그: Stdout 로그와 같음
  * 명령행: `python merge.py /data`

4. 저장 매핑 구성
![5](https://main.qcloudimg.com/raw/f9b75b95a370393766b000de3776c57e.png)
 - 경로 매핑 입력 > COS/CFS 경로: ‘fifa-predict’ 템플릿과 Stdout 로그 경로를 입력합니다.
 - 경로 매핑 입력 > 로컬 경로: /data.

5. 태스크 JSON 파일을 미리보고, 정확한지 확인 후, [저장] 버튼을 클릭합니다.

### E. 작업 제출
1. 왼쪽 탐색 모음 [작업] 옵션을 클릭하고 대상 지역을 선택한 뒤 [생성] 버튼을 클릭합니다.

2. 작업 기본 정보를 구성합니다. 예제는 다음과 같습니다.
  * 작업 이름: fifa;
  * 우선 순위: 기본값
  * 설명: fifa 2018 model.

3. 태스크 페이지 왼쪽 **fifa-predict**과 **fifa-merge** 태스크를 선택하고 마우스를 움직여 오른쪽 캔버스에 배치하십시오. **fifa-predict** 태스크를 클릭하고 화살표를 **fifa-merge** 태스크로 드래그합니다.
![6](https://main.qcloudimg.com/raw/af22a759548c860ce22bcb397898bbce.png)

4. 작업 흐름 오른쪽 **태스크 세부 정보**를 열어 구성이 확실한지 확인한 뒤, [완료] 버튼을 클릭합니다.

5. 작업 실행 정보 조회, [정보 조회]()를 참조하십시오.
![7](https://main.qcloudimg.com/raw/aec564df4954661c4a732c30bb7d9c2f.png)
 
6. 렌더링 결과 조회, [대상 정보 조회]()를 참조하십시오.
![8](https://main.qcloudimg.com/raw/2f545a92cb2518ffe75dbfa04e1ea532.png)

## 다음 단계에서는 무엇을 할 수 있을까요?
이 문서에는 쉬운 장치 러닝 사례를 나열하고.기본적인 기능만 보여줍니다. 사용자는 콘솔 사용 가이드에 따라 Batch Compute에 대한 고차형 능력을 지속적으로 테스트할 수 있습니다.
- **다양한 CVM 구성**: Batch는 다양한 CVM 구성 항목을 제공하기 때문에 비즈니스 시나리오에 따라 CVM 구성을 사용자 지정할 수 있습니다.
- **원격 저장 매핑**: Batch는 저장소 접근을 최적화하여 원격 저장 서비스 접근을 로컬 파일 시스템 작업으로 간소화합니다.
- **여러 개의 모델 동시 발생 및 훈련**: Batch는 동시 발생 수를 지정할 수 있으며 [환경 변수](https://intl.cloud.tencent.com/document/product/599/11752)를 통해 다른 동시 발생 인스턴스를 구분할 수 있습니다. 모든 인스턴스는 다른 훈련 데이터를 읽어 병행 모델링을 실현합니다.

