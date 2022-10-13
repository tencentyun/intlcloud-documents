StreamLive는 HLS&DASH 스트림에 대한 타임 시프트를 지원합니다. 이 기능은 CSS와 함께 사용해야 합니다.

타임 시프트를 구성하려면 아래 단계를 따르십시오.
1. CSS를 활성화합니다. 재생 도메인으로 CSS 콘솔로 시간 이동을 활성화하려는 도메인을 추가하고 CNAME 레코드를 추가합니다.
2. StreamLive의 타임 시프트 기능을 활성화하려면 티켓을 제출하십시오. 타임 시프트를 활성화하려는 계정의 APPID와 도메인 이름을 제공해야 합니다.
3. 계정에 대해 타임 시프트가 활성화된 후 출력 그룹 설정 페이지의 **TimeShift Information** 영역에서 **Switch**를 켜고 **PlayDomain**에 도메인 이름을 입력하고 **Startover Window**(초)를 지정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/661fcb79490e1de61a10b5d7ab90f494.png)

타임 시프트된 재생 URL의 형식은 다음과 같습니다.
- HLS: http://${play domain}/live/${region}_${Channel Id}-${p0 or p1}_${outputGroupName}/timeshift.m3u8?txMaster=1&delay={$delay}"
- DASH: http://${play domain}/live/${region}_${Channel Id}-${p0 or p1}_${outputGroupName}/timeshift.mpd?delay={$delay}"

>?
>- ${region}은 StreamLive Channel의 리전입니다. 유효한 값은 Bangkok -> ap-bangkok; Mumbai -> ap-mumbai; Seoul->ap-seoul; Tokyo->ap-tokyo; Frankfurt->eu-frankfurt입니다.
>- ${delay}는 재생 시작 시간과 현재 시간 사이의 시간입니다. 180초보다 작거나 Startover Window보다 클 수 없습니다.



예시:
- HLS: http://timeshift.domain.com/ap-bangkok_623ED795CD8247EDA2E1-p0_outputGroupName//timeshift.m3u8?txMaster=1&delay=180
- DASH: http://timeshift.domain.com/ap-bangkok_623ED795CD8247EDA2E1-p0_outputGroupName//timeshift.mpd?delay=180

