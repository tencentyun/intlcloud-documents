Tencent Effect는 다양한 뷰티 필터와 효과를 제공합니다. Tencent Effect SDK를 사용하려면 Tencent Effect 에디션 또는 기능을 1년 License로 구매할 수 있습니다. 과금 관련 자세한 내용은 [가격 리스트](https://www.tencentcloud.com/document/product/1143/45371)를 참고하십시오.

License 획득 후 [Tencent Effect 콘솔](https://console.tencentcloud.com/xmagic)에서 신규 애플리케이션에 바인딩하거나 기존 애플리케이션에 대한 Tencent Effect의 유효 기간을 연장할 수 있습니다.
본문은 평가판 또는 공식 License를 추가하는 방법과 기존 License를 갱신하는 방법을 안내합니다.

[](id:test)
## 평가판 License

### 평가판 License 신청[](id:create_test)

Tencent Effect SDK를 사용해 보려면 평가판 License를 신청할 수 있습니다. 평가판 License는 14일 동안 유효하며 한 번(총 28일) 갱신할 수 있습니다.
평가판으로 제공되는 Tencent Effect 에디션은 모든 기능을 갖춘 최고급 에디션 S1 - 04입니다. Tencent Effect SDK의 전체 기능을 사용해 볼 수 있습니다. S1 - 04 에디션의 기능은 [기능 설명](https://intl.cloud.tencent.com/document/product/1143/45376)을 참고하십시오. 에디션 S1-04에는 X1-01 키잉이 포함되지만 다른 키잉 기능은 제공하지 않습니다.

>! **Tencent Effect 라이선스를 발급받기 전에 검토를 통과해야 합니다**. 평가판 라이선스는 검토를 통과하는 순간부터 유효합니다. 처음 14일 후에 평가판 라이선스를 갱신하는 경우 라이선스의 새로운 만료일은 갱신일로부터 14일 이후가 됩니다.
>- 회사 정보를 제출하면 Tencent Effect 모듈의 상태가 **검토 진행 중**으로 변경됩니다. 검토 프로세스는 일반적으로 1-2일이 소요됩니다. 회사 정보를 `2022-05-24 12:47:33(UTC+8)`에 제출하고 `2022-05-24 15:23:46(UTC+8)`에 검토를 통과했다고 가정할 때, 평가판 라이선스는 14일 후 `2022-06-09 00:00:00(UTC+8)`에 만료됩니다.
>- 평가판 라이선스는 1회 무료로 갱신할 수 있습니다. 최초 14일 이내에 갱신하면 `2022-06-23 00:00:00(UTC+8)`에 만료됩니다. 예를 들어 `2022-08-06 22:26:20(UTC+8)`과 같이 최초 14일이 지난 이후에 갱신하면 `2022-08-22 00:00:00(UTC+8)`에 만료됩니다.

콘솔에서 **새 애플리케이션에 대한 평가판 License를 생성**하거나 **기존 평가판 애플리케이션에 새 기능을 활성화**할 수 있습니다.
<dx-tabs>
::: 옵션1: 새로운 평가판 License 생성

1. [**Tencent Effect 콘솔**](https://console.tencentcloud.com/xmagic)에 로그인하고 왼쪽 사이드바에서 **모바일 License**를 선택합니다. **평가판 License 생성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/54ac63cd985f1170b2d74eaac4d0cd1d.png)
2. `App Name`, `Package Name` 및 `Bundle ID`를 입력합니다. 사용할 기능을 선택합니다(**고급 S1 - 04**, **기능 X1-01** 및 **기능 X1-02**). **회사 이름, 업종**을 입력한 후 **사업자등록증**을 업로드하고 **확인**을 클릭하면 검토가 시작됩니다.

![](https://qcloudimg.tencent-cloud.cn/raw/e3d3bb59025c79ac4d46f45c67d1cc27.png)
3. 평가판 License가 성공적으로 생성되면 **SDK를 초기화할 때 전달해야 하는 License URL과 Key가 표시됩니다. 정보 사본을 저장해 두시기 바랍니다.** License 정보는 검토를 통과한 후에만 유효합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6b8d5e0cca6b37e136040a50a17d5099.png)

<dx-alert infotype="explain"> 
1. 평가판 License에 바인딩된 Bundle ID 및 Package Name을 수정하려면 오른쪽 **편집**을 클릭하고 수정 후 **확인**을 클릭합니다. Tencent Effect 모듈을 계속 사용하려면 **검토 과정을 다시 거쳐야 합니다**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/b2a4f9588cc7f0ba5131e631ace94d10.png" style="zoom: 67%;" />
2. 아직 바인딩할 Package Name 또는 Bundle Id가 없으면 ‘-’를 입력할 수 있습니다.
</dx-alert>

:::
::: 옵션2: 기존 평가판 애플리케이션에 새로운 기능 활성화
기존 Tencent Effect 평가판 애플리케이션에 새로운 기능 모듈을 신청하려면 아래 단계를 따르십시오.
1. 대상 평가판 애플리케이션을 선택하고 **새 기능 테스트**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/31d21e8d61ed556276a44706a244d804.png)
2. 사용할 기능을 선택합니다(**고급 S1 - 04**, **기능 X1-01** 및 **기능 X1-02**). **회사 이름**을 입력하고 **업종**을 선택한 후 회사의 **사업자등록증**을 업로드한 다음 **확인**을 클릭하면 검토가 시작됩니다. 
<img src="https://qcloudimg.tencent-cloud.cn/raw/99f950a4bb1396e31d69f2c28cdab64f.png" style="zoom:50%;" />
:::
</dx-tabs>

3. 정보를 제출하면 모듈 상태가 **검토 진행 중**으로 변경됩니다. **검토 정보 조회**를 클릭하여 제출한 정보를 볼 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/a349ab1958dc407c362fad72485dab5d.png" style="zoom:67%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/34446b73133115d11e18b54393361b98.png" style="zoom:67%;" />
4. 검토를 통과하면 모듈 상태가 **정상**으로 변경되며 이는 평가판 License가 발급되었음을 나타냅니다. Tencent Effect를 사용해 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/516e3b714bd158a452022c4c563e0756.png)
>? **검토에 불합격**한 경우 **검토 결과**를 클릭하여 거부 사유를 포함한 세부 정보를 볼 수 있습니다. 검토를 위해 정보를 다시 제출하려면 **다시 시도**를 클릭하십시오.

![](https://qcloudimg.tencent-cloud.cn/raw/d787f5e69875a0de1294a8dd0ab519f3.png)

[](id:renewal_test)
### 평가판 License 갱신
평가판 License는 기본적으로 14일 동안 유효합니다. **1회** 갱신하여 유효 기간을 14일 더 연장할 수 있습니다. **Tencent Effect** 모듈에서 **갱신**을 클릭한 다음 **확인**을 클릭하면 됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/688ba0f794f4ec63857583a436d78e7a.png)

>? Tencent Effect의 평가판 License는 **한번만 갱신할 수 있습니다**. 즉, 평가판 License를 최대 28일 동안 사용할 수 있습니다. 평가판 License가 만료된 후에도 Tencent Effect를 계속 사용하려면 [공식 License](#create_formal)를 구매하십시오.

[](id:upgrade_test)
### 공식 License로 업그레이드
공식 License로 업그레이드하려면 먼저 [Tencent Effect 에디션 구매](https://buy.cloud.tencent.com/vcube?type=magic)를 완료한 후 다음 단계를 진행하십시오.
1. Tencent Effect 모듈에서 **업그레이드**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d1915913278cbf6f3c188141cdcdea5f.png)
2. **바인딩**을 클릭하고 구매한 Tencent Effect 에디션을 선택한 다음 **확인**을 클릭합니다. 애플리케이션에 대한 공식 License가 활성화됩니다. 다시 검토 과정을 거칠 필요가 없습니다. 바인딩할 에디션이 없다면 [구매 페이지](https://buy.cloud.tencent.com/vcube?type=magic)로 이동하여 에디션을 구매하십시오.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9466fa0917c9220d849603ab6a29b190.png" style="zoom:50%;" />

[](id:formal)
## 공식 License
[](id:create_formal)
### 공식 License 구매
[Tencent Effect SDK 구매 페이지](https://buy.intl.cloud.tencent.com/vcube)에서 SDK 기능을 구매하여 공식 License를 얻을 수 있습니다. License는 1년 동안 유효하며 다음 해 익일 00:00:00(UTC+8)에 만료됩니다. 다양한 SDK 버전별 기능에 대해 알아보려면 [기능 설명](https://www.tencentcloud.com/document/product/1143/45376)을 참고하십시오.

에디션을 구매한 후 다음 단계를 따르십시오.
1. License를 바인딩합니다. **License를 새 애플리케이션에 바인딩**하거나 **이를 사용하여 기존 애플리케이션에 Tencent Effect를 활성화**할 수 있습니다. 
<dx-tabs>
::: 옵션1: 공식 License를 새 애플리케이션에 바인딩
1. [**Tencent Effect 콘솔**](https://console.cloud.tencent.com/vcube)에 로그인하고 왼쪽 사이드바에서 **모바일 License**를 선택합니다. **공식 License 생성**을 클릭합니다.  
![](https://qcloudimg.tencent-cloud.cn/raw/1840aafe0ac1fc54485f9d4a4b15b98a.png) 
2. `App Name`, `Package Name` 및 `Bundle ID`를 입력하고 **Tencent Effect**를 선택한 후 **다음**을 클릭합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f128fdb87a0cc07762bbb75e86b460e9.png" style="zoom:50%;" />
3. **바인딩**을 클릭하고 구매한 Tencent Effect 에디션을 선택한 다음 **확인**을 클릭합니다. 바인딩할 에디션이 없다면 [구매 페이지](https://buy.cloud.tencent.com/vcube?type=magic)로 이동하여 에디션을 구매하십시오. 
<img src="https://qcloudimg.tencent-cloud.cn/raw/db5cf0bb61ea8063d25a11dfafb89e90.png" style="zoom:50%;" />
>? **확인**을 클릭하기 전에 Bundle ID와 Package Name을 다시 확인하고 앱 스토어에 제출한 것과 동일한지 확인하십시오. **제출 후에는 정보를 수정할 수 없습니다.** 

:::
::: 옵션2: 기존 애플리케이션에 대한 기능 활성화
1. **Tencent Effect** 기능을 추가할 기존 공식 라이선스를 선택하고 **추가 기능 활성화**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7d00d56c1dd4c1658f4fde736276d322.png)
2. **Tencent Effect**를 선택하고 **다음**을 클릭합니다.  
<img src="https://qcloudimg.tencent-cloud.cn/raw/d88b7f921e294eafec2bbdbaab65edec.png" style="zoom:50%;" />
3. **바인딩**을 클릭하고 구매한 Tencent Effect 에디션을 선택한 다음 **확인**을 클릭합니다. 바인딩할 에디션이 없다면 [구매 페이지](https://buy.intl.cloud.tencent.com/vcube)로 이동하여 에디션을 구매하십시오.
<img src="https://qcloudimg.tencent-cloud.cn/raw/0df1ab29aec13532934eed6457b8936d.png" style="zoom:50%;" />)
:::
</dx-tabs>
2. Tencent Effect 모듈의 상태가 **정상**이면 License가 발급되었음을 나타냅니다. Tencent Effect를 사용해 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/75200f8c745038400c568ca5e4d241af.png)


[](id:upgrade_formal)
### 공식 License 기능 유효 기간 연장
[**Tencent Effect 콘솔** > **모바일 License**](https://console.tencentcloud.com/xmagic) 페이지에서 License의 유효 기간을 확인할 수 있습니다. Tencent Effect 공식 License의 유효 기간을 연장하려면 다음 단계를 따르십시오.
1. 갱신해야 하는 License를 선택하고 Tencent Effect SDK 모듈에서 **갱신**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a4b37fc395ce6ea395541825167ad284.png)
2. 현재 에디션과 **동일한 유형의 에디션**을 선택합니다. 페이지에 갱신된 기간의 시작 및 종료 시간이 표시됩니다. **확인**을 클릭합니다. 바인딩할 에디션이 없다면 [구매 페이지](https://buy.intl.cloud.tencent.com/vcube)에서 구매하십시오.
<img src="https://qcloudimg.tencent-cloud.cn/raw/decbe36048335926e3a964a6ae923fbe.png" style="zoom:50%;" />

>!현재 동일한 유형의 리소스만 갱신할 수 있습니다. 즉, S1 - 04 에디션을 바인딩한 경우 S1 - 04 에디션만 갱신할 수 있습니다. 바인딩된 에디션 유형을 변경하려면 [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category} 하거나 영업팀에 문의하십시오.

3. 갱신된 유효 기간을 확인합니다.
>! **공식 License 정보는 수정할 수 없습니다.** 구매한 에디션을 새 애플리케이션에 사용하려면 **공식 License 생성**을 클릭하여 새 애플리케이션에 바인딩합니다.
