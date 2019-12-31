## Outbound 대역폭 최댓값(업스트림 대역폭)

우리가 설치한 공용 네트워크 대역폭 최댓값은 Outbound 대역폭 최댓값 즉 CVM 에서 유출되는 대역폭을 의미합니다. 공용 네트워크의 대역폭 최댓값은 다양한 네트워크 청구 모드에 따라 다릅니다. 자세한 정보는 다음과 같습니다.
- 2019년 5월 31일 이전, 다음과 같은 규칙을 따라 실행하십시오.
<table>
<tr><th rowspan="2">네트워크 청구 모드</th><th colspan="2">인스턴스</th><th rowspan="2">대역폭 최댓값 설정 범위(Mbps)</th></tr>
<tr><th>인스턴스 청구 모드</th><th>인스턴스 구성</th></tr>
<tr><td>트래픽 과금</td><td>종량제 인스턴스</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>대역폭 과금</td><td>종량제 인스턴스</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>공유 대역폭</td><td colspan="2">ALL</td><td>0 - 200 또는 속도 제한 없음</td></tr>
</table>

- 2019년 5월 31일 이후, 다음과 같은 규칙을 따라 실행하십시오.
<table>
<tr><th rowspan="2">네트워크 청구 모드</th><th colspan="2">인스턴스</th><th rowspan="2">대역폭 최댓값 설정 범위(Mbps)</th></tr>
<tr><th style="width: 18.5607%;">인스턴스 청구 모드</th><th style="width: 24.5814%;">인스턴스 구성</th></tr>
<tr><td>트래픽 과금</td><td>종량제 인스턴스</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>대역폭 과금</td><td>종량제 인스턴스</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>공유 대역폭</td><td colspan="2">ALL</td><td>0 - 200 또는 속도 제한 없음</td></tr>
</table>


## Inbound 대역폭 최댓값(다운스트림 대역폭)

공용 네트워크의 Inbound 대역폭은 CVM 인스턴스에 유입되는 대역폭을 의미합니다.
- 사용자가 구매한 고정 대역폭이 10Mbps 이상인 경우 Tencent Cloud는 구매한 대역폭과 동일한 공용 네트워크 대역폭을 할당합니다. 
- 사용자가 구매한 고정 대역폭이 10Mbps 미만인 경우 Tencent Cloud는 10Mbps 공용 네트워크 대역폭을 할당합니다. 

## 대역폭 최댓값 올리기

실제 수요에 따라 다양한 조정 방식을 선택하십시오.
- [인스턴스의 청구 모드 조정](#AdjustInstanceMode)
- [네트워크의 청구 모드 조정(대역폭 과금)](#AdjustNetworkModeByBandwidth)
- [네트워크의 청구 모드 조정(대역폭 패키지 과금)](#AdjustNetworkModeByBandwidthPackage)

인스턴스 및 네트워크의 청구 모드를 조정할 수 없는 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM&step=1) 을 통해 대역폭 최댓값을 올릴 수 있습니다. 확인 후 빠르게 연락하겠습니다.

<span id="AdjustInstanceMode"></span>
### 인스턴스의 청구 모드 조정

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index) 에 로그인하십시오.
2. 대역폭 조정이 필요한 인스턴스를 찾고 오른쪽의[MORE]>[리소스 조정]>[네트워크 조정]을 클릭하십시오.
3. 팝업된 “네트워크 조정” 창에서 목표 대역폭 최댓값을 조정하고[확인]을 클릭하면 됩니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/853916b57df665bc5e1ee1e322ff0d92.png)

<span id="AdjustNetworkModeByBandwidth"></span>
### 네트워크의 청구 모드 조정(대역폭 과금)

1. 트래픽 과금 인스턴스를 대역폭 과금으로 조정합니다. 작업에 대한 자세한 내용은 [네트워크 구성 조정](https://intl.cloud.tencent.com/document/product/213/15517) 을 참조하십시오.
2. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index) 에 로그인하십시오.
3. 대역폭 조정이 필요한 인스턴스를 찾고 오른쪽의[MORE]>[리소스 조정]>[네트워크 조정]을 클릭하십시오.
4. 팝업된 “네트워크 조정” 창에서 목표 대역폭 최댓값을 조정하고[확인]을 클릭하면 됩니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/9371e74fc8a2816390a872fcbb46e4fa.png)

<span id="AdjustNetworkModeByBandwidthPackage"></span>
### 네트워크의 청구 모드 조정(대역폭 패키지 과금)

1. 트래픽 과금 인스턴스를 대역폭 패키지 과금으로 조정합니다.
> 대역폭 패키지의 인스턴스는 대역폭을 최댓값 없음으로 조정합니다. [대역폭 패키지 신청](https://cloud.tencent.com/act/apply/bwp_apply) 을 클릭하십시오.
>
2. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index) 에 로그인하십시오.
3. 대역폭 조정이 필요한 인스턴스를 찾고 오른쪽의[MORE]>[리소스 조정]>[네트워크 조정]을 클릭하십시오.
4. 팝업 창에서 네트워크 및 목표 대역폭을 조정하고[확인]을 클릭하면 됩니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/b05d6c586d2d21b75d83df8d71fe3873.png) 

