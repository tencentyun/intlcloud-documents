## CVM 인스턴스 구매 계정 제한

- Tencent Cloud 계정이 필요합니다. 회원가입 가이드는 [Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)을 참조하십시오.
- 실명 인증이 필요합니다. 실명 인증을 하지 않은 경우 중국 내 CVM 인스턴스를 구매할 수 없습니다. 인증 자격은 [실명 인증 가이드](https://intl.cloud.tencent.com/document/product/378/3629)를 참조하십시오.
- 종량제 CVM 생성 시 시스템이 CVM의 1시간 호스트 요금을 동결합니다. 주문을 접수하기 전에 계정의 잔액이 충분한지 확인하십시오.

## CVM 인스턴스 사용 제한

- 현재 가상화 소프트웨어 설치와 가상화의 재진행(예: VMware 또는 Hyper-V를 사용하는 경우)을 지원하지 않습니다.
- 현재 사운드 카드 애플리케이션 및 외부 하드웨어 디바이스(U 디스크, 외장 하드디스크, U-KEY 등)의 직접 로딩을 지원하지 않습니다.
- 공용망 게이트웨이는 현재 Linux 시스템만 지원합니다.

## CVM 인스턴스 구매 제한

- 각 가용존에서 사용자당 구매 가능한 종량제 CVM 인스턴스의 **총 수량**은 30개입니다.
- 자세한 내용은 [CVM 인스턴스 구매 제한](https://intl.cloud.tencent.com/document/product/213/2664)을 참조하십시오.


## 이미지 관련 제한

- 공용 이미지는 현재 사용 제한이 없습니다.
- 사용자 정의 이미지: 각 리전마다 최대 10개의 사용자 정의 이미지를 지원합니다.
- 공유 이미지: 각 사용자 정의 이미지는 최대 50명의 Tencent Cloud 사용자와 공유할 수 있으며, 동일한 리전 내의 계정에만 공유할 수 있습니다.
- 자세한 내용은 [이미지 유형 제한](https://intl.cloud.tencent.com/document/product/213/4941)을 참조하십시오.

## EIP 관련 제한

#### 할당 제한

| 리소스 | 제한 |
|---------|:---------:|
| Tencent Cloud 계정별 각 리전(Region)에 할당된 EIP 개수 | 20개 |
| Tencent Cloud 계정별 각 리전의 일일 주문 횟수	 | 할당된 EIP 개수 * 2회 |
| EIP 바인딩 해제 시, 매일 각 계정에 갱신되는 공용 IP 무료 재할당 횟수 | 10회 |

#### CVM의 공용 IP 바인딩 제한

2019년 9월 18일(포함)부터 CPU 설정에 따라 단일 CVM의 공용 IP 바인딩 제한 수량이 변경되었습니다. 구체적인 수치는 다음 표와 같습니다.
>! 2019년 9월 18일 0시 이전에 구매한 CVM은 해당되지 않으며, CVM의 공용 IP 바인딩 수량은 서버가 지원하는 [내부 IP 수량](https://intl.cloud.tencent.com/document/product/576/18527)과 같습니다.
>

| CVM의 CPU 수 | 공용 IP 바인딩 제한 수량(일반 공용 IP 및 EIP 포함) |
|---------|---------|
| CPU: 1 - 5 | 2 |
| CPU: 6 - 11 | 3 |
| CPU: 12 - 17 | 4 |
| CPU: 18 - 23 | 5 |
| CPU: 24 - 29 | 6 |
| CPU: 30 - 35 | 7 |
| CPU: 36 - 41 | 8 |
| CPU: 42 - 47 | 9 |
| CPU: ≥ 48 | 10 |

## ENI 관련 제한

CPU와 메모리 구성에 따라 CVM이 바인딩할 수 있는 ENI 수와 단일 ENI가 바인딩할 수 있는 내부 IP 수의 차이가 큽니다. ENI 및 단일 ENI IP 할당 수는 아래 표와 같습니다.
>! 단일 ENI의 IP 바인딩 수는 ENI가 바인딩할 수 있는 최대 IP 수를 의미하나, 반드시 최대 수량에 맞춰 EIP를 할당하지는 않습니다. 계정의 EIP는 [EIP 사용 제한](https://intl.cloud.tencent.com/document/product/213/5733)에 따라 할당합니다.

<dx-tabs>
::: CVM이\s지원하는\sENI\s바인딩\s할당액
<table >
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">모델</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">인스턴스 유형</th>
    <th width="86%" colspan="10" style = "text-align:center;">ENI 할당액</th>
   </tr>
   <tr >
    <th style = "text-align:center;">CPU: 싱글코어</th>
    <th style = "text-align:center;">CPU: 듀얼코어</th>
    <th style = "text-align:center;">CPU: 4코어</th>
    <th style = "text-align:center;">CPU: 6코어</th>
    <th style = "text-align:center;">CPU: 8코어</th>
    <th style = "text-align:center;">CPU: 10코어</th>
    <th style = "text-align:center;">CPU: 12코어</th>
    <th style = "text-align:center;">CPU: 14코어</th>
    <th style = "text-align:center;">CPU: 16코어</th>
    <th style = "text-align:center;">CPU: &gt;16코어</th>
   </tr>
   <tr >
    <th rowspan="9" style = "text-align:center;">표준형</th>
    <th style = "text-align:center;">표준형 S5</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준 스토리지 확장형 S5se</th>
    <td >-</td>
    <td >-</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 SA2</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 S4</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">표준 네트워크 최적화형 SN3ne</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >8</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 S3</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 SA1</th>
    <td >2</td>
    <td >2</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 S2</th>
    <td >2</td>
    <td >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 S1</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="2" style = "text-align:center;">고성능 I/O</th>
    <th style = "text-align:center;">고성능 I/O IT5</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">고성능 I/O IT3</th>
    <td  >-</td>
    <td  >-</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="5" style = "text-align:center;">메모리형</th>
    <th  style = "text-align:center;">메모리형 M5</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">메모리형 M4</th>
    <td >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">메모리형 M3</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">메모리형 M2</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">메모리형 M1</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="4" style = "text-align:center;">컴퓨팅형</th>
    <th  style = "text-align:center;">컴퓨팅형 C4</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">컴퓨팅 네트워크 강화형 CN3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">컴퓨팅형 C3</th>
    <td  >-</td>
    <td >-</td>
    <td >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;" >컴퓨팅형 C2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th  rowspan="7" style = "text-align:center;">GPU 모델</th>
   </tr>
   <tr >
    <th class="xl71" x:str style = "text-align:center;">GPU 컴퓨팅형 GN6</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU 컴퓨팅형 GN6S</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU 컴퓨팅형 GN7</th>
    <td >-</td>
    <td >-</td>
   <td  >4</td>
    <td >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">GPU 컴퓨팅형 GN8</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr >
    <th  style = "text-align:center;">GPU 컴퓨팅형 GN10X</th>
   <td >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >6</td>
      <td  >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU 컴퓨팅형 GN10Xp</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td >8</td>
   </tr>
   <tr >
    <th rowspan="3" style = "text-align:center;">빅 데이터형</th>
    <th  style = "text-align:center;">빅 데이터형 D3</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">빅 데이터형 D2</th>
    <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td>8</td>
    <td>8</td>
   </tr>
  </table>
:::
::: CVM\s단일\sENI가\s지원하는\s내부\sIP\s바인딩\s할당액
<table >
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">모델</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">인스턴스 유형</th>
    <th width="86%" colspan="10" style = "text-align:center;">단일 ENI의 내부 IP 바인딩 할당액</th>
   </tr>
   <tr >
    <th style = "text-align:center;">CPU: 싱글코어</th>
    <th style = "text-align:center;">CPU: 듀얼코어</th>
    <th style = "text-align:center;">CPU: 4코어</th>
    <th style = "text-align:center;">CPU: 6코어</th>
    <th style = "text-align:center;">CPU: 8코어</th>
    <th style = "text-align:center;">CPU: 10코어</th>
    <th style = "text-align:center;">CPU: 12코어</th>
    <th style = "text-align:center;">CPU: 14코어</th>
    <th style = "text-align:center;">CPU: 16코어</th>
    <th style = "text-align:center;">CPU: &gt;16코어</th>
   </tr>
   <tr >
    <th rowspan="9" style = "text-align:center;">표준형</th>
    <th style = "text-align:center;">표준형 S5</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준 스토리지 확장형 S5se</th>
    <td >-</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 SA2</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 S4</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">표준 네트워크 최적화형 SN3ne</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >30</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 S3</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 SA1</th>
    <td >메모리=1G: 2<br/>메모리&gt;1G: 6</td>
    <td >10</td>
    <td >메모리=8G: 10<br/>메모리=16G: 20</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 S2</th>
    <td >6</td>
    <td >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 S1</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="2" style = "text-align:center;">고성능 I/O</th>
    <th style = "text-align:center;">고성능 I/O IT5</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">고성능 I/O IT3</th>
    <td  >-</td>
    <td  >-</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="5" style = "text-align:center;">메모리형</th>
    <th  style = "text-align:center;">메모리형 M5</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">메모리형 M4</th>
    <td >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">메모리형 M3</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">메모리형 M2</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">메모리형 M1</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="4" style = "text-align:center;">컴퓨팅형</th>
    <th  style = "text-align:center;">컴퓨팅형 C4</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">컴퓨팅 네트워크 강화형 CN3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">컴퓨팅형 C3</th>
    <td  >-</td>
    <td >-</td>
    <td >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;" >컴퓨팅형 C2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th  rowspan="7" style = "text-align:center;">GPU 모델</th>
    <th  style = "text-align:center;">GPU 컴퓨팅형 GN2</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
   </tr>
   <tr >
    <th class="xl71" x:str style = "text-align:center;">GPU 컴퓨팅형 GN6</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU 컴퓨팅형 GN6S</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU 컴퓨팅형 GN7</th>
    <td >-</td>
    <td >-</td>
   <td  >10</td>
    <td >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">GPU 컴퓨팅형 GN8</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th  style = "text-align:center;">GPU 컴퓨팅형 GN10X</th>
   <td >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >20</td>
      <td  >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU 컴퓨팅형 GN10Xp</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td >30</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">FPGA 모델</th>
    <th style = "text-align:center;">FPGA 가속형 FX4</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="3" style = "text-align:center;">빅 데이터형</th>
    <th  style = "text-align:center;">빅 데이터형 D3</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">빅 데이터형 D2</th>
    <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">빅 데이터형 D1</th>
    <td >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th colspan="2" style = "text-align:center;">CPM 2.0</th>
    <td colspan="10" style = "text-align:center;">현재 ENI 바인딩을 지원하지 않습니다.</td>
   </tr>
  </table>
:::
</dx-tabs>


## 대역폭 관련 제한

- 아웃바운드 대역폭 최댓값(다운스트림 대역폭):
 - 2020년 2월 24일 00:00 이전에 생성한 기기의 경우, 다음의 규칙을 따릅니다. 
<table>
<tr><th rowspan="2">네트워크 과금 방식</th><th colspan="2">인스턴스</th><th rowspan="2">대역폭 최댓값 설정 가능 범위(Mbps)</th></tr>
<tr><th>인스턴스 과금 방식</th><th>인스턴스 구성</th></tr>
<tr><td>트래픽 과금</td><td>종량제 인스턴스</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>대역폭 과금</td><td>종량제 인스턴스</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>공유 대역폭</td><td colspan="2">ALL</td><td>0 - 2000</td></tr>
</table>

 - 2020년 2월 24일 00:00 이후에 생성한 기기의 경우, 다음의 규칙을 따릅니다.
<table>
<tr><th rowspan="2">네트워크 과금 방식</th><th colspan="2">인스턴스</th><th rowspan="2">대역폭 최댓값 설정 가능 범위(Mbps)</th></tr>
<tr><th style="width: 18.5607%;">인스턴스 과금 방식</th><th style="width: 24.5814%;">인스턴스 구성</th></tr>
<tr><td>트래픽 과금</td><td>종량제 인스턴스</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>대역폭 과금</td><td>종량제 인스턴스</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>공유 대역폭</td><td colspan="2">ALL</td><td>0 - 2000</td></tr>
</table>

- 인바운드 대역폭 최댓값(업스트림 대역폭):
	- 사용자가 구매한 고정 대역폭이 10Mbps보다 높은 경우, Tencent Cloud는 구매한 대역폭과 동일한 외부 네트워크 인바운드 대역폭을 할당합니다.
	- 사용자가 구매한 고정 대역폭이 10Mbps보다 낮은 경우, Tencent Cloud는 10Mbps의 외부 네트워크 인바운드 대역폭을 할당합니다.

## 디스크 관련 제한

<table>
	<tr><th>제한 유형</th><th>제한 설명</th></tr>
	<tr><td>CBS 능력</td><td>2018년 5월부터 CVM과 함께 구매하는 데이터 디스크는 모두 CBS로 CVM에서 언마운트한 후 다시 마운트할 수 있습니다. 해당 기능은 모든 <a href="https://intl.cloud.tencent.com/document/product/213/35071">가용존</a>에서 사용할 수 있습니다.</td></tr>
	<tr><td>CBS 성능 제한</td><td> I/O 성능은 동시에 적용됩니다. </br>예를 들어 1TB의 SSD CBS가 최대 랜덤 26,000 IOPS에 도달한다면 읽기/쓰기 IOPS도 각각 이 값에 도달할 수 있음을 의미합니다. 또한 여러 성능 제한으로 인해 해당 예시에서 block size가 4KB/8KB인 I/O를 사용하면 최대 IOPS에 도달할 수 있지만, block size가 16KB인 I/O를 사용하면 최대 IOPS에 도달할 수 없습니다(처리량 260MB/s 제한에 도달).</td></tr>
	<tr><td>단일 CVM이 마운트할 수 있는 CBS 수</td><td>는 최대 20블록입니다. </td></tr>
	<tr><td>단일 리전의 스냅샷 할당액</td><td>64 + 리전 내 CBS 수량 * 64(개)</td></tr>
	<tr><td>CBS가 마운트할 수 있는 CVM 제한</td><td>CVM과 CBS가 반드시 동일 가용존에 있어야 합니다. </td></tr>
	<tr><td>스냅샷 롤백 제한</td><td>스냅샷 데이터는 스냅샷을 생성한 소스 CBS로만 롤백할 수 있습니다. </td></tr>
	<tr><td>스냅샷 생성 CBS 유형 제한</td><td>데이터 디스크 스냅샷으로만 새로운 CBS를 생성할 수 있습니다.</td></tr>
	<tr><td>스냅샷 생성 CBS 크기 제한</td><td>스냅샷으로 생성한 새로운 CBS의 용량은 반드시 스냅샷 소스 CBS의 용량 이상이어야 합니다.</td></tr>
</table>


## 보안 그룹 관련 제한

- 보안 그룹은 리전별로 구분하므로, 하나의 CVM은 동일 리전의 보안 그룹에만 바인딩할 수 있습니다.
- 보안 그룹은 [네트워크 환경](https://intl.cloud.tencent.com/document/product/213/5227)의 모든 CVM 인스턴스에 적용됩니다.
- 사용자는 리전마다 항목별로 최대 50개의 보안 그룹을 설정할 수 있습니다.
- 하나의 보안 그룹의 인바운드 또는 아웃바운드의 액세스 정책으로 각각 최대 100건까지 설정할 수 있습니다.
- 하나의 CVM에 여러 보안 그룹에 추가할 수 있으며, 하나의 보안 그룹을 여러 CVM에 동시 연결할 수 있습니다.
- **기본 네트워크**의 CVM이 바인딩한 보안 그룹은 Tencent Cloud의 관계형 데이터베이스(MySQL, MariaDB, SQL Server, PostgreSQL) 및 NoSQL 데이터베이스(Redis, Memcached)의 데이터 패킷을 **필터링할 수 없습니다.** 해당 유형의 인스턴스 트래픽을 필터링하려면 iptables를 사용해야 합니다.
- 할당액에 대한 제한은 아래 표와 같습니다.
<table>
<tr><th>기능 설명</th><th>제한</th></tr>
<tr><td>보안 그룹 개수</td><td>50개/리전</td></tr>
<tr><td>보안 그룹 규칙 수</td><td>100개/인바운드, 100개/아웃바운드</td></tr>
<tr><td>단일 보안 그룹의 연결 가능한 CVM 인스턴스 수</td><td>2,000개</td></tr>
<tr><td>CVM 인스턴스당 연결 가능한 보안 그룹 수</td><td>5개</td></tr>
<tr><td>보안 그룹당 참조 가능한 보안 그룹 ID 수</td><td>10개</td></tr>
</table>

## VPC 관련 제한

| 리소스| 제한(개) |
|---------|---------|
| 각 계정의 리전별 VPC 수 | 20	 |
| 각 VPC 내의 서브넷 수 | 100 |
| 각 VPC에 연결 가능한 기본 네트워크 호스트 수| 100 |
| 각 VPC의 라우팅 테이블 수 | 10 |
| 각 서브넷에 연결된 라우팅 테이블 수 | 1 |
| 각 라우팅 테이블의 라우팅 정책 수 | 50 |
| 각 VPC의 HAVIP 기본 할당 수 | 10 |

