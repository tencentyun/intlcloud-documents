온라인 마이그레이션은 시스템 다운타임 없이 소스 서버 또는 가상 머신의 시스템 및 애플리케이션을  IDC 또는 기타 클라우드 플랫폼에서 Tencent Cloud로 마이그레이션 또는 동기화하는 마이그레이션 방식입니다.
Tencent Cloud에서 제공하는 마이그레이션 툴인 go2tencentcloud를 사용하면 이미지를 생성, 업로드 및 가져올 필요 없이 소스 서버의 모든 시스템과 애플리케이션을 대상 CVM으로 직접 마이그레이션할 수 있습니다. 클라우드 배포, 클라우드 간 마이그레이션, 계정 간 또는 리전 간 마이그레이션, 하이브리드 클라우드 배포에 대한 기업의 비즈니스 요구 사항을 충족할 수 있습니다.

<dx-alert infotype="explain" title="">
본문에서 언급하는 소스 서버는 타사 클라우드 플랫폼의 물리적 서버, 가상 머신 또는 클라우드 서버일 수 있습니다. 소스 서버는 AWS, Google Cloud Platform, VMware, Alibaba Cloud 또는 Huawei Cloud와 같은 가상 머신 플랫폼이 포함되지만 이에 국한되지 않습니다.
</dx-alert>



## 적용 시나리오

온라인 마이그레이션은 다음 시나리오에 적합합니다(포함하지만 국한되지 않음).
- IT 아키텍처 클라우드화
- 하이브리드 클라우드 아키텍처 배포
- 클라우드 간 마이그레이션
- 계정 간 또는 리전 간 마이그레이션

## 오프라인 마이그레이션과의 차이점

오프라인 마이그레이션에서는 소스 서버의 시스템 디스크 또는 데이터 디스크용 이미지를 생성한 다음 이미지를 CVM(Cloud Virtual Machine) 또는 CBS(Cloud Block Storage)로 마이그레이션해야 합니다. 온라인 마이그레이션은 이미지를 생성할 필요가 없습니다. 소스 서버에서 마이그레이션 도구를 실행하여 대상 CVM으로 마이그레이션할 수 있습니다.

## 마이그레이션 시작
온라인 마이그레이션에는 두 가지 방법을 사용할 수 있습니다. 필요에 따라 적절한 것을 선택할 수 있습니다.
<table class="tg">
<thead>
  <tr>
    <th width="25%">마이그레이션 방식</th>
    <th width="25%">개요</th>
    <th width="25%">적용 시나리오</th>
    <th width="25%">특징</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky"><a href=" https://www.tencentcloud.com/document/product/213/55046">온라인 마이그레이션: 클라이언트에서 마이그레이션 소스 가져오기</a></td>
    <td class="tg-0pky">소스 인스턴스에 로그인한 후 도구를 실행하여 마이그레이션 소스를 가져온 다음 콘솔에서 마이그레이션 작업 생성 및 진행 </td>
    <td class="tg-0pky"><li>공중망을 통한 마이그레이션&amp;사설망을 통한 마이그레이션<br></li><li>다른 클라우드 플랫폼에서 Tencent Cloud로 마이그레이션</li><li>고객 IDC에서 Tencent Cloud로 마이그레이션</li></td>
    <td class="tg-0pky">높은 호환성</td>
  </tr>
  <tr>
    <td class="tg-0pky"><a href="https://intl.cloud.tencent.com/document/product/213/53265">온라인 마이그레이션: 콘솔 원클릭 마이그레이션</a></td>
    <td class="tg-0pky">콘솔에 로그인하여 ID 인증을 마친 후 마이그레이션 소스를 빠르게 가져온 다음 마이그레이션 작업 생성</td>
    <td class="tg-0pky"><li>소스 서버에 로그인할 필요 없음</li><li>공중망을 통한 마이그레이션</li><li>클라우드 간 마이그레이션: 소스 인스턴스가 Alibaba Cloud에 있는 시나리오에 적용 가능</li></td>
    <td class="tg-0pky">원클릭 일괄 마이그레이션</td>
  </tr>
</tbody>
</table>

## FAQ

자세한 내용은 [서버 마이그레이션 관련 FAQ](https://intl.cloud.tencent.com/document/product/213/32395)를 참고하십시오.
