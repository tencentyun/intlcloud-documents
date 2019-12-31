
<span id = "celueyufa"></span>
### 정책 구문
CAM 정책:

```
{	 
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"], 
               "condition": {"key":{"value"}} 
           } 
       ] 
} 

```
- **version**은 필수 항목입니다. 현재는 오직 “2.0”만 허용합니다.
- **statement**는 하나 또는 여러 개의 권한의 자세한 정보를 기술하는 데 사용합니다. 이 요소에는 effect, action, resource, condition 등의 기타 여러 요소의 권한 또는 권한 집합이 포함됩니다. 하나의 정책에는 하나의 statement 요소만 가지고 있습니다.
 1. **action**은 허용 또는 거절의 작업을 기술하는 데 사용합니다. action은 API(접두사 name으로 표시) 또는 기능 집합(특정한 API 구성, 접두사 permid로 표시)이 가능합니다. 이 요소는 필수 항목입니다.
 2. **resource**는 권한 부여의 구체적인 데이터를 기술합니다. resource는 6단식 기술을 사용하며, 모든 제품마다 리소스의 정보 정의의 차이가 있습니다. 리소스 정보를 어떻게 지정할 지에 대한 것은 작성한 리소스 선언에 대한 제품 문서를 참조하십시오. 이 요소는 필수 항목입니다.
 3. **condition**은 정책의 효력이 발생하는 규제 조건을 기술합니다. condition에는 오퍼레이터, 작업 키와 작업 값 구성이 포함됩니다. 작업 값은 시간, IP 주소 등의 정보를 포함합니다. 어떤 서비스는 조건에 기타 값을 지정하는 것을 허용합니다. 이 요소는 필수 항목입니다.
 4. **effect**는 선언으로 발생한 결과가 “허용”인지 “명시적 거절”인지 기술합니다. allow(허용) 및 deny(명시적 거절) 두 가지 상황을 포함합니다. 이 요소는 필수 항목입니다.

<span id = "caozuo"></span>
### CVM의 작업

CAM 정책 명령어에서 CAM을 지원하는 어떤 서비스로부터 임의의 API 작업을 지정할 수 있습니다. CVM에 대하여 name/cvm:은 접두사 API입니다. 예를 들어 name/cvm:RunInstances 또는 name/cvm:ResetInstancesPassword가 있습니다.
만약 단일 명령어에 여러 개의 작업을 지정하고 싶을 경우, 다음과 같이 쉼표를 사용하여 작업을 분리하십시오.
```
"action":["name/cvm:action1","name/cvm:action2"]
```
와일드카드를 사용해서도 여러 항목의 작업을 지정할 수 있습니다. 예를 들어, 다음과 같이 표시해 명칭이 단어 “Describe”로 시작하는 모든 작업을 지정할 수 있습니다.
```
"action":["name/cvm:Describe*"]
```
만약 CVM의 모든 작업을 지정할 경우, 다음과 같이 * 와일드카드를 사용하십시오.
```
"action"：["name/cvm:*"]
```

<span id = "ziyuanlujing"></span> 
### CVM의 리소스 경로
각각의 CAM 정책 명령어는 모두 자신에게 적용되는 리소스가 있습니다.
리소스 경로의 일반 형식은 아래와 같습니다.
```
qcs:project_id:service_type:region:account:resource
```
**project_id**: 프로젝트 정보를 기술하는 것은 CAM 초기 로직을 호환하기 위한 것이므로 입력하지 않아도 됩니다.
**service_type**: CVM과 같은 제품 약칭
**region**: bj와 같은 리전 정보
**account**: uin/164256472와 같은 리소스 소유자의 계정 정보
**resource**: instance/instance_id1 또는 instance/*와 같은 각 제품의 구체적인 리소스 정보

예를 들어, 명령 중의 특정 인스턴스(i-15931881scv4)를 사용하여 아래와 같이 리소스를 지정할 수 있습니다.
```
"resource":[ "qcs::cvm:bj:uin/164256472:instance/i-15931881scv4"]
```
* 와일드카드를 사용할 경우에도 아래와 같이 특정 계정의 모든 인스턴스를 지정할 수 있습니다.
```
"resource":[ "qcs::cvm:bj:uin/164256472:instance/*"]
```

모든 리소스를 지정해야 하거나 특정 API 작업이 리소스 권한을 지원하지 않을 경우, 아래와 같이 Resource 요소에서 * 와일드카드를 사용하십시오.
```
"resource": ["*"]
```
단일 명령어에 동시에 여러 리소스를 지정하고 싶을 경우, 쉼표를 이용해 분리하십시오. 다음은 두 개의 리소스를 지정한 예시를 보여 줍니다.
```
"resource":["resource1","resource2"]
```
아래의 표는 CVM이 사용할 수 있는 리소스와 대응하는 리소스의 기술 방법을 서술하였습니다.
<style>
table th:nth-of-type(1){
width:250px;
}
table th:nth-of-type(2){
width:500px;
}
</style>
아래의 표에서 $가 접두사인 단어는 모두 별명입니다.
- 이중, project는 프로젝트 ID를 대신 지칭합니다.
- 이중, region은 리전을 대신 지칭합니다.
- 이중, account는 계정 ID를 대신 지칭합니다.

| 리소스 | 권한 부여 정책 중 리소스 기술 방법 |
|-------|-------|
|인스턴스|  qcs::cvm:$region:$account:instance/$instanceId|
|키|  qcs::cvm:$region:$account:keypair/$keyId|
|VPC|  qcs::vpc:$region:$account:vpc/$vpcId|
|서브넷|   qcs::vpc:$region:$account:vpc/$vpcId|
|시스템 디스크|  qcs::cvm:$region:$account:systemdisk/*|
|미러 이미지|   qcs::cvm:$region:$account:image/*|
|서브넷|  qcs::vpc:$region:$account:subnet/$subnetId|
|데이터 디스크|  qcs::cvm:$region:$account:datadisk/*|
|보안 그룹|  qcs::cvm:$region:$account:sg/$sgId|
|EIP|  qcs::cvm:$region:$account:eip/*|

 

<span id = "tiaojianmiyue"></span>
### CVM의 조건 키
정책 명령어에서 정책 효력 발생 시간 조건을 선택적 지정으로 제어할 수 있습니다. 모든 조건에는 하나 또는 다중 키 값의 쌍이 포함됩니다. 조건부 키는 대소문자 구분이 없습니다.

- 만약 여러 조건을 지정했거나 단일 조건에서 여러 키를 지정할 경우, 논리 AND 연산을 통해 평가가 진행됩니다.
- 단일 조건에서 다중 값을 가진 키를 지정할 경우, 논리 OR 연산을 통해 평가를 진행합니다. 반드시 모든 조건이 매칭되어야 권한이 부여됩니다.
아래의 표는 CVM을 서버에 특정하기 위한 조건부 키에 대해 기술합니다.
<table class="tableblock frame-all grid-all spread">
<colgroup>
<col style="width: 25%;">
<col style="width: 25%;">
<col style="width: 50%;">
</colgroup>
<thead>
<tr>
<th class="tableblock halign-left valign-top">조건부 키</th>
<th class="tableblock halign-left valign-top">참조 유형</th>
<th class="tableblock halign-left valign-top">키 값 쌍</th>
</tr>
</thead>
<tbody>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:instance_type</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:instance_type=<code>instance_type</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p> 이중에서 <code>instance_type</code>는 S1.SMALL1과 같이 인스턴스 유형을 지칭합니다.</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:image_type</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:image_type=<code>image_type</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p> 이중에서 <code>image_type</code>는 IMAGE_PUBLIC과 같이 미러 이미지 유형을 지칭합니다.</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>vpc:region</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>vpc:region=<code>region</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p>이중에서 <code>region</code>는 ap-guangzhou와 같이 리전을 지칭합니다.</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:disk_size</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>Integer</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:disk_size=<code>disk_size</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p> 이중에서 <code>disk_size</code>는 500과 같이 디스크 크기를 지칭합니다.</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:disk_type</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm_disk_type=<code>disk_type</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p>이중에서 <code>disk_type</code>는 CLOUD_BASIC과 같이 디스크 유형을 지칭합니다.</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:region</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:region=<code>region</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p>이중에서 <code>region</code>는 ap-guangzhou와 같이 리전을 지칭합니다.</p>
</li>
</ul>
</div></div></td>
</tr>
</tbody>
</table>
