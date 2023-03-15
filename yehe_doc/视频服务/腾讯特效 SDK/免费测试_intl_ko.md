**Tencent Effect SDK는 다양한 뷰티 필터와 효과를 제공합니다. 무료 평가판 License(28일 동안 유효)를 신청하여 SDK를 사용해 볼 수 있습니다.**

[](id:test)
## 모바일 애플리케이션용 평가판 License

### 체험판 License 신청[](id:create_test)

Tencent Effect SDK를 사용해 보려면 평가판 License를 신청할 수 있습니다. 평가판 License는 14일 동안 유효하며 한 번(총 28일) 갱신할 수 있습니다.
평가판으로 제공되는 Tencent Effect 에디션은 모든 기능을 갖춘 최고급 에디션 S1 - 04입니다. Tencent Effect SDK의 전체 기능을 사용해 볼 수 있습니다. S1 - 04 에디션의 기능은 [기능 설명](https://intl.cloud.tencent.com/document/product/1143/45376)을 참고하십시오. 에디션 S1-04에는 X1-01 키잉이 포함되지만 다른 키잉 기능은 제공하지 않습니다.

>!**Tencent Effect 라이선스를 발급받기 전에 검토를 통과해야 합니다**. 평가판 라이선스는 검토를 통과하는 즉시 유효합니다. 처음 14일 후에 평가판 라이선스를 갱신하는 경우 라이선스의 새로운 만료 시간은 갱신일로부터 14일이 됩니다.
>- 회사 정보를 제출하면 Tencent Effect 모듈의 상태가 **검토 진행 중**으로 변경됩니다. 검토 프로세스는 일반적으로 1-2일이 소요됩니다. 회사 정보를 `2022-05-24 12:47:33(UTC+8)`에 제출하고 `2022-05-24 15:23:46(UTC+8)`에 검토를 통과했다고 가정할 때, 평가판 라이선스는 14일 후 `2022-06-09 00:00:00(UTC+8)`에 만료됩니다.
>- 평가판 라이선스는 1회 무료로 갱신할 수 있습니다. 최초 14일 이내에 갱신하면 `2022-06-23 00:00:00(UTC+8)`에 만료됩니다. 예를 들어 `2022-08-06 22:26:20(UTC+8)`과 같이 최초 14일이 지난 이후에 갱신하면 `2022-08-22 00:00:00(UTC+8)`에 만료됩니다.

콘솔에서 **새 애플리케이션에 대한 평가판 License를 생성**하거나 **기존 애플리케이션에 대한 평가판에 대한 새 기능을 활성화**할 수 있습니다.
<dx-tabs>
::: 옵션1: 새로운 평가판 License 생성

1. [Tencent Effect 콘솔](https://console.tencentcloud.com/xmagic)에 로그인하고 왼쪽 사이드바에서 **모바일 License**를 선택합니다. **평가판 License 생성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/84f8ab5111e32c16ef6553b14ac72fd7.png)
2. `App Name`, `Package Name` 및 `Bundle ID`를 입력합니다. 사용할 기능을 선택합니다(**고급 S1 - 04**, **기능 X1-01** 및 **기능 X1-02**). **회사 이름, 업종**을 입력한 후 **사업자등록증**을 업로드하고 **확인**을 클릭하면 검토가 시작됩니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/0d4f80aa8fd068a9d562ee5246a1e63a.png" style="zoom:50%;" />
3. 평가판 License가 성공적으로 생성되면 **SDK를 초기화할 때 전달해야 하는 License URL과 Key가 표시됩니다. 정보 사본을 저장해 두시기 바랍니다.** License 정보는 검토를 통과한 후에만 유효합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d2bec2a1877a5b1ac83a4ae07e30db39.png)
<dx-alert infotype="explain"> 
<li>평가판 License에 바인딩된 Bundle ID 및 Package Name을 수정하려면 오른쪽 **편집**을 클릭하고 수정 후 **확인**을 클릭합니다. Tencent Effect 모듈을 계속 사용하려면 **검토 과정을 다시 거쳐야 합니다**.</li>
>![](https://qcloudimg.tencent-cloud.cn/raw/9b8eae6f515542f2e2b08f9f1d21f495.png)
<li>Package Name 또는 Bundle Id가 없으면 ‘-’를 입력할 수 있습니다.</li></dx-alert>

:::
::: 옵션2: 기존 평가판 애플리케이션에 새로운 기능 활성화
기존 Tencent Effect 평가판 애플리케이션에 새로운 기능 모듈을 신청하려면 아래 단계를 따르십시오.
1. 대상 평가판 애플리케이션을 선택하고 **새 기능 테스트**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5ec68592f2bb1f24335b15d6bff1a384.png)
2. 사용할 기능을 선택합니다(**고급 S1 - 04**, **기능 X1-01** 및 **기능 X1-02**). **회사 이름**을 입력하고 **업종**을 선택한 후 회사의 **사업자등록증**을 업로드한 다음 **확인**을 클릭하면 검토가 시작됩니다. 
<img src="https://qcloudimg.tencent-cloud.cn/raw/7ee87ffbd3015d1ed31176bc48133595.png" style="zoom:80%;" />
:::
</dx-tabs>

3. 정보를 제출하면 모듈 상태가 **검토 진행 중**으로 변경됩니다. **검토 정보 조회**를 클릭하여 제출한 정보를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a27c350d9de411a9b629318703cbe2a4.png)
![](https://qcloudimg.tencent-cloud.cn/raw/4924c69299fa4d78ba7905a9111433af.png)
4. 검토를 통과하면 모듈 상태가 **정상**으로 변경되며 이는 평가판 License가 발급되었음을 나타냅니다. Tencent Effect를 사용해 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f7e039ac73e24766cbaa240b98b06a4c.png)
>? **검토에 불합격**한 경우 **검토 결과**를 클릭하여 거부 사유를 포함한 세부 정보를 볼 수 있습니다. 검토를 위해 정보를 다시 제출하려면 **다시 시도**를 클릭하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/7e2e93d6e4091fbcab1bf9c865868bd5.png)

[](id:renewal_test)
### 평가판 License 연장
평가판 License는 기본적으로 14일 동안 유효합니다. **1회** 갱신하여 유효 기간을 14일 더 연장할 수 있습니다. **Tencent Effect** 모듈에서 **갱신**을 클릭한 다음 **확인**을 클릭하면 됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/95f05996f1ae77f5b32fb051d3490c68.png)

>? 평가판 License는 **한번만 갱신할 수 있습니다**. 즉, 평가판 License는 최대 28일 동안 사용할 수 있습니다. 평가판 License가 만료된 후에도 계속 사용하려면 [공식 License](#create_formal)를 구매하십시오.

[](id:upgrade_test)
### 공식 License로 업그레이드
공식 License로 업그레이드하려면 먼저 [Tencent Effect 에디션 구매](https://buy.cloud.tencent.com/vcube?type=magic) 후 다음 단계를 수행하십시오.
1. Tencent Effect 모듈에서 **업그레이드**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7d0508a70907b37be34ee78bae12c118.png)
2. **바인딩**을 클릭하고 구매한 Tencent Effect 에디션을 선택한 다음 **확인**을 클릭합니다. 애플리케이션에 대한 공식 License가 활성화됩니다. 다시 검토 과정을 거칠 필요가 없습니다. 바인딩할 에디션이 없다면 [구매 페이지](https://buy.cloud.tencent.com/vcube?type=magic)로 이동하여 에디션을 구매하십시오.
<img src="https://qcloudimg.tencent-cloud.cn/raw/20688364d5736456e24b29840c67140f.png" style="zoom:67%;" />