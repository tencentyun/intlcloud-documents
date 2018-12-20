
Aegis Anti-DDoS는 HTTP CC 고급 방어 전략을 제공합니다. CC 방어 전략은 HTTP 설정 요청 수가 설정한 QPS 값을 초과할 때 CC 방어를 트리거합니다. 더 자세한 구성 설명은 [**사용자 지정 고급 보안 전략**](https://cloud.tencent.com/document/product/685/18800#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AE.89.E5.85.A8.E7.AD.96.E7.95.A5)을 참조하십시오.

## CC 방어 전략 추가
1. 사용자는 [Aegis 고도 방어 콘솔](https://console.cloud.tencent.com/gamesec)에 진입하여 좌측 리스트에서 [HTTP CC 방어 고급 전략]을 클릭하고 “HTTP CC 방어 고급 전략”에서 [신규 전략 추가]를 클릭합니다. 추가되면 “작업” 줄에서 [구성]을 클릭하여 전략 구성 페이지에 들어갑니다.
![1](https://i.imgur.com/yDiQsHG.png)
2. 비즈니스 특성과 방어 수요에 따라 HTTP QPS 요청 임계값, URL 화이트리스트, IP 블랙리스트/화이트리스트, CC 사용자 지정 방어 모드 등 전략을 구성합니다. 저장을 클릭하면 전략 추가에 성공합니다.
![2](https://i.imgur.com/mfY0Xyt.png)

## CC 방어 전략으로 방어 IP 직접 바인딩
1. [HTTP CC 방어 고급 전략]을 클릭하고 "HTTP CC 방어 고급 전략" 에서 "전략 ID"를 클릭합니다.
![3](https://i.imgur.com/VYBlSMr.png)
2. [IP 리스트 바인딩]을 클릭하고 [IP 추가]를 클릭합니다.
![4](https://i.imgur.com/Nj10vJm.png)

## DDoS 고도 방어 IP로 CC 방어 전략 바인딩
1. [DDoS 고도 방어 IP]를 클릭하여 "DDoS 고도 방어 IP"에서 "고도 방어 IP"를 선택하여 "DDoS 고도 방어 IP" 세부 정보 페이지에 들어갑니다.
![5](https://i.imgur.com/pAeeKuk.png)
2. "고급 구성 정보"를 클릭합니다. [바인딩]을 클릭하여 CC 방어 전략을 선택하고 [확인]을 클릭합니다.
![6](https://i.imgur.com/i37QogR.png)

## DDoS 고도 방어 패키지의 방어 IP를 위해 CC 방어 전략 구성
1. [DDoS 고도 방어 패키지]를 클릭하여, "DDoS 고도 방어 패키지" 에서 "고도 방어 패키지 ID"를 선택하여 "DDoS 고도 방어 패키지" 세부 정보 페이지에 들어갑니다.
![7](https://i.imgur.com/ME4OtML.png)
2. [방어 IP 리스트]를 클릭하여 구성해야 할 IP를 선택하고 “CC 방어 전략 구성”을 클릭합니다.
![8](https://i.imgur.com/E9k6P1r.png)

