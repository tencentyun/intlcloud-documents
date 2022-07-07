## CVM 인스턴스 구매 계정의 제한

- 사용자는 Tencent Cloud 계정을 등록해야 합니다. [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985)을 참고하십시오.
- 종량제 클라우드 서버를 생성할 때 시스템은 1시간 동안 호스트 비용을 동결하므로 지불 진행을 위해 계정에 충분한 잔액을 충전하십시오.

## CVM 인스턴스의 이용 제한

- 버츄얼 소프트웨어 설치와 재실행 버츄얼(VMware 또는 Hyper-V을 설치하여 사용하는 경우)은 지원하지 않습니다.
- 현재 사운드 카드 애플리케이션을 사용하거나 외부 하드웨어 디바이스(U 디스크, 외장 하드디스크, U-KEY 등)를 직접 로딩할 수 없습니다.
- 공용망 게이트웨이는 현재 Linux 시스템만 지원합니다.

## CVM 인스턴스의 구매 제한

- 각각의 가용존에서 사용자가 구매할 수 있는 종량제 CVM 인스턴스의 **총 수량**은 30개 또는 60개이며 CVM 구매 페이지의 실제 상황에 따라 정해집니다.
- 자세한 내용은 [CVM 인스턴스 구매 제한](https://intl.cloud.tencent.com/document/product/213/2664)을 참고하십시오.


## 미러 이미지 관련 제한

- 공용 이미지는 현재 사용 제한이 없습니다.
- 사용자 정의 이미지: 리전마다 최대 10개의 사용자 정의 이미지를 지원합니다.
- 공유 이미지: 사용자 정의 이미지는 최대 50개의 Tencent cloud 사용자에게 공유될 수 있으며, 상대방 사용자 계정의 같은 리전 내에서만 공유됩니다. 
- 자세한 내용은 [이미지 유형 제한](https://intl.cloud.tencent.com/document/product/213/4941)을 참고하십시오.


## ENI 관련 제한

CPU와 메모리 설정에 따라 CVM이 바인딩할 수 있는 ENI 수와 단일 ENI가 바인딩할 수 있는 개인 IP 수는 크게 다르며, ENI 및 단일 ENI IP 할당 수는 아래 표와 같습니다.
>! 단일 ENI의 바인딩 IP 수량은 ENI로 바인딩할 수 있는 IP 수의 최대 수량을 의미하는 것으로 최대 수량에 따른 EIP 할당은 보장되지 않으며, 계정의 EIP 할당은 [EIP 사용 제한](https://intl.cloud.tencent.com/document/product/213/5733)에 따라 제공됩니다.

<dx-tabs>
::: CVM이 지원하는 ENI 바인딩 할당량
<table >
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">모델</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">인스턴스 유형</th>
    <th width="86%" colspan="10" style = "text-align:center;">ENI 할당량</th>
   </tr>
   <tr >
    <th style = "text-align:center;">CPU: 1코어</th>
    <th style = "text-align:center;">CPU: 2코어</th>
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
    <th rowspan="2" style = "text-align:center;">고IO형</th>
    <th style = "text-align:center;">고IO형 IT5</th>
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
    <th  style = "text-align:center;">고IO형 IT3</th>
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
    <th style = "text-align:center;">컴퓨팅 네트워크 확장형 CN3</th>
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
    <th style = "text-align:center;" >컴퓨팅형 C2</th>
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
    <th  rowspan="6" style = "text-align:center;">GPU 모델</th>
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
    <td  >8</td>
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
    <td  >8</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">FPGA 모델</th>
    <th style = "text-align:center;">FPGA 가속형 FX4</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >8</td>
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
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">빅 데이터형 D1</th>
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
    <th colspan="2" style = "text-align:center;">베어 메탈 클라우드 서버</th>
    <td colspan="10" style = "text-align:center;">ENI 바인딩 미지원</td>
   </tr>
  </table>
:::
::: CVM 단일 ENI에 바인딩된 개인 IP 할당량
<table >
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">모델</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">인스턴스 유형</th>
    <th width="86%" colspan="10" style = "text-align:center;">단일 ENI에 바인딩된 개인 IP 할당량</th>
   </tr>
   <tr >
    <th style = "text-align:center;">CPU: 1코어</th>
    <th style = "text-align:center;">CPU: 2코어</th>
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
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td >-</td>
    <td  >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준 스토리지 확장형 S5se</th>
    <td >-</td>
    <td >-</td>
    <td  >20</td>
    <td >-</td>
    <td  >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 SA2</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td >-</td>
    <td  >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 S4</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td >-</td>
    <td  >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">표준 네트워크 최적화형 SN3ne</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td >-</td>
    <td  >20</td>
    <td >-</td>
    <td  >30</td>
    <td >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 S3</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
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
    <td  >10</td>
    <td >메모리=8G: 10<br/>메모리=16G: 20</td>
    <td >-</td>
    <td  >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">표준형 S2</th>
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
    <th rowspan="2" style = "text-align:center;">고IO형</th>
    <th style = "text-align:center;">고IO형 IT5</th>
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
    <th  style = "text-align:center;">고IO형 IT3</th>
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
    <th style = "text-align:center;">컴퓨팅 네트워크 확장형 CN3</th>
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
    <th style = "text-align:center;" >컴퓨팅형 C2</th>
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
    <td  >30</td>
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
    <td  >30</td>
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
    <td  >30</td>
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
    <th colspan="2" style = "text-align:center;">베어 메탈 클라우드 서버</th>
    <td colspan="10" style = "text-align:center;">ENI 바인딩 미지원</td>
   </tr>
  </table>
:::
</dx-tabs>


## 대역폭 관련 제한

- 아웃바운드 대역폭 최댓값(다운스트림 대역폭): 
 - 2020년 2월 24일 00:00 이후에 생성한 기기의 경우, 다음의 규칙을 따릅니다.
<table>
<tr><th rowspan="2">네트워크 청구 모드</th><th colspan="2">인스턴스</th><th rowspan="2">대역폭 최댓값 설정 범위(Mbps)</th></tr>
<tr><th style="width: 18.5607%;">인스턴스 과금 방식</th><th style="width: 24.5814%;">인스턴스 구성</th></tr>
<tr><td>트래픽 과금</td><td>종량제 인스턴스</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>대역폭 과금</td><td>종량제 인스턴스</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>공유 대역폭</td><td colspan="2">ALL</td><td>0 - 2000</td></tr>
</table>

 - 2020년 2월 24일 00:00 이전에 생성한 기기의 경우, 다음의 규칙을 따릅니다. 
<table>
<tr><th rowspan="2">네트워크 청구 모드</th><th colspan="2">인스턴스</th><th rowspan="2">대역폭 최댓값 설정 범위(Mbps)</th></tr>
<tr><th>인스턴스 과금 방식</th><th>인스턴스 구성</th></tr>
<tr><td>트래픽 과금</td><td>종량제 인스턴스</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>대역폭 과금</td><td>종량제 인스턴스</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>공유 대역폭</td><td colspan="2">ALL</td><td>0 - 2000</td></tr>
</table>


- 인바운드 대역폭 최댓값(다운링크 대역폭): 
	- 사용자가 구매한 고정 대역폭이 10Mbps보다 큰 경우, Tencent Cloud는 구매한 대역폭과 동일한 인바운드 대역폭을 할당합니다. 
	- 사용자가 구매한 고정 대역폭이 10Mbps보다 낮은 경우, Tencent Cloud는 10Mbps 아웃바운드 대역폭을 할당합니다.

## 디스크 관련 제한

<table>
	<tr><th>제한 유형</th><th>제한 설명</th></tr>
	<tr><td>CBS 능력</td><td>2018년 5월부터 CVM과 함께 구매하는 데이터 디스크는 모두 엘라스틱 CBS로 CVM에서 언마운트한 후 다시 마운트할 수 있습니다. 해당 기능은 모든 <a href="https://intl.cloud.tencent.com/document/product/213/35071">가용존</a>에서 사용할 수 있습니다. </td></tr>
	<tr><td>CBS 성능 제한</td><td> I/O 성능이 동시에 적용됩니다. </br>예를 들어 1TB의 SSD CBS가 최대 랜덤 IOPS 26,000에 도달한다면 읽기 IOPS와 쓰기 IOPS 모두 해당 값에 도달할 수 있음을 의미합니다. 동시에 여러 성능 제한으로 인하여 해당 예시에서 block size가 4KB/8KB인 I/O를 사용하면 IOPS 최대치에 도달할 수 있지만, block size가 16KB인 I/O를 사용하면 IOPS 최대치에 도달할 수 없습니다(처리량은 260MB/s의 제한에 도달함).</td></tr>
	<tr><td>단일 CVM이 마운트할 수 있는 엘라스틱 CBS 수량</td><td>은 최대 20블록입니다. </td></tr>
	<tr><td>단일 리전의 스냅샷 할당량</td><td>64 + 리전 내 CBS 수량 * 64(개). </td></tr>
	<tr><td>CBS 마운트 가능 CVM 제한</td><td>CVM과 CBS가 반드시 동일 가용존에 있어야 합니다. </td></tr>
	<tr><td>스냅샷 롤백 제한</td><td>스냅샷 데이터는 스냅샷을 생성한 소스 CBS로만 롤백할 수 있습니다. </td></tr>
	<tr><td>스냅샷 생성 CBS 유형 제한</td><td>데이터 디스크 스냅샷으로만 새로운 엘라스틱 CBS를 생성할 수 있습니다. </td></tr>
	<tr><td>스냅샷 생성 CBS 크기 제한</td><td>스냅샷으로 생성한 새로운 CBS의 용량은 반드시 스냅샷 소스 CBS의 용량과 같거나 커야 합니다. </td></tr>
</tr>
</table>



## 보안 그룹 관련 제한

- 보안 그룹은 리전을 구분하고 한 대의 CVM은 동일한 리전 내의 보안 그룹만 바인딩합니다.
- 보안 그룹은 [네트워크 환경](https://intl.cloud.tencent.com/document/product/213/5227)의 모든 CVM 인스턴스에 적용됩니다.
- 사용자는 리전마다 항목별로 최대 50개의 보안 그룹을 설정할 수 있습니다.
- 하나의 보안 그룹의 인바운드 또는 아웃바운드의 액세스 정책으로 각각 최대 100건까지 설정할 수 있습니다.
- 하나의 CVM은 여러 개의 보안 그룹에 추가할 수 있고 하나의 보안 그룹은 여러 개의 CVM을 동시에 연결할 수 있습니다.
- **기본 네트워크** 내 CVM에 바인딩된 보안 그룹은 Tencent Cloud의 인/아웃 관계형 데이터베이스(MySQL, MariaDB, SQL Server, PostgreSQL), NoSQL 데이터베이스(Redis, Memcached)의 데이터 패키지를 **필터링할 수 없습니다.** 이러한 인스턴스의 트래픽을 필터링하려면 iptables 사용 또는 방화벽 제품 구매를 통해 구현할 수 있습니다.
- 할당량에 대한 제한은 다음과 같습니다.
<table>
<tr><th>기능 설명</th><th>제한</th></tr>
<tr><td>보안 그룹 개수</td><td>50개/리전</td></tr>
<tr><td>보안 그룹 규칙 수</td><td>100건/인바운드, 100건/아웃바운드</td></tr>
<tr><td>단일 보안 그룹의 연결 가능 CVM 인스턴스 수</td><td>2,000개</td></tr>
<tr><td>각 CVM 인스턴스의 연결 가능 보안 그룹 개수</td><td>5개</td></tr>
<tr><td>각 보안 그룹의 참조 가능 보안 그룹 ID 개수</td><td>10개</td></tr>
</table>

## VPC 관련 제한

| 리소스| 제한(개) | 
|---------|---------|
| 각 계정, 각 리전 내의 VPC 개수 | 20 | 
| 각 VPC 내의 서브넷 수 | 100 |
| 각 VPC가 지원하는 기본 네트워크 호스트 연결 개수| 100 |
| 각 VPC 내의 라우팅 테이블 개수 | 10 |
| 각 서브넷의 라우팅 테이블 연결 개수 | 1 |
| 각 라우팅 테이블의 라우팅 정책 수 | 50 |
| 각 VPC의 HAVIP 기본 쿼터수 | 10 |

