
TKE(Tencent Kubernetes Engine) 클러스터는 각 사용자의 각 리전에 고정 할당량을 분배합니다.

### TKE 할당량 제한

다음은 각 사용자가 구매할 수 있는 컨테이너 클러스터의 수를 설명합니다. 클러스터가 더 필요한 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS) 하십시오.
>!2019년10월21일부터 클러스터에서 지원되는 최대 노드 수가 5,000개로 증가되었습니다.
>


<table>
	<tr>
	<th>할당량 항목</th>
	<th>기본값</th>
	<th>확인 위치</th>
	<th>할당량 추가 지원 여부</th>
	</tr>
	<tr>
	<td>단일 리전의 클러스터</td>
	<td>5</td>
	<td rowspan=5><a href="https://console.cloud.tencent.com/tke2">TKE 개요 페이지의 오른쪽 하단 섹션</a></td>
	<td rowspan=5>Yes</td>
	</tr>
	<tr>
	<td>단일 클러스터의 노드</td>
	<td>5000</td>
	</tr>
	<tr>
	<td>단일 리전의 이미지 네임스페이스</td>
	<td>10</td>
	</tr>
	<tr>
	<td>단일 리전의 이미지 레지스트리</td>
	<td>500</td>
	</tr>
	<tr>
	<td>단일 이미지의 이미지 태그</td>
	<td>100</td>
	</tr>
</table>



### CVM 할당량 제한

Tencent Cloud TKE용으로 구매한 CVM 인스턴스에는 CVM 구매 한도가 적용됩니다. 자세한 내용은 [구매 제한](https://intl.cloud.tencent.com/document/product/213/2664)을 참고하십시오. 사용자가 기본적으로 구매할 수 있는 최대 CVM 수는 다음 표를 참고하십시오. 항목에 대해 더 높은 할당량이 필요한 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM&level3_id=156&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E8%B4%AD%E4%B9%B0%E9%85%8D%E9%A2%9D%E6%8F%90%E5%8D%87%E7%94%B3%E8%AF%B7&queue=1&scene_code=12701&step=2) 하시기 바랍니다.

<table>
	<tr>
	<th>할당량 항목</th>
	<th>기본값</th>
	<th>확인 위치</th>
	<th>할당량 추가 지원 여부</th>
    </tr>
	<td>단일 가용존 사용량 과금 CVM</td>
	<td>30 - 60</td>
	<td><a href="https://console.cloud.tencent.com/cvm/overview">CVM 인스턴스 페이지-각 리전의 리소스</a></td>
	<td>Yes</td>
</table>




### 클러스터 설정 제한
>?클러스터 설정은 클러스터 크기를 제한하며 현재 수정할 수 없습니다.
>

| 설정 항목 | 주소 범위 | 영향 범위 | 확인 위치 | 수정 지원 여부 |
| ----- | ----- | ---- | --------- | ---------- |
| VPC 네트워크-서브넷 | 사용자 | 추가할 수 있는 노드 수 |[VPC subnet list page for the cluster - Available IP address](https://console.cloud.tencent.com/vpc/subnet)| <ul class="params"><li>No</li><li>Yes, 새 서브넷 생성 가능</li></ul>|
| 컨테이너 IP 범위의 CIDR 블록 |사용자 |<ul class="params"><li>클러스터당 최대 노드</li><li>클러스터당 최대 service</li><li>노드당 최대 Pod</li></ul> |클러스터 기본 정보 페이지-컨테이너 IP 주소 범위 | No |

<style>
	.params{margin-bottom:0px !important;}
</style>


### 리소스 할당량 제한




2021년 1월 13일부터 TKE는 노드수(nodeNum)가 5개 미만(0 < nodeNum ≤ 5)이거나 노드가 5개 이상 20개 미만(5 < nodeNum < 20)인 클러스터의 네임스페이스에 리소스 할당량 세트를 자동으로 적용합니다. 이러한 할당량은 클러스터에 배포된 애플리케이션의 잠재적 Bug로 인한 클러스터 제어 플레인이 불안정하지 않도록 보호하는 데 사용되며, 제거할 수 없습니다.

다음 명령을 실행하여 할당량을 확인할 수 있습니다.
```
kubectl get resourcequota tke-default-quota -o yaml
```

지정된 네임스페이스의 `tke-default-quota` 객체를 확인해야 하는 경우 `--namespace` 옵션을 추가하여 네임스페이스를 지정할 수 있습니다.

구체적인 할당량 한도는 다음과 같습니다.
                                  

<table>
<thead>
<tr>
<th align="left">클러스터 규모</th>
<th align="left">할당량 제한</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">0 &lt; nodeNum &le; 5</td>
<td align="left">총 Pod: 4000, configMap: 3000, CustomResourceDefinition(CRD): 4000 </td>
</tr>
<tr>
<td>5 &lt; nodeNum &lt; 20</td>
<td>총 Pod: 8000, configMap: 6000, CustomResourceDefinition(CRD): 8000</td>
</tr>
<tr>
<td> 20 &le; nodeNum </td>
<td>무제한</td>
</tr>
</tbody></table>






할당량을 늘리려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하여 신청할 수 있습니다.


