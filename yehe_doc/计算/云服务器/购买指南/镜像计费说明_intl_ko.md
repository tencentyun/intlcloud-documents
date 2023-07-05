본문은 CVM 인스턴스 이미지 요금에 대해 설명합니다.

## 과금 개요
이미지 사용 시 일정 요금이 발생할 수 있으며, 이미지 유형별 요금은 다음과 같습니다.
<table class="tg">
<thead>
  <tr>
    <th width="10%">이미지 유형</th>
    <th width="90%">설명</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">공용 이미지</td>
    <td class="tg-0pky">오픈 소스 이미지와 상업용 이미지 포함: <br><li>오픈 소스 이미지를 사용할 때 라이선스 비용을 지불할 필요가 없습니다. </li><li>상업용 이미지를 사용하면 License 비용이 청구됩니다. Tencent Cloud는 현재 Windows Server 이미지와 Red Hat Enterprise Linux 이미지의 두 가지 상용 이미지를 제공합니다. </td></li>
  </tr>
  <tr>
    <td class="tg-0pky">사용자 정의 이미지</td>
    <td class="tg-0pky">두 가지 과금 항목 포함: <br><li>스냅샷 요금: 이미지는 CBS 스냅샷 서비스를 사용합니다. 따라서 사용자 정의 이미지를 유지하면 스냅샷 요금이 발생합니다. 중국 내 리전은 <a href="https://intl.cloud.tencent.com/document/product/362/32415">Free Tier</a> 80GB를 제공하며, 초과분은 용량에 따라 과금됩니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/362/32415">Snapshot Billing Overview</a>를 참고하십시오. </li><li>이미지 요금: 사용자 정의 이미지의 출처가 유료 이미지인 경우 사용 요금이 발생합니다. </li></td>
  </tr>
  <tr>
    <td class="tg-0pky">공유 이미지</td>
    <td class="tg-0pky">공유 이미지는 다른 Tencent Cloud 계정과 공유하는 사용자 정의 이미지입니다. 공유 이미지의 출처가 유료 이미지인 경우 사용 요금이 발생합니다. </td>
  </tr>
</tbody>
</table>

<span id="redhat"></span>

## Windows Server 이미지
#### 과금 예시

예시: 싱가포르 1존, 스탠다드 S5.MEDIUM2 인스턴스, 종량제 과금 방식.
- Windows 인스턴스 요금은 0.05 USD/시간입니다. ‘이미지’는 무료입니다. 다음 이미지 참고:
![](https://qcloudimg.tencent-cloud.cn/raw/af8b0002847ce5f1542a90a1990e27ce.png)


## Red Hat Enterprise Linux 이미지 
Red Hat Enterprise Linux는 상용 OS입니다. Tencent Cloud를 통한 정식 라이선스 이미지(**Tencent Cloud 라이선스**)는 요금에 라이선스 요금이 포함되어 있습니다. 모든 리전에 동일한 가격이 적용됩니다.
<dx-alert infotype="explain" title="">
- Tencent Cloud에서 Red Hat Enterprise Linux 이미지 라이선스 구매 시 할인(스팟 인스턴스에 대한 할인 포함) 및 크레딧은 사용할 수 없습니다.
- Red Hat Enterprise Linux 이미지를 사용하기 위해 Red Hat Enterprise Linux에 대해 인증된 인스턴스 모델을 선택할 수 있습니다. 지원되는 이미지 태그 및 인스턴스 모델은 [FAQs about Red Hat Enterprise Linux Image](https://www.tencentcloud.com/document/product/213/55135)를 참고하십시오.
- Red Hat Enterprise Linux 이미지는 베타 테스트 중입니다. 베타에 참여하려면 [티켓 제출](https://cloud.tencent.com/apply/p/2yj9npvw8lq)하여 신청할 수 있습니다.
</dx-alert>

### 라이선스 Red Hat Enterprise Linux 이미지 가격

| 사양 | 시간당 종량제(최소 과금 단위: 1시간)|
|---------|---------|
| 4 vCPU 이하 | 0.06 USD/시간 |
| 4 vCPU 이상 | 0.13 USD/시간 |

<dx-alert infotype="explain" title="">
**스팟 인스턴스**를 생성할 때 라이선스가 부여된 Red Hat Enterprise Linux 이미지를 선택하면 이미지는 종량제 방식으로 청구되며 **스팟 인스턴스** 할인을 받을 수 없습니다.
</dx-alert>

### OS 재설치 이미지 과금
- Red Hat Enterprise Linux와 다른 인스턴스 간에 인스턴스의 OS를 전환할 수 있습니다. 이 경우 이미지 요금은 새 이미지를 기준으로 계산됩니다. 중국 본토 이외의 리전에서는 Windows OS와 Linux OS 간에 전환할 수 없습니다.
- 종량제 인스턴스의 경우 라이선스가 부여된 Red Hat Enterprise Linux에 OS를 다시 설치하면 종량제 과금 방식으로 이미지가 청구됩니다. 청구 주기 동안 Red Hat Enterprise Linux 이미지를 사용하면 해당 주기에 대한 이미지 라이선스 요금을 지불해야 합니다.
**사례**:
2023년 1월 1일 오전 8:00에 CentOS 인스턴스를 구매하였으며, 오전 8:00～9:00에는 이미지 사용 요금이 발생하지 않았습니다. 오전 9시 30분에 Red Hat Enterprise Linux로 인스턴스 OS를 재설치하여, 오전 9:00～10:00 청구 주기에는 이미지 라이선스 요금이 발생하였습니다. 오전 10:30에 인스턴스 OS를 CentOS로 재설치하여, 오전 10:00～11:00 청구 주기에는 이미지 라이선스 요금이 발생하였습니다. 오전 11:00 이후에는 이미지 라이선스 요금을 지불하지 않아도 됩니다.

### RI 모드 이미지 과금
- Linux 인스턴스에 대해 RI를 선택하면 Red Hat Enterprise Linux 이미지에 대한 라이선스 요금을 별도로 지불해야 합니다.
- Tencent Cloud에서 라이선스가 부여된 Red Hat Enterprise Linux 이미지가 있는 종량제 인스턴스는 인스턴스 구성이 RI와 일치할 때 할인을 받을 수 있습니다. 단, 별도로 청구되는 이미지 라이선스는 할인이 적용되지 않습니다.


### 구성 변경

Red Hat Enterprise Linux OS를 사용하는 인스턴스에 대한 구성 및 과금 방식을 변경할 수 없습니다.



