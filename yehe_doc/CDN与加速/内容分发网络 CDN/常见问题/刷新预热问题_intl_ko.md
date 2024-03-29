[](id:q6)
### 어떤 상황에서 퍼지와 프리패치 기능을 사용해야 합니까?
- 퍼지: 원본 서버에서 업데이트할 리소스, 제거할 제한된 리소스 또는 변경할 도메인 이름 구성이 있는 경우 사용자가 최신 리소스에 액세스할 수 있도록 하기 위해 노드 캐시에서 이전 리소스나 이전 구성에 대한 사용자 액세스를 방지할 수 있는 퍼지 작업을 제출할 수 있습니다. 자세한 내용은 [캐시 퍼지](https://intl.cloud.tencent.com/document/product//228/6299)를 참고하십시오.
- 프리패치: 운영 활동, 설치 패키지 또는 릴리스할 업그레이드 패키지의 경우 프리패치 작업을 제출하여 정적 리소스를 CDN 가속 노드로 프리패치하면 원본 서버의 부담을 줄이고 서비스 가용성 및 사용자 경험을 개선할 수 있습니다. 자세한 내용은 [캐시 프리패치](https://intl.cloud.tencent.com/document/product//228/39000)를 참고하십시오.

[](id:q1)
### 퍼지와 프리패치는 어떤 차이가 있나요?
- 퍼지 후, 해당 리소스의 전체 네트워크 CDN 노드 상의 캐시가 제거됩니다. 사용자의 요청이 노드에 도달하면 노드는 원본 서버로부터 해당하는 리소스를 불러온 다음, 사용자에게 리턴 및 노드에 캐시함으로써 최신 리소스를 가져올 수 있도록 합니다.
- 프리패치 후 리소스는 전체 네트워크 CDN 노드에 미리 캐시됩니다. 사용자가 노드에 도달하도록 요청하면 노드에서 직접 리소스를 얻을 수 있습니다.

[](id:q2)
### 퍼지와 프리패치의 조건은 어떻게 되나요? 적용 시간은 얼마나 걸리나요?
- 캐시 퍼지
 - URL 퍼지: 일일 URL 퍼지 수량은 최대 10000개이며, 1회당 제출 가능한 URL 퍼지 수량은 최대 1000개입니다. 퍼지 작업 적용 소요시간은 약 5분입니다. 파일 캐시 만료 시간이 5분 미만인 경우, 퍼지 도구를 사용하지 않고 타임 아웃 업데이트를 기다리는 것이 좋습니다.
 - 디렉터리 새로고침: 일일 디렉터리 새로고침 수는 최대 100개를 넘지 않습니다. 새로고침 시마다 제출하는 URL 디렉터리 수는 500개를 넘지 않으며 새로고침 작업이 적용되는 데까지 약 5분 정도 소요됩니다. 폴더에 설정한 캐시 만료 시간이 5분 미만이라면, 새로고침 툴을 사용하지 말고 타임아웃 업데이트까지 기다리시기를 권장합니다.
- 리소스 프리패치
 - URL 프리패치: 매일 최대 1000개의 URL을 프리패치할 수 있으며, 프리패치 작업당 최대 500개의 URL을 제출할 수 있습니다. 파일 크기에 따라 프리패치가 적용되는 데 약 5~30분이 소요됩니다.

[](id:q3)
### 원본 서버에서 리소스가 변경되면 CDN 캐시 노드의 캐시가 실시간으로 업데이트되나요?
아니요. CDN 캐시 노드의 캐시는 실시간으로 업데이트되지 않습니다.
- 원본 서버의 리소스가 변경되고 캐시가 여전히 유효한 경우 CDN 캐시 노드는 캐시를 업데이트하기 위해 Origin-pull을 수행하지 않으므로 원본 서버의 리소스가 캐시와 다릅니다. 이 경우 콘솔에서 적절한 [캐시 유효성 구성](https://intl.cloud.tencent.com/document/product//228/35317)을 지정할 수 있습니다.
- 캐시 유효 기간이 너무 짧으면 CDN이 원본 서버에서 콘텐츠를 자주 가져오고 원본 서버에서 더 많은 트래픽을 소비하게 됩니다. 너무 길면 캐시가 느리게 업데이트됩니다.
- 리소스의 캐시를 업데이트해야 하는 경우 [캐시 퍼지](https://intl.cloud.tencent.com/document/product//228/6299) 후 [프리패치](https://intl.cloud.tencent.com/document/product//228/39000)하여 CDN이 원본 서버에서 최신 리소스를 가져오도록 합니다. 최신 리소스에 대한 요청을 CDN에 보낼 수도 있습니다.



[](id:q5)
### 퍼지와 프리패치 기록을 확인하는 방법은 무엇입니까?
CDN 콘솔에서 퍼지와 프리패치 기록을 확인할 수 있습니다. 자세한 내용은 [작업 기록](https://intl.cloud.tencent.com/document/product//228/42176)을 참고하십시오.

[](id:q6)
### 사용자 정의 요청 헤더를 포함한 상태로 프리패치할 수 있나요?
현재는 지원되지 않습니다.


### 퍼지와 프리패치의 일일 할당량 한도를 늘리려면 어떻게 해야 합니까?
CDN 콘솔의 [할당량 관리](https://intl.cloud.tencent.com/document/product//228/46738)에서 할당량 사용량을 확인한 후 필요에 따라 임시 또는 영구 할당량을 요청할 수 있습니다. URL 퍼지 할당량, 디렉터리 퍼지 할당량 및 URL 프리패치 할당량과 같은 할당량 유형이 지원됩니다.
- 임시 할당량: 한시적으로 적용할 수 있는 할당량으로 유효 기간 내에서 사용할 수 있습니다. 만료되면 할당량 유형은 영구적으로 종료됩니다.
- 영구 할당량: 무기한 사용할 수 있는 할당량입니다. 영구 할당량 신청은 처리하는 데 시간이 오래 걸리므로 필요에 따라 임시 할당량을 요청하는 것이 좋습니다.

 
### 프리패치 시 주의해야 할 점은 무엇인가요?
캐시가 아직 유효한 파일을 프리패치하면 CDN은 파일 업데이트를 위해 Origin-pull을 수행하지 않습니다. 프리패치 작업을 제출하기 전에 캐시를 퍼지하는 것이 좋습니다.
- 프리패치 중 CDN은 원본 서버에서 필요한 콘텐츠를 가져옵니다. 대량의 프리패치 작업을 제출하면 원본 서버의 대역폭 사용량이 크게 증가합니다. 따라서 적절한 수의 프리패치 작업을 제안합니다.
- CDN은 엣지와 중간 레이어 노드의 이중 가속 구조를 제공합니다. 리소스가 중국 본토에서 프리패치되면 중국 본토의 중간 레이어 노드로 프리패치되고, 중국 본토 외부에서 프리패치된 리소스의 경우 중국 본토 외부의 엣지 노드로 프리패치됩니다. 리소스를 엣지 노드로 미리 가져올 때 발생하는 트래픽에 대해 요금이 청구됩니다.
