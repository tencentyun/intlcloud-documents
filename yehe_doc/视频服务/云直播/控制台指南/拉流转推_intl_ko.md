라이브 스트리밍 소스에 스트림 푸시 기능이 없거나 주문형 비디오를 스트리밍하려는 경우 릴레이 기능을 사용하여 기존 라이브 스트리밍 소스 또는 비디오에서 콘텐츠를 신속하게 가져온 다음 대상 주소로 전달할 수 있습니다. 스트림을 직접 푸시할 필요가 없습니다.
![](https://main.qcloudimg.com/raw/8f0b044ce2104efdc1ed835287b9b683.png)

## 전제 조건
- [Tencent Cloud CSS 서비스](https://intl.cloud.tencent.com/product/css) 활성화 및 CSS 콘솔 로그인을 완료해야 합니다.
- [푸시 도메인 이름](https://intl.cloud.tencent.com/document/product/267/35970)이 추가되어 있어야 합니다.

## 주의 사항
- 릴레이 작업은 최대 **20개**까지 생성할 수 있습니다.
- 릴레이 기능은 **릴레이 작업 시간**을 기준으로 과금됩니다. 자세한 내용은 [릴레이](https://intl.cloud.tencent.com/document/product/267/41059)를 참고하십시오.
- CSS는 콘텐츠를 풀링하고 릴레이하는 역할만 담당합니다.**콘텐츠가 승인되었으며 관련 법률 및 규정을 준수하는지 확인하십시오. 저작권 침해 또는 법률 또는 규정 위반 발생 시 CSS는 귀하에 대한 서비스를 중단하고 법적 책임을 물을 권리가 있습니다**.
- 로컬 릴레이 모드가 **2022년 11월 23일 00:00**부터 유료화되었습니다. 자세한 내용은 [부가 기능](https://www.tencentcloud.com/document/product/267/51555)을 참고하십시오.

[](id:create)
## 작업 생성
1. **CSS 툴킷** > **[릴레이](https://console.cloud.tencent.com/live/tools/relay)**를 선택하고 **작업 생성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f41c7a329a9fed7a901bca252a973f35.png)
2. 기본 정보를 입력합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d10fb06aba921e27791441a112039586.png)

<table>
<tr><th width="15%">설정 항목</th><th>설정 설명</th></tr>
<tr>
<td>작업 설명</td>
<td>작업에 대한 설명.</td>
</tr><tr>
<td>작업 시간</td>
<td>기본 설정: <code>현재 시간</code>에서 <code>현재 시간 + 24시간</code>까지. 선택 가능한 작업 시간: 현재 시간부터 1년 이내의 임의의 시간 ~ 7일 이내.<br>현재 시간이 2022년 03월 24일 11:50:01이라고 가정하면 <ul style="margin:0"><li/>선택 가능한 시간은 2022년 3월 24일 11:50:01부터 2022년 03월 30일 11:50:01까지 입니다. <li/>종료 시간은 2022년 03월 30일 11:50:01을 초과할 수 없습니다. </ul></td>
</tr><tr>
<td>이벤트 콜백 알림</td>
<td>릴레이 작업 이벤트를 수신할 콜백 주소를 입력합니다. </td>
</tr></table>

3. 콘텐츠 소스 정보를 입력하고 리전을 선택합니다.
    - 리전: 랜덤(중국 대륙), 화북 지역(베이징), 화동 지역(상하이), 화남 지역(광저우), 아시아 태평양 동남부(싱가포르), 아시아 태평양 동남부(방콕), 동북아(서울), 남아시아(뭄바이), 홍콩·마카오·대만 지역(중국홍콩).
    - 랜덤(중국 대륙) 리전을 선택하면 시스템이 가까운 리전을 자동 할당합니다.
4. 콘텐츠 유형은 **라이브 스트리밍**, **사용자 지정 비디오 경로** 또는 **이미지**를 선택할 수 있습니다.
 - **라이브 스트리밍**:
    - 라이브 스트리밍 URL을 입력합니다(**1개**만 입력 가능).
   ![](https://qcloudimg.tencent-cloud.cn/raw/6795d964f41e63fa90f0c09e3ddcf060.png)
    - 백업 활성화를 선택하면 시스템이 프라이머리 소스에서 콘텐츠를 가져오지 못하는 경우 자동으로 백업 소스로 전환됩니다. 프라이머리가 복구된 후 수동으로 다시 전환해야 합니다. 백업 소스는 단일 비디오 루프만 지원됩니다.
 - **사용자 지정 비디오 경로**:
    - **복수**(최대 30개)의 소스 URL을 입력할 수 있습니다.
    - **반복**을 선택하여 재생을 무한정 반복하거나 **지정**을 선택하여 재생 횟수(1 ~ 100)를 지정합니다.
    - 로컬 모드를 활성화하면 MP4 형식의 소스가 릴레이되기 전에 로컬 노드에 캐시되어 더 매끄럽고 안정적인 재생을 보장합니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/cc30dc26f64d17f90f3e4fc76d2d9cd0.png)
 - **이미지**:
    - 이미지를 업로드하거나 이미지 URL을 입력합니다. **미리보기**를 클릭하여 이미지를 미리 볼 수 있습니다.
    - JPEG, JPG, PNG 또는 BMP 형식의 이미지가 지원됩니다. 이미지 URL을 입력하면 이미지 크기에 제한이 없습니다. 이미지를 업로드하는 경우 2M를 초과할 수 없습니다.
 ![](https://qcloudimg.tencent-cloud.cn/raw/506182c6890e8f357177c78b190ff6db.png) 

>? 
>- 재생 횟수가 지정된 값에 도달하거나 작업이 종료 시간에 도달하면 시스템은 릴레이 작업을 중지합니다.
>- 작업 수정 후:
   - 재생 횟수만 변경하면 새로운 값에 따라 재생합니다. 현재 재생 작업이 있을 경우 1회로 기록됩니다.
   - 원본 URL과 재생 횟수를 모두 변경하면 새 구성이 적용된 후(즉시 또는 현재 재생이 끝난 후) 횟수가 1부터 시작됩니다.
   - destination URL을 변경하면 재생 횟수가 초기화됩니다.
>- 로컬에 캐시된 MP4 파일을 릴레이하면 파일이 릴레이된 시간에 따라 부가 기능 요금이 부과됩니다.

5. 콘텐츠를 수신할 destination URL을 입력합니다.
   1. **주소 생성기**를 클릭하여 URL 생성 페이지로 이동합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/9724d77727e21ba1798485d03d6e3246.png)
   2. 기존 푸시 도메인 이름을 선택하고 Appname, StreamName 및 만료 시간을 입력합니다. **확인**을 클릭하면 푸시 스트림 주소가 생성되며, 해당 주소는 destination 주소란에 자동으로 입력됩니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/b1b6f0b832bacb15b281d71fc653afb0.png)
>! 주소 만료 기한은 작업 종료 시간 이후로 설정되어야 합니다. 작업이 시작된 후 타깃 푸시 스트림 주소를 업데이트하면 작업이 중단되고 다시 푸시 됩니다.

6. 워터마크 구성 옆의 ![](https://qcloudimg.tencent-cloud.cn/raw/b64d8a4343b3a1e340db3adb9002db60.png)을(를) 클릭하여 워터마크를 활성화할 수 있습니다. PNG, JPG 또는 GIF 형식의 워터마크 이미지가 지원됩니다.
- 워터마크 유형을 선택합니다.
    - **사용자 지정 워터마크 URL**을 선택한 경우 사용할 워터마크 이미지의 URL을 입력하고 미리보기를 클릭하여 미리보기 합니다.
    - **이미지 업로드**를 선택한 경우 이미지 선택을 클릭하여 워터마크 이미지를 업로드합니다. 더 나은 시각적 효과를 위해 PNG 형식의 투명한 이미지 사용을 권장합니다. 이미지 크기는 2M를 초과할 수 없습니다.
- 다음 두 가지 방법 중 하나로 워터마크 이미지를 배치합니다.
    - 워터마크 이미지를 드래그합니다.
    - X 축 및 Y 축 값을 설정합니다.
    - **저장**을 클릭하면 워터마크 구성이 완료됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a58673819adbc0d2dff5ecf25406816f.png)
>? 
>- 콘텐츠 유형을 이미지로 선택한 경우 워터마크 설정이 지원되지 않습니다.
>- 워터마크를 사용하면 [트랜스 코딩 요금](https://intl.cloud.tencent.com/document/product/267/39604)이 발생합니다.

7. 입력 완료 후 **저장**을 클릭합니다.

## 작업 관리
[](id:view)
### 작업 세부 사항 보기
[작업 리스트](https://console.cloud.tencent.com/live/tools/relay)에서 조회할 릴레이 작업을 선택하고 해당 '작업 비고/ID'를 클릭하면 오른쪽 팝업 창에 해당 작업의 작업 세부 정보가 표시됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c2bad33a6a735a218fa79b98f3738275.png)

>? 작업 세부 정보 아래에 있는 편집, 입력 소스 전환, 재시작 및 비활성화 버튼을 클릭할 수 있습니다.

### 작업 상태 조회
[작업 리스트](https://console.cloud.tencent.com/live/tools/relay)에서 작업의 작업 상태를 볼 수 있으며, 조회할 릴레이 작업을 선택하고 해당 '작업 비고/ID'를 클릭하면 오른쪽의 팝업 창에는 작업의 실행 상태가 표시됩니다.

![](https://qcloudimg.tencent-cloud.cn/raw/cd498cb1fd678e39b0942383c278e82b.png)

<table>
<thead><tr><th>작업 상태</th><th>실행 상태</th><th>의미</th></tr></thead>
<tbody><tr>
<td>시작되지 않음</td>
<td>비활성화</td>
<td>작업이 아직 시작되지 않았습니다.</td>
</tr><tr>
<td rowspan=2>유효함</td>
<td>활성화</td>
<td>작업이 시작되었으며 예정대로 실행됩니다.</td>
</tr><tr>
<td>비활성화</td>
<td>작업이 시작되었지만 예정대로 실행되지 않습니다.</td>
</tr><tr>
<td>비활성화됨</td>
<td>비활성화</td>
<td>작업이 비활성화되었습니다.</td>
</tr><tr>
<td>만료됨</td>
<td>비활성화</td>
<td>작업이 만료되었습니다.</td>
</tr>
</tbody></table>

[](id:change)
### 작업 수정
1. [작업 리스트](https://console.cloud.tencent.com/live/tools/relay)에서 수정할 작업을 찾은 후 **편집**을 클릭하여 수정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a0a83bf06f9b5ae9743b68b19e4c40cd.png)
2. 실제 필요에 따라 작업 정보를 수정하고 **저장**을 클릭합니다.
 - 리전 및 콘텐츠 유형은 변경할 수 없습니다.
 - 작업 종료 시간 변경 시 작업이 종료될 때까지 destination URL이 유효한지 확인해야 합니다. destination URL를 변경하면 작업이 중단되고 재시작됩니다.
 - 라이브 스트리밍 소스에 대한 워터마크 설정을 변경하면 수정 사항이 즉시 적용됩니다. 주문형 비디오 소스의 경우 워터마크 설정에 대한 수정 사항은 다음 비디오 파일부터 적용됩니다. 워터마크 설정을 수정하면 재생이 끊길 수 있습니다. 워터마크 기능이 없는 타사 사이트로 릴레이하는 경우에만 릴레이용 워터마크 기능을 사용하는 것이 좋습니다. CSS에 릴레이 하는 경우 CSS의 라이브 워터마크 기능 사용을 권장합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d950a8029e1944e9029445dd8e428933.png)
3. 팝업 창에서 다음 정보를 확인합니다.
   - 작업의 **시작 시간, 종료 시간 및 재생 횟수**를 수정했다고 가정했을 때, 팝업 창에 다음 정보가 표시됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/4cadcabeef99828ab4be144040cbfd19.png)
   - **사용자 지정 비디오 경로**의 원본 URL이 변경된 경우 **현재 동영상 종료 후**(기본값) 또는 **즉시** 변경 사항을 적용할지 선택해야 합니다. 변경 사항이 적용된 후 릴레이는 첫 번째 소스 URL에서 재시작됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9591b91b7e5e307860c9ea2244b4e14e.png)
    - 변경 내용에 **destination URL**이 포함된 경우, **확인**을 클릭하면 현재 릴레이 작업이 **중지되고 재시작**됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0a7e04f65ae8bbdd9cb7ef3bc0ece656.png)
4. 정보가 올바른지 확인한 후 **확인**을 클릭하면 작업 내용 수정이 완료됩니다.

[](id:copy)

### 작업 복제
1. [작업 리스트](https://console.cloud.tencent.com/live/tools/relay)에서 복제할 작업을 선택하고 우측의 **복사**를 클릭하여 릴레이 작업 생성 페이지로 이동합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/28a0a3542ab9ab838d26dfc565f321d1.png)
2. 복제된 작업의 정보가 자동으로 채워집니다. 필요에 따라 [수정](#create)할 수 있습니다.
3. **저장**을 클릭하면 새로운 릴레이 작업이 생성됩니다.

[](id:reboot)
### 작업 재시작
작업 재시작 후, 작업 **상태는 변경되지 않으며**, 실행 중인 작업은 **처음부터 다시 실행**됩니다. 작업을 재시작하려면 다음을 수행하십시오.

1. [작업 리스트](https://console.cloud.tencent.com/live/tools/relay)에서 대상 릴레이 작업을 선택하고 우측의 **재시작**을 클릭합니다.
2. 릴레이 작업 재시작 진행 여부를 확인하고 **재시작**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d1b03e226297e44cbb7504d57c54af4f.png)

[](id:disable)
### 작업 비활성화
작업을 비활성화하면 **작업이 바로 중지됩니다**. 작업을 재시작하려면 [활성화](#enable)해야 합니다. 작업을 비활성화하려면 다음을 수행하십시오.

1. [작업 리스트](https://console.cloud.tencent.com/live/tools/relay)에서 대상 릴레이 작업을 선택하고 우측의 **비활성화**를 클릭합니다.
2. 릴레이 작업 비활성화 진행 여부를 확인하고 **비활성화**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c3acfb89f425b50ba53a8d63075091d8.png)


[](id:enable)
### 작업 활성화
작업이 활성화되면 **작업이 처음부터 재시작됩니다**. 작업을 활성화하려면 다음을 수행하십시오.

1. [작업 리스트](https://console.cloud.tencent.com/live/tools/relay)에서 비활성화된 대상 릴레이 작업을 선택하고 우측의 **활성화**를 클릭합니다.
2. 릴레이 작업 활성화 진행 여부를 확인하고 **확인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/77417a9c8406fe9d763c4d3960d98b21.png)

[](id:delete)
### 작업 삭제
삭제된 작업은 **복구할 수 없습니다**. 작업을 삭제하려면 다음을 수행하십시오.

1. [작업 리스트](https://console.cloud.tencent.com/live/tools/relay)에서 삭제할 릴레이 작업을 찾고 우측의 **삭제**를 클릭합니다.
2. 릴레이 작업 삭제 진행 여부를 확인하고 **삭제**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/44a15ad52bfc81f62c0aa907cdc7eb5c.png)

[](id:batch)
### 배치 작업
한 번에 **최대 10개의 릴레이 작업**을 삭제, 비활성화 및 활성화할 수 있습니다.
1. [작업 리스트](https://console.cloud.tencent.com/live/tools/relay)에서 삭제, 비활성화 또는 활성화할 릴레이 작업을 선택합니다.
2. 배치 작업을 클릭하고 **삭제**, **비활성화** 또는 **활성화**를 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7401eade6f5e04b9eadf71e04211f6e0.png)
3. 팝업 창에서 **삭제** / **비활성화** / **활성화**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5874636c548a4733281cd33eaca35abe.png)

   
## 만료된 작업 자동 삭제

작업은 종료 시간 후에 만료됩니다. 릴레이 작업이 너무 많으면 새 작업을 생성하지 못할 수 있습니다. 이를 방지하기 위해 시스템이 지정된 시간에 만료된 작업을 자동으로 삭제하도록 자동 삭제를 활성화할 수 있습니다. 삭제된 작업은 복구할 수 없습니다.

1. **CSS 툴킷** > **[릴레이](https://console.cloud.tencent.com/live/tools/relay)**를 선택하고 **설정**을 클릭합니다.
2. ![](https://qcloudimg.tencent-cloud.cn/raw/7ed257d05a4283dc233ef406520187b4.png) 버튼을 클릭하여 자동 삭제를 활성화합니다.
3. 만료된 작업이 삭제되기 전에 보관할 시간(1-24시간)을 지정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/4d579b1d0776ea22b5d994e3b7357ea3.png)