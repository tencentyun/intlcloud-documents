
CBS의 성능은 보통 CBS 용량에 따라 달라지므로, CBS의 성능이 최대치에 도달하지 못한 경우 용량 조정을 통해 성능을 개선할 수 있습니다. 확장형 SSD CBS는 기본 성능의 최대치에 도달하면 추가 성능 설정으로 기본 성능보다 향상된 성능 구현이 가능합니다. 조건에 부합할 경우 필요에 따라 추가 성능을 설정하고 언제든지 조정할 수 있습니다. 자세한 내용은 [확장형 SSD CBS 성능 설명](https://intl.cloud.tencent.com/document/product/362/39611)을 참조하십시오.
>!
>- 현재 **확장형 SSD CBS**만 성능의 단독 조정을 지원합니다.
>- [기본 성능](https://intl.cloud.tencent.com/document/product/362/39611#.E5.A2.9E.E5.BC.BA.E5.9E.8B-ssd-.E4.BA.91.E7.A1.AC.E7.9B.98.E5.9F.BA.E5.87.86.E6.80.A7.E8.83.BD)이 최대치에 도달해야 [추가 성능](https://intl.cloud.tencent.com/document/product/362/39611#.E5.A2.9E.E5.BC.BA.E5.9E.8B-ssd-.E4.BA.91.E7.A1.AC.E7.9B.98.E9.A2.9D.E5.A4.96.E6.80.A7.E8.83.BD) 단독 조정이 가능합니다.
>- CBS 성능 조정 중에도 비즈니스를 수행하고 원활하게 사용할 수 있습니다.








## CBS 성능 조정 요금 설명

### 성능 업그레이드

- 종량제 CBS: 사용 즉시 과금이 시작되며 신규 설정 가격으로 요금이 부과됩니다.

### 성능 다운그레이드


- 종량제 CBS: 사용 즉시 과금이 시작되며 신규 설정 가격으로 요금이 부과됩니다.

## 성능 업그레이드

#### 콘솔을 통한 성능 업그레이드
전제 조건 충족 시 다음과 같은 방식으로 성능을 업그레이드할 수 있습니다.

1. [CBS 콘솔](https://console.cloud.tencent.com/cvm/cbs)에 로그인합니다.
2. 리전을 선택하고 성능을 조정할 CBS를 선택합니다.
3. 타깃 CBS의 [더보기]>[성능 조정]을 선택합니다.
4. '성능 조정' 팝업 창에서 성능을 조정할 타깃 설정을 선택합니다.
5. 설명을 선택하면 조정이 시작됩니다.

#### API를 통한 성능 업그레이드
ModifyDiskExtraPerformance 인터페이스를 사용하여 지정 CBS의 성능을 업그레이드할 수 있습니다. 자세한 작업 방법은 [CBS 추가 성능 조정](https://intl.cloud.tencent.com/document/product/362/40191)을 참조하십시오.


## 성능 다운그레이드

#### 콘솔을 통한 성능 다운그레이드
전제 조건 충족 시 다음과 같은 방식으로 성능을 다운그레이드할 수 있습니다.

1. [CBS 콘솔](https://console.cloud.tencent.com/cvm/cbs)에 로그인합니다.
2. 리전을 선택하고 성능을 조정할 CBS를 선택합니다.
3. 타깃 CBS의 [더보기]>[성능 조정]을 선택합니다.
4. '성능 조정' 팝업 창에서 성능을 조정할 타깃 설정을 선택합니다.
5. 설명을 선택하면 조정이 시작됩니다.

#### API를 통한 성능 다운그레이드
ModifyDiskExtraPerformance 인터페이스를 사용하여 지정 CBS의 성능을 다운그레이드할 수 있습니다. 자세한 작업 방법은 [CBS 추가 성능 조정](https://intl.cloud.tencent.com/document/product/362/40191)을 참조하십시오.

