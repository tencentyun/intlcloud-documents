## 작업 시나리오
Tencent Cloud는 지난 3일 동안의 CVM 인스턴스 부하에 따라 인스턴스 설정 조정 방안을 제안합니다. 이 제안은 클라우드 모니터링에서 수집한 CPU, 메모리 등 모니터링 데이터를 기반으로 하며, 분석 후 실제 상황에 따라 인스턴스 설정 조정 여부를 결정할 수 있습니다.


## 관련 설명
- 인스턴스 설정 조정 방안은 인스턴스의 지난 3일의 평균 부하 데이터(데이터는 5분마다 통계)를 기반으로 결정되며, 작업 부하가 일정 기간 동안 비교적 안정적인 인스턴스에 적합하고, CPU 또는 메모리의 피크가 매우 짧은 인스턴스에는 적합하지 않습니다.
- GPU, FPGA 등 이기종 모델 및 CPM(Cloud Physical Machine)에는 적용되지 않으며, [알람 생성](https://intl.cloud.tencent.com/document/product/213/5179)을 통해 인스턴스 사용량을 능동적으로 모니터링할 수 있습니다.
- 이 제안은 참고용으로, 인스턴스 사용량 모니터링에 대한 요구 수준이 높은 경우 능동적인 모니터링을 위해 [클라우드 모니터링](https://intl.cloud.tencent.com/document/product/248/32799)을 사용하는 것이 좋습니다.

## 작업 단계
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/instance/index?rid=1)에 로그인하여, 인스턴스 리스트 페이지로 이동합니다.
2. 인스턴스 리스트 페이지에서 인스턴스의 모니터링 표시줄에 <img src="https://main.qcloudimg.com/raw/b966dd0b540ed2caa752be60c0f99230.png" style="margin:-6px 0px" width="20px"> 경고 아이콘이 나타나면 해당 인스턴스에 설정 조정 제안 방안이 존재하는 것입니다.
3. <img src="https://main.qcloudimg.com/raw/b966dd0b540ed2caa752be60c0f99230.png" style="margin:-6px 0px" width="20px"> 경고 아이콘을 클릭하면 ‘설정 조정 제안’ 창이 팝업됩니다.
4. ‘설정 조정 제안’ 창에서 인스턴스 사용에 따른 추천 모델을 조회할 수 있으며, ‘더 많은 추천 모델 조회’를 선택하면 다른 추천 모델을 조회할 수 있습니다.
5. 인스턴스 설정을 제안에 따라 조정하려면 ‘인스턴스 설정 조정 요금 설명을 읽고 동의합니다’를 선택한 후 **Adjust Now**를 클릭합니다.

