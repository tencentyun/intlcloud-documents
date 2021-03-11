## 작업 시나리오

여러 대의 인스턴스 생성 과정에서 사용자가 일정한 규칙성을 갖춘 인스턴스 이름을 원할 경우, 당사는 대량 인스턴스 생성 접미사 숫자 자동 오름차순 기능 및 패턴 스트링 지정 기능을 제공합니다. 사용자는 구매 페이지와 클라우드 API 두 가지 방식을 통해 구현할 수 있습니다.

- 사용자는 n개 인스턴스를 구매해야 하고 "CVM+순번"과 유사한 인스턴스 이름의 생성을 원할 때(즉 인스턴스 이름은 CVM1, CVM2, CVM3 등인 인스턴스), [접미사 숫자 자동 오름차순](#AutoAscending)을 통해 구현할 수 있습니다.
- 사용자는 n개 인스턴스를 생성해야 하고 인스턴스의 순번을 x부터 시작하여 점차 증가하는 것으로 지정해야 할 때, [단일 패턴 스트링 지정](#SpecifySingleString)을 통해 구현할 수 있습니다.
- 사용자는 여러 개의 접두사가 있고 각 접두사마다 모두 순번을 지정하는 인스턴스 n개 생성을 원할 때, [여러 개 패턴 스트링 지정](#SpecifyMultipleStrings)을 통해 구현할 수 있습니다.


## 작업 순서

<span id="AutoAscending"></span>
### 접미사 숫자 자동 오름차순

대량 구매한 인스턴스를 접두사가 동일하고 순번만 점차 증가하는 인스턴스 이름으로 설정할 수 있습니다.
>생성 성공한 인스턴스는 기본 순번이 1부터 시작되어 점차 증가하며 시작 순번을 지정할 수 없습니다.
>
아래의 작업은 사용자가 인스턴스 3대 구매하였고 생성을 원하는 인스턴스 이름이 “CVM+순번”(즉 인스턴스 이름은 CVM1, CVM2와  CVM3)인 것을 예로 듭니다.

#### 구매 페이지 작업

1. [인스턴스 생성](http://intl.cloud.tencent.com/document/product/213/4855)을 참조하여 인스턴스 3대 구매하고 "2.호스트 설정"에서 **"접두사+순번"**의 이름 짓기 규칙으로 인스턴스 이름을 작성합니다. 즉 인스턴스 이름을 `CVM`으로 작성합니다. 아래 그림 참조
![](https://main.qcloudimg.com/raw/820a52077080be5da4c1fb4715452e6b.png)
2. 페이지 제시어에 따라 단계별로 작업하고 결제를 완료합니다.
4. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)로 돌아가 신규 생성 인스턴스를 조회하면 대량 구매한 인스턴스는 접두사가 동일하고 순번이 점차 증가한다는 것을 바로 발견할 수 있습니다. 아래 그림 참조
![](https://main.qcloudimg.com/raw/27de624cd251910d47bea8e7732b284b.png)

#### API 작업

클라우드 API [RunInstances](https://intl.cloud.tencent.com/document/api/213/15730)에서 InstanceName 필드를 `CVM`으로 지정합니다.

### 패턴 스트링 지정

대량 구매한 인스턴스를 복잡하고 순번을 지정한 인스턴스 이름으로 설정할 수 있습니다. 인스턴스 이름은 단일 또는 여러 개 패턴 스트링의 지정을 지원합니다. 인스턴스 이름을 설정할 때 실제 수요에 따라 설정해주세요.

지정 패턴 스트링의 이름 짓기: **{R:x}**，x는 인스턴스 이름을 생성하는 초기 순번을 표시합니다.

<span id="SpecifySingleString"></span>
#### 단일 패턴 스트링 지정

아래의 작업은 사용자가 인스턴스 3대 생성해야 하고 인스턴스의 순번을 3부터 시작하여 점차 증가하는 것으로 지정하는 것을 예로 듭니다.

##### 구매 페이지 작업

1. [인스턴스 생성](http://intl.cloud.tencent.com/document/product/213/4855)을 참조하여 인스턴스를 구매하고 “2.호스트 설정”에서 **“접두사+지정 패턴 스트링{R:x}”**의 이름 짓기 규칙으로 인스턴스 이름을 작성합니다. 즉 인스턴스 이름을 `CVM{R:3}`으로 작성합니다. 아래 그림 참조
![](https://main.qcloudimg.com/raw/4e09732d612222f619cf7a1e8da1ee06.png)
2. 페이지 제시어에 따라 단계별로 작업하고 결제를 완료합니다.
3. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)로 돌아가 신규 생성 인스턴스를 조회하면 대량 구매한 인스턴스는 접두사가 동일하고 순번이 3부터 시작하여 점차 증가한다는 것을 바로 발견할 수 있습니다. 아래 그림 참조
![](https://main.qcloudimg.com/raw/78dc40cf4baa707573ad95a77bed4e1d.png)

##### API 작업

클라우드 API [RunInstances](https://intl.cloud.tencent.com/document/api/213/15730)에서 InstanceName 필드를 `CVM{R:3}`로 지정합니다.

<span id="SpecifyMultipleStrings"></span>
#### 여러 개 패턴 스트링 지정

아래의 작업은 사용자가 인스턴스 3대 생성해야 하고 생성을 원하는 인스턴스 이름에 cvm, Big와 test 접두사를 포함하고 cvm과 Big 접두사의 뒤에 순번이 따르며 순번은 각각 13과 2부터 시작하여 점차 증가(즉 인스턴스 이름은 cvm13-Big2-test, cvm14-Big3-test, cvm15-Big4-test)하는 것을 예로 듭니다.

##### 구매 페이지 작업

1. [인스턴스 생성](http://intl.cloud.tencent.com/document/product/213/4855)을 참조하여 인스턴스 3대 구매하고 “2.호스트 설정”에서 **“접두사+지정 패턴 스트링{R:x}-접두사+지정 패턴 스트링{R:x}-접두사”**의 이름 짓기 규칙으로 인스턴스 이름을 작성합니다. 즉 인스턴스 이름을 `cvm{R:13}-Big{R:2}-test`로 작성합니다. 아래 그림 참조
![](https://main.qcloudimg.com/raw/1042e86262bc7ce3939f1842a8025c23.png)
2. 페이지 제시어에 따라 단계별로 작업하고 결제를 완료합니다.
3. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)로 돌아가 신규 생성 인스턴스를 조회하면 대량 구매한 인스턴스는 각 접두사가 지정한 순번에 따라 점차 증가한다는 것을 바로 발견할 수 있습니다. 아래 그림 참조
![](https://main.qcloudimg.com/raw/a3c5e58daf07381ffde5abc019edad33.png)

##### API 작업

클라우드 API  [RunInstances](https://intl.cloud.tencent.com/document/api/213/15730)에서 InstanceName 필드를 ` cvm{R:13}-Big{R:2}-test`로 지정합니다.

