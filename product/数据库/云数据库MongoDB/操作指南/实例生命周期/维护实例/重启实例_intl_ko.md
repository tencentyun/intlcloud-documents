## 설명 ##
TencentDB for MongoDB의 아키텍처에 따라 인스턴스를 다시 시작하는 과정은 Mongo를 다시 시작하고 MongoDB를 다시 시작하는 부분으로 나뉩니다. 인스턴스를 다시 시작하면 플래시 브레이크가 발생할 수 있습니다. 특히 Mongod가 다시 시작될 때 쓰기 데이터가 있으면, 롤백을 일으켜 데이터 손실을 초래할 수 있습니다. 다시 시작하는 동안 TencentDB for MongoDB 인스턴스는 정상적인 서비스를 제공할 수 없으므로 비즈니스에 미치는 영향을 피하기 위해 미리 준비하십시오. Mongod를 다시 시작하는 것은 화이트리스트에 의해 제어되고 필요한 경우 티켓을 제출하여 당사에 문의하십시오. 다시 시작하는 것은 위험성이 높은 작업이므로 조심해서 수행하십시오.
## 작업 가이드 ##
Tencent Cloud 공식 웹사이트에 로그인하여, [TencentDB for MongoDB 콘솔](https://console.cloud.tencent.com/mongodb)로 이동하여 복제본 세트 또는 샤딩 인스턴스 리스트에 들어갑니다. 다시 시작할 인스턴스를 선택하고 [다시 시작] 버튼을 클릭하면, 작업을 실행합니다. 자세한 내용은 다음 그림을 참조하십시오.
![](https://main.qcloudimg.com/raw/f9970b086c8d84dee900e72e320f2fbf.png)
또 하나는 각 인스턴스에서 [작업] - [추가] - [다시 시작]을 클릭하는 방식입니다. 자세한 내용은 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/712e6bc5b00ede03cccf0855affe0d22.png)
"다시 시작"을 클릭한 후, 팝업창의 내용은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/b6331e32eb64212ceb7fc4bed98ddff7.png)
다시 시작할 구성 요소를 체크하고 확인을 클릭하여 작업 완료를 기다리면 됩니다.
