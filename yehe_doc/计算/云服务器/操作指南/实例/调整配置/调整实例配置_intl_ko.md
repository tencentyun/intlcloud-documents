## 작업 시나리오

Tencent Cloud 인스턴스의 하드웨어 디바이스는 빠르고 편리하게 조정할 수 있으며, 이는 CVM의 효율성을 나타내는 중요한 지표입니다. 본 문서는 설정 업그레이드, 설정 다운그레이드, 모델 간의 설정 변경 등에 대한 작업 방법 및 관련된 주의 사항을 소개합니다.

## 전제 조건

인스턴스가 종료 상태 및 시작 상태에서 설정 변경 작업을 진행할 수 있습니다. 시작 상태의 인스턴스는 강제 종료 또는 재시작 후 작업 결과가 적용됩니다.
<dx-alert infotype="notice" title="">
- 작업 인스턴스가 **종료** 상태인 경우 콘솔을 직접 변경할 수 있습니다.
- 작업 인스턴스가 **시작** 상태인 경우 온라인으로 설정을 변경할 수 있으며, 작업 완료 후 강제 종료 및 재시작하여 설정 변경이 적용되었는지 확인해야 합니다.
- 온라인에서 **일괄 작업** 변경을 진행할 수 있습니다. 일괄 작업 머신 중 **시작** 상태의 머신이 있을 경우에도 사용자는 강제 종료 또는 재시작 후 작업이 적용되었는지 확인해야 합니다.
</dx-alert>




## 제한 및 영향

### 설정 변경 제한

**시스템 디스크와 데이터 디스크가 CBS**인 인스턴스만 설정 변경을 지원합니다.
- 설정 업그레이드
  횟수에 제한 없이 설정을 즉시 업그레이드합니다.
- 설정 다운그레이드
 - 종량제 인스턴스는 언제든지 설정 다운그레이드를 진행할 수 있으며, 다운그레이드 횟수는 무제한입니다.
- 인스턴스 패밀리 간의 변경: 서로 다른 인스턴스 패밀리는 상호 설정 변경이 가능하여 데이터 마이그레이션 문제를 해결합니다.
  설정 변경 작업 시, 설정을 변경할 인스턴스의 사양은 현재 가용존이 타깃 사양을 제공하는지 여부와 관련이 있으므로 다음 제한 사항을 주의하십시오.
 - **스팟 인스턴스**는 모델 간의 설정 변경을 지원하지 않습니다.
 - **전용 인스턴스**는 모델 간의 설정 변경을 지원하지 않으며, 설정 변경 범위는 인스턴스가 있는 CDH의 남은 리소스 수량에 의해 제한됩니다.
 - **GPU, FPGA 등의 이종 인스턴스**는 인스턴스 패밀리 간의 설정 변경을 위한 소스 인스턴스의 사양과 타깃 인스턴스의 사양을 지원하지 않습니다.
 - **기본 네트워크 인스턴스의 설정**은 조정을 지원하지 않으며, VPC 인스턴스의 조정만 지원합니다.
 - 타깃 인스턴스 사양이 현재 사양에 설정된 CBS 유형을 지원하지 않을 경우 변경 지원하지 않습니다.
 - 타깃 인스턴스 사양이 현재 사양에 설정된 이미지 유형을 지원하지 않을 경우 변경을 지원하지 않습니다.
 - 타깃 인스턴스 사양이 현재 사양에 설정된 ENI 또는 수량을 지원하지 않을 경우 조정을 지원하지 않습니다. 자세한 내용은 [탄력적 네트워크 사용 제한](https://intl.cloud.tencent.com/document/product/576/18527)을 참고하십시오.
 - 타깃 인스턴스 사양이 현재 사양의 외부 네트워크 대역폭 최댓값을 지원하지 않을 경우 변경을 지원하지 않습니다. 자세한 내용은 [공용 네트워크 대역폭 최댓값](https://intl.cloud.tencent.com/document/product/213/12523)을 참고하십시오.

###  관련 영향

조정 후 극소수의 인스턴스만 개인 IP가 변경됩니다. 개인 IP가 변경됐을 경우 변경 페이지에 안내 문구를 표시하며, 관련 표시가 없으면 개인 IP가 변경되지 않았음을 나타냅니다.

##  작업 순서


<dx-alert infotype="explain" title="">
- 서비스에 변경 발생 시, 설정 변경을 통해 구현할 수 있습니다.
- 설정 업그레이드 시, 업그레이드로 인해 발생한 요금을 지불하십시오.
- 설정 다운그레이드 시, 요금 환불 관련 세부 정보를 확인하십시오. 강제 종료 및 재시작 후 새로운 설정이 적용되며, CVM는 새로운 설정으로 즉시 실행됩니다.
</dx-alert>




<dx-tabs>
::: 콘솔을 통한 변경
#### 단일 변경

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인한 뒤 CVM 페이지로 이동합니다.
2. 실제 사용된 뷰 모드에 따라 작업을 진행합니다.
   - **리스트 뷰**: 변경할 인스턴스의 오른쪽 작업 열에서 **더보기** > **리소스 변경** > **설정 변경**을 선택합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/f92499c75d28291b6248ae0963aa2d00.png)
   - **탭 모드**: 아래 이미지와 같이 변경할 인스턴스의 페이지 오른쪽 상단의 **더보기** > **리소스 변경** > **설정 변경**을 선택합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/2589614a237cecfee9c14c78b0c0f5a4.png) 
3. 아래 이미지와 같이, '타깃 설정 선택'에서 인스턴스 상태 및 작업을 확인한 뒤, **필요한 모델 및 인스턴스 사양을 선택하고 사양 및 성능 매개변수를 자세히 확인합니다.** 확인이 끝나면 **다음**을 클릭합니다.
    ![](https://main.qcloudimg.com/raw/818fbf0dfa791ad5d5a76186eefba019.png)
4. 인스턴스의 과금 방식에 따라 요금을 확인한 뒤 **다음 단계**를 클릭합니다.
	- **사용량 과금 인스턴스**: 아래 이미지와 같이 새로운 사양 적용 시 동결해야 하는 금액을 확인합니다. 설정 변경 후, 종량제 요금이 첫 단계부터 적용되므로 관련 규칙을 자세히 확인한 뒤 작업을 진행하십시오.
	  ![](https://main.qcloudimg.com/raw/25f8630836acdfe274357142d8609c5d.png)
5. 인스턴스 실행 상태에 따라 '종료 알림' 안내 문구가 다르므로, 주의하여 읽어주시기 바랍니다.
 - 인스턴스가 실행 중일 경우, 아래 이미지와 같이 안내 문구를 확인한 뒤 '강제 종료에 동의'를 선택합니다.
![](https://main.qcloudimg.com/raw/e016f2cc674938acd0046115f007669b.png)
 - 인스턴스가 종료 상태일 경우, 아래 이미지와 같이 안내 문구가 다시 나타납니다.
![](https://main.qcloudimg.com/raw/8385495393237523d0d71460a7b7009b.png)
6. **변경 시작**을 클릭하여 주문 페이지로 이동한 뒤, 결제를 완료합니다. 
:::
::: \sAPI를 통한 변경 
ResetInstancesType 인터페이스를 사용하여 인스턴스 설정을 변경할 수 있습니다. 자세한 내용은 [인스턴스 설정 변경](https://intl.cloud.tencent.com/document/product/213/33239)의 API 문서를 참고하십시오.
:::
</dx-tabs>
