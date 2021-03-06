## 실행 배경

사용자가 URL 리스트를 데이터 원본 주소로 사용해 데이터 마이그레이션을 진행하고 싶은 경우, COS에서는 다음과 같은 마이그레이션 방법을 지원합니다.
<table>
   <tr>
      <th>마이그레이션 방법</th>
      <th>설명</th>
   </tr>
   <tr>
	 <td nowrap="nowrap"><a href="#msp">마이그레이션 서비스 플랫폼(MSP)</a></td>
      <td>MSP는 여러 마이그레이션 툴을 통합하여 시각화 인터페이스를 제공하는 플랫폼으로, 사용자가 손쉽게 대규모 데이터 마이그레이션 작업을 모니터링하고 관리할 수 있습니다. MSP의 "파일 마이그레이션 툴"은 사용자가 데이터를 다른 공유 클라우드 및 데이터 원본 서버에서 COS로 마이그레이션하는 데 도움을 줍니다.</td>
   </tr>
   <tr>
	 <td><a href="#huiyuan">COS Origin-pull</a></td>
      <td>COS Origin-pull은 데이터 원본 서버에서 읽기 및 쓰기 액세스 요청이 있는 데이터를 자동으로 Tencent Cloud COS에 마이그레이션합니다. 해당 마이그레이션 방법은 데이터를 빠르게 핫/콜드 티어링을 진행하는데 도움이 될 뿐만 아니라 서비스 시스템의 핫 데이터에 대한 읽기 및 쓰기 액세스 속도를 향상시켜줍니다.</td>
   </tr>
   <tr>
	 <td><a href="#cos">COS Migration</a></td>
      <td>COS Migration은 COS 데이터 마이그레이션 기능이 결합된 통합형 툴입니다. 사용자는 간단한 설정 작업을 통해 데이터를 COS에 신속하게 마이그레이션할 수 있습니다.</td>
   </tr>
</table>

데이터 원본 서버에서 클라우드에 마이그레이션하는 과정에서 사용자가 데이터 원본 서버의 핫 데이터만 모두 클라우드에 마이그레이션하고 콜드 데이터는 원본 서버에 보관하고 싶은 경우, [COS Origin-pull](#huiyuan) 마이그레이션 방법을 사용할 수 있습니다. COS Origin-pull은 읽기 및 쓰기 액세스 요청이 있는 핫 데이터만 COS에 마이그레이션하며, 저빈도 액세스의 비즈니스 데이터는 자동으로 핫/콜드 티어링합니다.


>현재 COS는 인증 정보가 있는 URL 데이터에 대한 마이그레이션을 지원하지 않습니다.

## 마이그레이션 실행
<span id=msp>

### 마이그레이션 서비스 플랫폼(MSP)

마이그레이션 작업 순서는 다음과 같습니다.

1. [MSP](https://console.cloud.tencent.com/msp)에 로그인합니다.
1. 왼쪽 메뉴바에서 [마이그레이션 툴]을 클릭하고 "파일 마이그레이션 툴"을 찾아 [시작하기]를 클릭합니다.
2. 마이그레이션 작업을 생성하고 작업 정보를 설정합니다.
3. 작업을 실행합니다.

자세한 작업 방법은 [URL 리스트 마이그레이션](https://intl.cloud.tencent.com/document/product/1036/33185)을 참조하십시오.


#### 작업 팁

데이터 마이그레이션 중 데이터 소스 읽기 속도는 서로 다른 네트워크 환경에 따라 차이가 있을 수 있으며, 사용자는 실제 상황에 따라 "파일 마이그레이션 작업 생성" 시 비교적 높은 QPS 동시 접속률을 선택하여 마이그레이션 속도를 향상시킬 수 있습니다.

<span id=huiyuan>

### COS Origin-pull



마이그레이션 작업 순서는 다음과 같습니다.

1. COS 콘솔로 이동하여 마이그레이션할 데이터의 타깃 버킷에 Origin-pull 설정을 활성화합니다.
2. 버킷의 Origin-pull 주소를 설정한 후 저장합니다.
3. 서비스 시스템의 읽기 및 쓰기 요청을 Tencent Cloud COS로 전송합니다.

자세한 작업 방법은 [Origin-pull 설정](https://intl.cloud.tencent.com/document/product/436/31508) 문서를 참조하십시오.

#### 작업 팁

다음은 원본 데이터에 대한 핫/콜드 티어링을 완료하여, 핫 데이터를 Tencent Cloud COS에 무결성 마이그레이션해 핫 데이터의 읽기 요청 속도를 향상시킬 수 있는 방법입니다.

1. 서비스 시스템의 읽기 및 쓰기 요청을 COS로 전환합니다. COS 콘솔의 Origin-pull 기능 설정 페이지에서 Origin-pull 주소를 데이터 원본 서버로 설정합니다. 이때의 시스템 구조는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/455212542dc210f556b4d55ee86c9776.jpg)
2. 일정 시간이 지나면 콜드 데이터는 여전히 원본 서버에 남아 있지만 핫 데이터는 Tencent Cloud COS에 마이그레이션되어 있으며, 마이그레이션 과정 중 서비스 시스템은 영향을 받지 않습니다.



<span id=cos>

### COS Migration

마이그레이션 작업 순서는 다음과 같습니다.

1. Java 환경을 설치합니다.
2. COS Migration 툴을 설치합니다.
3. 구성 파일을 수정합니다.
4. 툴을 실행합니다.

자세한 방법은 [COS Migration 툴](https://intl.cloud.tencent.com/document/product/436/15392) 문서를 참조하십시오.



#### 작업 팁
COS Migration을 설정하여 마이그레이션 속도를 최대로 향상시키는 방법을 소개합니다.


1. 자체 네트워크 환경에 따라 파일 크기를 구분하는 임계값과 마이그레이션 동시 접속 수를 조정하여 대용량 파일은 멀티파트 방식으로 전송하고 저용량 파일은 동시 접속 방식으로 전송하는 최적의 마이그레이션 방식을 실현합니다. 툴의 실행 시간을 조정하고 대역폭 제한을 설정해 비즈니스 운영에 데이터 마이그레이션의 대역폭 점유로 인한 영향이 미치지 않도록 합니다. 해당 사항은 구성 파일 config.ini의 `[common]`에서 조정할 수 있으며, 다음 매개변수를 수정해 조정합니다.
<table>
   <tr>
      <th>매개변수 이름</td>
      <th>매개변수 설명</td>
   </tr>
   <tr>
      <td>smallFileThreshold</td>
      <td>저용량 파일의 임계값 매개변수입니다. 임계값 이상인 경우 멀티파트 업로드를 실행하며, 기본값은 5MB입니다.</td>
   </tr>
   <tr>
      <td>bigFileExecutorNum</td>
      <td>대용량 파일의 동시 접속 수이며, 기본값은 8입니다.<br>외부 네트워크를 통해 COS에 접속하고 대역폭이 비교적 작은 경우 해당 동시 접속 수를 작게 설정하십시오.</td>
   </tr>
   <tr>
      <td>smallFileExecutorNum</td>
      <td>저용량 파일의 동시 접속 수이며, 기본값은 64입니다. <br>외부 네트워크를 통해 COS에 접속하고 대역폭이 비교적 작은 경우 해당 동시 접속 수를 작게 설정하십시오.</td>
   </tr>
   <tr>
      <td>executeTimeWindow</td>
      <td>해당 매개변수로 마이그레이션 툴이 매일 실행되는 시간대를 정의합니다. 다른 시간에는 휴면 상태가 되며, 휴면 상태에서는 마이그레이션을 일시 중지하고 다음 번 시간 창이 자동으로 이어서 실행할 때까지 마이그레이션 진도를 유지합니다.</td>
   </tr>
</table>
2. 분산형 병렬 전송 방식을 사용해 마이그레이션 속도를 더욱 향상시킬 수 있습니다. 여러 서버에 COS Migration을 설치하고 각 서버별로 서로 다른 원본 데이터를 마이그레이션하는 방법을 고려할 수 있습니다.
