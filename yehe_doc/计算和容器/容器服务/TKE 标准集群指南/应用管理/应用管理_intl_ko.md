## 작업 시나리오

본 문서는 TKE 콘솔에서 애플리케이션을 생성, 업데이트, 롤백 및 삭제하는 방법을 설명합니다.

## 관련 설명

애플리케이션 관리는 Kubernetes v1.8 이상 클러스터에만 적용됩니다.

## 작업 단계

### 애플리케이션 생성

1. TKE 콘솔에 로그인하고 왼쪽 사이드바에서 [[Application](https://console.cloud.tencent.com/tke2/helm)]을 클릭합니다.
2. ‘Application’ 페이지 상단에서 애플리케이션을 생성할 클러스터 및 리전을 선택하고 [Create]를 클릭합니다.
3. ‘Create Application’ 페이지에서 다음 그림과 같이 다음 매개변수에 따라 애플리케이션에 대한 기본 정보를 설정합니다.
![](https://main.qcloudimg.com/raw/f636846a914a1ec71c4f6c1870cfa831.png)
주요 매개변수 정보는 다음과 같습니다.
 - **Application Name**: 사용자 정의 애플리케이션 이름을 입력합니다.
 - **Source**: [Marketplace], [TCR Private Repository] 또는 [Third-party Source]를 선택합니다. 자세한 내용은 다음 표를 참고하십시오.
 <table>
 <tr>
	 <th width="17%">소스</th>
	 <th>설정 항목</th>
 </tr>
 <tr>
	 <td>마켓플레이스</td>
	 <td>
	 클러스터 유형 또는 애플리케이션 시나리오별로 Chart를 필터링합니다. 필요한 애플리케이션 패키지 및 Chart 버전을 선택합니다. 매개변수를 편집할 수도 있습니다.
	 </td>
 </tr>
  <tr>
	 <td>TCR 개인 저장소</td>
	 <td><ul class="params">
	 <li>Tcr 인스턴스 이름: 필요에 따라 <a href="https://intl.cloud.tencent.com/document/product/1051/35480">TCR</a> 엔터프라이즈 버전 인스턴스를 선택합니다.</li>
	 <li>네임스페이스: 필요에 따라 지정된 TCR 인스턴스의 네임스페이스를 선택합니다. 네임스페이스가 지정되면 네임스페이스 아래의 Chart가 애플리케이션 목록 페이지에 표시됩니다.</li>
	 <li>Chart 버전 및 매개변수: 해당 버전을 선택합니다. 매개변수를 편집할 수도 있습니다.</li>
	 </ul></td>
 </tr>
  <tr>
	 <td>3rd party 소스</td>
	 <td><ul class="params">
	 <li>Chart 주소: 공식 및 자체 구축 Helm Repo 저장소가 지원됩니다. 반드시 <code>http</code>로 시작하고 <code>.tgz</code>로 이 매개변수의 값은 끝나야 합니다. 이 예시에서 값은 <code>http://139.199.162.50/test/nginx-0.1.0.tgz</code>입니다.</li>
	 <li>유형: [Public] 및 [Private]를 사용할 수 있습니다. 필요에 따라 그 중 하나를 선택하십시오.</li>
	 <li>매개변수: 필요에 따라 매개변수를 편집합니다.</li>
	 </ul></td>
 </tr>
 </table>
4. [Done]을 클릭합니다.

### 애플리케이션 업데이트

1. [TKE Console](https://console.cloud.tencent.com/tke2/helm)로 이동하고 왼쪽 사이드바에서 [Application]을 클릭하여 ‘Application’ 페이지로 이동합니다.
2. ‘Application’ 목록에서 업데이트할 애플리케이션을 찾아 오른쪽에 있는 [Update Application]을 클릭합니다.
3. 표시된 ‘Update Application’ 창에서 필요에 따라 주요 정보를 설정하고 [Done]을 클릭합니다.

### 애플리케이션 롤백

1. [TKE Console](https://console.cloud.tencent.com/tke2/helm)로 이동하고 왼쪽 사이드바에서 [Application]을 클릭하여 애플리케이션 페이지로 이동합니다.
2. ‘Application’ 목록에서 업데이트할 애플리케이션을 클릭하면 애플리케이션 세부 정보 페이지로 이동합니다.
3. 다음 그림과 같이 애플리케이션 세부 정보 페이지에서 [Version History] 탭을 클릭하고 필요한 버전을 찾은 후 오른쪽에 있는 [Roll Back]을 클릭합니다.
   ![](https://main.qcloudimg.com/raw/47fc42e6601945f665fa270c31c8b085.png)
4. 표시된 ‘Rollback Application’ 창에서 다음 그림과 같이 [OK]를 클릭합니다.
   ![](https://main.qcloudimg.com/raw/c0b642ce3f89898c1c59c85911c484d6.png)

### 애플리케이션 삭제

1. [TKE Console](https://console.cloud.tencent.com/tke2/helm)로 이동하고 왼쪽 사이드바에서 [Application]을 클릭하여 애플리케이션 페이지로 이동합니다.
2. ‘Application’ 목록에서 삭제할 애플리케이션을 찾아 오른쪽에서 [Delete]를 선택합니다.
3. 표시된 ‘Delete Application’ 창에서 [OK]를 클릭합니다.
