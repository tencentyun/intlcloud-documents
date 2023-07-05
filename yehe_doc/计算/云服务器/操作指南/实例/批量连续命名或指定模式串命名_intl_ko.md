## 작업 시나리오

여러 대의 인스턴스 생성 과정에서 사용자가 일정한 규칙성을 갖춘 인스턴스 이름/호스트 이름을 원할 경우, 당사는 인스턴스 배치 생성 접미사 숫자 자동 오름차순 기능 및 스트링 패턴 지정 기능을 제공합니다. 사용자는 구매 페이지와 클라우드 API 두 가지 방식을 통해 구현할 수 있습니다.

- n개의 인스턴스를 구입하고, ‘CVM+순번’과 유사한 인스턴스 이름/호스트 이름을 생성하려면(즉 인스턴스 이름/호스트 이름이 CVM1, CVM2, CVM3 등인 인스턴스), [접미사 숫자 자동 오름차순](#AutoAscending)을 통해 구현할 수 있습니다.
- n개의 인스턴스를 구입하고, 인스턴스 이름/호스트 이름의 순번을 x부터 시작하여 점차 증가하는 것으로 지정하려면, [단일 스트링 패턴 지정](#SpecifySingleString)을 통해 구현할 수 있습니다.
- n개의 접두사가 있고 각 접두사마다 모두 순번을 지정하는 인스턴스 이름/호스트 이름 n개를 생성하려면, [여러 스트링 패턴 지정](#SpecifyMultipleStrings)을 통해 구현할 수 있습니다.

## 적용 범위

본문은 **인스턴스 이름 설정** 및 **호스트 이름 설정**에 적용됩니다.

## 작업 단계

<dx-alert infotype="explain" title="">
다음 작업 단계는 인스턴스 이름 설정의 예시입니다. 이름 설정 유형에 따라 호스트 이름 설정 단계가 조금씩 다릅니다.
</dx-alert>



### 접미사 숫자 자동 오름차순[](id:AutoAscending)

배치 구입한 인스턴스를 접두사가 동일하고 순번만 점차 증가하는 인스턴스 이름으로 설정할 수 있습니다.
<dx-alert infotype="notice" title="">
생성 성공한 인스턴스는 기본 순번이 1부터 시작되어 점차 증가하며, 시작 순번을 지정할 수 없습니다.
</dx-alert>
아래의 작업은 사용자가 인스턴스를 3대 구입하였고 생성을 원하는 인스턴스 이름이 ‘CVM+순번’(즉, CVM1, CVM2와 CVM3)이라고 가정합니다.

<dx-tabs>
::: 구매 페이지 작업
1. 아래 이미지와 같이 [인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하여 인스턴스를 3대 구입하고, ‘네트워크 및 호스트 설정’에서 **‘접두사+순번’**의 이름 생성 규칙으로 인스턴스 이름(`CVM`)을 입력합니다.
![](https://main.qcloudimg.com/raw/820a52077080be5da4c1fb4715452e6b.png)
2. 페이지 안내에 따라 단계별로 작업하고 결제를 완료합니다.
:::
::: API\s 작업
클라우드 API [RunInstances](https://intl.cloud.tencent.com/zh/document/product/213/33237)에서 관련 필드 설정:
- 인스턴스 이름: InstanceName 필드를 `CVM`으로 지정합니다.
- 호스트 이름: HostName 필드를 `CVM`으로 지정합니다.
:::
</dx-tabs>


### 스트링 패턴 지정[](id:SpecifyStrings)

배치 구입한 인스턴스에 복잡한 지정 순번 이름을 설정할 수 있습니다. 인스턴스 이름은 단일 또는 여러 개 스트링 패턴의 지정을 지원합니다. 실제 필요에 따라 인스턴스 이름을 설정하십시오.

지정 스트링 패턴의 이름 생성: **{R:x}**, x는 인스턴스 이름을 생성하는 초기 순번을 표시합니다.


#### 단일 스트링 패턴 지정[](id:SpecifySingleString)

아래의 작업은 사용자가 인스턴스를 3대 구입하였고, 인스턴스 순번을 3부터 시작하여 점차 증가하는 것으로 지정하였다고 가정합니다.

<dx-tabs>
::: 구매 페이지 작업
1. 아래 이미지와 같이 [인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하여 인스턴스를 구입하고 ‘네트워크 및 호스트 설정’에서 **‘접두사+지정 스트링 패턴{R:x}’**의 이름 생성 규칙으로 인스턴스 이름(`CVM{R:3}`)을 입력합니다.
![](https://main.qcloudimg.com/raw/4e09732d612222f619cf7a1e8da1ee06.png)
2. 페이지 안내에 따라 단계별로 작업하고 결제를 완료합니다.
:::
::: API\s 작업
클라우드 API [RunInstances](https://intl.cloud.tencent.com/zh/document/product/213/33237)에서 관련 필드 설정:
- 인스턴스 이름: InstanceName 필드를 `CVM{R:3}`로 지정합니다.
- 호스트 이름: HostName 필드를 `CVM{R:3}`로 지정합니다.
:::
</dx-tabs>


#### 여러 스트링 패턴 지정[](id:SpecifyMultipleStrings)

하기 작업은 사용자가 인스턴스 3대를 생성하고, 인스턴스 이름에 cvm, Big 및 test 접두사를 포함하며, cvm과 Big 접두사의 뒤의 순번은 각각 13과 2부터 시작하여 점차 증가(즉 인스턴스 이름은 cvm13-Big2-test, cvm14-Big3-test, cvm15-Big4-test)한다고 가정합니다.

<dx-tabs>
::: 구매 페이지 작업
1. 아래 이미지와 같이 [인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하여 인스턴스 3대를 구입하고 ‘네트워크 및 호스트 설정’에서 **‘접두사+지정 스트링 패턴{R:x}-접두사+지정 스트링 패턴{R:x}-접두사’**의 이름 생성 규칙으로 인스턴스 이름(`cvm{R:13}-Big{R:2}-test`)을 작성합니다.
![](https://main.qcloudimg.com/raw/1042e86262bc7ce3939f1842a8025c23.png)
2. 페이지 안내에 따라 단계별로 작업하고 결제를 완료합니다.

:::
::: API\s 작업
클라우드 API [RunInstances](https://intl.cloud.tencent.com/zh/document/product/213/33237)에서 관련 필드 설정:
- 인스턴스 이름: InstanceName 필드를 `cvm{R:13}-Big{R:2}-test`로 지정합니다.
- 호스트 이름: HostName 필드를 `cvm{R:13}-Big{R:2}-test`로 지정합니다.
:::
</dx-tabs>


## 검증 기능
[접미사 숫자 자동 오름차순](#AutoAscending) 또는 [스트링 패턴 지정](#SpecifyStrings)을 통해 인스턴스를 배치 생성한 후 다음 작업으로 검증할 수 있습니다.

### 인스턴스 이름 설정 검증
아래 이미지와 같이 [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인하여 새로 생성된 인스턴스를 확인하면, 배치 구입한 인스턴스의 이름이 설정된 규칙에 따라 생성되는 것을 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/a3c5e58daf07381ffde5abc019edad33.png)

### 호스트 이름 설정 검증
1. [](id:hostname_step01)CVM 인스턴스를 재시작 및 로그인합니다.
2. 인스턴스 운영 체제 유형에 따라 다른 단계를 선택합니다.
<dx-tabs>
::: Linux\s 인스턴스
운영 체제 인터페이스에서 다음 명령을 실행합니다.
```
hostname
```
:::
::: Windows\s 인스턴스
CMD TCCLI를 열고 다음 명령을 실행합니다.
```
hostname
```
:::
</dx-tabs>
3. [](id:hostname_step03)`hostname` 명령의 반환 결과를 확인합니다.
다음과 같은 결과가 반환되면 설정이 완료된 것입니다.
```
cvm13-Big2-test
```
4. [1단계](#hostname_step01) - [3단계](#hostname_step03)를 반복하여 다른 배치 구입 인스턴스를 차례로 인증합니다.



