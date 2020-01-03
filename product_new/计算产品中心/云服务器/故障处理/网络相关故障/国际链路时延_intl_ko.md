## 문제 설명
북미 리전 클라우드 서버 로그인 지연 시간이 너무 깁니다.

## 문제 분석
전국의 국제 라우팅 엑시트가 적고 그 외 다른 이유로 인하여 동시 발생 횟수가 많을 때, 국제 링크가 꽉 차서 액세스가 불안정하게 됩니다. Tencent Cloud는 이 상황을 ISP에 피드백했습니다.
현재, 북미 리전 클라우드 서버를 구매했을 경우, 국내에서 관리 OPS 진행이 필요하며, 홍콩 리전에서 구매한 클라우드 서버를 사용하여 귀하가 구매한 북미 리전 클라우드 서버에 중계하여 로그인함으로써 이 문제를 해결할 수 있습니다.

## 해결 솔루션
1. 홍콩 리전의 Windows 클라우드 서버를 구매하여 “점프 서버”로 사용하십시오.
> 
> - “사용자 정의 구성” 페이지의 “1. 리전 및 모델 선택”에서 [홍콩] 리전을 선택하십시오.
> [여기를 클릭하여 구매 진행 >>](https://buy.cloud.tencent.com/cvm?tab=custom&step=1&regionId=5&zoneId=0&instanceType=S2ne.SMALL2&platform=CentOS&systemDiskType=CLOUD_PREMIUM&systemDiskSize=50&bandwidthType=BANDWIDTH_PREPAID&loginSet=SET_PASSWORD)
> - Windows 클라우드 서버는 북미 리전의 Windows 및 Linux 클라우드 서버에 로그인을 지원하며 구매를 추천합니다.
> - **홍콩 리전의 Windows 클라우드 서버를 구매할 경우, 최소 1Mbps의 대역폭을 구매해야 하며, 그렇지 않으면 점프 서버 로그인이 불가능합니다.** 
>
2. 구매 완료 후, 필요에 따라 중국 리전 Windows 클라우드 서버 로그인 방식을 선택하십시오:
 - [RDP 파일로 Windows 클라우드 서버에 로그인](https://intl.intl.cloud.tencent.com/document/product/213/5435)
 - [원격 데스크톱 연결로 Windows 클라우드 서버에 로그인](https://cloud.tencent.com/document/product/213/35703)
 - [VNC로 Windows 클라우드 서버에 로그인](https://cloud.tencent.com/document/product/213/35704)
3. 홍콩 리전의 Windows 클라우드 서버 내에서 필요에 따라 북미 리전 클라우드 서버 로그인 방식을 선택하십시오.
 - 북미 리전의 Linux 클라우드 서버 로그인하기
    - [표준 로그인 방식으로 Linux 클라우드 서버에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)
    - [원격 로그인 소프트웨어로  Linux 클라우드 서버에 로그인](https://cloud.tencent.com/document/product/213/35699)
    - [VNC로 Linux 클라우드 서버에 로그인](https://cloud.tencent.com/document/product/213/35701)
 - 북미 리전의 Windows 클라우드 서버에 로그인하기 
    - [RDP 파일로 Windows 클라우드 서버에 로그인](https://intl.intl.cloud.tencent.com/document/product/213/5435)
    - [원격 데스크톱 연결로 Windows 클라우드 서버에 로그인](https://cloud.tencent.com/document/product/213/35703)
    - [VNC로 Windows 클라우드 서버에 로그인](https://cloud.tencent.com/document/product/213/35704)
