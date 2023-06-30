[ENI](https://intl.cloud.tencent.com/products/eni)(Elastic Network Interface)는 VPC 내의 CVM을 바인딩하는 일종의 탄력적 네트워크 인터페이스로서 여러 CVM 사이에서 자유롭게 마이그레이션할 수 있습니다. ENI는 관리 네트워크 설정 및 신뢰도 높은 네트워크 솔루션의 구축에 큰 도움이 됩니다.

ENI는 VPC, 가용존 및 서브넷 속성을 갖고 있어 동일한 가용존의 CVM만 바인딩할 수 있습니다. 1대의 CVM는은 여러 ENI를 바인딩할 수 있으며 구체적인 바인딩 수량은 CVM 규격에 따라 결정됩니다.

## 개념

 - **프라이머리 ENI 및 세컨더리 ENI:** VPC의 CVM 구축 시 연동 생성된 ENI가 프라이머리 ENI이고, 사용자가 자체 생성한 ENI는 세컨더리 ENI가 됩니다. 그 중 프라이머리 ENI는 바인딩 및 바인딩 해제를 지원하지만, 세컨더리 ENI는 바인딩 및 바인딩 해제를 지원하지 않습니다.
 - **프라이머리 사설 IP:** ENI의 프라이머리 사설 IP는 ENI 생성 시 시스템에서 랜덤으로 할당하거나 사용자가 자체 설정할 수 있습니다. 프라이머리 ENI의 프라이머리 사설 IP는 수정할 수 있으나, 세컨더리 ENI의 프라이머리 사설 IP는 수정할 수 없습니다.
 - **세컨더리 사설 IP:** ENI의 프라이머리 IP 외에 바인딩된 세컨더리 사설 IP는 사용자가 ENI를 생성 또는 편집 시 자체 설정할 수 있으며 바인딩 및 해제할 수 있습니다.
 - **EIP:** ENI의 사설 IP와 하나씩 바인딩해야 합니다.
 - **보안 그룹:** ENI는 하나 또는 하나 이상의 보안 그룹을 바인딩할 수 있습니다.
 - **MAC 주소:** ENI는 전역에서 유니크한 MAC 주소를 보유합니다.

## 응용 시나리오
- **내부 네트워크, 외부 네트워크, 관리 네트워크 격리**:
중요한 비즈니스의 네트워크 배포에는 일반적으로 사설, 공용 및 관리 네트워크 간의 격리가 필요합니다. 다양한 라우팅 및 보안 그룹 정책을 통해 데이터 보안 및 네트워크 격리를 보장할 수 있습니다. 서로 다른 서브넷에 있는 세 개의 ENI를 CVM 서버에 바인딩하여 이러한 격리를 구현할 수 있습니다.
- **신뢰도 높은 애플리케이션 배포:**
시스템 아키텍처의 주요 컴포넌트는 다중 서버 핫 백업을 통해 높은 시스템 가용성을 보장해야 합니다. Tencent Cloud는 유연한 바인딩 및 바인딩 해제를 지원하는 ENI 및 사설 IP를 제공하며, 이를 사용하여 Keepalived 기반 재해 복구 솔루션을 구성하여 주요 컴포넌트의 고가용성을 달성할 수 있습니다.

## 사용 제한

CPU와 메모리 설정에 따라 CVM이 바인딩할 수 있는 ENI 수와 단일 ENI가 바인딩할 수 있는 사설 IP 수는 크게 다르며, ENI 및 단일 ENI IP 할당 수는 아래 표와 같습니다.


<dx-alert infotype="notice" title="">
단일 ENI에 바인딩된 사설 IP의 수는 허용되는 최대 수량을 나타냅니다. EIP 할당량은 이 상한선을 기준으로 제공되지 않고 EIP 할당량 한도를 기준으로 제공됩니다.
</dx-alert>


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
    <td  >8</td>
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
    <td  >8</td>
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
    <th colspan="2" style = "text-align:center;">CPM 2.0</th>
    <td colspan="10" style = "text-align:center;">ENI 바인딩 미지원</td>
   </tr>
  </table>
:::
::: CVM 단일 ENI에 바인딩된 사설 IP 할당량
<table >
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">모델</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">인스턴스 유형</th>
    <th width="86%" colspan="10" style = "text-align:center;">단일 ENI에 바인딩된 사설 IP 할당량</th>
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
    <td >10</td>
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
    <td colspan="10" style = "text-align:center;">ENI 바인딩 미지원</td>
   </tr>
  </table>
:::
</dx-tabs>

## API 개요
ENI 및 CVM과 관련된 API는 다음 표와 같습니다. 더 많은 ENI 관련 작업은 [ENI API Category](https://intl.cloud.tencent.com/document/product/215/15755)를 참고하십시오.

| 인터페이스 기능 | Action ID |  기능 설명 |
|---------|---------|---------|
| ENI 생성 | [CreateNetworkInterface](https://intl.cloud.tencent.com/document/api/215/15818)  |  ENI 생성 |
| ENI 사설 IP 신청  | [AssignPrivateIpAddresses](https://intl.cloud.tencent.com/document/api/215/15813) | ENI 사설 IP 신청 |
| ENI 바인딩 CVM | [AttachNetworkInterface](https://intl.cloud.tencent.com/document/api/215/15819) | ENI 바인딩 CVM |
