지연된 재생 기능은 StreamLive가 실시간으로 입력을 수집하기를 원하지만 콘텐츠를 처리하거나 즉시 출력을 생성하지 않으려는 경우에 유용합니다. 지연된 재생을 사용하면 Input을 트랜스코딩하고 Output용으로 패키징하기 전에 지정된 기간 동안 입력을 Hold할 수 있습니다. 현재 이 기능은 RTMP_PUSH 입력에 대해서만 작동합니다. Delay 재생을 구성하려면 아래 단계를 따르십시오.
1. 지연 재생을 구성하려는 **Input**을 클릭합니다. Input이 현재 실행 중인 채널에 바인딩된 경우 먼저 Stop Channel해야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9b45272668f6d18330fc932df4c9a4d0.png)
2. **Edit**를 클릭하고 **Delay** 시간을 켜고 지연 시간(10 - 600초)을 지정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/65f41a79185c43c1a3c7ab76bd192f53.png)

**Confirm**을 클릭합니다. 이제 즉시 Output을 생성하는 대신 지정된 지연 시간 후에만 Input이 처리됩니다.

